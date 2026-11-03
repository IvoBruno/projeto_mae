# Instituto Federal do Piauí (IFPI) - Campus Parnaíba

## ELOMATERNO: REDE DIGITAL SOLIDÁRIA DE APOIO A MÃES SOLO

### Arquitetura Hexagonal, Apoio Comunitário e Circulação Solidária de Enxovais na Economia do Cuidado

**Autor:** Ivo Bruno Gomes Araujo

**Orientador(a):** Prof. Me. Antonio Santos de Sousa

**Área de Concentração:** Engenharia de Software Aplicada / Sistemas Colaborativos de Impacto Social

## 1. CONTEXTUALIZAÇÃO E MOTIVAÇÃO SOCIAL

Os microdados do Censo Demográfico (IBGE, 2023) e o levantamento do IBRE/FGV (Feijó, 2023) registram mais de 10,3 milhões de lares monoparentais chefiados por mulheres no Brasil, frente a 1,6 milhão sob responsabilidade masculina exclusiva. Essa diferença se soma à desigualdade na jornada diária. As mulheres dedicam o dobro de horas semanais aos afazeres domésticos e ao cuidado dos filhos em comparação aos homens, mas recebem salários entre 20,9% e 30% menores (IBGE, 2023; Souza; Franco; Gomes, 2022).

Nos atendimentos do Núcleo Cível da Defensoria Pública analisados por Sousa (2025), essa sobrecarga decorre do abandono paterno e da inadimplência recorrente na pensão alimentícia. Apenas nos últimos cinco anos, o país acumulou mais de 734 mil registros de nascimento sem o nome do pai (ARPEN-Brasil, 2025). Quando o genitor trabalha na informalidade ou está desempregado, a cobrança judicial e a prisão civil tornam-se lentas demais para cobrir gastos imediatos com alimentação, fraldas e vestuário infantil.

Esse quadro atinge sobretudo mulheres pretas e pardas das periferias urbanas e do interior. Com orçamento restrito e forte dependência do Programa Bolsa Família, essas mães recorrem a redes informais de vizinhança e parentesco. O apoio cotidiano acaba concentrado em outras mulheres da própria família, como avós, irmãs e filhas mais velhas, que também enfrentam limites financeiros e físicos (Machado; Pereira, 2020; Araújo; Amorim, 2025).

## 2. O PROBLEMA DE PESQUISA E A SOLUÇÃO TECNOLÓGICA

Diante da sobrecarga das redes familiares e da falta de canais digitais voltados à proteção de mulheres em situação de vulnerabilidade, este trabalho parte da seguinte questão de pesquisa:

> **Como um sistema computacional desacoplado, seguro e orientado por recorte territorial administrativo pode conectar mães solo, doadores de insumos infantis e redes solidárias locais para reduzir a carência material imediata e o isolamento materno?**

O **EloMaterno** responde a essa questão por meio de uma aplicação web responsiva dividida em dois módulos principais:

1. **Vitrine Colaborativa de Enxovais e Mural de Pedidos:** Catálogo digital para doação de artigos infantis (berços, roupas, carrinhos, fraldas e fórmulas) e publicação de demandas urgentes. A busca utiliza filtros por Estado, Município, Bairro e Zona, sem coletar ou exibir logradouros e coordenadas geográficas.
2. **Fórum Comunitário de Acolhimento:** Espaço para troca de experiências, dicas cotidianas, desabafos e dúvidas jurídicas básicas. O módulo conta com bloqueio automático de dados pessoais sensíveis nas postagens públicas.

## 3. OBJETIVOS DO TRABALHO

### 3.1 Objetivo Geral

Desenvolver e validar o Produto Mínimo Viável (MVP) da plataforma web **EloMaterno**, estruturada em Arquitetura Hexagonal e voltada à conexão segura entre mães solo, doadores de itens infantis e voluntários comunitários, com proteção de dados pessoais (LGPD) e busca por recorte territorial administrativo.

### 3.2 Objetivos Específicos

