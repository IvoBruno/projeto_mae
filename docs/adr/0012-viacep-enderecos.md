# ADR-0012: Preenchimento de endereço via ViaCEP

- **Status:** Aceito
- **Data:** 2026-10-13
- **Requisitos relacionados:** RF-02, RF-27

## Contexto

O cadastro exige endereço (CEP, logradouro, bairro, cidade, estado). Digitação manual é lenta e propensa a erros em dispositivos móveis. O README prevê a integração com o ViaCEP na tela de cadastro (§8).

## Decisão

Consultar a API pública **ViaCEP** (`https://viacep.com.br/ws/{cep}/json/`) **diretamente do frontend** ao completar o CEP, preenchendo os campos, que continuam editáveis. O backend revalida o formato do CEP e dos campos recebidos e não depende do ViaCEP para aceitar o cadastro.

## Alternativas consideradas

- **Chamada via backend (proxy):** centraliza cache e tratamento de falhas, mas adiciona carga e latência.
- **BrasilAPI ou base local de CEPs:** alternativas ao ViaCEP; a base local é pesada para o MVP.
- **Somente digitação manual:** sem dependência externa, mas com pior usabilidade.

## Consequências

- **Positivas:** menos digitação e menos erros; sem custo.
- **Negativas:** dependência de disponibilidade e limites do serviço externo (mitigada pelo fallback manual). O ViaCEP não retorna coordenadas, então o preenchimento de `coordenadas` exigirá geocodificação à parte ([Q-02](../historico-deliberacoes.md)).

