# ADR-0013: Ambiente local com Docker Compose

- **Status:** Aceito
- **Data:** 2026-10-13
- **Requisitos relacionados:** RNF-10, RNF-19, RNF-20

## Contexto

O ambiente local precisa de PostgreSQL 15+, backend e frontend configurados de forma idêntica e reproduzível entre máquinas de desenvolvimento e integração contínua (README §8, Sprint 1).

## Decisão

Orquestrar o ambiente de desenvolvimento com **Docker Compose** (`docker-compose.yml` na raiz), com os serviços:

- `db`: imagem oficial leve `postgres:15-alpine`, com volume persistente.
- `api`: Spring Boot, executando as migrations Flyway no startup.
- `web` (opcional): Vite dev server.

Variáveis de ambiente em `.env` (ignorado pelo Git) com um `.env.example` versionado.

## Alternativas consideradas

- **Instalação local manual:** sem Docker, porém não reproduzível.
- **Testcontainers apenas nos testes:** complementar, e recomendado para testes de integração, mas não substitui o ambiente de desenvolvimento.

## Consequências

- **Positivas:** onboarding com um comando; paridade com a produção.
- **Negativas:** exige Docker instalado e consome mais recursos da máquina.
