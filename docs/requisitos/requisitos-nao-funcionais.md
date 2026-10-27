# Requisitos Não Funcionais (RNF)

Fonte principal: [README §3, §5, §6, §9](../../README.md) e deliberações documentadas em [Questões em Aberto](../historico-deliberacoes.md).

---

## Desempenho e Escalabilidade

| ID | Requisito | Métrica / Critério | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RNF-01** | Tempo de resposta dos endpoints da API sob regime de teste de carga. | Percentil 95 (p95) < 300 ms em testes de carga locais ou homologados (ex.: k6/JMeter) com 20 usuários simultâneos em instâncias aquecidas (*warm start*). | README §9; [Q-011](../historico-deliberacoes.md) | [0001](../adr/0001-arquitetura-desacoplada-spa-api-rest.md) |
| **RNF-02** | Otimização de mídia e consumo de dados móveis (3G/4G). | 1 foto por item servida exclusivamente pela CDN Cloudinary com transformações automáticas `f_auto,q_auto,w_500`, minimizando peso de download. | README §5; [Q-012](../historico-deliberacoes.md) | [0008](../adr/0008-cloudinary-midia.md) |
| **RNF-03** | Arquitetura backend *stateless* para permitir escala horizontal e deploy simples em PaaS. | Nenhum estado de sessão ou memória mantido no servidor da API. | README §5 | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RNF-04** | Listagens com paginação obrigatória e consultas indexadas no banco. | Máximo de 20 registros por página; índices relacionais B-Tree nas chaves de filtro (`estado`, `cidade`, `zona`, `bairro`, `categoria`, `status`). | [Q-02, Q-012](../historico-deliberacoes.md) | [0006](../adr/0006-postgresql-indexacao-territorial.md) |

---

## Segurança

| ID | Requisito | Métrica / Critério | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RNF-05** | Armazenamento seguro de senhas com algoritmo de hashing robusto. | Hashes gerados via BCrypt com fator de custo adequado; proibição de senhas em texto claro em logs ou banco. | README §5 | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RNF-06** | Autenticação *stateless* com JWT e autorização por papéis (RBAC). | Tokens JWT assinados (HS256) com validade de 2 a 4 horas mantidos em `localStorage`; autorização via `@PreAuthorize`; Content-Security-Policy (CSP) contra XSS. | README §5; [Q-04](../historico-deliberacoes.md) | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RNF-07** | Validação simétrica e estrita de entradas no cliente e no servidor. | Zod no cliente para feedback imediato e Bean Validation nos adaptadores de entrada REST; requisições inválidas rejeitadas com HTTP 400. | README §5 | [0004](../adr/0004-formularios-react-hook-form-zod.md) |
| **RNF-08** | Criptografia em trânsito e controle restrito de origens de acesso. | Tráfego 100% via HTTPS/TLS; configuração de CORS no backend restrita estritamente ao domínio do frontend na Vercel e ambiente de dev local. | README §5; [Q-05](../historico-deliberacoes.md) | [0011](../adr/0011-deploy-render-railway-vercel.md) |
| **RNF-09** | Mitigação de ataques de força bruta e abusos em endpoints públicos. | Rate limiting em rotas críticas (`/auth/login`, `/auth/cadastro`, submissão de tópicos). | Inferido | — |
| **RNF-10** | Isolamento e guarda segura de segredos de infraestrutura. | Chaves JWT, credenciais de banco e presets do Cloudinary gerenciados estritamente via variáveis de ambiente, nunca commitados no Git. | README §8; [Q-05](../historico-deliberacoes.md) | [0013](../adr/0013-docker-compose-ambiente-local.md) |

---

## Privacidade e Conformidade (LGPD)

| ID | Requisito | Métrica / Critério | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RNF-11** | *Privacy by Design* e moderação proativa de dados sensíveis (PII). | Validador Regex no backend bloqueia postagens contendo telefone, CPF ou endereço completo com HTTP 422 e mensagem orientativa, sem registrar o conteúdo sensível nos logs. | README §3.2, §6; [Q-06](../historico-deliberacoes.md) | [0009](../adr/0009-moderacao-pii-regex.md) |
| **RNF-12** | Proteção de dados de contato no fluxo de doações (Match Seguro). | O telefone do doador e da receptora nunca é retornado em listagens públicas; sua revelação ocorre apenas via link WhatsApp (`wa.me`) após o **duplo aceite formal** do match. | README §6.2; [Q-01](../historico-deliberacoes.md) | [0010](../adr/0010-match-seguro-whatsapp.md) |
| **RNF-13** | Minimização de dados pessoais e territoriais sob base legal do consentimento. | Cadastro fundado em autodeclaração (sem certidões ou dados de menores) e persistência territorial restrita a `estado`, `cidade`, `bairro` e `zona` (sem `logradouro` residencial exato nem coordenadas geográficas); checkbox explícito de aceite dos Termos de Uso e Política de Privacidade. | [Q-02, Q-09, Q-13](../historico-deliberacoes.md); LGPD art. 6º | [0006](../adr/0006-postgresql-indexacao-territorial.md), [0012](../adr/0012-viacep-enderecos.md) |
| **RNF-14** | Atendimento ao direito de exclusão do titular (LGPD art. 18). | Exclusão de conta executada via *soft delete* (`ativo = false`) com anonimização completa de nome, e-mail e telefone (`"Usuária Desativada"`), preservando a integridade das doações e tópicos já concluídos. | [Q-13](../historico-deliberacoes.md); LGPD art. 16/18 | — |

