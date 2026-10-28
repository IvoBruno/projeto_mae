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

Ao observar a realidade do Piauí e, mais especificamente, do município de Parnaíba, os indicadores do Instituto Brasileiro de Geografia e Estatística (IBGE) ajudam a traçar o perfil dessa comunidade. De acordo com o Censo Demográfico (IBGE, 2023), Parnaíba possui 162.159 habitantes, sendo o segundo município mais populoso do estado e o principal polo urbano da Planície Litorânea. No cenário estadual, as mulheres já respondem pela chefia da maioria dos domicílios (50,36%, um salto de 11,61 pontos percentuais em comparação aos 38,75% de 2010), e cerca de 18,11% dos lares são formados por mães solo com seus filhos (IBGE, 2023). Além disso, Parnaíba tem o segundo maior volume de atendimento do Programa Bolsa Família no Piauí, amparando cerca de 18,5 mil famílias (18.549 registros em 2024), atrás somente da capital Teresina (IBGE, 2024).

Apesar dessa demanda expressiva no município, o apoio comunitário e a doação de itens infantis ainda acontecem de maneira dispersa, muitas vezes restritos a grupos informais em redes sociais abertas. Nesses ambientes, a mãe solo que precisa pedir ajuda com fraldas, leite ou enxoval acaba exposta, sem garantias mínimas de privacidade ou organização dos pedidos.

A partir desse cenário, define-se a seguinte questão norteadora para o trabalho: **como desenvolver um aplicativo móvel seguro, baseado em Arquitetura Hexagonal e privacidade de dados, que facilite a doação de itens infantis e o apoio mútuo entre mães solo em Parnaíba-PI?**

## 3 JUSTIFICATIVA E RELEVÂNCIA SOCIOTÉCNICA

### 3.1 Relevância Social e Empírica

A proposta do aplicativo divide-se em duas frentes principais de atuação social. A primeira refere-se ao fórum comunitário, no qual será possível criar tópicos sobre assuntos específicos da maternidade ou publicar dúvidas para debate com os demais membros da plataforma. O objetivo desse espaço é funcionar como uma rede de apoio direta para as mães solo, permitindo a interação tanto com outras mulheres em situações similares quanto com especialistas voluntários dispostos a repassar orientações técnicas. O intuito principal é gerar conexão interpessoal, conforme defendido por Brito, Almeida Junior e Medeiros (2022, p. 692): "Nessa perspectiva, os suportes online, ou apoio social virtual, podem ser procurados como uma alternativa aos grupos de apoio tradicionais, presenciais, por serem mais acessíveis. Tais grupos online geralmente têm um modus operandi que privilegia a interação entre usuários e a aprendizagem colaborativa".

A segunda frente abrange o painel Vitrine de Doações e Pedidos de Ajuda, voltado a centralizar a oferta de itens para doação e os pedidos de materiais necessários às mães e seus filhos. Essa funcionalidade justifica-se pelos dados do IBGE sobre o alto volume de famílias beneficiárias do Programa Bolsa Família em Parnaíba, voltado a pessoas em situação de vulnerabilidade social. Para manter a simplicidade e a segurança das usuárias, o contato final ocorre fora da plataforma: como o sistema não possui chat interno, o número de telefone é direcionado ao aplicativo WhatsApp somente quando ambas as partes concordam com a doação.

### 3.2 Relevância Científica e Tecnológica

## 4 OBJETIVOS DO TRABALHO

### 4.1 Objetivo Geral

Desenvolver um aplicativo móvel voltado à criação de uma rede digital de apoio para mães solo em Parnaíba-PI, reunindo em uma mesma plataforma a doação e solicitação de itens essenciais aos primeiros anos da criança (como móveis, enxovais, fórmulas e fraldas) e um fórum seguro para troca de experiências e dúvidas sobre a maternidade, com foco na proteção da privacidade das usuárias.

### 4.2 Objetivos Específicos

- Modelar a estrutura do aplicativo utilizando o padrão de Arquitetura Hexagonal (*Ports and Adapters*), isolando as regras de negócio das dependências externas de banco de dados e interface;
- Implementar o módulo de fórum comunitário para publicação de dúvidas, criação de tópicos por categoria e interação entre mães solo e especialistas voluntários;
- Desenvolver o módulo de Vitrine de Doações e Pedidos de Ajuda para cadastro, filtragem por bairro/município e solicitação de itens infantis essenciais;
- Construir o fluxo de consentimento mútuo para redirecionamento seguro ao WhatsApp, garantindo que o telefone de contato só seja compartilhado após o aceite da solicitação;
- Avaliar o funcionamento dos módulos desenvolvidos por meio de testes automatizados de unidade e integração nas rotas da API e na interface móvel.

