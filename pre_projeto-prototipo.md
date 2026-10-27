INSTITUTO FEDERAL DE EDUCAÇÃO, CIÊNCIA E TECNOLOGIA DO PIAUÍ

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


# 1 IDENTIFICAÇÃO DO TEMA E DELIMITAÇÃO

Ao analisar os indicadores socioeconômicos da maternidade no Brasil, evidenciam-se disparidades estruturais expressivas. Uma dessas manifestações refere-se ao contingente de famílias monoparentais femininas — comumente denominadas “mães solo” —, definidas por Souza et al. (2024) como “famílias monoparentais, compostas por apenas um dos genitores no papel de responsável pela criação, manutenção e educação dos filhos. Embora possam ser chefiadas tanto por homens quanto por mulheres, são as mulheres que predominam amplamente nesse tipo de arranjo, dando origem à configuração denominada família monoparental feminina, ou, em termos mais recentes, ‘mãe solo’”.

Segundo Feijó (2023), “entre os anos de 2012 e 2022, o número de domicílios com mães solo [no Brasil] cresceu 17,8%, passando de 9,6 milhões para 11,3 milhões”. No cenário regional, dados dos cartórios de Registro Civil (ARPEN-Brasil) indicam que, no Piauí, 7,7% (2023) e 7,06% (2024) dos nascimentos foram registrados apenas com o nome da mãe — acumulando mais de 22 mil crianças sem o nome do pai na certidão ao longo da última década no estado —, revelando, em parte, o expressivo contingente de mulheres e crianças em situação de desamparo e sobrecarga unilateral.

Tendo em vista esse cenário, torna-se relevante investigar formas sociotécnicas de mitigar os impactos causados pela escassez de redes de apoio. A complexidade do fenômeno impede abordagens simplistas, uma vez que, conforme apontam Souza et al. (2024), “os resultados indicam que a maternidade solo está relacionada a desigualdades de natureza racial, educacional e territorial, e identificam-se contrastes importantes entre contextos urbanos e rurais, bem como entre diferentes níveis de instrução”.

Nesse contexto, este trabalho propõe o desenvolvimento de um aplicativo para dispositivos móveis voltado a consolidar uma rede digital solidária de apoio entre mães solo, articulando também uma plataforma para circulação e doação de itens essenciais à primeira infância, tais como móveis, enxovais, fórmulas e fraldas. A proposta engloba um espaço colaborativo seguro para compartilhamento de experiências e esclarecimento de dúvidas cotidianas, estruturando uma plataforma em que mães solo possam solicitar itens conforme suas necessidades urgentes e membros da comunidade possam cadastrar doações conforme sua disponibilidade, observando preceitos de privacidade e proteção de dados.


# 2 PROBLEMATIZAÇÃO E QUESTÃO NORTEADORA


# 3 JUSTIFICATIVA E RELEVÂNCIA SOCIOTÉCNICA


## 3.1 Relevância Social e Empírica


## 3.2 Relevância Científica e Tecnológica


# 4 OBJETIVOS DO TRABALHO


## 4.1 Objetivo Geral


## 4.2 Objetivos Específicos


# 5 REFERENCIAL TEÓRICO PRELIMINAR


## 5.1 A Maternidade Solo no Brasil e a Economia do Cuidado


## 5.2 O Paradigma da Tecnologia Social e Redes Colaborativas (RTS)


## 5.3 Arquitetura Hexagonal (Ports & Adapters) e Blindagem de Domínio


## 5.4 Privacidade por Padrão (Privacy by Design) e a LGPD


# 6 METODOLOGIA E PROCEDIMENTOS TÉCNICOS PROPOSTOS


## 6.1 Classificação e Enquadramento Metodológico


## 6.2 Ciclo de Desenvolvimento Ágil Adaptado (6 Sprints Quinzenais)


## 6.3 Levantamento Preliminar de Requisitos (RFs e RNFs)


## 6.4 Arquitetura e Pilha Tecnológica Selecionada


## 6.5 Procedimentos de Teste e Garantia da Qualidade


# 7 RECURSOS MATERIAIS E ORÇAMENTO PREVISTO


# 8 CRONOGRAMA DE EXECUÇÃO FÍSICA


# 9 RESULTADOS ESPERADOS E ENTREGÁVEIS


# REFERÊNCIAS
