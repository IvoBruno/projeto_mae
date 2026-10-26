# ADR-0004: Formulários com React Hook Form + Zod

- **Status:** Aceito
- **Data:** 2026-10-13
- **Requisitos relacionados:** RF-01, RF-02, RF-08, RF-14, RNF-07, RNF-17

## Contexto

O sistema tem vários formulários (cadastro, tópico, item, pedido). É necessário evitar requisições inválidas e dar feedback imediato (README §5).

## Decisão

Usar **React Hook Form** para o estado dos formulários e **Zod** para os esquemas de validação, integrados por `@hookform/resolvers`. Os esquemas ficam em `src/schemas/` e as regras espelham o Bean Validation do backend.

## Alternativas consideradas

- **Formik + Yup:** funcional, mas com mais re-renders e inferência de tipos mais fraca.
- **Validação manual:** menos dependências, mas repetitiva e propensa a erros.

## Consequências

- **Positivas:** inferência de tipos TypeScript a partir dos esquemas; poucos re-renders; erros por campo.
- **Negativas:** a validação existe em dois lugares (Zod e Bean Validation), então os dois precisam ficar sincronizados. O servidor continua sendo a fonte de verdade.
