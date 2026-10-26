# ADR-0007: Versionamento do esquema com Flyway

- **Status:** Aceito
- **Data:** 2026-10-13
- **Requisitos relacionados:** RNF-19, RNF-20

## Contexto

O esquema evolui a cada sprint (S1: `usuario`/`endereco`; S2: `topico`/`comentario`; S3: `item_doacao`; S4: `pedido_ajuda`; S5: `match_doacao`, `conversa`, `mensagem`; S6: otimizações de índices e testes de carga). É necessário reproduzir o banco em local, CI e produção.

## Decisão

Usar **Flyway** com scripts SQL versionados em `src/main/resources/db/migration` (`V1__usuario_endereco.sql`, …). O Hibernate é configurado com `ddl-auto=validate`, nunca `update`. A extensão PostGIS é criada em uma migration.

## Alternativas consideradas

- **Liquibase:** mais recursos, mas mais verboso (XML/YAML).
- **`hibernate.ddl-auto=update`:** rápido, mas não confiável nem auditável em produção.
- **Scripts manuais:** sem controle de versão do estado do banco.

## Consequências

- **Positivas:** histórico auditável, ambientes idênticos e migrations executadas no startup.
- **Negativas:** migrations aplicadas são imutáveis (correções exigem uma nova migration); é preciso escrever SQL com a sintaxe do PostgreSQL.
