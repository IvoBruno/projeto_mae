# ADR-0012: Autopreenchimento territorial via ViaCEP sem persistência de logradouro

- **Status:** Aceito
- **Data:** 2026-10-27 (atualizado para minimização territorial LGPD)
- **Requisitos relacionados:** RF-02, RNF-13

## Contexto

O cadastro exige apenas o recorte territorial administrativo da usuária (`estado`, `cidade`, `bairro` e `zona` opcional) para viabilizar a filtragem local de doações e pedidos de ajuda sem armazenar o endereço residencial exato nem coordenadas geográficas ([ADR-0006](0006-postgresql-indexacao-territorial.md)). Ainda assim, a digitação manual de Estado, Município e Bairro é propensa a erros de grafia em dispositivos móveis.

## Decisão

Consultar opcionalmente a API pública **ViaCEP** (`https://viacep.com.br/ws/{cep}/json/`) **diretamente do frontend** quando a usuária informar o CEP:

1. **Extração Seletiva e Minimização (LGPD):** O frontend aproveita exclusivamente `uf` (`estado`), `localidade` (`cidade`) e `bairro` retornados pelo ViaCEP, **descartando o campo `logradouro` e complementos** antes da submissão ao backend.
2. **Edição Manual e Campo `zona`:** Os campos permanecem editáveis (cobrindo inclusive CEPs gerais de municípios ou áreas rurais que retornam `bairro` vazio) e são complementados pela seleção opcional de `zona` (`NORTE`, `SUL`, `LESTE`, `OESTE`, `CENTRO`, `RURAL`).
3. **Independência do Backend:** O backend valida o formato dos atributos territoriais recebidos e não depende da disponibilidade do ViaCEP para concluir o cadastro.

## Alternativas consideradas

- **Persistência integral do retorno do ViaCEP (incluindo `logradouro`):** Rejeitada por armazenar dado de localização residencial desnecessário à operação da plataforma, ampliando riscos sob a LGPD.
- **Chamada via backend (proxy):** Centraliza cache, mas adiciona carga e latência desnecessárias ao servidor da API.
- **Somente digitação manual sem CEP:** Sem dependência externa, porém com maior fricção ergonômica em telas móveis e maior incidência de divergências ortográficas em nomes de bairros.

## Consequências

- **Positivas:** Preenchimento rápido e padronizado de Estado, Município e Bairro no celular, a custo zero, preservando estritamente a minimização de dados pessoais.
- **Negativas:** Dependência eventual de disponibilidade da API pública para o atalho automático (mitigada pelo preenchimento/edição manual sempre habilitado e pelo suporte explícito a `zona` para áreas com CEP único).

