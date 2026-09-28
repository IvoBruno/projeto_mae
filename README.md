# Instituto Federal do Piauí (IFPI) - Campus Parnaíba

## PROJETO MÃE: REDE DIGITAL SOLIDÁRIA DE APOIO A MÃES SOLO

### Articulação entre Engenharia de Software, Suporte Comunitário e Mitigação de Vulnerabilidades na Economia do Cuidado

**Autor:** Ivo Bruno Gomes Araujo  
**Orientador(a):** Prof. Dr. Antonio Santos de Sousa  
**Área de Concentração:** Engenharia de Software Aplicada / Sistemas Colaborativos de Impacto Social

## 1. CONTEXTUALIZAÇÃO E MOTIVAÇÃO SOCIAL

De acordo com os microdados do Censo Demográfico do Instituto Brasileiro de Geografia e Estatística (IBGE, 2022) e levantamentos da Fundação Getúlio Vargas (FGV IBRE, 2023), o Brasil possui mais de 10,3 milhões de lares monoparentais chefiados exclusivamente por mulheres, em contraste expressivo com apenas 1,6 milhão sob responsabilidade paterna exclusiva. Essa configuração demográfica reflete uma disparidade estrutural: as mulheres dedicam, em média, o dobro de horas semanais aos afazeres domésticos e cuidados em relação aos homens, auferindo rendimentos cerca de 20,9% a 30% inferiores aos salários masculinos.

Conforme demonstrado nos atendimentos sociojurídicos do Núcleo Cível da Defensoria Pública e nas análises de Sousa (2025), a sobrecarga enfrentada por famílias monoparentais decorre da naturalização do abandono paterno (com mais de 730 mil registros sem o nome do pai no último quinquênio, segundo a ARPEN-Brasil) e da constante inadimplência na prestação de alimentos. Em cenários de desemprego ou trabalho informal do genitor, a via judicial da prisão civil por dívida alimentar torna-se insuficiente para suprir as urgências imediatas de subsistência infantil.

Como consequência, as mães solo — majoritariamente pretas e pardas das periferias urbanas — enfrentam uma precariedade material crônica, dependendo da complementação de renda via programas de transferência como o Bolsa Família (PBF) e de redes de apoio informais que, por sua vez, encontram-se restritas e sobrecarregadas por outras mulheres da família (avós, irmãs e filhas mais velhas).

## 2. O PROBLEMA DE PESQUISA E A SOLUÇÃO TECNOLÓGICA

Diante do esgotamento das redes de parentesco tradicionais e da carência de equipamentos públicos universais de acolhimento e suporte infantil, coloca-se a seguinte questão de pesquisa:

> **Como um sistema computacional desacoplado, seguro e georreferenciado pode facilitar a conexão entre mães solo, doadores de insumos materiais de primeira necessidade e redes solidárias locais, mitigando a carência material imediata e o isolamento socioafetivo?**

O **Projeto Mãe** responde a essa problemática ao conceber uma plataforma web responsiva orientada a dois módulos operacionais complementares:

1. **Vitrine Colaborativa de Insumos e Enxovais:** Catálogo digital de doações de artigos de puericultura e itens de higiene infantil (berços, roupas, carrinhos, fraldas e fórmulas), permitindo manifestação de interesse orientada por geolocalização e proximidade espacial.
2. **Fórum Comunitário Temático e de Acolhimento:** Ambiente dialógico para troca de experiências, orientações práticas cotidianas, desabafos e elucidação de dúvidas sociojurídicas básicas, dotado de filtros ativos de proteção à privacidade das usuárias.

## 3. OBJETIVOS DO TRABALHO

### 3.1 Objetivo Geral

Conceber, arquitetar, implementar e validar o Produto Mínimo Viável (MVP) de uma aplicação web desacoplada voltada ao fortalecimento da rede de suporte a mães solo, provendo mecanismos seguros de catalogação de doações de enxovais infantis e mediação comunitária com foco em usabilidade e proteção de dados pessoais.

