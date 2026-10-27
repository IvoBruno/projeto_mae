# ADR-0006: PostgreSQL 15+, minimização territorial e indexação B-Tree

- **Status:** Aceito
- **Data:** 2026-10-27 (atualizado para recorte estritamente territorial sem geolocalização)
- **Requisitos relacionados:** RF-02, RF-16, RF-20, RNF-04, RNF-13

## Contexto

O domínio do EloMaterno é estritamente relacional (usuárias, endereços territoriais, itens, matches, pedidos de ajuda, tópicos e comentários) e demanda integridade referencial ACID. Quanto à aproximação entre doadores e mães solo, o uso de coordenadas geográficas exatas (`latitude`/`longitude` via GPS ou geocodificação) e o armazenamento de logradouros residenciais impõem dois problemas críticos: (1) risco elevado à segurança física e à privacidade de mulheres com histórico de violência doméstica caso ocorra inferência espacial ou exposição de dados; e (2) dependência desnecessária de extensões geoespaciais (PostGIS) e APIs externas de geocodificação para um fluxo cuja entrega final é combinada diretamente entre as partes após duplo aceite. Ademais, em municípios do interior e áreas rurais, CEPs gerais frequentemente não retornam bairro específico no ViaCEP, tornando útil o agrupamento complementar por **Zona**.

## Decisão

Adotar o **PostgreSQL 15+** padrão como Sistema Gerenciador de Banco de Dados relacional, operando exclusivamente com **recorte territorial administrativo** (`Estado`, `Município`, `Bairro` e `Zona`), sem armazenamento nem processamento de posição geográfica:

1. **Minimização de Dados Territoriais (LGPD, art. 6º, III):**
   - A tabela `ENDERECO` persiste exclusivamente: `id` (`UUID`), `usuario_id` (`UUID`), `cep` (`VARCHAR(9)`, opcional), `estado` (`VARCHAR(2)`), `cidade` (`VARCHAR(100)`), `bairro` (`VARCHAR(100)`) e `zona` (`ENUM('NORTE', 'SUL', 'LESTE', 'OESTE', 'CENTRO', 'RURAL')`, opcional).
   - **Não são coletados nem persistidos** `logradouro`, número residencial, complemento ou coordenadas geográficas (`latitude`/`longitude`). Mesmo quando o ViaCEP retorna o logradouro no cliente durante o autopreenchimento por CEP, esse campo é descartado antes do envio à API.
2. **Papel do Atributo `zona`:**
   - Permite agrupar bairros adjacentes em municípios médios/grandes (`NORTE`, `SUL`, `LESTE`, `OESTE`, `CENTRO`) quando a usuária deseja ampliar a busca além do próprio bairro, bem como contemplar moradoras de comunidades fora do perímetro urbano (`RURAL`) atendidas por CEPs municipais genéricos.
3. **Estratégia de Indexação Relacional (B-Tree):**
   - Criação via Flyway de índices relacionais **B-Tree** seletivos e compostos nas colunas de filtragem (`CREATE INDEX idx_endereco_territorio ON endereco (estado, cidade, zona, bairro)`), combinados aos índices de `categoria` e `status` nas tabelas de catálogo (`RNF-04`).
4. **Padrão de Chaves e Integridade:**
   - Chaves primárias (PK) padronizadas em `UUID` para todas as entidades, impedindo enumeração sequencial de recursos em URLs públicas.

## Alternativas consideradas

- **Geolocalização por coordenadas e extensão PostGIS (`GEOMETRY(Point)` / `ST_DWithin`):** Descartada definitivamente por contrariar o princípio de minimização de dados da LGPD para um público hipervulnerável, exigir geocodificação externa e adicionar complexidade operacional sem ganho real frente ao recorte por Estado, Município, Bairro e Zona.
- **Armazenamento completo de endereço residencial (`logradouro` e número):** Descartada porque a plataforma não realiza despacho logístico nem cobrança de frete; reter o endereço exato criaria passivo desnecessário de segurança da informação.
- **Banco NoSQL orientado a documentos (MongoDB):** Descartado por sacrificar garantias relacionais declarativas essenciais para auditoria de consentimento, anonimização em _soft delete_ e consistência transacional de matches.

## Consequências

- **Positivas:**
  - Eliminação na origem (_by design_) do risco de vazamento de coordenadas GPS ou endereço residencial exato das mães solo.
  - Simplificação da infraestrutura local (`postgres:15-alpine`) e em nuvem, dispensando extensões geoespaciais.
  - Consultas territoriais rápidas e determinísticas via índices B-Tree nativos (`p95 < 300 ms`).
  - Cobertura inclusiva tanto de bairros urbanos quanto da zona rural.
- **Negativas / Riscos:**
  - Não permite ordenação contínua por distância métrica em quilômetros, delegando a avaliação de conveniência de deslocamento à combinação de Município, Zona e Bairro selecionada pela usuária.