- Estruturar o núcleo do backend em Java 17+ com Spring Boot 3 sob Arquitetura Hexagonal (_Ports & Adapters_), com autenticação _stateless_ via JWT (BCrypt) e controle de acesso por papéis (`MAE_SOLO`, `DOADOR`, `VOLUNTARIO`, `ADMIN`).
- Implementar o módulo de Fórum Comunitário com categorização temática e filtro validador no servidor (Regex, HTTP 422) para bloquear a publicação acidental de telefones, CPFs e endereços.
- Construir a Vitrine de Enxovais com envio direto de imagens para a CDN Cloudinary e consultas indexadas por árvore B-Tree no PostgreSQL 15+ (`estado`, `cidade`, `zona`, `bairro`), sem retenção de logradouro ou GPS.
- Desenvolver o Mural de Pedidos de Ajuda classificados por nível de urgência (`BAIXA`, `MEDIA`, `ALTA`), com filtro territorial e atalho de apoio direto para doadores.
- Implementar a máquina de estados de `MatchDoacao` com exigência de duplo aceite antes da liberação do link parametrizado do WhatsApp (`wa.me`), além da exclusão lógica de conta com anonimização de dados pessoais.
- Verificar a qualidade do sistema por testes de arquitetura (ArchUnit), ensaios de carga (k6 para `p95 < 300 ms`), checagem de acessibilidade móvel (WCAG 2.1 AA em telas a partir de 360 px) e implantação contínua em nuvem gratuita.

## 4. FUNDAMENTAÇÃO TEÓRICA E INTERSECCIONALIDADE

A base teórica do projeto reúne estudos da Sociologia, do Serviço Social e da Psicologia Social para explicar as raízes materiais e afetivas da monoparentalidade feminina no Brasil:

- **Divisão Sexual do Trabalho e Dispositivo Materno:** Com base em Saffioti (2015), Hirata e Kergoat (2007) e Zanello (2020), discute-se como o trabalho reprodutivo não remunerado recai sobre as mulheres. Essa estrutura naturaliza a sobrecarga doméstica materna enquanto desobriga socialmente os homens do cuidado diário.
- **Marcadores Sociais da Diferença e Território:** Os levantamentos econométricos com microdados da PNAD Contínua (Souza et al., 2024; Souza; Franco; Gomes, 2022) e a análise de Toledo, Martins e Ferreira (2022) mostram que a chefia monoparental feminina concentra-se entre mulheres negras, de menor renda e moradoras de periferias ou municípios do interior.
- **Representações Sociais e Redes de Apoio:** Araújo e Amorim (2025) e Machado e Pereira (2020) examinam o contraste entre o estereótipo da "mulher guerreira" e o desgaste mental vivido no isolamento doméstico. O fortalecimento de vínculos horizontais entre mulheres reduz esse estresse e orienta o desenho dos espaços de acolhimento e circulação solidária da plataforma.

## 5. DECISÕES ARQUITETURAIS E STACK TECNOLÓGICA

Para viabilizar a construção e a manutenção do sistema por um único desenvolvedor _fullstack_ ao longo de 12 semanas, a escolha tecnológica priorizou tipagem estática no servidor, ferramentas consolidadas no mercado e hospedagem gratuita:

| Camada / Componente              | Tecnologia Selecionada                     | Justificativa Técnica no Projeto                                                                                                                     |
| :------------------------------- | :----------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Backend Framework**            | Java 17+ / Spring Boot 3                   | Tipagem estática, ecossistema maduro, injeção de dependência e separação limpa entre regras de domínio e adaptadores REST/JPA.                       |
| **Segurança & Sessão**           | Spring Security + JWT                      | Autenticação _stateless_ via tokens assinados (HS256), senhas com hash BCrypt e controle de acesso baseado em papéis (RBAC).                         |
| **Frontend SPA**                 | React.js (Vite) + Tailwind CSS             | Compilação rápida, componentização de formulários e modais, e estilização responsiva voltada a dispositivos móveis (_mobile-first_).                 |
| **Gerenciamento de Formulários** | React Hook Form + Zod                      | Validação declarativa de esquemas no navegador com retorno visual imediato de erros campo a campo antes do envio à API.                              |
| **Banco de Dados Relacional**    | PostgreSQL 15+                             | Transações ACID, versionamento de esquema com Flyway e índices B-Tree compostos para buscas por Estado, Município, Bairro e Zona.                    |
| **Armazenamento de Mídia**       | Cloudinary CDN                             | Envio direto de fotos pelo cliente (_unsigned presets_) e compressão automática na URL (`f_auto,q_auto,w_500`) para poupar franquia de dados móveis. |
| **Infraestrutura / Deploy**      | Render (API) + Supabase/Neon (DB) + Vercel | Integração contínua via GitHub, certificados HTTPS automáticos e banco PostgreSQL gratuito sem prazo de expiração durante a avaliação acadêmica.     |