### 3.2 Objetivos Específicos

- Modelar uma arquitetura multicamadas RESTful fundamentada em Java com Spring Boot no backend e React no frontend (Single-Page Application).
- Estruturar o banco de dados relacional (PostgreSQL) com suporte a tipos geométricos espaciais (PostGIS) para futuros filtros de proximidade quilométrica.
- Estabelecer controles de privacidade e moderação de conteúdo (PII Scrubber via Regex) para impedir a exposição pública de dados sensíveis de contato nos fóruns.
- Viabilizar integração pragmática de armazenamento e manipulação de mídia em nuvem (Cloudinary) para compressão e exibição otimizada de imagens de doações.
- Conduzir o desenvolvimento iterativo sob práticas ágeis adaptadas ao contexto de desenvolvedor solo, fatiando a entrega em 4 sprints quinzenais estruturadas.

## 4. FUNDAMENTAÇÃO TEÓRICA E INTERSECCIONALIDADE

A fundamentação teórica deste projeto articula contribuições da Sociologia, Serviço Social e Psicologia Social, demonstrando que a condição da maternidade solo no Brasil não é um desvio de comportamento individual, mas um fenômeno sociopolítico estruturado:

- **Divisão Sexual do Trabalho e o Dispositivo Materno:** Fundamentada em Saffioti (2015), Hirata e Kergoat (2007) e Zanello (2020), a análise demonstra como o patriarcado e a organização capitalista delegam à mulher o trabalho reprodutivo não remunerado (economia do cuidado). Esse processo naturaliza o sacrifício e o confinamento da mãe no espaço doméstico enquanto exime o homem das responsabilidades parentais cotidianas.
- **Marcadores Sociais da Diferença e Interseccionalidade:** Conforme os estudos empíricos com microdados da PNADC (Duarte et al.; Souza et al., 2022) e Toledo et al. (2022), a maternidade solo brasileira possui cor, classe e território definidos. Mulheres pretas e pardas, residentes em periferias urbanas e com baixa escolaridade, apresentam as maiores razões de chance (_odds ratio_) de chefiar lares monoparentais em situação de extrema vulnerabilidade social e dependência do Bolsa Família.
- **Representações Sociais e Redes Pessoais Significativas:** Araújo e Amorim (2025) e Machado e Pereira (2020) evidenciam a ambivalência da vivência materna entre o mito da "mulher guerreira" e o sofrimento gerado pela sobrecarga física e mental. A quebra ou inexistência de redes de apoio externas consolida o isolamento social, tornando urgente o desenvolvimento de artefatos sociotécnicos capazes de rearticular o tecido comunitário de solidariedade.

## 5. DECISÕES ARQUITETURAIS E STACK TECNOLÓGICA

Para atender às restrições de um ciclo de desenvolvimento conduzido por um único programador fullstack, priorizou-se uma pilha tecnológica de alta produtividade, tipagem estática confiável no servidor e ecossistema maduro:

| Camada / Componente              | Tecnologia Selecionada                        | Justificativa Técnica no Projeto                                                                                                                                   |
| :------------------------------- | :-------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Backend Framework**            | Java 17+ / Spring Boot 3                      | Robustez na tipagem, ecossistema corporativo sólido, inversão de controle e facilidade de gestão de regras de negócio com Spring Data JPA e Bean Validation.       |
| **Segurança & Sessão**           | Spring Security + JWT                         | Autenticação _stateless_ com tokens seguros, criptografia de senhas com BCrypt e isolamento de permissões com Role-Based Access Control (RBAC).                    |
| **Frontend SPA**                 | React.js (Vite) + Tailwind CSS                | Alta performance no processo de _build_, ecossistema de componentes reutilizáveis e estilização utilitária ágil com foco em acessibilidade e responsividade móvel. |
| **Gerenciamento de Formulários** | React Hook Form + Zod                         | Validação declarativa de esquemas no cliente, impedindo requisições inválidas e proporcionando feedback imediato de preenchimento.                                 |
| **Banco de Dados Relacional**    | PostgreSQL 15+ com PostGIS                    | Integridade referencial estrita (ACID), suporte a esquemas complexos e capacidade de cálculo geométrico nativo (`ST_DWithin`) para proximidade.                    |
| **Armazenamento de Mídia**       | Cloudinary CDN                                | Upload direto via _unsigned presets_, transformações de imagem na URL (`f_auto,q_auto,w_500`), reduzindo o consumo de banda e o processamento no backend.          |
| **Infraestrutura / Deploy**      | Render / Railway (Back e DB) + Vercel (Front) | Baixa complexidade operacional de CI/CD, provimento simplificado de certificados SSL e custos contidos em camadas gratuitas de validação.                          |

