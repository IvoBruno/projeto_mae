# ADR-0005: Autenticação stateless com Spring Security + JWT e armazenamento seguro

- **Status:** Aceito
- **Data:** 2026-10-13 (atualizado conforme resolução Q-04 e Q-07)
- **Requisitos relacionados:** RF-01, RF-03, RF-04, RF-05, RNF-03, RNF-05, RNF-06

## Contexto

A API REST precisa autenticar usuárias e aplicar autorização granular por perfil (`MAE_SOLO`, `DOADOR`, `VOLUNTARIO`, `ADMIN`). O backend deve ser *stateless* para operar com baixo consumo em PaaS gratuito (Render), e o frontend é uma SPA desacoplada hospedada na Vercel (domínio distinto). É necessário definir o mecanismo de autenticação, o ciclo de vida do token e onde armazená-lo no cliente com segurança e viabilidade técnica ([Q-04](../historico-deliberacoes.md)).

## Decisão

1. **Backend (Infraestrutura de Segurança):**
   - **Spring Security** configurado com `SessionCreationPolicy.STATELESS` e filtro customizado `JwtAuthenticationFilter` (`OncePerRequestFilter`).
   - Senhas criptografadas exclusivamente com **BCrypt** (fator de custo 10+).
   - Tokens JWT assinados com algoritmo HMAC-SHA256 (HS256) com chave secreta gerida via variável de ambiente (`JWT_SECRET`).
   - Tempo de expiração do token configurado entre **2 a 4 horas**, forçando renovação periódica sem exigir infraestrutura de persistência de sessão.
   - **Autorização (RBAC):** Baseada no enum `USUARIO.perfil`:
     - `MAE_SOLO`: acesso total para criar e gerenciar pedidos de ajuda, solicitar itens da vitrine e também cadastrar itens de doação para circulação solidária ([Q-07](../historico-deliberacoes.md)).
     - `DOADOR`: cadastrar itens para doação e manifestar apoio a pedidos de ajuda.
     - `VOLUNTARIO`: participação comunitária no fórum identificado por selo visual ([Q-08](../historico-deliberacoes.md)).
     - `ADMIN`: moderação e gestão técnica da plataforma.
2. **Frontend (Gerenciamento e Persistência de Sessão):**
   - O token JWT é armazenado em **`localStorage`** do navegador e injetado no cabeçalho `Authorization: Bearer <token>` em todas as requisições autenticadas via Axios/Fetch interceptors.
   - Gerenciamento de estado de autenticação centralizado no `AuthContext` do React.
   - **Mitigação de XSS:** O React escapa valores automaticamente na renderização JSX (proibição de `dangerouslySetInnerHTML`) e o cabeçalho HTTP `Content-Security-Policy` (CSP) é configurado na Vercel para impedir a execução de scripts inline não autorizados.

## Alternativas consideradas

- **Cookie `HttpOnly` com `SameSite=None; Secure`:** Oferece proteção superior contra leitura por scripts em caso de XSS, mas introduz complexidade severa de CORS entre domínios distintos (`*.vercel.app` e `*.onrender.com`), além de risco de bloqueio de cookies de terceiros em versões recentes do Safari e Chrome. Rejeitada em prol da simplicidade e estabilidade do MVP.
- **Sessão com cookie no servidor (Stateful):** Exige armazenamento de sessão centralizado (ex.: Redis), aumentando os custos e a complexidade operacional da nuvem.
- **OAuth2/OIDC externo (Google, Gov.br):** Excelente para desonerar a guarda de credenciais, porém adiciona dependências externas complexas para o ciclo da Sprint 1 (duas semanas). Registrado para evolução futura.

## Consequências

- **Positivas:**
  - Backend 100% *stateless*, facilitando reinicializações do container no Render sem perda de sessões.
  - Integração limpa entre Vercel e Render sem atritos de cookies de terceiros entre origens cruzadas.
  - Papéis claros e flexíveis para as mães solo no ecossistema da aplicação.
- **Negativas / Riscos:**
  - Tokens em `localStorage` permanecem vulneráveis se houver vulnerabilidade XSS explorável. A proteção depende de rigor na sanitização de dados no frontend e política CSP.
  - Revogação imediata de token antes da expiração não é suportada sem uma blacklist em memória/banco (mitigado pela expiração curta de 2h a 4h).