---

## Usabilidade e Acessibilidade

| ID | Requisito | Métrica / Critério | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RNF-15** | Design responsivo com abordagem *mobile-first*. | Interface totalmente adaptável a telas a partir de 360 px de largura, com botões e alvos de toque ergonomicamente adequados ao uso em smartphones. | README §2, §5, §9 | [0003](../adr/0003-frontend-react-vite-tailwind.md) |
| **RNF-16** | Acessibilidade e conformidade com heurísticas de usabilidade móvel. | Interface aderente às diretrizes WCAG 2.1 nível AA (contraste de cores, navegação por teclado e semântica acessível para leitores de tela). | README §5, §9 | [0003](../adr/0003-frontend-react-vite-tailwind.md) |
| **RNF-17** | Feedback compreensível, linguagem acolhedora e ausência de jargões técnicos. | Erros e validações reportados campo a campo em português claro, com tom empático e livre de terminologia técnica intimidadora. | README §5; [Q-06](../historico-deliberacoes.md) | [0003](../adr/0003-frontend-react-vite-tailwind.md) |

---

## Manutenibilidade, Portabilidade e Operação

| ID | Requisito | Métrica / Critério | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RNF-18** | Arquitetura Hexagonal (Ports & Adapters) no backend RESTful. | Isolamento estrito do domínio em relação a frameworks e adaptadores de I/O e persistência; conformidade arquitetural validada continuamente por testes automatizados com **ArchUnit**. | Decisão de Projeto; [Q-07](../historico-deliberacoes.md) | [0001](../adr/0001-arquitetura-desacoplada-spa-api-rest.md), [0002](../adr/0002-backend-java-spring-boot.md) |
| **RNF-19** | Versionamento incremental do esquema de banco de dados. | Migrations automatizadas via **Flyway**; banco de dados recriável a partir do zero de maneira determinística e auditável. | README §8 | [0007](../adr/0007-flyway-migrations.md) |
| **RNF-20** | Reprodutibilidade do ambiente de desenvolvimento local. | Ambiente completo orquestrado via `docker compose up` contendo contêiner oficial de banco PostgreSQL 15+ (`postgres:15-alpine`) e aplicação. | README §8 | [0013](../adr/0013-docker-compose-ambiente-local.md) |
| **RNF-21** | Infraestrutura em nuvem contínua com custo contido (camadas gratuitas estáveis). | Frontend na **Vercel**, backend na **Render** (Docker container) e banco de dados PostgreSQL 15+ gerenciado no **Supabase** ou **Neon** gratuito e estável (sem expiração precoce). | README §5, §9; [Q-05](../historico-deliberacoes.md) | [0011](../adr/0011-deploy-render-railway-vercel.md) |
| **RNF-22** | Cobertura e validação contínua de testes automatizados. | Testes unitários puros do domínio/casos de uso e testes de integração dos adaptadores de entrada e saída executados a cada pull request via GitHub Actions. | README §8, §9 | — |
| **RNF-23** | Observabilidade operacional e respeito à privacidade nos logs. | Proibição de registro de PII ou senhas nos logs; endpoint de *health check* provido pelo Spring Boot Actuator (`/health`). | Inferido | — |

---

## Restrições de Projeto

| ID | Restrição | Origem |
| :-- | :-- | :-- |
| **RNF-24** | Ciclo de desenvolvimento estruturado em 6 sprints de duas semanas cada (12 semanas / 84 dias no total) por um único desenvolvedor fullstack. | README §3.2, §5, §8 |
| **RNF-25** | Compatibilidade com os navegadores web mais utilizados (Google Chrome, Mozilla Firefox, Safari e Microsoft Edge) em plataformas móveis e desktop. | Inferido |

> **Nota sobre disponibilidade operacional:** A camada gratuita do Render pode apresentar latência inicial (*cold start*) na primeira requisição após inatividade. Para fins de avaliação de desempenho acadêmica ([RNF-01]), os testes formais de carga devem ser executados com instâncias aquecidas (*warm start*).
