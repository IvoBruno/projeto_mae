# Requisitos Funcionais (RF)

Fonte principal: [README §2, §6, §7, §8](../../README.md) e deliberações documentadas no [Histórico de Deliberações](../historico-deliberacoes.md). O desenvolvimento está organizado em **6 sprints de duas semanas cada** (12 semanas no total).

---

## 1. Autenticação e Cadastro — Sprint 1 (Semanas 1 e 2 / Dias 1 a 14)

| ID | Requisito | Prioridade | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RF-01** | O sistema deve permitir o cadastro de usuária com nome, e-mail único, senha (criptografada em BCrypt), telefone (formato WhatsApp), perfil autodeclarado (`MAE_SOLO`, `DOADOR`, `VOLUNTARIO`) e aceite obrigatório dos Termos de Uso e Política de Privacidade (LGPD). | Must | README §7, §8; [Q-09, Q-13](../historico-deliberacoes.md) | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RF-02** | O cadastro deve coletar apenas o recorte territorial administrativo (`estado`, `cidade`, `bairro` e `zona` opcional `NORTE \| SUL \| LESTE \| OESTE \| CENTRO \| RURAL`), oferecendo autopreenchimento a partir do `cep` via integração frontend com a API pública ViaCEP, sem persistir `logradouro`/rua exata nem coordenadas geográficas. | Must | README §6, §7, §8; [Q-02](../historico-deliberacoes.md) | [0006](../adr/0006-postgresql-indexacao-territorial.md), [0012](../adr/0012-viacep-enderecos.md) |
| **RF-03** | O sistema deve autenticar a usuária por e-mail e senha, emitindo um token JWT *stateless*. | Must | README §5, §8 | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RF-04** | O cliente deve persistir o token em `localStorage`, manter a sessão no `AuthContext` e proteger as rotas privadas da aplicação. | Must | README §8; [Q-04](../historico-deliberacoes.md) | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RF-05** | O sistema deve aplicar autorização baseada em papéis (RBAC):<br>• `MAE_SOLO`: permissão universal (solicitar itens, cadastrar pedidos de ajuda e doar itens para economia circular);<br>• `DOADOR`: cadastrar itens para doação e atender pedidos de ajuda;<br>• `VOLUNTARIO`: participação acolhedora em tópicos com badge visual *"Voluntário(a) da Rede"* no fórum;<br>• `ADMIN`: moderação e gestão da plataforma. | Must | README §5; [Q-07, Q-08](../historico-deliberacoes.md) | [0005](../adr/0005-autenticacao-jwt-spring-security.md) |
| **RF-06** | A usuária deve poder editar seus dados e solicitar exclusão de conta via *soft delete* (`ativo = false`) com anonimização imediata de nome, e-mail e telefone para `"Usuária Desativada"`, preservando a integridade histórica de tópicos e doações. | Should | [Q-13](../historico-deliberacoes.md); LGPD art. 18 | — |

---

## 2. Fórum Comunitário — Sprint 2 (Semanas 3 e 4 / Dias 15 a 28)

| ID | Requisito | Prioridade | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RF-07** | Listar tópicos com paginação e filtro por categoria (`DUVIDAS`, `DESABAFO`, `DICAS`, `JURIDICO`), destacando visualmente autores voluntários com badge *"Voluntário(a) da Rede"*. | Must | README §8; [Q-08](../historico-deliberacoes.md) | [0001](../adr/0001-arquitetura-desacoplada-spa-api-rest.md) |
| **RF-08** | Usuária autenticada pode criar tópico (título, conteúdo, categoria) por meio de modal interativo. | Must | README §8 | — |
| **RF-09** | Exibir detalhe do tópico com seus comentários em ordem cronológica de publicação. | Must | README §8 | — |
| **RF-10** | Usuária autenticada pode comentar em um tópico. A interface deve atualizar a lista instantaneamente de forma otimista, contando com botão "Atualizar respostas" e refetch suave periódico. | Must | README §8; [Q-03](../historico-deliberacoes.md) | — |
| **RF-11** | O backend deve inspecionar e rejeitar automaticamente (HTTP 422) tópicos e comentários contendo números de telefone, CPF ou endereços completos via Regex, retornando mensagem educativa de preservação da segurança física e privacidade. | Must | README §2, §3.2, §6.1; [Q-06](../historico-deliberacoes.md) | [0009](../adr/0009-moderacao-pii-regex.md) |
| **RF-12** | O perfil `ADMIN` pode remover tópicos e comentários inadequados ou ofensivos. | Should | Inferido (RBAC) | — |
| **RF-13** | O autor pode editar ou excluir o próprio tópico/comentário enquanto não houver desdobramentos de moderação. | Could | Inferido | — |

---

## 3. Vitrine de Enxovais — Sprint 3 (Semanas 5 e 6 / Dias 29 a 42)

| ID | Requisito | Prioridade | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RF-14** | Usuários permitidos (`DOADOR` e `MAE_SOLO`) podem cadastrar item de doação (título, descrição, categoria, estado de conservação e 1 foto) via formulário "Quero Doar". | Must | README §8; [Q-07, Q-12](../historico-deliberacoes.md) | — |
| **RF-15** | O formulário deve realizar upload direto de 1 foto para o Cloudinary (unsigned preset) com preview no cliente, persistindo a URL segura em `foto_url`. | Must | README §3.2, §8; [Q-12](../historico-deliberacoes.md) | [0008](../adr/0008-cloudinary-midia.md) |
| **RF-16** | Exibir galeria de itens disponíveis com filtros combinados por categoria, estado de conservação, Estado, Município (`cidade`), Bairro e Zona (`NORTE`, `SUL`, `LESTE`, `OESTE`, `CENTRO`, `RURAL`) da doação. | Must | README §2, §8; [Q-02](../historico-deliberacoes.md) | [0006](../adr/0006-postgresql-indexacao-territorial.md) |
| **RF-17** | Exibir detalhe completo do item com foto em alta qualidade/transformação otimizada, descrição e status de disponibilidade. | Must | Inferido | [0008](../adr/0008-cloudinary-midia.md) |
| **RF-18** | O doador pode editar dados, remover o anúncio ou alterar o status do próprio item enquanto não houver match concluído. | Must | README §8 | — |