## 5 REFERENCIAL TEÓRICO PRELIMINAR

### 5.1 A Maternidade Solo no Brasil e a Economia do Cuidado

### 5.2 O Paradigma da Tecnologia Social e Redes Colaborativas (RTS)

### 5.3 Arquitetura Hexagonal (Ports & Adapters) e Blindagem de Domínio

### 5.4 Privacidade por Padrão (Privacy by Design) e a LGPD

## 6 METODOLOGIA E PROCEDIMENTOS TÉCNICOS PROPOSTOS

### 6.1 Classificação e Enquadramento Metodológico

### 6.2 Ciclo de Desenvolvimento Ágil Adaptado (6 Sprints Quinzenais)

### 6.3 Levantamento Preliminar de Requisitos (RFs e RNFs)

### 6.4 Arquitetura e Pilha Tecnológica Selecionada

### 6.5 Procedimentos de Teste e Garantia da Qualidade

## 7 RECURSOS MATERIAIS E ORÇAMENTO PREVISTO

## 8 CRONOGRAMA DE EXECUÇÃO FÍSICA

## 9 RESULTADOS ESPERADOS E ENTREGÁVEIS

## REFERÊNCIAS

ASSOCIAÇÃO NACIONAL DOS REGISTRADORES DE PESSOAS NATURAIS (ARPEN-BRASIL). **Portal da Transparência do Registro Civil: módulo Pais Ausentes**. Brasília: Arpen-Brasil, 2024. Disponível em: https://transparencia.registrocivil.org.br/painel-registral/pais-ausentes. Acesso em: 27 out. 2026.

BRITO, Renatha Celiana da Silva; ALMEIDA JUNIOR, José Jailson de; MEDEIROS, Anna Cecília Queiroz de. Online no puerpério: interações de um grupo de apoio virtual. **Revista Brasileira de Saúde Materno Infantil**, Recife, v. 22, n. 3, p. 691-697, jul./set. 2022. DOI: https://doi.org/10.1590/1806-9304202200030014.

FEIJÓ, Janaina. Mães solo no mercado de trabalho crescem 1,7 milhão em dez anos. **Blog do IBRE/FGV**, Rio de Janeiro: Fundação Getulio Vargas, 18 maio 2023. Disponível em: https://portal.fgv.br/artigos/maes-solo-mercado-trabalho-crescem-17-milhao-dez-anos. Acesso em: 27 out. 2026.

FINAMORI, Sabrina; BATISTA, Maria Alice Marcelina. Categorias empíricas e analíticas: mães-solo e monoparentalidade feminina. **Mediações - Revista de Ciências Sociais**, Londrina, v. 27, n. 3, p. 1-19, 2022. DOI: https://doi.org/10.5433/2176-6665.2022v27n3e46105.

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). **Censo Demográfico 2022: composição domiciliar e características da população**. Rio de Janeiro: IBGE, 2023. Disponível em: https://www.ibge.gov.br. Acesso em: 28 out. 2026.

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA (IBGE). **Pesquisa Nacional por Amostra de Domicílios Contínua (PNAD Contínua): características gerais dos domicílios e dos moradores 2023**. Rio de Janeiro: IBGE, 2024. Disponível em: https://www.ibge.gov.br. Acesso em: 28 out. 2026.

MACHADO, Mariana Silva; PEREIRA, Claudia Regina Ramos. Redes pessoais significativas de mulheres responsáveis por famílias monoparentais em vulnerabilidade social. **Estudos de Psicologia**, Natal, v. 25, n. 4, p. 399-411, 2020. DOI: https://doi.org/10.22491/1678-4669.20200041.

SOUZA, Beatriz Duarte de; JANUÁRIO, Laila Siqueira Ribeiro; LIMA, João Pedro de Amorim Lucena; TEIXEIRA, Keuler Hissa. Mães solo e desigualdades sociais: uma análise regional e educacional no Brasil. _In_: ENCONTRO NACIONAL DE ECONOMIA, 52., 2024. **Anais...** Maceió: Universidade Federal de Alagoas (UFAL/FEAC), 2024.
