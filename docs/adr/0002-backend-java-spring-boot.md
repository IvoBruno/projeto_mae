# ADR-0002: Backend em Java 17+ com Spring Boot 3 e Arquitetura Hexagonal

- **Status:** Aceito
- **Data:** 2026-10-13 (atualizado para Arquitetura Hexagonal)
- **Requisitos relacionados:** RNF-05, RNF-06, RNF-07, RNF-18

## Contexto

O backend precisa de tipagem estática, segurança robusta, validação declarativa e persistência relacional, com alta produtividade para um único desenvolvedor (README §5). Para assegurar a manutenibilidade e a testabilidade das regras de negócio (notadamente moderação de conteúdo sensível e fluxos de doação), o backend deve adotar a **Arquitetura Hexagonal (ADR-0001)**, mantendo o domínio desacoplado do framework Spring Boot.

## Decisão

Usar **Java 17+ e Spring Boot 3** como infraestrutura de suporte e injeção de dependência, organizando a aplicação estritamente sob o padrão **Ports & Adapters (Hexagonal)**:

- **Papel do Spring Boot:** Atua nas bordas da aplicação (adaptadores e configuração), nunca no núcleo de domínio.
  - Adaptadores de entrada utilizam **Spring Web** para expor endpoints REST.
  - Adaptadores de saída de persistência utilizam **Spring Data JPA/Hibernate** para comunicação com PostgreSQL.
  - **Spring Security** gerencia a autenticação e autorização stateless via JWT ([ADR-0005](0005-autenticacao-jwt-spring-security.md)) como componente de infraestrutura/segurança.
  - **Spring Boot Actuator** provê métricas e *health check* (`/health`).
- **Organização de Pacotes (Bounded Context + Hexagonal):**
  Dividido por módulos/contextos delimitados (`auth`, `forum`, `vitrine`, `match`), com estrutura interna padronizada:
  ```
  br.edu.ifpi.elomaterno.<modulo>/
  ├── domain/                     <-- Núcleo Puro (sem anotações Spring/JPA)
  │   ├── model/                  (Entidades e Value Objects de negócio)
  │   └── exception/              (Exceções de domínio)
  ├── application/                <-- Casos de Uso e Portas
  │   ├── ports/
  │   │   ├── in/                 (Interfaces de Casos de Uso - Driving Ports)
  │   │   └── out/                (Interfaces de SPI / Repositórios - Driven Ports)
  │   └── service/                (Implementação dos Casos de Uso)
  └── infrastructure/             <-- Adaptadores e Configuração
      ├── adapters/
      │   ├── in/web/             (REST Controllers, DTOs de Request/Response, Mappers)
      │   └── out/persistence/    (JPA Entities, Spring Data Repositories, Mappers)
      └── config/                 (Spring @Configuration para amarração/IoC)
  ```
- **Conformidade Arquitetural Automatizada:** Uso de testes com **ArchUnit** para validar que classes em `domain` e `application` não importem pacotes de `infrastructure`, Spring Framework ou Hibernate/JPA.

## Alternativas consideradas

- **Arquitetura tradicional em camadas (controllers, services, repositories):** Rejeitada por acoplar o modelo de negócio a entidades JPA gerenciadas pelo Hibernate e misturar regras de negócio com anotações de infraestrutura.
- **Node.js/NestJS:** Uma linguagem em todo o stack, mas com menor tipagem estática e suporte corporativo menos alinhado aos objetivos acadêmicos do projeto.
- **Quarkus/Micronaut:** *Startup* mais rápido, mas ecossistema e documentação menos consolidados no contexto local do que Spring Boot 3.

## Consequências

- **Positivas:**
  - O núcleo de domínio permanece puro e desacoplado, facilitando testes unitários rápidos sem necessidade de contexto Spring ou banco de dados.
  - Mudanças de infraestrutura (banco, formato de API, clientes externos) não afetam a lógica de negócio.
  - Regras de arquitetura verificáveis continuamente em CI através de testes ArchUnit.
- **Negativas:**
  - Maior volume de código inicial devido a mappers (conversão entre entidades de domínio, entidades JPA e DTOs) e interfaces de portas.
  - Exige disciplina rigorosa para manter beans de domínio e serviços independentes do ciclo de vida direto do Spring (utilizando classes de `@Configuration` para injeção).