---

## 4. Mural de Pedidos de Ajuda — Sprint 4 (Semanas 7 e 8 / Dias 43 a 56)

| ID | Requisito | Prioridade | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RF-19** | Mãe solo autenticada pode publicar pedido de ajuda de urgência (título, necessidade material, urgência e status) e gerenciar sua finalização. | Must | README §8; [Q-07](../historico-deliberacoes.md) | — |
| **RF-20** | Exibir mural de pedidos de ajuda, permitindo ordenação por nível de urgência (`BAIXA`, `MEDIA`, `ALTA`) e data de publicação, além de filtro territorial por Estado, Município, Bairro e Zona. | Must | README §8; [Q-02](../historico-deliberacoes.md) | [0006](../adr/0006-postgresql-indexacao-territorial.md) |
| **RF-20b** | Doador autenticado pode manifestar intenção de apoio clicando em "Quero Ajudar" em um pedido do mural, gerando canal seguro via link WhatsApp com a mãe solicitante; a autora pode marcar o pedido como `ATENDIDO`. | Must | [Q-10](../historico-deliberacoes.md) | [0010](../adr/0010-match-seguro-whatsapp.md) |

---

## 5. Match Seguro e Painel da Usuária — Sprint 5 (Semanas 9 e 10 / Dias 57 a 70)

| ID | Requisito | Prioridade | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RF-21** | Ao clicar em "Quero este Item", o sistema registra `MatchDoacao` com status `SOLICITADO` (canal `WHATSAPP`), vinculando o item à mãe interessada sem revelar o telefone do doador publicamente. | Must | README §6.2, §8; [Q-01](../historico-deliberacoes.md) | [0010](../adr/0010-match-seguro-whatsapp.md) |
| **RF-22** | O doador visualiza a manifestação no painel (com primeiro nome, município, bairro e zona da interessada) e clica em **"Aceitar Doação"** (status `EM_NEGOCIACAO`). Somente após o aceite o link parametrizado do WhatsApp (`wa.me/55...`) é liberado para ambas as partes combinarem a entrega. | Must | README §6.2, §8; [Q-01](../historico-deliberacoes.md) | [0010](../adr/0010-match-seguro-whatsapp.md) |
| **RF-23** | Painel "Minhas Doações e Solicitações" lista os itens anunciados, pedidos cadastrados e matches em andamento de cada usuária. | Must | README §8 | — |
| **RF-24** | Doador e interessada podem atualizar o ciclo de vida do match (`EM_NEGOCIACAO` → `CONCLUIDO` ou `CANCELADO`). | Must | README §7; [Q-01](../historico-deliberacoes.md) | [0010](../adr/0010-match-seguro-whatsapp.md) |
| **RF-25** | Ao concluir um match (`CONCLUIDO`), o item associado deve passar automaticamente para indisponível e deixar de ser exibido na vitrine geral. | Should | Inferido | — |
| **RF-26** | O sistema deve impedir match duplicado ativo da mesma usuária sobre o mesmo item, bem como impedir que um doador solicite match sobre o próprio item publicado. | Should | Inferido | [0001](../adr/0001-arquitetura-desacoplada-spa-api-rest.md) |

---

## 6. Evolução (fora do MVP)

| ID | Requisito | Prioridade | Origem / Decisão | ADR |
| :-- | :-- | :-- | :-- | :-- |
| **RF-27** | Sistema de mensageria interna e chat integrado (`conversa`/`mensagem`, `canal_utilizado = CHAT`), eliminando a necessidade de redirecionamento externo para o WhatsApp. | Won't (V2) | README §7, §8; [Q-01](../historico-deliberacoes.md) | [0010](../adr/0010-match-seguro-whatsapp.md) |

---

## Matriz Sprint × Requisitos

| Sprint | Período | Foco Temático | Requisitos Funcionais |
| :-- | :-- | :-- | :-- |
| **1** | Semanas 1 e 2 (Dias 1 a 14) | Fundação & Autenticação | RF-01, RF-02, RF-03, RF-04, RF-05, RF-06 |
| **2** | Semanas 3 e 4 (Dias 15 a 28) | Fórum Comunitário & Moderação | RF-07, RF-08, RF-09, RF-10, RF-11, RF-12, RF-13 |
| **3** | Semanas 5 e 6 (Dias 29 a 42) | Vitrine de Enxovais & Mídia (Cloudinary) | RF-14, RF-15, RF-16, RF-17, RF-18 |
| **4** | Semanas 7 e 8 (Dias 43 a 56) | Mural de Pedidos de Ajuda & Apoio | RF-19, RF-20, RF-20b |
| **5** | Semanas 9 e 10 (Dias 57 a 70) | Match com Duplo Aceite & Painel da Usuária | RF-21, RF-22, RF-23, RF-24, RF-25, RF-26 |
| **6** | Semanas 11 e 12 (Dias 71 a 84) | Qualidade (ArchUnit, k6), CI/CD & Deploy MVP | Validação transversal dos RNFs (RNF-01 a RNF-25) |
| **V2** | Pós-MVP | Evolução da Plataforma | RF-27 |