## 6. SEGURANÇA COMUNITÁRIA E CONFORMIDADE COM A LGPD

Muitas mães solo enfrentam disputas judiciais de guarda e alimentos ou possuem histórico de violência doméstica. Por essa razão, a plataforma aplica controles de _Privacy by Design_ desde a camada de domínio:

1. **Bloqueio de PII (Personally Identifiable Information) e Minimização Territorial:** O backend utiliza validadores com expressões regulares (`@SemPII`) para recusar automaticamente (HTTP 422) tópicos e comentários que contenham números de telefone, CPFs ou endereços residenciais. Além disso, conforme o art. 6º, III, da LGPD, o banco de dados **não coleta nem armazena coordenadas GPS ou nomes de rua (`logradouro`)**, e restringe os registros a Estado, Município, Bairro e Zona.
2. **Match Seguro com Duplo Aceite:** No MVP, o interesse por um item cria um registro na tabela `MatchDoacao` com status `SOLICITADO`. O telefone das partes permanece oculto nas listagens públicas e só é liberado via link parametrizado do WhatsApp (`wa.me/55...`) após o aceite formal do doador.

## 7. MODELAGEM CONCEITUAL DE DADOS (DER LÓGICO)

O diagrama abaixo apresenta o modelo relacional do sistema para contas de usuárias, recorte territorial minimizado, vitrine de doações, mural de pedidos de ajuda e fórum comunitário:

```text
+-----------------------------------------------------------------------------------+
|                                   USUARIO                                         |
+-----------------------------------------------------------------------------------+
| PK  id                 : UUID                                                     |
|     nome               : VARCHAR(150)                                             |
|     email              : VARCHAR(150) UNIQUE                                      |
|     senha_hash         : VARCHAR(255)                                             |
|     telefone           : VARCHAR(20)          -- Formatado para WhatsApp          |
|     perfil             : ENUM('MAE_SOLO', 'DOADOR', 'VOLUNTARIO', 'ADMIN')        |
|     ativo              : BOOLEAN DEFAULT TRUE                                     |
|     created_at         : TIMESTAMP                                                |
+-----------------------------------------------------------------------------------+
                                         │ 1
                                         ├────────────────────────┬────────────────────────┐
                                         │ 1                      │ 1                      │ 1
                                         ▼ 1                      ▼ N                      ▼ N
+----------------------------------------+     +------------------+----+     +-------------+------+
|               ENDERECO                 |     |      ITEM_DOACAO      |     |    PEDIDO_AJUDA    |
+----------------------------------------+     +-----------------------+     +--------------------+
| PK  id           : UUID                |     | PK  id          : UUID|     | PK  id       : UUID|
| FK  usuario_id   : UUID                |     | FK  doador_id   : UUID|     | FK  mae_id   : UUID|
|     cep          : VARCHAR(9) (OPC.)   |     |     titulo      : VC  |     |     titulo   : VC  |
|     estado       : VARCHAR(2)          |     |     descricao   : TEXT|     |     necessid : TEXT|
|     cidade       : VARCHAR(100)        |     |     categoria   : ENUM|     |     urgencia : ENUM|
|     bairro       : VARCHAR(100)        |     |     conservacao : ENUM|     |     status   : ENUM|
|     zona         : ENUM('NORTE','SUL', |     |     foto_url    : VC  |     |     criado_em: TIME|
|                    'LESTE','OESTE',    |     |     status      : ENUM|     +--------------------+
|                    'CENTRO','RURAL')   |     |     created_at  : TIME|
+----------------------------------------+     +-----------------------+
                                                           │ 1
                                                           ▼ N
                                               +---------------------------------------------------+
                                               |                   MATCH_DOACAO                    |
                                               +---------------------------------------------------+
                                               | PK  id               : UUID                       |
                                               | FK  item_id          : UUID                       |
                                               | FK  interessada_id   : UUID (FK -> USUARIO)       |
                                               |     status           : ENUM('SOLICITADO',         |
                                               |                             'EM_NEGOCIACAO',      |
                                               |                             'CONCLUIDO',          |
                                               |                             'CANCELADO')          |
                                               |     canal_utilizado  : ENUM('WHATSAPP', 'CHAT')   |
                                               |     created_at       : TIMESTAMP                  |
                                               +---------------------------------------------------+

                                   MÓDULO DE FÓRUM COMUNITÁRIO
+----------------------------------------+              +------------------------------------------+
|                 TOPICO                 |              |                COMENTARIO                |
+----------------------------------------+              +------------------------------------------+
| PK  id           : UUID                | 1          N | PK  id           : UUID                  |
| FK  autor_id     : UUID (-> USUARIO)   ├─────────────►| FK  topico_id    : UUID (-> TOPICO)      |
|     titulo       : VARCHAR(200)        |              | FK  autor_id     : UUID (-> USUARIO)     |
|     conteudo     : TEXT                |              |     conteudo     : TEXT                  |
|     categoria    : ENUM('DUVIDAS',     |              |     created_at   : TIMESTAMP             |
|                         'DESABAFO',    |              +------------------------------------------+
|                         'DICAS',       |
|                         'JURIDICO')    |
|     created_at   : TIMESTAMP           |
+----------------------------------------+
```

