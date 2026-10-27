# ADR-0010: Match seguro via `MatchDoacao` com duplo aceite e link WhatsApp

- **Status:** Aceito
- **Data:** 2026-10-27 (atualizado conforme resolução Q-01, Q-02 e Q-10)
- **Requisitos relacionados:** RF-20b, RF-21, RF-22, RF-24, RF-27, RNF-12

## Contexto

Doador e receptora precisam combinar os detalhes logísticos da entrega do item. No entanto, um chat interno completo exige mensageria bidirecional, persistência de mensagens e moderação ativa, o que excederia o escopo do MVP de 12 semanas (6 sprints de 2 semanas). Por outro lado, expor o telefone do doador ou da mãe em murais públicos violaria gravemente a privacidade e a segurança física de mulheres vulneráveis ([Q-01](../historico-deliberacoes.md)). A entrega imediata do número sem consentimento prévio do doador também geraria riscos de assédio e invasão de privacidade.

## Decisão

Adotar o **Fluxo de Match Seguro com Duplo Aceite** mediado pela entidade `MatchDoacao` (`item_id`, `interessada_id`, `status`, `canal_utilizado = WHATSAPP`):

1. **Manifestação de Interesse (Passo 1):**
   - A mãe solo autenticada visualiza o item na vitrine e clica em "Quero este Item".
   - O backend registra o match com status inicial **`SOLICITADO`**.
   - **Nenhum telefone é revelado** neste momento.
2. **Avaliação e Aceite do Doador (Passo 2):**
   - O doador recebe um alerta no seu painel ("Minhas Doações"), visualizando apenas o **primeiro nome e o recorte territorial (`cidade`, `bairro` e `zona`, quando informada)** da solicitante.
   - O doador clica em **"Aceitar Doação"**, alterando o status do match para **`EM_NEGOCIACAO`**.
3. **Liberação Mútua do Link de Contato (Passo 3):**
   - Somente após a aprovação do doador, o backend disponibiliza o link seguro formatado para o WhatsApp:
     `https://wa.me/55<telefone>?text=Olá! Sou do EloMaterno e combinaremos a entrega do item: <titulo_item>`
   - Ambas as partes recebem o link em seus respectivos painéis privados, garantindo que o número permaneça protegido contra varreduras e acessos públicos.
4. **Ciclo de Vida do Match:**
   - Transição permitida: `SOLICITADO` → `EM_NEGOCIACAO` → `CONCLUIDO` (item sai da vitrine) ou `CANCELADO`.
5. **Simetria para Pedidos de Ajuda ([Q-10](../historico-deliberacoes.md)):**
   - No mural de pedidos de urgência, o doador clica em "Quero Ajudar", gerando contato seguro via WhatsApp com a mãe solicitante; a autora pode marcar o pedido como `ATENDIDO`.
6. **Evolução para V2:**
   - As tabelas `conversa` e `mensagem` com `canal_utilizado = CHAT` são criadas nas migrations da Sprint 5 apenas como base arquitetural para um futuro chat interno totalmente integrado, sem intermediação pelo WhatsApp ([RF-27](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)).

## Alternativas consideradas

- **Liberação imediata do link ao clicar em "Quero este Item":** Mais simples, mas permitiria que qualquer usuário cadastrado obtivesse instantaneamente o número de telefone de doadores, expondo-os a spam, assédio e perda de controle sobre seus donativos. Rejeitada em prol do *Privacy by Design*.
- **Chat interno completo no MVP:** Isolaria toda a comunicação na plataforma, mas exigiria WebSockets, notificações push e moderação de texto em tempo real, inviabilizando as metas de entrega em 6 sprints de duas semanas.
- **Exibição direta de telefone no anúncio:** Totalmente rejeitada por violar a LGPD e o princípio de segurança comunitária.

## Consequências

- **Positivas:**
  - Respeito integral ao consentimento e privacidade de doadores e mães solo.
  - Elimina a exposição pública de números telefônicos em APIs ou telas abertas.
  - Baixo custo de implementação, adaptando o ciclo de estados da entidade `MatchDoacao`.
- **Negativas / Riscos:**
  - A negociação final ocorre fora da plataforma (no aplicativo WhatsApp), impossibilitando auditoria automática do desfecho (a conclusão depende de ação manual dos usuários no sistema).
