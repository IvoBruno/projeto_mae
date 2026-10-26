# Registros de Decisões Arquiteturais (ADR)

Formato: [MADR](https://adr.github.io/madr/) simplificado — Contexto, Decisão, Alternativas, Consequências. Os ADRs documentam decisões declaradas no [README §5](../../README.md) e em outras seções, com a justificativa e as alternativas descartadas. As alternativas são análise complementar.

**Status possíveis:** `Proposto` · `Aceito` · `Substituído por ADR-XXXX` · `Obsoleto`.

| ADR | Título | Status |
| :-- | :-- | :-- |
| [0001](0001-arquitetura-desacoplada-spa-api-rest.md) | Arquitetura desacoplada: SPA + Backend Hexagonal (Ports & Adapters) | Aceito |
| [0002](0002-backend-java-spring-boot.md) | Backend em Java 17 + Spring Boot 3 e Arquitetura Hexagonal | Aceito |
| [0003](0003-frontend-react-vite-tailwind.md) | Frontend em React (Vite) + Tailwind CSS | Aceito |
| [0004](0004-formularios-react-hook-form-zod.md) | Formulários com React Hook Form + Zod | Aceito |
| [0005](0005-autenticacao-jwt-spring-security.md) | Autenticação stateless com Spring Security + JWT e armazenamento seguro | Aceito |
| [0006](0006-postgresql-postgis.md) | PostgreSQL 15+ com PostGIS e indexação territorial | Aceito |
| [0007](0007-flyway-migrations.md) | Versionamento do esquema com Flyway | Aceito |
| [0008](0008-cloudinary-midia.md) | Armazenamento de mídia no Cloudinary | Aceito |
| [0009](0009-moderacao-pii-regex.md) | Moderação de PII por Regex no backend com rejeição e feedback educativo | Aceito |
| [0010](0010-match-seguro-whatsapp.md) | Match seguro via `MatchDoacao` com duplo aceite e link WhatsApp | Aceito |
| [0011](0011-deploy-render-railway-vercel.md) | Deploy em Vercel (Frontend), Render (API) e Supabase/Neon (PostgreSQL com PostGIS) | Aceito |
| [0012](0012-viacep-enderecos.md) | Preenchimento de endereço via ViaCEP | Aceito |
| [0013](0013-docker-compose-ambiente-local.md) | Ambiente local com Docker Compose | Aceito |

## Como criar um novo ADR

1. Copie o [template](0000-template.md) para `NNNN-titulo-curto.md` (numeração sequencial).
2. Preencha as seções e adicione o ADR à tabela acima.
3. Nunca edite um ADR aceito. Crie um novo ADR e marque o antigo como `Substituído`.