## 8. METODOLOGIA DE EXECUÇÃO: ROADMAP EM 6 SPRINTS (DUAS SEMANAS CADA)

O cronograma distribui o desenvolvimento ao longo de 12 semanas (6 sprints de 2 semanas cada, com duração total de 84 dias):

| Iteração e Foco                                                            | Metas de Backend e Banco de Dados                                                                                                                                                                                                | Metas de Frontend e Interface                                                                                                                                                              | DevOps e Critérios de Validação                                                                                                                  |
| :------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sprint 1 (Semanas 1 e 2 / Dias 1 a 14):** `Fundação & Auth`              | Setup Spring Boot 3 sob Arquitetura Hexagonal; Migrations Flyway das tabelas `usuario` e `endereco` (com recorte territorial minimizado); Spring Security com JWT stateless; Endpoints de registro e login com BCrypt.           | Setup React com Vite e Tailwind CSS; Contexto de autenticação (`AuthContext`); Telas de Login e Cadastro com autopreenchimento territorial integrado ao ViaCEP (sem persistir logradouro). | Ambiente local orquestrado via Docker Compose (`postgres:15-alpine`); Registro e login autenticado com persistência de token no cliente.         |
| **Sprint 2 (Semanas 3 e 4 / Dias 15 a 28):** `Fórum Comunitário`           | Migrations de `topico` e `comentario`; Endpoints de listagem paginada por categorias; Validador de domínio/anotação `@SemPII` via Regex com HTTP 422 contra vazamento de contatos.                                               | Feed do fórum com paginação; Tela de detalhamento de tópicos com submissão de comentários em atualização otimista; Modal para abertura de novos tópicos com selos visuais de voluntários.  | Usuárias conseguem publicar e debater em tópicos comunitários com bloqueio ativo e orientativo a postagens com números de telefone ou CPF.       |
| **Sprint 3 (Semanas 5 e 6 / Dias 29 a 42):** `Vitrine de Enxovais`         | Migrations da tabela `item_doacao`; Endpoints de CRUD de itens de puericultura; Filtros indexados por categoria, estado de conservação, Estado, Município, Bairro e Zona; Integração com SDK Cloudinary.                         | Galeria de itens responsiva com filtros combinados; Formulário "Quero Doar" com upload direto de 1 foto via preset Cloudinary e preview; Tela de detalhes do item.                         | Upload eficiente de imagens com aplicação automática de presets Cloudinary (`f_auto,q_auto,w_500`) e persistência das URLs seguras no banco.     |
| **Sprint 4 (Semanas 7 e 8 / Dias 43 a 56):** `Pedidos de Ajuda`            | Migrations da tabela `pedido_ajuda`; Endpoints para cadastro de pedidos com níveis de urgência (`BAIXA`, `MEDIA`, `ALTA`) e filtro territorial; Endpoint de atendimento direto ("Quero Ajudar").                                 | Mural de pedidos de ajuda com ordenação por urgência/data e filtro por Município/Bairro/Zona; Formulário para necessidades materiais urgentes; Ação "Quero Ajudar" para doadores.          | Mães solo cadastram pedidos emergenciais (ex.: fraldas, fórmulas) e doadores conseguem manifestar intenção de atendimento diretamente.           |
| **Sprint 5 (Semanas 9 e 10 / Dias 57 a 70):** `Match Seguro & Painel`      | Criação de `MatchDoacao` com máquina de estados (duplo aceite); Endpoint de manifestação de interesse; Liberação de link parametrizado do WhatsApp (`wa.me`) pós-aceite; Migrations preparatórias de `conversa`/`mensagem` (V2). | Botão "Quero este Item"; Painel "Minhas Doações e Solicitações" para doadores aprovarem solicitações e ambas as partes acessarem o canal WhatsApp seguro; Gestão de status de conclusão.   | Fluxo completo de match com proteção ativa aos telefones das usuárias; Doações concluídas saem da vitrine geral.                                 |
| **Sprint 6 (Semanas 11 e 12 / Dias 71 a 84):** `Qualidade, CI/CD & Deploy` | Testes de conformidade arquitetural com ArchUnit; Testes de carga com k6 para validação formal de latência (p95 < 300 ms em instâncias aquecidas); Pipeline de CI/CD via GitHub Actions.                                         | Auditoria de acessibilidade e usabilidade móvel (WCAG 2.1 AA e heurísticas para mobile); Ajustes de responsividade em telas a partir de 360 px.                                            | Deploy automatizado da API no Render (Docker), banco PostgreSQL 15+ no Supabase/Neon e frontend na Vercel; Validação de testes de ponta a ponta. |