## 6. SEGURANÇA COMUNITÁRIA E CONFORMIDADE COM A LGPD

Em virtude do público-alvo envolver mulheres que vivenciam litígios judiciais, histórico de violência doméstica ou vulnerabilidade socioeconômica, a plataforma adota o princípio de _Privacy by Design_:

1. **Filtro de Conteúdo e Moderação de PII (Personally Identifiable Information):** O backend implementa interceptores e validadores customizados via expressões regulares (Regex) para identificar e rejeitar automaticamente publicações no fórum que contenham números de telefone, CPFs ou endereços completos. As usuárias são instruídas a manter os diálogos públicos focados em acolhimento.
2. **Estratégia de Match Seguro:** No MVP, a conexão entre doador e recebedora é originada pela criação de um registro na entidade `MatchDoacao`. Ao manifestar interesse, a receptora recebe um link parametrizado para o WhatsApp do doador (`wa.me/55...`), assegurando que contatos não fiquem expostos no mural geral.

## 7. MODELAGEM CONCEITUAL DE DADOS (DER LÓGICO)

O diagrama abaixo ilustra o relacionamento relacional do sistema, contemplando a fundação dos módulos de autenticação, catálogo de itens, tópicos comunitários e a preparação para o canal de mensageria:

```
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
|               ENDERECO                 |     |      ITEM_DOACAO      |     |    PEDIDO_AJUDA     |
+----------------------------------------+     +-----------------------+     +--------------------+
| PK  id           : UUID                |     | PK  id          : UUID|     | PK  id       : UUID|
| FK  usuario_id   : UUID                |     | FK  doador_id   : UUID|     | FK  mae_id   : UUID|
|     cep          : VARCHAR(9)          |     |     titulo      : VC  |     |     titulo   : VC  |
|     logradouro   : VARCHAR(200)        |     |     descricao   : TEXT|     |     necessid : TEXT|
|     bairro       : VARCHAR(100)        |     |     categoria   : ENUM|     |     urgencia : ENUM|
|     cidade       : VARCHAR(100)        |     |     conservacao : ENUM|     |     status   : ENUM|
|     estado       : VARCHAR(2)          |     |     foto_url    : VC  |     |     criado_em: TIME|
|     coordenadas  : GEOMETRY(Point)     |     |     status      : ENUM|     +--------------------+
+----------------------------------------+     |     created_at  : TIME|
                                               +-----------------------+
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

## 8. METODOLOGIA DE EXECUÇÃO: ROADMAP EM SPRINTS QUINZENAIS

O cronograma do projeto distribui as metas técnicas ao longo de 60 dias de desenvolvimento estruturado (4 iterações de 15 dias):

| Iteração e Foco                                      | Metas de Backend e Banco de Dados                                                                                                             | Metas de Frontend e Interface                                                                                                              | DevOps e Critérios de Validação                                                                                                      |
| :--------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------- |
| **Sprint 1 (Dias 1 a 15)**<br>`Fundação & Auth`      | Setup Spring Boot 3; Migrations Flyway das tabelas `usuario` e `endereco`; Spring Security com JWT; Endpoints de registro e login com BCrypt. | Setup React com Vite e Tailwind; Contexto de autenticação (`AuthContext`); Telas de Login e Cadastro integradas ao serviço ViaCEP.         | Ambiente de desenvolvimento local orquestrado via Docker Compose; Registro e login autenticado com persistência de token no cliente. |
| **Sprint 2 (Dias 16 a 30)**<br>`Fórum Comunitário`   | Migrations de `topico` e `comentario`; Endpoints de listagem paginada por categorias; Sanitização PII via regex contra vazamento de contatos. | Feed do fórum com paginação; Tela de detalhamento de tópicos com respostas em tempo real; Modal para abertura de novos tópicos.            | Usuárias conseguem publicar e debater em tópicos comunitários com bloqueio ativo a postagens com números de telefone ou CPF.         |
| **Sprint 3 (Dias 31 a 45)**<br>`Vitrine de Enxovais` | Migrations de `item_doacao` e `pedido_ajuda`; Integração com SDK Cloudinary; Endpoints de CRUD de itens e pedidos de urgência.                | Galeria de itens com filtros de categoria e estado de conservação; Formulário "Quero Doar" com upload e preview de foto; Mural de pedidos. | Upload eficiente de imagens com aplicação automática de presets Cloudinary (`f_auto,q_auto`) e persistência das URLs no banco.       |
| **Sprint 4 (Dias 46 a 60)**<br>`Match & Deploy MVP`  | Criação de `MatchDoacao`; Endpoint de manifestação de interesse; Migrations das tabelas `conversa`/`mensagem` (suporte à V2).                 | Botão "Quero este Item" com redirecionamento formatado ao WhatsApp (`wa.me`); Painel "Minhas Doações e Solicitações".                      | Deploy do PostgreSQL (Supabase/Render), backend (Render/Railway) e frontend (Vercel); Execução de testes de ponta a ponta.           |

## 9. CONTRIBUIÇÕES ESPERADAS E CRITÉRIOS DE AVALIAÇÃO ACADÊMICA

Como Trabalho de Conclusão de Curso na modalidade de Relato Técnico de Software, o projeto gerará contribuições em dois planos principais:

1. **Plano Tecnológico / Computacional:** Documentação de padrões arquiteturais sólidos no contexto de desenvolvedor solo, detalhando decisões de escalabilidade, estratégias de moderação de privacidade via software e práticas de integração contínua e deploy de baixo custo.
2. **Plano Social e Comunitário:** Disponibilização de uma tecnologia social funcional focada nas dores materiais e afetivas da maternidade monoparental, operando como instrumento complementar às redes de assistência pública.

A avaliação do software basear-se-á em testes funcionais dos casos de uso de cadastro, publicação e doação, medição do tempo médio de resposta dos endpoints da API (`< 300 ms`) e conformidade com as heurísticas de usabilidade para interfaces web móveis.

## 10. REFERÊNCIAS BIBLIOGRÁFICAS

ARAÚJO, Maria Helena Pereira de Oliveira; AMORIM, Betânia Maria Oliveira de. Contos de dor, amor e alegria: representações sociais da maternidade solo. **Psicologia & Sociedade**, v. 37, e289724, 2025. DOI: [10.1590/1807-0310/2025v37289724](http://dx.doi.org/10.1590/1807-0310/2025v37289724).

ARPEN-BRASIL. Associação Nacional dos Registradores de Pessoas Naturais. **Portal da Transparência do Registro Civil: Painel Pais Ausentes**, 2022. Disponível em: <https://transparencia.registrocivil.org.br>. Acesso em: 15 fev. 2026.

ÁVILA, Maria Betânia; FERREIRA, Verônica. Trabalho produtivo e reprodutivo no cotidiano das mulheres brasileiras. _In:_ ÁVILA, M. B.; FERREIRA, V. (Orgs.). **Trabalho remunerado e trabalho doméstico no cotidiano das mulheres**. Recife: SOS CORPO, 2014. p. 13-50.

BRASIL. **Lei nº 10.406, de 10 de janeiro de 2002**. Institui o Código Civil. Brasília, DF: Presidência da República, 2002.

BRASIL. **Lei nº 13.709, de 14 de agosto de 2018**. Lei Geral de Proteção de Dados Pessoais (LGPD). Brasília, DF: Presidência da República, 2018.

BRASIL. **Lei nº 15.069, de 23 de dezembro de 2024**. Institui a Política Nacional de Cuidados. Brasília, DF: Presidência da República, 2024.

DUARTE, Beatriz; JANUÁRIO, Laila; LUCENA, João; HISSA, Keuler. **Maternidade solo no Brasil: uma análise dos seus determinantes a partir de um modelo Logit**. Trabalho de Conclusão de Curso (Graduação em Ciências Econômicas) – Faculdade de Economia, Administração e Contabilidade, Universidade Federal de Alagoas (UFAL), Maceió, 2024.

FEIJÓ, Janaína. **Mães solo no mercado de trabalho crescem 1,7 milhão em dez anos**. Blog do IBRE/FGV, 2023. Disponível em: <https://blogdoibre.fgv.br>. Acesso em: 10 fev. 2026.

HIRATA, Helena; KERGOAT, Danièle. Novas configurações da divisão sexual do trabalho. **Cadernos de Pesquisa**, v. 37, n. 132, p. 595-609, 2007.

IBGE. Instituto Brasileiro de Geografia e Estatística. **Censo Demográfico 2022: Domicílios e composições familiares**. Rio de Janeiro: IBGE, 2023.

MACHADO, Mônica Sperb; PEREIRA, Caroline Rubin Rossato. Redes Pessoais Significativas de mulheres responsáveis por famílias monoparentais em vulnerabilidade social. **Estudos de Psicologia (Natal)**, v. 25, n. 4, p. 399-411, 2020. DOI: [10.22491/1678-4669.20200040](https://doi.org/10.22491/1678-4669.20200040).

MENDONÇA, Laura Nascimento. **O panorama da monoparentalidade feminina no Brasil: reflexos das leis da guarda compartilhada (13.058/14) e de alimentos (5.478/68)**. 2023. 27 f. Trabalho de Conclusão de Curso (Graduação em Direito) – Faculdade de Direito, Universidade Federal de Uberlândia, Uberlândia, 2023.

SAFFIOTI, Heleieth Iara Bongiovani. **Gênero, patriarcado, violência**. 2. ed. São Paulo: Expressão Popular / Fundação Perseu Abramo, 2015.

SOUSA, Andreyna Karollayne Saraiva de. **Maternidade solo no Brasil: determinantes sociais da divisão desigual das responsabilidades parentais**. 2025. 40 f. Trabalho de Conclusão de Curso (Graduação em Serviço Social) – Centro de Ciências Sociais Aplicadas, Universidade Federal do Rio Grande do Norte, Natal, 2025.

SOUZA, Sandro César Iunes; FRANCO, Jader Gama; GOMES, Marcos Roberto. Maternidade solo e interações de gênero: fatores agravantes das desigualdades salariais no Brasil? **A Economia em Revista - AERE**, v. 30, n. 3, p. 63-76, 2022.

TOLEDO, Laise Regina Di Maio Campos; MARTINS, Rovena Zanotti Mendes; FERREIRA, Vanessa Fabri. As determinações sócio-históricas na configuração das famílias monoparentais chefiadas por mulheres em situação de vulnerabilidade social. _In:_ **Anais do XVII Congresso Brasileiro de Assistentes Sociais (CBAS)**, p. 1-13, 2022.

ZANELLO, Valeska. **Saúde mental, gênero e dispositivos: cultura e processos de subjetivação**. Curitiba: Editora Appris, 2020.
