# INSTITUTO FEDERAL DE EDUCAÇÃO, CIÊNCIA E TECNOLOGIA DO PIAUÍ

CAMPUS PARNAÍBA

CURSO DE TECNOLOGIA EM ANÁLISE E DESENVOLVIMENTO DE SISTEMAS

IVO BRUNO GOMES ARAUJO

ELOMATERNO: REDE DIGITAL SOLIDÁRIA DE APOIO A MÃES SOLO

Concepção, Arquitetura Hexagonal e Validação de um Artefato Sociotécnico Seguro para Circulação de Enxovais e Suporte Comunitário

PARNAÍBA - PI

2026

IVO BRUNO GOMES ARAUJO

ELOMATERNO: REDE DIGITAL SOLIDÁRIA DE APOIO A MÃES SOLO

Concepção, Arquitetura Hexagonal e Validação de um Artefato Sociotécnico Seguro para Circulação de Enxovais e Suporte Comunitário

Proposta de Trabalho de Conclusão de Curso (Pré-Projeto de Pesquisa e Desenvolvimento de Software) apresentada à Coordenação do Curso de Informática do Instituto Federal de Educação, Ciência e Tecnologia do Piauí (IFPI) – Campus Parnaíba, como requisito parcial para aprovação na disciplina de TCC 1 e homologação do plano de execução do Relatório Técnico de Software (RTS).

Área de Concentração: Engenharia de Software Aplicada / Sistemas Colaborativos e Tecnologias Sociais.

Linha de Pesquisa: Arquitetura de Software, Segurança da Informação e Sistemas de Informação de Impacto Social.

Orientador: Prof. Me. Antonio Santos de Sousa

PARNAÍBA - PI

2026

## SUMÁRIO

