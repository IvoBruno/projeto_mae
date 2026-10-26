# ADR-0006: PostgreSQL 15+ com PostGIS e indexação territorial

- **Status:** Aceito
- **Data:** 2026-10-13 (atualizado conforme resolução Q-02 e Q-12)
- **Requisitos relacionados:** RF-02, RF-16, RF-27, RNF-04

## Contexto

O domínio do EloMaterno é estritamente relacional (usuárias, endereços, itens, matches, tópicos e comentários) e demanda integridade referencial ACID. No que tange à proximidade geográfica, o README propõe uma vitrine orientada por geolocalização, mas o serviço de preenchimento de endereço (ViaCEP) entrega apenas dados textuais (logradouro, bairro, cidade e estado), sem coordenadas de latitude e longitude ([Q-02](../historico-deliberacoes.md)). É necessário definir a estratégia de dados espaciais no banco e como a proximidade será viabilizada no MVP versus evolução.

## Decisão

Adotar o **PostgreSQL 15+** como banco de dados principal, com a extensão espacial **PostGIS** habilitada desde a primeira migration via Flyway:

1. **Estratégia do MVP (Filtro Territorial por Bairro e Cidade):**
   - As doações serão filtradas no MVP através de índices relacionais B-Tree nas colunas textuais `cidade`, `bairro` e `estado` da tabela `ENDERECO`, aproveitando diretamente os dados preenchidos de forma rápida pelo ViaCEP no cadastro.
   - Isso atende à necessidade imediata de aproximar doadores e receptoras locais sem depender de APIs externas de geocodificação.
2. **Preparação Estrutural para Evolução (PostGIS na V2):**
   - A tabela `ENDERECO` é provisionada com a coluna `coordenadas GEOMETRY(Point, 4326)` e índice espacial GiST (`CREATE INDEX idx_endereco_coordenadas ON endereco USING GIST (coordenadas)`).
   - No MVP, o campo aceita valores nulos. Na V2 ([RF-27](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)), a geocodificação automática via serviço externo converterá endereços em pontos geográficos, permitindo o filtro por raio em quilômetros via operador `ST_DWithin`.
3. **Padrão de Chaves e Integridade:**
   - Chaves primárias (PK) padronizadas em `UUID` para todas as entidades, impedindo enumeração sequencial de recursos em URLs públicas.

## Alternativas consideradas

- **Integração obrigatória com Nominatim / OpenStreetMap no cadastro do MVP:** Exigiria consulta HTTP síncrona a uma API pública durante o cadastro para obter coordenadas geográficas. Descartada pelo risco de instabilidade, latência adicional e limites estritos de requisições por minuto que poderiam travar o cadastro de mães solo em momentos de pico.
- **Cálculo de distância via Fórmula de Haversine em SQL padrão:** Dispensaria a extensão PostGIS, mas não se beneficiaria de índices espaciais GiST e traria perda de desempenho em consultas de raio em grande escala.
- **Banco NoSQL (MongoDB com 2dsphere):** Embora suporte consultas geoespaciais, sacrificaria a integridade referencial relacional essencial para o fluxo de auditoria, doações e usuários.

## Consequências

- **Positivas:**
  - Robustez relacional e ACID com suporte espacial nativo no mesmo banco de dados.
  - O MVP entra no ar rápido com filtro por cidade/bairro sem dependências frágeis de geocodificação.
  - A base de dados já nasce pronta para consultas avançadas em quilômetros na V2 sem necessidade de refatorações estruturais de esquema.
- **Negativas / Riscos:**
  - Exige que o serviço de banco de dados na nuvem suporte a extensão PostGIS (atendido pela seleção do Supabase/Neon no [ADR-0011](0011-deploy-render-railway-vercel.md)).
