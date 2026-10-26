# ADR-0003: Frontend em React (Vite) + Tailwind CSS

- **Status:** Aceito
- **Data:** 2026-10-13
- **Requisitos relacionados:** RNF-15, RNF-16, RNF-17

## Contexto

A interface deve ser responsiva, com foco em acessibilidade e uso em dispositivos móveis, pois o público-alvo acessa majoritariamente por celular (README §2, §5, §9).

## Decisão

Adotar **React.js com Vite** como SPA e **Tailwind CSS** para estilização utilitária, com:

- Abordagem _mobile-first_ e componentes reutilizáveis (cards de item, formulários, modais).
- Estado de autenticação em `AuthContext` ([ADR-0005](0005-autenticacao-jwt-spring-security.md)).
- Roteamento com React Router e rotas protegidas.
- Linguagem: TypeScript, em linha com a preferência por tipagem estática.

## Alternativas consideradas

- **Next.js:** SSR/SEO, mas desnecessário (a aplicação é autenticada e o README pede SPA).
- **Vue/Svelte:** curva de aprendizado semelhante, mas ecossistema menor para este caso.
- **CSS Modules ou Bootstrap:** menor produtividade para layouts responsivos customizados, ou visual mais genérico.
- **Create React App:** descontinuado e com build mais lento que o Vite.

## Consequências

- **Positivas:** build e HMR rápidos; ecossistema amplo; layout responsivo ágil.
- **Negativas:** SPA não é indexável por buscadores (aceitável: conteúdo é autenticado); classes utilitárias exigem disciplina de componentização.