1. [IDENTIFICAÇÃO DO TEMA E DELIMITAÇÃO](#1-identificação-do-tema-e-delimitação)
2. [PROBLEMATIZAÇÃO E QUESTÃO NORTEADORA](#2-problematização-e-questão-norteadora)
3. [JUSTIFICATIVA E RELEVÂNCIA SOCIOTÉCNICA](#3-justificativa-e-relevância-sociotécnica)

- 3.1 [Relevância Social e Empírica](#31-relevância-social-e-empírica)
- 3.2 [Relevância Científica e Tecnológica](#32-relevância-científica-e-tecnológica)

4. [OBJETIVOS DO TRABALHO](#4-objetivos-do-trabalho)

- 4.1 [Objetivo Geral](#41-objetivo-geral)
- 4.2 [Objetivos Específicos](#42-objetivos-específicos)

5. [REFERENCIAL TEÓRICO PRELIMINAR](#5-referencial-teórico-preliminar)

- 5.1 [A Maternidade Solo no Brasil e a Economia do Cuidado](#51-a-maternidade-solo-no-brasil-e-a-economia-do-cuidado)
- 5.2 [O Paradigma da Tecnologia Social e Redes Colaborativas (RTS)](#52-o-paradigma-da-tecnologia-social-e-redes-colaborativas-rts)
- 5.3 [Arquitetura Hexagonal (Ports & Adapters) e Blindagem de Domínio](#53-arquitetura-hexagonal-ports--adapters-e-blindagem-de-domínio)
- 5.4 [Privacidade por Padrão (Privacy by Design) e a LGPD](#54-privacidade-por-padrão-privacy-by-design-e-a-lgpd)

6. [METODOLOGIA E PROCEDIMENTOS TÉCNICOS PROPOSTOS](#6-metodologia-e-procedimentos-técnicos-propostos)

- 6.1 [Classificação e Enquadramento Metodológico](#61-classificação-e-enquadramento-metodológico)
- 6.2 [Ciclo de Desenvolvimento Ágil Adaptado (6 Sprints Quinzenais)](#62-ciclo-de-desenvolvimento-ágil-adaptado-6-sprints-quinzenais)
- 6.3 [Levantamento Preliminar de Requisitos (RFs e RNFs)](#63-levantamento-preliminar-de-requisitos-rfs-e-rnfs)
- 6.4 [Arquitetura e Pilha Tecnológica Selecionada](#64-arquitetura-e-pilha-tecnológica-selecionada)
- 6.5 [Procedimentos de Teste e Garantia da Qualidade](#65-procedimentos-de-teste-e-garantia-da-qualidade)

7. [RECURSOS MATERIAIS E ORÇAMENTO PREVISTO](#7-recursos-materiais-e-orçamento-previsto)
8. [CRONOGRAMA DE EXECUÇÃO FÍSICA](#8-cronograma-de-execução-física)
9. [RESULTADOS ESPERADOS E ENTREGÁVEIS](#9-resultados-esperados-e-entregáveis)

- [REFERÊNCIAS](#referências)

---

## 1 IDENTIFICAÇÃO DO TEMA E DELIMITAÇÃO

A análise dos dados sobre a maternidade no Brasil chama atenção para o crescimento contínuo das chamadas “mães solo”. Esse grupo é definido por Souza et al. (2024, p. 2) como “famílias monoparentais, compostas por apenas um dos genitores no papel de responsável pela criação, manutenção e educação dos filhos. Embora possam ser chefiadas tanto por homens quanto por mulheres, são as mulheres que predominam amplamente nesse tipo de arranjo, dando origem à configuração denominada família monoparental feminina, ou, em termos mais recentes, ‘mãe solo’”.

Segundo levantamento de Feijó (2023), “entre os anos de 2012 e 2022, o número de domicílios com mães solo [no Brasil] cresceu 17,8%, passando de 9,6 milhões para 11,3 milhões”. Essa realidade também se reflete no Piauí. Dados do módulo Pais Ausentes, mantido pelo Portal da Transparência do Registro Civil (ARPEN-Brasil, 2026), mostram que 7,5% dos nascimentos em 2024 e 7,8% em 2025 foram registrados apenas com o nome da mãe. Ao longo da última década, o estado acumulou mais de 22 mil crianças sem o nome do pai na certidão, o que dimensiona a quantidade de mulheres e filhos afetados pelo abandono paterno.

Diante desse quadro, cabe buscar alternativas práticas que ajudem a amenizar os danos causados pela falta de uma rede de apoio. Como o problema tem raízes estruturais, ele não admite soluções isoladas, já que, ainda segundo Souza et al. (2024, p. 1), “os resultados indicam que a maternidade solo está relacionada a desigualdades de natureza racial, educacional e territorial, e identificam-se contrastes importantes entre contextos urbanos e rurais, bem como entre diferentes níveis de instrução”.

## 2 PROBLEMATIZAÇÃO E QUESTÃO NORTEADORA

O período de gestação e puerpério traz mudanças físicas e psicológicas intensas para a mulher. Como explicam Brito, Almeida Junior e Medeiros (2022, p. 692), “o puerpério é caracterizado como uma fase de transição na vida da mulher, que a torna vulnerável diante da presença de inúmeros desafios físicos e biopsicossociais, como alterações corporais, hormonais, preocupações e inseguranças”. Por conta disso, existe uma necessidade clara de suporte à mãe durante os primeiros anos da criança, sobretudo quando essa mulher se encontra em condição de vulnerabilidade social e cria os filhos sozinha.

Ao observar a realidade do Piauí e, mais especificamente, do município de Parnaíba, os indicadores do Instituto Brasileiro de Geografia e Estatística (IBGE) ajudam a traçar o perfil dessa comunidade. De acordo com o Censo Demográfico (IBGE, 2023), Parnaíba tem 162.159 habitantes. É o segundo município mais populoso do estado e o principal polo urbano da Planície Litorânea. No cenário estadual, as mulheres já respondem pela chefia da maioria dos domicílios (50,36%, um salto de 11,61 pontos percentuais em comparação aos 38,75% de 2010), e cerca de 18,11% dos lares são formados por mães solo com seus filhos (IBGE, 2023). Além disso, Parnaíba tem o segundo maior volume de atendimento do Programa Bolsa Família no Piauí, com média de 18,5 mil famílias atendidas (18.549 registros em 2024), atrás somente da capital Teresina (IBGE, 2024).

Apesar dessa demanda expressiva no município, o apoio comunitário e a doação de itens infantis ainda acontecem de maneira dispersa, muitas vezes restritos a grupos informais em redes sociais abertas. Nesses ambientes, a mãe solo que precisa pedir ajuda com fraldas, leite ou enxoval acaba exposta. Faltam garantias mínimas de privacidade e organização dos pedidos.

A partir desse cenário, define-se a seguinte questão norteadora para o trabalho: **como desenvolver um aplicativo móvel seguro, baseado em Arquitetura Hexagonal e privacidade de dados, que facilite a doação de itens infantis e o apoio mútuo entre mães solo em Parnaíba-PI?**

## 3 JUSTIFICATIVA E RELEVÂNCIA SOCIOTÉCNICA

### 3.1 Relevância Social e Empírica

A proposta do aplicativo divide-se em duas frentes principais de atuação social. A primeira refere-se ao fórum comunitário, no qual será possível criar tópicos sobre assuntos específicos da maternidade ou publicar dúvidas para debate com os demais membros da plataforma. O objetivo desse espaço é funcionar como uma rede de apoio direta para as mães solo. Ali ocorrerá a interação tanto com outras mulheres em situações similares quanto com especialistas voluntários dispostos a repassar orientações técnicas. O intuito principal é gerar conexão interpessoal, conforme defendido por Brito, Almeida Junior e Medeiros (2022, p. 692): "Nessa perspectiva, os suportes online, ou apoio social virtual, podem ser procurados como uma alternativa aos grupos de apoio tradicionais, presenciais, por serem mais acessíveis. Tais grupos online geralmente têm um modus operandi que privilegia a interação entre usuários e a aprendizagem colaborativa".

A segunda frente abrange o painel Vitrine de Doações e Pedidos de Ajuda, voltado a centralizar a oferta de itens para doação e os pedidos de materiais necessários às mães e seus filhos. Essa funcionalidade justifica-se pelos dados do IBGE sobre o alto volume de famílias beneficiárias do Programa Bolsa Família em Parnaíba, voltado a pessoas em situação de vulnerabilidade social. Para manter a simplicidade e a segurança das usuárias, o contato final ocorre fora da plataforma. Como o sistema não possui chat interno, o número de telefone é direcionado ao aplicativo WhatsApp somente quando ambas as partes concordam com a doação.

### 3.2 Relevância Científica e Tecnológica

Em grupos de WhatsApp e Facebook já usados pela comunidade, quem pede ou oferece doações acaba expondo o próprio número de telefone para desconhecidos. O EloMaterno resolve esse problema ao adotar a política de _Privacy by Design_ e tratar a proteção de dados como requisito desde o início do projeto. Como apontam Moura e Coutinho (2024, p. 3), "a elicitação dos requisitos de software que precisam estar em conformidade com a LGPD no início do processo é algo essencial". Por conta disso, o acesso à plataforma é controlado por tokens JWT e perfis de permissão (Buçko et al., 2023), enquanto a localização dos itens considera apenas estado, município e bairro. O telefone das usuárias fica oculto no sistema e o redirecionamento para o WhatsApp só ocorre quando as duas partes aceitam a doação.

Outro ponto abordado no trabalho é o uso da Arquitetura Hexagonal (_Ports and Adapters_) junto com testes automatizados. Em uma análise de 83 projetos desenvolvidos por estudantes, De Luca et al. (2025) identificaram que um dos erros mais comuns no meio acadêmico é misturar a camada de tela diretamente com o código de banco de dados, o que dificulta a manutenção. Para evitar essa falha, o núcleo de regras de negócio do EloMaterno fica separado das ferramentas externas (Rayarao; Dhone; Narzullaeva, 2026) e as rotas da API passam por testes de unidade e integração que verificam as respostas do servidor (Baniaș et al., 2021).

Por fim, o código-fonte aberto e a documentação técnica permitem que a própria comunidade e outros estudantes da área de tecnologia usem o sistema como base para novos trabalhos. Além de rodar em serviços gratuitos de nuvem, o projeto deixa uma estrutura pronta para quem quiser evoluir a ferramenta no futuro.

## 4 OBJETIVOS DO TRABALHO

### 4.1 Objetivo Geral

Desenvolver um aplicativo móvel voltado à criação de uma rede digital de apoio para mães solo em Parnaíba-PI, com recursos para a doação e solicitação de itens essenciais aos primeiros anos da criança (como móveis, enxovais, fórmulas e fraldas) e um fórum seguro para troca de experiências e dúvidas sobre a maternidade, focado na proteção da privacidade das usuárias.

### 4.2 Objetivos Específicos

- Estruturar a API e o aplicativo no padrão de Arquitetura Hexagonal (_Ports and Adapters_) para separar as regras de negócio do banco de dados e da interface;
- Construir o fórum comunitário com suporte à criação de tópicos por categoria, envio de dúvidas e respostas de mães solo e especialistas voluntários;
- Implementar a Vitrine de Doações e Pedidos de Ajuda com busca de itens infantis por estado, município e bairro;
- Criar o mecanismo de aceite mútuo que libera o contato via WhatsApp apenas depois que as duas partes confirmam a doação;
- Testar as rotas da API e as telas principais com testes automatizados de unidade e integração.

## 5 REFERENCIAL TEÓRICO PRELIMINAR

### 5.1 A Maternidade Solo no Brasil e a Economia do Cuidado

A maternidade aplica um peso desigual a mulheres e homens na sociedade, desde a gestação até a criação e suporte financeiro à criança. Conforme afirmado por Sousa (2025), os homens têm a designação prioritária à esfera produtiva, enquanto a esfera reprodutiva recai sobre as mulheres. Ao compararmos essa afirmação com o dado apresentado também por Sousa (2025, p. 28), de que quase metade das mulheres no contexto analisado (47%) não recebe pensão alimentícia ou ajuda financeira dos genitores, e também com o cenário descrito por Souza et al. (2024, p. 5), onde a mulher está sujeita a uma "tripla penalidade" (tempo escasso, renda insuficiente e ausência de redes de apoio efetivas), o panorama para as responsabilidades de criação dos filhos se torna ainda menos otimista.

### 5.2 O Paradigma da Tecnologia Social e Redes Colaborativas (RTS)

Uma das ferramentas mais poderosas à disposição para amenizar, em partes, os problemas enfrentados por mães solo são as interações sociais, ainda que virtuais. Como observado por Brito, Almeida Junior e Medeiros (2022, p. 694), "As mulheres utilizam suas próprias experiências sobre a maternidade na intenção de ajudar outras mulheres, de modo a criar uma rede de apoio (social e emocional), especialmente para as primíparas [mulheres na primeira gestação], proporcionando informação, incentivo e empatia". O contato direto com outros indivíduos que passaram ou passam por situações análogas ajuda a criar um sentimento de comunidade e pertencimento. Além disso, cria um espaço seguro para desabafo e ressignificação de experiências angustiantes, como descrito por Araújo e Amorim (2025, p. 6).

Para além disso, a criação de uma plataforma centralizada que facilita doações tem impacto direto e imediato na qualidade de vida das mães solo inseridas nos demográficos de vulnerabilidade financeira, pois supre, ao menos parcialmente, a lacuna deixada pela falta de renda apropriada e de apoio financeiro por parte dos genitores. Como observam Araújo e Amorim (2025, p. 9), a renda vinda de programas como o Bolsa Família, "ainda que seja essencial para as despesas básicas do lar, não é suficiente", o que torna o apoio de terceiros decisivo para que essas mães tenham acesso a produtos infantis como enxoval, fraldas, fórmulas ou móveis que elas não conseguiriam comprar por conta própria.

### 5.3 Arquitetura Hexagonal (Ports & Adapters) e Blindagem de Domínio

Podemos observar, na forma como os projetos estudantis são comumente estruturados, certa tendência a pontos de atrito arquitetônico que geram, a depender do tamanho e da complexidade do projeto, dificuldade de escalabilidade e manutenibilidade. Segundo De Luca et al. (2025), escolhas inadequadas na estrutura do código geram dívida técnica e queda no desempenho e na confiabilidade, e a partir disso podemos entender a relevância que toma o cuidado e a atenção com esses detalhes de projeto.

Ao nos debruçarmos na tarefa de entender onde esses erros mais aparecem, notamos que há uma predominância na questão tangente ao acoplamento, ou seja, não existe uma divisão clara de qual a responsabilidade de cada componente. Isso acaba levando a cenários como o descrito por De Luca et al. (2025, p. 9), em que 25% dos projetos de alunos analisados colocavam chamadas de banco de dados (DAO) diretamente dentro da interface gráfica (GUI). Este trabalho aborda esse cenário com a aplicação formal e, até certo ponto, rígida dos princípios S.O.L.I.D. e dos padrões de projeto chamados de Arquitetura Hexagonal (Rayarao; Dhone; Narzullaeva, 2026), para diminuir o acoplamento e facilitar tanto a leitura e manutenção do código quanto futuras expansões do escopo geral da aplicação.

### 5.4 Privacidade por Padrão (Privacy by Design) e a LGPD

Observemos a questão da privacidade por dois prismas que podem parecer distintos, mas chegam ao mesmo ponto. O primeiro refere-se ao cuidado necessário com os dados de pessoas em situações de vulnerabilidade econômica e social. Como visto em Araújo e Amorim (2025, p. 11), são frequentes entre mães solo os relatos de "violência doméstica dos tipos física, psicológica, sexual, patrimonial e moral perpetradas pelos ex-companheiros", um dado que pede maior atenção e delicadeza, visto que, ao expor dados sensíveis, corre-se o risco de entregar informações a terceiros mal-intencionados, inclusive ex-parceiros que as usuárias podem estar evitando.

O outro ponto de vista a tratar de segurança é a Lei Geral de Proteção de Dados (LGPD), que legisla sobre a forma como os dados são armazenados e expostos, bem como sobre a clareza para o usuário quanto ao motivo da coleta. Essas diretrizes podem ser, de forma geral, entendidas em Moura e Coutinho (2024, p. 4), quando apontam que "a coleta de dados deve estar associada a uma necessidade ou finalidade específica, bem definida, deve ser clara e estar em conformidade com as diretrizes vigentes na legislação".

## 6 METODOLOGIA E PROCEDIMENTOS TÉCNICOS PROPOSTOS

### 6.1 Classificação e Enquadramento Metodológico

A proposta de Pesquisa Aplicada se enquadra perfeitamente no contexto apresentado, gerando assim um produto prático que pretende resolver, ou ao menos amenizar, um problema real e concreto, especialmente, mas não se restringindo, ao cenário local do município de Parnaíba, no Piauí. Temos em mãos um estudo exploratório e de desenvolvimento experimental, pois parte do estudo do contexto e das dificuldades da maternidade solo e de proteção de dados para projetar e construir um produto mínimo viável (MVP) funcional.

Dentro desse ponto de vista, temos duas abordagens igualmente produtivas: a primeira é a qualitativa, onde são abordadas a pesquisa bibliográfica e documental, juntamente com os dados coletados, através dos quais busca-se traduzir uma demanda social de acolhimento e privacidade. A segunda é quantitativa, ao medir parâmetros como tempo de resposta da API e cobertura de testes, por exemplo.

### 6.2 Ciclo de Desenvolvimento Ágil Adaptado (6 Sprints Quinzenais)

Observando-se o fato de que o desenvolvimento será realizado por apenas um desenvolvedor, foi optado pela adoção de um modelo Scrum/Kanban, com adaptações pertinentes ao escopo e aos recursos disponíveis. Tendo em vista as características citadas, o planejamento se apresenta com a divisão em 6 sprints de duas semanas cada, totalizando 12 semanas de codificação, previstas para abordarem o projeto da seguinte forma:

- _Sprint 1_: Estrutura base em Arquitetura Hexagonal, banco de dados, cadastro com CEP e login (JWT).
- _Sprint 2_: Fórum comunitário (tópicos, respostas e bloqueio automático de telefone/CPF em postagens abertas).
- _Sprint 3_: Vitrine de doações de itens infantis com fotos e filtro por estado, cidade e bairro.
- _Sprint 4_: Mural de pedidos de ajuda para mães solo.
- _Sprint 5_: Fluxo de aceite mútuo da doação e redirecionamento para o WhatsApp.
- _Sprint 6_: Testes automatizados finais, ajustes de desempenho e publicação em nuvem gratuita.

### 6.3 Levantamento Preliminar de Requisitos (RFs e RNFs)

Quadro 1 – Requisitos Funcionais (RF) do MVP EloMaterno

| Código | Requisito                              | Descrição                                                                                                                                                                                                          |
| ------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| RF01   | Cadastro e Autenticação por Perfil     | Permitir o registro e o login de usuárias com atribuição de papéis (`MAE_SOLO`, `DOADOR`, `VOLUNTARIO`, `ADMIN`) e preenchimento territorial via CEP (Estado, Município, Bairro e Zona), sem armazenar logradouro. |
| RF02   | Fórum Comunitário Categorizado         | Permitir a criação de tópicos e comentários organizados por categorias (`DUVIDAS`, `DESABAFO`, `DICAS`, `JURIDICO`) com identificação visual para voluntários.                                                     |
| RF03   | Bloqueio Automático de Dados Sensíveis | Validar no servidor o texto de tópicos e comentários para impedir a publicação acidental de números de telefone, CPFs ou endereços residenciais (retorno HTTP 422).                                                |
| RF04   | Vitrine Colaborativa de Enxovais       | Permitir o cadastro, a listagem e a filtragem de itens infantis para doação por categoria, estado de conservação, Estado, Município, Bairro e Zona, com envio de foto.                                             |
| RF05   | Mural de Pedidos de Ajuda              | Permitir que mães solo publiquem demandas materiais classificadas por nível de urgência (`BAIXA`, `MEDIA`, `ALTA`) e que doadores filtrem esses pedidos por recorte territorial.                                   |
| RF06   | Match de Doação com Aceite Mútuo       | Gerenciar as solicitações de doação (`SOLICITADO`, `EM_NEGOCIACAO`, `CONCLUIDO`, `CANCELADO`) e liberar o link de contato via WhatsApp (`wa.me`) somente após a aprovação do doador.                               |
| RF07   | Exclusão Lógica e Anonimização         | Permitir que a usuária encerre sua conta a qualquer momento, aplicando exclusão lógica e anonimização de seus dados pessoais identificáveis.                                                                       |

Quadro 2 – Requisitos Não Funcionais (RNF) do MVP EloMaterno

| Código | Requisito                                    | Descrição                                                                                                                                                               |
| ------ | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| RNF01  | Isolamento Arquitetural                      | Estruturar o back-end sob Arquitetura Hexagonal (Ports & Adapters), mantendo o domínio desacoplado de frameworks web e de persistência, verificado via ArchUnit.        |
| RNF02  | Autenticação Stateless e Criptografia        | Gerenciar sessões via tokens JWT assinados (HS256) e armazenar senhas com algoritmo de hash BCrypt.                                                                     |
| RNF03  | Privacidade e Minimização Territorial (LGPD) | Restringir a coleta de localização a Estado, Município, Bairro e Zona, sem retenção de rua, número residencial ou coordenadas GPS no banco de dados.                    |
| RNF04  | Desempenho de Consultas                      | Garantir tempo de resposta inferior a 300 ms no percentil 95 (`p95 < 300 ms`) nas listagens paginadas, utilizando índices compostos B-Tree no banco de dados.           |
| RNF05  | Otimização de Mídia e Dados Móveis           | Comprimir e redimensionar automaticamente as imagens enviadas à vitrine via CDN (`f_auto,q_auto,w_500`) para reduzir o consumo de franquia móvel das usuárias.          |
| RNF06  | Responsividade e Acessibilidade Móvel        | Adequar a interface ao padrão mobile-first em telas a partir de 360 px de largura, observando os critérios de contraste e navegação das diretrizes WCAG 2.1 (nível AA). |

### 6.4 Arquitetura e Pilha Tecnológica Selecionada

Quadro 3 – Pilha Tecnológica (Stack) Selecionada para o EloMaterno

| Camada / Componente        | Tecnologia Selecionada                   | Finalidade no Projeto                                                                                                                |
| -------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Arquitetura de Software    | Arquitetura Hexagonal (Ports & Adapters) | Isolamento das regras de negócio e das políticas de privacidade em relação ao banco de dados e aos controladores REST.               |
| Back-end (API REST)        | Java 17+ / Spring Boot 3                 | Construção da API RESTful com tipagem estática, injeção de dependências e validação de regras de domínio.                            |
| Segurança e Sessão         | Spring Security + JWT + BCrypt           | Autenticação stateless, criptografia de credenciais e controle de acesso baseado em papéis (RBAC).                                   |
| Front-end (SPA)            | React.js (Vite) + Tailwind CSS           | Construção de interface reativa, componentizada e responsiva (mobile-first).                                                         |
| Validação de Formulários   | React Hook Form + Zod                    | Validação declarativa de esquemas no navegador com retorno visual imediato antes do envio à API.                                     |
| Banco de Dados e Migrações | PostgreSQL 15+ / Flyway                  | Persistência relacional com suporte a transações ACID, versionamento de esquema e índices B-Tree compostos para buscas territoriais. |
| Armazenamento de Imagens   | Cloudinary CDN                           | Hospedagem externa de fotos dos itens doados com compressão automática na entrega.                                                   |
| Qualidade e Testes         | JUnit 5 + ArchUnit + k6                  | Testes unitários de regras de domínio, verificação automatizada da arquitetura e ensaios de carga da API.                            |
| Infraestrutura e Deploy    | Docker + Render + Supabase/Neon + Vercel | Conteinerização do ambiente local e publicação contínua em serviços de nuvem de camada gratuita (free tier).                         |

### 6.5 Procedimentos de Teste e Garantia da Qualidade

Para que as escolhas arquitetônicas descritas anteriormente não fiquem restritas ao campo teórico, o processo de validação do EloMaterno acompanha cada uma das seis _sprints_ de desenvolvimento. O foco central dessa etapa é impedir que erros de implementação comprometam tanto o isolamento das camadas quanto a proteção dos dados pessoais das mães cadastradas.

Na prática, a verificação do _back-end_ divide-se em duas frentes complementares. A primeira utiliza o JUnit 5 para testar de forma isolada as regras de negócio do domínio, como o filtro que bloqueia números de telefone e CPFs no fórum e a exigência de aceite mútuo antes da liberação do link do WhatsApp, além do ArchUnit para checar se nenhuma classe de tela ou de banco de dados violou os limites da Arquitetura Hexagonal. A segunda frente trata das rotas da API REST, ponto em que, conforme demonstrado por Baniaș et al. (2021), faz-se necessário submeter o servidor tanto a requisições válidas quanto a entradas propositalmente incorretas para confirmar se os códigos de retorno HTTP e o tempo de resposta se comportam dentro do esperado.

Por fim, na última _sprint_, entram os ensaios de desempenho e de interface antes da publicação em nuvem. Com o uso da ferramenta k6, serão simulados acessos simultâneos às listagens da vitrine e do fórum para verificar a meta de resposta abaixo de 300 milissegundos, enquanto a interface móvel passará por checagem de responsividade em telas pequenas e de acessibilidade segundo os critérios da WCAG 2.1.

Quadro 4 – Estratégia de Testes e Critérios de Validação do MVP

| Tipo de Teste                           | Ferramenta                   | Alvo de Verificação                                                                         | Critério de Aceite / Meta                                                                                  |
| --------------------------------------- | ---------------------------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Testes de Unidade                       | JUnit 5                      | Regras de negócio do domínio (`@SemPII`, máquina de estados de `MatchDoacao` e anonimização) | Cobertura mínima de 80% nas classes do núcleo de domínio, sem falhas nas regras críticas de privacidade.   |
| Testes de Arquitetura                   | ArchUnit                     | Isolamento entre o pacote de domínio e os adaptadores externos (REST e JPA)                 | Zero violações de dependência direta entre controladores/interface e camada de banco de dados.             |
| Testes de Integração da API             | Spring Boot Test / MockMvc   | Contratos das rotas REST, autenticação JWT, permissões por perfil e códigos de erro (HTTP 401, 403, 422) | Retorno correto dos códigos HTTP para entradas válidas e bloqueio efetivo de postagens com dados sensíveis. |
| Ensaios de Carga e Desempenho           | k6                           | Consultas paginadas da Vitrine de Doações e do Fórum Comunitário com filtros territoriais   | Tempo de resposta no percentil 95 inferior a 300 ms (`p95 < 300 ms`) sob carga simulada.                   |
| Inspeção de Usabilidade e Acessibilidade | Chrome DevTools / Lighthouse | Telas da aplicação web em resolução móvel (_mobile-first_)                                  | Layout funcional a partir de 360 px de largura e conformidade com os critérios de contraste da WCAG 2.1 (nível AA). |

## 7 RECURSOS MATERIAIS E ORÇAMENTO PREVISTO

## 8 CRONOGRAMA DE EXECUÇÃO FÍSICA

## 9 RESULTADOS ESPERADOS E ENTREGÁVEIS

## REFERÊNCIAS

ARAÚJO, Maria Helena Pereira de Oliveira; AMORIM, Betânia Maria Oliveira de. Contos de dor, amor e alegria: representações sociais da maternidade solo. **Psicologia & Sociedade**, Porto Alegre, v. 37, e289724, p. 1-16, 2025. DOI: <https://doi.org/10.1590/1807-0310/2025v37289724>.

ASSOCIAÇÃO NACIONAL DOS REGISTRADORES DE PESSOAS NATURAIS (ARPEN-BRASIL). **Portal da Transparência do Registro Civil: módulo Pais Ausentes**. Brasília: Arpen-Brasil, 2026. Disponível em: <https://transparencia.registrocivil.org.br/painel-registral/pais-ausentes>. Acesso em: 27 out. 2026.

BANIAȘ, Ovidiu; FLOREA, Diana; GYALAI, Robert; CURIAC, Daniel-Ioan. Automated specification-based testing of REST APIs. **Sensors**, Basel, v. 21, n. 16, art. 5375, p. 1-20, ago. 2021. DOI: <https://doi.org/10.3390/s21165375>.

BRITO, Renatha Celiana da Silva; ALMEIDA JUNIOR, José Jailson de; MEDEIROS, Anna Cecília Queiroz de. Online no puerpério: interações de um grupo de apoio virtual. **Revista Brasileira de Saúde Materno Infantil**, Recife, v. 22, n. 3, p. 691-697, jul./set. 2022. DOI: <https://doi.org/10.1590/1806-9304202200030014>.

BUÇKO, Ahmet; VISHI, Kamer; KRASNIQI, Bujar; REXHA, Blerim. Enhancing JWT authentication and authorization in web applications based on user behavior history. **Computers**, Basel, v. 12, n. 4, art. 78, p. 1-18, abr. 2023. DOI: <https://doi.org/10.3390/computers12040078>.

DE LUCA, Marco; DI MARTINO, Sergio; DI MEGLIO, Sergio; FASOLINO, Anna Rita; STARACE, Luigi Libero Lucio; TRAMONTANA, Porfirio. Rookie mistakes: measuring software quality in student projects to guide educational enhancement. **arXiv preprint arXiv:2507.12488**, Ithaca, p. 1-18, jul. 2025. Disponível em: <https://arxiv.org/pdf/2507.12488.pdf>. Acesso em: 3 nov. 2026.

FEIJÓ, Janaina. Mães solo no mercado de trabalho crescem 1,7 milhão em dez anos. **Blog do IBRE/FGV**, Rio de Janeiro: Fundação Getulio Vargas, 18 maio 2023. Disponível em: <https://portal.fgv.br/artigos/maes-solo-mercado-trabalho-crescem-17-milhao-dez-anos>. Acesso em: 27 out. 2026.

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). **Censo Demográfico 2022: composição domiciliar e características da população**. Rio de Janeiro: IBGE, 2023. Disponível em: <https://www.ibge.gov.br>. Acesso em: 28 out. 2026.

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). **Pesquisa Nacional por Amostra de Domicílios Contínua (PNAD Contínua): características gerais dos domicílios e dos moradores 2023**. Rio de Janeiro: IBGE, 2024. Disponível em: <https://www.ibge.gov.br>. Acesso em: 28 out. 2026.

MOURA, Lucas Vieira de; COUTINHO, Emanuel Ferreira. LGPD e requisitos de software: desafios e oportunidades de pesquisa. In: WORKSHOP SOBRE ASPECTOS SOCIAIS, HUMANOS E ECONÔMICOS DE SOFTWARE (WASHES), 9., 2024, Brasília. **Anais** [...]. Porto Alegre: Sociedade Brasileira de Computação (SBC), 2024. p. 1-6. DOI: <https://doi.org/10.5753/washes.2024.2311>.

RAYARAO, Surya Rao; DHONE, Rajeshwar; NARZULLAEVA, Ozoda. Hexagonal Architecture and Clean Architecture patterns in enterprise Spring Boot applications: a comprehensive analysis of ports, adapters, and microservices integration. **Authorea Preprints**, Hoboken, p. 1-64, jan. 2026. DOI: <https://doi.org/10.22541/au.176903300.01498666/v1>.

SOUSA, Andreyna Karollayne Saraiva de. **Maternidade solo no Brasil**: determinantes sociais da divisão desigual das responsabilidades parentais. 2025. 40 f. Trabalho de Conclusão de Curso (Graduação em Serviço Social) – Centro de Ciências Sociais Aplicadas, Universidade Federal do Rio Grande do Norte, Natal, 2025.

SOUZA, Beatriz Duarte de; JANUÁRIO, Laila Siqueira Ribeiro; LIMA, João Pedro de Amorim Lucena; TEIXEIRA, Keuler Hissa. Mães solo e desigualdades sociais: uma análise regional e educacional no Brasil. In: ENCONTRO NACIONAL DE ECONOMIA, 52., 2024, Natal. **Anais** [...]. Niterói: Associação Nacional dos Centros de Pós-Graduação em Economia (ANPEC), 2024. p. 1-20.
