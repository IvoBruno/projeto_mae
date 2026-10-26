# ADR-0009: Moderação de PII por Regex no backend com rejeição e feedback educativo

- **Status:** Aceito
- **Data:** 2026-10-13 (atualizado conforme resolução Q-06)
- **Requisitos relacionados:** RF-11, RNF-11, RNF-23

## Contexto

O público da plataforma compreende mães solo e mulheres em situação de vulnerabilidade social, muitas das quais possuem histórico prévio de violência doméstica, abandono parental e litígios judiciais. A publicação inadvertida de dados de contato direto (telefones pessoais, CPFs ou endereços residenciais) em murais comunitários abertos representa risco grave à segurança física das usuárias e aos princípios da LGPD. Diante da ausência de uma equipe humana de moderação 24/7, o sistema necessita de uma estratégia técnica automatizada e determinística, resolvendo se o conteúdo sensível deve ser mascarado silenciosamente (*scrubbed*) ou sumariamente rejeitado ([Q-06](../historico-deliberacoes.md)).

## Decisão

Adotar a estratégia de **Rejeição Automática com Resposta Educativa** (HTTP 422 Unprocessable Entity):

1. **Validação no Backend:**
   - Aplicada a todo conteúdo textual livre submetido por usuárias (título e corpo de tópicos no fórum, comentários e descrições livres).
   - Implementada no núcleo da aplicação (validação de domínio nos casos de uso) e como anotação Bean Validation nos adaptadores de entrada REST (`@SemPII`).
   - Conjunto de expressões regulares (Regex) voltadas a padrões brasileiros:
     - Telefones (fixos e celulares com DDD, variações de nono dígito, separadores, espaços e código de país `+55`).
     - CPFs (com ou sem máscara de pontuação).
     - Endereços e logradouros (`rua`, `av.`, `avenida`, `travessa`, `quadra`, `lote` associados a números ou CEPs).
   - **Normalização Prévia:** Remoção de caracteres de ofuscação (espaços intercalados, pontuação arbitrária e conversão de números por extenso recorrentes).
2. **Resposta da API e Feedback no Cliente:**
   - Ao identificar violação de PII, a API rejeita a requisição com código **HTTP 422**.
   - Mensagem retornada: *"Para sua segurança e privacidade, não compartilhe telefones, documentos ou endereços públicos no fórum. Utilize os canais seguros da plataforma."*
   - O conteúdo rejeitado **não é registrado nos logs operacionais da aplicação**, evitando que os logs se tornem um vetor de vazamento de PII ([RNF-23](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)).

## Alternativas consideradas

- **Mascaramento silencioso com asteriscos (`***`):** Embora o termo literal "PII Scrubber" possa sugerir substituição, alterar o texto da usuária sem seu consentimento pode distorcer o sentido do desabafo ou da dúvida jurídica, além de não educar a mulher sobre os riscos da exposição de seus dados.
- **Modelos de Inteligência Artificial / LLM / Reconhecimento de Entidades Nomeadas (NER):** Oferecem maior flexibilidade semântica, porém adicionam custos com APIs pagas, latência e dependência de rede externa para cada comentário publicado.

## Consequências

- **Positivas:**
  - Solução leve, determinística, com custo computacional desprezível (< 5 ms de processamento).
  - Promove a conscientização e a soberania da usuária sobre sua própria privacidade.
  - Testabilidade completa via testes unitários de casos de borda e evasão.
- **Negativas / Riscos:**
  - Expressões regulares podem gerar falsos positivos em citações numéricas legítimas (ex.: citação de números de leis ou artigos de códigos) ou não capturar ofuscações intencionais extremamente complexas. Isso é mitigado pela presença do perfil `ADMIN` para moderação complementar ([RF-12](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)).