## 9. CONTRIBUIÇÕES ESPERADAS E CRITÉRIOS DE AVALIAÇÃO ACADÊMICA

Como Trabalho de Conclusão de Curso na modalidade de Relatório Técnico de Software (RTS), o projeto entrega resultados em duas frentes:

1. **Engenharia de Software:** Implementação documentada de Arquitetura Hexagonal verificada por testes automatizados (ArchUnit), moderação de privacidade no domínio e operação em nuvem gratuita por um único desenvolvedor.
2. **Impacto Social:** Disponibilização de uma ferramenta aberta para circulação local de itens de puericultura e acolhimento entre mães solo, em complemento aos serviços públicos de assistência.

A validação técnica abrange testes automatizados dos casos de uso (cadastro, fórum, vitrine, mural e match), aferição de tempo de resposta da API (`p95 < 300 ms` sob carga de 20 usuários simultâneos) e conformidade com os critérios WCAG 2.1 nível AA em telas móveis.

## 10. REFERÊNCIAS BIBLIOGRÁFICAS

ARAÚJO, Maria Helena Pereira de Oliveira; AMORIM, Betânia Maria Oliveira de. Contos de dor, amor e alegria: representações sociais da maternidade solo. **Psicologia & Sociedade**, v. 37, e289724, 2025. DOI: [10.1590/1807-0310/2025v37289724](http://dx.doi.org/10.1590/1807-0310/2025v37289724).

ARPEN-BRASIL. Associação Nacional dos Registradores de Pessoas Naturais. **Portal da Transparência do Registro Civil: Painel Pais Ausentes**, 2025. Disponível em: <https://transparencia.registrocivil.org.br>. Acesso em: 15 fev. 2026.

ÁVILA, Maria Betânia; FERREIRA, Verônica. Trabalho produtivo e reprodutivo no cotidiano das mulheres brasileiras. _In:_ ÁVILA, M. B.; FERREIRA, V. (Orgs.). **Trabalho remunerado e trabalho doméstico no cotidiano das mulheres**. Recife: SOS CORPO, 2014. p. 13-50.

BRASIL. **Lei nº 10.406, de 10 de janeiro de 2002**. Institui o Código Civil. Brasília, DF: Presidência da República, 2002.

BRASIL. **Lei nº 13.709, de 14 de agosto de 2018**. Lei Geral de Proteção de Dados Pessoais (LGPD). Brasília, DF: Presidência da República, 2018.

BRASIL. **Lei nº 15.069, de 23 de dezembro de 2024**. Institui a Política Nacional de Cuidados. Brasília, DF: Presidência da República, 2024.

FEIJÓ, Janaína. **Mães solo no mercado de trabalho crescem 1,7 milhão em dez anos**. Blog do IBRE/FGV, 2023. Disponível em: <https://blogdoibre.fgv.br>. Acesso em: 10 fev. 2026.

HIRATA, Helena; KERGOAT, Danièle. Novas configurações da divisão sexual do trabalho. **Cadernos de Pesquisa**, v. 37, n. 132, p. 595-609, 2007.

IBGE. Instituto Brasileiro de Geografia e Estatística. **Censo Demográfico 2022: Domicílios e composições familiares**. Rio de Janeiro: IBGE, 2023.

MACHADO, Mônica Sperb; PEREIRA, Caroline Rubin Rossato. Redes Pessoais Significativas de mulheres responsáveis por famílias monoparentais em vulnerabilidade social. **Estudos de Psicologia (Natal)**, v. 25, n. 4, p. 399-411, 2020. DOI: [10.22491/1678-4669.20200040](https://doi.org/10.22491/1678-4669.20200040).

MENDONÇA, Laura Nascimento. **O panorama da monoparentalidade feminina no Brasil: reflexos das leis da guarda compartilhada (13.058/14) e de alimentos (5.478/68)**. 2023. 27 f. Trabalho de Conclusão de Curso (Graduação em Direito) – Faculdade de Direito, Universidade Federal de Uberlândia, Uberlândia, 2023.

SAFFIOTI, Heleieth Iara Bongiovani. **Gênero, patriarcado, violência**. 2. ed. São Paulo: Expressão Popular / Fundação Perseu Abramo, 2015.

SOUSA, Andreyna Karollayne Saraiva de. **Maternidade solo no Brasil: determinantes sociais da divisão desigual das responsabilidades parentais**. 2025. 40 f. Trabalho de Conclusão de Curso (Graduação em Serviço Social) – Centro de Ciências Sociais Aplicadas, Universidade Federal do Rio Grande do Norte, Natal, 2025.

SOUZA, Beatriz Duarte de; JANUÁRIO, Laila Siqueira Ribeiro; LIMA, João Pedro de Amorim Lucena; TEIXEIRA, Keuler Hissa. **Mães solo e desigualdades sociais: uma análise regional e educacional no Brasil**. 2024. 23 f. Trabalho de Conclusão de Curso (Graduação em Ciências Econômicas) – Faculdade de Economia, Administração e Contabilidade, Universidade Federal de Alagoas (UFAL), Maceió, 2024.

SOUZA, Sandro César Iunes; FRANCO, Jader Gama; GOMES, Marcos Roberto. Maternidade solo e interações de gênero: fatores agravantes das desigualdades salariais no Brasil? **A Economia em Revista - AERE**, v. 30, n. 3, p. 63-76, 2022.

TOLEDO, Laise Regina Di Maio Campos; MARTINS, Rovena Zanotti Mendes; FERREIRA, Vanessa Fabri. As determinações sócio-históricas na configuração das famílias monoparentais chefiadas por mulheres em situação de vulnerabilidade social. _In:_ **Anais do XVII Congresso Brasileiro de Assistentes Sociais (CBAS)**, p. 1-13, 2022.

ZANELLO, Valeska. **Saúde mental, gênero e dispositivos: cultura e processos de subjetivação**. Curitiba: Editora Appris, 2020.
