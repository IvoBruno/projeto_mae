# ADR-0001: Arquitetura desacoplada — SPA + Backend Hexagonal (Ports & Adapters)

- **Status:** Aceito
- **Data:** 2026-10-13 (atualizado para Arquitetura Hexagonal)
- **Requisitos relacionados:** RNF-01, RNF-03, RNF-18, RNF-21

## Contexto

O projeto (README §2 e §3.2) exige uma aplicação web desacoplada e responsiva. O desenvolvimento é conduzido por uma única pessoa em 12 semanas (6 sprints de 2 semanas). Frontend e backend têm ciclos de deploy e custos de hospedagem distintos (Vercel vs. Render/Railway). Além disso, as regras de negócio em torno de moderação de dados sensíveis (LGPD/PII), fluxo de doações e matches demandam proteção e forte isolamento em relação a frameworks e bancos de dados para garantir testabilidade e evolução sustentável.

## Decisão

Adotar **arquitetura desacoplada com SPA no frontend e Arquitetura Hexagonal (Ports & Adapters) no backend RESTful**:

- **Frontend:** Single-Page Application (React/Vite) que consome a API via HTTP/JSON.
- **Backend:** Organizado segundo a **Arquitetura Hexagonal (Ports & Adapters)**, dividindo o sistema entre o Núcleo da Aplicação (Core) e Adaptadores de Infraestrutura:
  - **Domínio (Domain):** Entidades puras, objetos de valor (Value Objects) e regras de negócio essenciais, livres de dependências externas ou anotações de infraestrutura (inclusive sem anotações JPA diretas no modelo de domínio).
  - **Aplicação (Application / Use Cases):** Casos de uso e orquestração de regras de negócio:
    - **Portas de Entrada (Driving / Inbound Ports):** Interfaces que expõem os casos de uso oferecidos pela aplicação (ex.: `CriarTopicoUseCase`, `ManifestarInteresseDoacaoUseCase`).
    - **Portas de Saída (Driven / Outbound Ports):** Interfaces (SPIs) que declaram dependências de infraestrutura necessárias (ex.: `UsuarioRepositoryPort`, `ItemDoacaoRepositoryPort`, `MediaStoragePort`).
  - **Adaptadores de Entrada (Driving Adapters):**
    - Controladores REST (Spring Web) que interceptam requisições HTTP, validam DTOs de entrada, executam os casos de uso pelas portas de entrada e convertem resultados em DTOs de resposta.
  - **Adaptadores de Saída (Driven Adapters):**
    - **Persistência:** Implementações das portas de saída utilizando Spring Data JPA / Hibernate, com entidades JPA específicas (`*Entity`) e mappers bidirecionais para as entidades de domínio.
    - **Serviços Externos:** Clientes de integração (ex.: SDK Cloudinary para upload de imagens).
- **Banco:** PostgreSQL 15+ com PostGIS acessado exclusivamente por meio dos adaptadores de saída de persistência.
- **Contrato de API:** Descrito via OpenAPI (springdoc) para guiar o consumo pelo frontend.

## Alternativas consideradas

- **Arquitetura Tradicional em Camadas (Controller → Service → Repository):** Embora comum no ecossistema Spring Boot, tende a acoplar o modelo de domínio diretamente ao esquema de banco de dados (entidades anêmicas com anotações JPA) e a espalhar regras entre serviços com dependência direta de repositórios JPA, reduzindo a testabilidade pura do domínio.
- **Monólito com renderização no servidor (Thymeleaf/JSP):** Menos peças, mas contraria o requisito de desacoplamento e dificulta a evolução para um futuro aplicativo móvel nativo.
- **Next.js Fullstack:** Reduz o número de projetos, mas o projeto estabelece Java/Spring Boot no backend acadêmico.
- **GraphQL:** Flexível, mas adiciona complexidade e curva de aprendizado desnecessárias para o escopo do MVP.

## Consequências

- **Positivas:**
  - Isolamento estrito das regras de negócio em relação a frameworks e infraestrutura de banco de dados.
  - Testabilidade superior: regras de negócio testáveis via testes unitários puros sem carregar o contexto do Spring ou banco em memória.
  - Baixo acoplamento: adaptadores (ex.: troca de provedor de mídia ou estratégia de persistência) podem ser substituídos sem impacto no núcleo da aplicação.
  - Separação clara de responsabilidades e deploy independente entre SPA e API.
- **Negativas:**
  - Maior quantidade de classes e interfaces (portas de entrada e saída, DTOs de transporte, mappers e entidades JPA separadas das entidades de domínio).
  - Demanda disciplina arquitetural para preservar a inversão de dependência (recomendado o uso de testes com ArchUnit).
