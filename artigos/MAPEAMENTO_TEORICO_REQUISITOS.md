# Mapeamento Teórico-Tecnológico: Articulação entre Literatura Científica e Requisitos de Software

> **EloMaterno:** Rede Digital Solidária de Apoio a Mães Solo  
> **Instituição:** Instituto Federal do Piauí (IFPI) — Campus Parnaíba  
> **Autor:** Ivo Bruno Gomes Araujo  
> **Orientador:** Prof. Me. Antonio Santos de Sousa  

Este documento estabelece a ponte sócio-técnica entre os diagnósticos empíricos e teóricos extraídos dos artigos científicos presentes nesta pasta e as decisões de engenharia de software formalizadas nos documentos de **Requisitos Funcionais (RF)**, **Requisitos Não Funcionais (RNF)** e **Registros de Decisões Arquiteturais (ADR)** do projeto.

---

## 1. Síntese dos Artigos Científicos Analisados

Os três estudos que fundamentam este projeto abordam a maternidade solo no Brasil a partir de prismas complementares das Ciências Humanas e Sociais Aplicadas:

1. **ARAÚJO, Maria Helena Pereira de Oliveira; AMORIM, Betânia Maria Oliveira de (2025):**  
   *Abordagem da Psicologia Social.* A partir de pesquisa-ação com mães solo beneficiárias do Programa Bolsa Família e da metodologia participativa da "Tenda do Conto", analisa as representações sociais da maternidade monoparental. Identifica a dor do abandono paterno, a sobrecarga física e mental, a culpa gerada pelo mito da mãe sacrificada e os relatos frequentes de violência doméstica e de gênero por parte dos ex-parceiros.
2. **SOUZA, Beatriz Duarte de; JANUÁRIO, Laila Siqueira Ribeiro; LIMA, João Pedro de Amorim Lucena; TEIXEIRA, Keuler Hissa (2024):**  
   *Abordagem da Economia Aplicada.* A partir de microdados da PNAD Contínua (IBGE, 2023) e estimação de modelo econométrico *logit*, investiga os determinantes da monoparentalidade feminina. Demonstra que a maternidade solo possui forte recorte racial (90% do crescimento concentrado entre mulheres negras/pardas), educacional e regional (maior prevalência no Norte e Nordeste e em periferias urbanas), na qual a carência econômica crônica restringe o acesso a bens essenciais de puericultura.
3. **SOUSA, Andreyna Karollayne Saraiva de (2025):**  
   *Abordagem do Serviço Social e Direito das Famílias.* Investiga a divisão sexual do trabalho e a naturalização do trabalho reprodutivo não remunerado (economia do cuidado). Demonstra que os mecanismos sociojurídicos tradicionais (ação de alimentos e prisão civil do genitor devedor) são lentos e ineficazes quando o pai atua no mercado informal ou está desempregado, não suprindo as necessidades alimentares e materiais imediatas da criança.

---

## 2. Matriz de Rastreabilidade Sócio-Técnica

A tabela a seguir correlaciona diretamente as carências e diagnósticos extraídos dos artigos com os módulos, requisitos e decisões arquiteturais correspondentes na aplicação:

| Dimensão Crítica / Problema Empírico | Evidência Científica no Artigo | Resposta Tecnológica do EloMaterno | Requisitos Funcionais (RF) | Requisitos Não Funcionais (RNF) | Decisões Arquiteturais (ADR) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Inadimplência de alimentos e carência material imediata de puericultura** | A via judicial da prisão civil por dívida de pensão não resolve a fome ou a falta imediata de itens básicos de subsistência infantil (SOUSA, 2025). | **Vitrine Colaborativa de Doações e Mural de Pedidos de Ajuda:** intermediação comunitária direta para circulação solidária de berços, carrinhos, fraldas e roupas. | [RF-14 a RF-20b](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md) | [RNF-01, RNF-02](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md#desempenho-e-escalabilidade) | [ADR-0008 (Cloudinary)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0008-cloudinary-midia.md) |
| **Solidão, sofrimento psíquico e esgotamento da rede familiar de apoio** | Mães solo sofrem com o isolamento afetivo, ambivalência emocional e sobrecarga, demandando espaços de escuta horizontal como a "Tenda do Conto" (ARAÚJO; AMORIM, 2025). | **Fórum Comunitário Temático:** espaço dialógico para desabafos, orientações práticas cotidianas e acolhimento mútuo entre pares sem estigmatização. | [RF-07 a RF-10](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md) | [RNF-17](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md#usabilidade-e-acessibilidade) | [ADR-0001 (Hexagonal/REST)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0001-arquitetura-desacoplada-spa-api-rest.md) |
| **Histórico de violência doméstica e risco de perseguição/exposição** | Mulheres relatam histórico de agressões físicas/psicológicas e conflitos com ex-companheiros, tornando a privacidade questão de segurança física (ARAÚJO; AMORIM, 2025; SOUSA, 2025). | **Filtro de PII Proativo e Match com Duplo Aceite:** rejeição automática de dados de contato no fórum e liberação de telefone via WhatsApp somente após aprovação do doador. | [RF-11, RF-21, RF-22](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md) | [RNF-05, RNF-06, RNF-11, RNF-12](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md#privacidade-e-conformidade-lgpd) | [ADR-0009 (Moderação PII)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0009-moderacao-pii-regex.md), [ADR-0010 (Match WhatsApp)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0010-match-seguro-whatsapp.md), [ADR-0005 (JWT)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0005-autenticacao-jwt-spring-security.md) |
| **Concentração da vulnerabilidade em periferias urbanas, interior e zona rural** | Famílias chefiadas por mães solo estão massivamente no Nordeste/Norte, fora de capitais (75,5%) e em periferias urbanas (com 8,6% em área rural), com restrição orçamentária para deslocamentos longos (SOUZA et al., 2024). | **Filtro Territorial Administrativo e Privacidade de Localização:** recorte indexado por Estado, Município, Bairro e Zona (`NORTE`, `SUL`, `LESTE`, `OESTE`, `CENTRO`, `RURAL`), sem persistir logradouro nem coordenadas GPS. | [RF-02, RF-16, RF-20](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md) | [RNF-04, RNF-13](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md#desempenho-e-escalabilidade) | [ADR-0006 (PostgreSQL / B-Tree)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0006-postgresql-indexacao-territorial.md), [ADR-0012 (ViaCEP)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0012-viacep-enderecos.md) |
| **Exclusão digital, conexões limitadas (3G/4G) e uso predominante de smartphone** | Perfil socioeconômico de baixa escolaridade e renda restrita a benefícios sociais impõe o celular como único dispositivo de acesso à internet (SOUZA et al., 2024; ARAÚJO; AMORIM, 2025). | **Interface Mobile-First Otimizada:** aplicação responsiva de alta performance, com compressão de imagens na CDN para economia de dados do usuário. | [RF-01, RF-15, RF-16](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md) | [RNF-01, RNF-02, RNF-15, RNF-16](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md) | [ADR-0003 (React/Tailwind)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0003-frontend-react-vite-tailwind.md), [ADR-0008 (Cloudinary)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0008-cloudinary-midia.md) |
| **Necessidade de garantia ética, rigor técnico e sustentabilidade do software** | O software atende a um público hipervulnerável, exigindo código robusto, testável e sem vazamento de regras de negócio em camadas técnicas acopladas. | **Arquitetura Hexagonal com Ports & Adapters:** núcleo de domínio puro, isolamento das regras de negócio e testes automatizados de arquitetura. | [RF-05, RF-24, RF-26](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md) | [RNF-18, RNF-19, RNF-22](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md#manutenibilidade-portabilidade-e-operacao) | [ADR-0001 (Hexagonal)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0001-arquitetura-desacoplada-spa-api-rest.md), [ADR-0002 (Spring Boot / ArchUnit)](file:///home/ivo/Projetos/projeto_mae/docs/adr/0002-backend-java-spring-boot.md) |

---

## 3. Detalhamento dos Eixos de Articulação

### 3.1. Eixo 1: A Vitrine Solidária como Mitigação da Ineficácia da Execução de Alimentos

Conforme demonstrado por **Sousa (2025, p. 23-28)**, embora o art. 1.634 do Código Civil preveja responsabilidade compartilhada entre pai e mãe, a realidade prática é de naturalização do abandono paterno. Quando as mães recorrem ao Poder Judiciário em busca de alimentos, enfrentam morosidade processual e, em muitos casos, a insolvência ou ocultação de renda do genitor informal. Nesse intervalo, as necessidades vitais das crianças (vestuário, berço para sono seguro, alimentação e higiene) não podem esperar o desfecho judicial.

- **Correspondência no Sistema:**
  - O módulo de **Vitrine de Enxovais** e o **Mural de Pedidos de Ajuda** ([RF-14 a RF-20](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)) funcionam como uma rede complementar de economia circular e solidária.
  - A inclusão de fotos com upload e renderização otimizada ([ADR-0008](file:///home/ivo/Projetos/projeto_mae/docs/adr/0008-cloudinary-midia.md), [RF-15](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)) permite que a mãe avalie previamente o estado de conservação do item (novo, seminovo, usado), evitando frustrações e deslocamentos desnecessários.
  - O filtro territorial administrativo por Estado, Município, Bairro e Zona ([ADR-0006](file:///home/ivo/Projetos/projeto_mae/docs/adr/0006-postgresql-indexacao-territorial.md), [RF-16, RF-20](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)) aproxima doadores e recebedoras da mesma região urbana ou rural sem coletar coordenadas geográficas exatas nem logradouros residenciais, mitigando simultaneamente custos de deslocamento e riscos à segurança física.

### 3.2. Eixo 2: A "Tenda do Conto Digital" e a Desconstrução da Culpa Materna

O trabalho de **Araújo e Amorim (2025, p. 6-12)** expõe que a maternidade solo impõe uma ambivalência psicológica intensa: ao mesmo tempo em que a sociedade romantiza a "mulher guerreira", impõe-se a ela a culpa solitária por qualquer escassez ou dificuldade enfrentada pelos filhos. A vivência empírica da *Tenda do Conto* revelou que a simples existência de um ambiente seguro e horizontal para falar sobre medos, sobrecargas e desabafos reduz o estresse parental e quebra a sensação de isolamento.

- **Correspondência no Sistema:**
  - O **Fórum Comunitário** ([RF-07 a RF-10](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)) transpõe os princípios da *Tenda do Conto* para o meio virtual, fornecendo a categoria explícita `DESABAFO`, além de `DUVIDAS`, `DICAS` e orientações do eixo `JURIDICO`.
  - A interface adota diretrizes de usabilidade acolhedora ([RNF-17](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)), com mensagens claras, empáticas e livres de jargões técnicos punitivos em caso de erros de preenchimento.

### 3.3. Eixo 3: Privacy by Design como Escudo Protetor contra Violência e Assédio

Tanto **Araújo e Amorim (2025)** quanto **Sousa (2025)** destacam a vulnerabilidade das mães solo a históricos prévios de violência doméstica e conflitos com os genitores. Em contextos onde muitas mães precisam manter distância de agressores ou evitar a exposição pública de suas rotinas e domicílios, a publicação aberta de números de telefone e endereços seria desastrosa.

- **Correspondência no Sistema:**
  - **Sanitização de PII (Personally Identifiable Information) por Regex** ([ADR-0009](file:///home/ivo/Projetos/projeto_mae/docs/adr/0009-moderacao-pii-regex.md), [RF-11](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md), [RNF-11](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)): intercepta preventivamente no backend postagens no fórum que contenham números de telefone, CPFs ou endereços completos, rejeitando a submissão com aviso explicativo e sem registrar os dados nos logs ([RNF-23](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)).
  - **Minimização Territorial na Origem:** a entidade `ENDERECO` ([ADR-0006](file:///home/ivo/Projetos/projeto_mae/docs/adr/0006-postgresql-indexacao-territorial.md)) não armazena `logradouro` nem posição geográfica, restringindo-se a Estado, Município, Bairro e Zona ([RNF-13](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)).
  - **Fluxo de Match Seguro via WhatsApp** ([ADR-0010](file:///home/ivo/Projetos/projeto_mae/docs/adr/0010-match-seguro-whatsapp.md), [RF-21, RF-22](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md), [RNF-12](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)): o telefone do doador ou da mãe nunca é exibido em listagens públicas abertas. A conexão ocorre estritamente por link parametrizado (`wa.me`) após manifestação formal de interesse (`MatchDoacao`) e aceite do doador, exigindo autenticação prévia ([RNF-06](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)).

### 3.4. Eixo 4: Desigualdades Territoriais, Exclusão Digital e Performance

O estudo econométrico de **Souza et al. (2024, p. 12-16)** aponta que a probabilidade de chefiar uma família monoparental é desproporcionalmente maior em áreas urbanas de menor renda e nas regiões periféricas. Essas usuárias acessam a web predominantemente via planos de dados móveis pré-pagos e aparelhos celulares com capacidades de processamento modestas.

- **Correspondência no Sistema:**
  - **Arquitetura SPA Responsiva e Mobile-First** ([ADR-0003](file:///home/ivo/Projetos/projeto_mae/docs/adr/0003-frontend-react-vite-tailwind.md), [RNF-15, RNF-16](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)): garante navegabilidade fluida a partir de telas com largura de 360px.
  - **Otimização Extrema de Imagens na CDN** ([ADR-0008](file:///home/ivo/Projetos/projeto_mae/docs/adr/0008-cloudinary-midia.md), [RNF-02](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)): aplicação automática das diretivas `f_auto,q_auto,w_500` no Cloudinary, minimizando o consumo da franquia de internet da usuária.
  - **API REST Stateless com Latência Reduzida** ([ADR-0001](file:///home/ivo/Projetos/projeto_mae/docs/adr/0001-arquitetura-desacoplada-spa-api-rest.md), [RNF-01](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)): meta de tempo médio de resposta `< 300 ms`, conferindo agilidade mesmo sob redes móveis instáveis.
  - **Agilidade no Cadastro via ViaCEP sem Retenção de Rua** ([ADR-0012](file:///home/ivo/Projetos/projeto_mae/docs/adr/0012-viacep-enderecos.md), [RF-02](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-funcionais.md)): autopreenchimento de Estado, Município e Bairro no mobile a partir do CEP digitado, descartando o logradouro antes da persistência.

### 3.5. Eixo 5: Arquitetura Hexagonal como Garantia de Confiabilidade do Domínio Social

Projetos sociais desenvolvidos em contexto acadêmico ou solo frequentemente enfrentam o risco de abandono ou fragilidade estrutural quando regras complexas de negócio (moderação, segurança de menores, concorrência em doações) ficam misturadas a código de banco de dados ou frameworks descartáveis.

- **Correspondência no Sistema:**
  - **Arquitetura Hexagonal (Ports & Adapters)** ([ADR-0001](file:///home/ivo/Projetos/projeto_mae/docs/adr/0001-arquitetura-desacoplada-spa-api-rest.md), [ADR-0002](file:///home/ivo/Projetos/projeto_mae/docs/adr/0002-backend-java-spring-boot.md), [RNF-18](file:///home/ivo/Projetos/projeto_mae/docs/requisitos/requisitos-nao-funcionais.md)): o núcleo de domínio (`domain`) permanece 100% puro, sem anotações JPA ou acoplamento com o Spring Framework.
  - As regras de negócio (ex.: verificação de regras de elegibilidade, ciclo de vida do `MatchDoacao`, sanitização de dados) são protegidas e testáveis isoladamente através de testes unitários ultrarrápidos e suites de arquitetura com **ArchUnit**.

---

## 4. Referências Bibliográficas (Normas ABNT NBR 6023:2018)

ARAÚJO, Maria Helena Pereira de Oliveira; AMORIM, Betânia Maria Oliveira de. Contos de dor, amor e alegria: representações sociais da maternidade solo. **Psicologia & Sociedade**, Porto Alegre, v. 37, e289724, p. 1-17, 2025. DOI: [10.1590/1807-0310/2025v37289724](https://doi.org/10.1590/1807-0310/2025v37289724). Disponível em: <http://dx.doi.org/10.1590/1807-0310/2025v37289724>. Acesso em: 13 out. 2026.

ARPEN-BRASIL. Associação Nacional dos Registradores de Pessoas Naturais. **Portal da Transparência do Registro Civil: Painel Pais Ausentes**, 2022. Disponível em: <https://transparencia.registrocivil.org.br>. Acesso em: 15 fev. 2026.

BRASIL. **Lei nº 10.406, de 10 de janeiro de 2002**. Institui o Código Civil. Brasília, DF: Presidência da República, 2002. Disponível em: <https://www.planalto.gov.br/ccivil_03/leis/2002/l10406compilada.htm>. Acesso em: 13 out. 2026.

BRASIL. **Lei nº 13.709, de 14 de agosto de 2018**. Lei Geral de Proteção de Dados Pessoais (LGPD). Brasília, DF: Presidência da República, 2018. Disponível em: <https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm>. Acesso em: 13 out. 2026.

BRASIL. **Lei nº 15.069, de 23 de dezembro de 2024**. Institui a Política Nacional de Cuidados. Brasília, DF: Presidência da República, 2024. Disponível em: <https://www.planalto.gov.br/ccivil_03/_ato2023-2026/2024/lei/l15069.htm>. Acesso em: 13 out. 2026.

FEIJÓ, Janaína. **Mães solo no mercado de trabalho crescem 1,7 milhão em dez anos**. Blog do IBRE/FGV, 2023. Disponível em: <https://blogdoibre.fgv.br>. Acesso em: 10 fev. 2026.

HIRATA, Helena; KERGOAT, Danièle. Novas configurações da divisão sexual do trabalho. **Cadernos de Pesquisa**, São Paulo, v. 37, n. 132, p. 595-609, 2007. DOI: [10.1590/S0100-15742007000300005](https://doi.org/10.1590/S0100-15742007000300005). Acesso em: 13 out. 2026.

IBGE. Instituto Brasileiro de Geografia e Estatística. **Censo Demográfico 2022: Domicílios e composições familiares**. Rio de Janeiro: IBGE, 2023.

SAFFIOTI, Heleieth Iara Bongiovani. **Gênero, patriarcado, violência**. 2. ed. São Paulo: Expressão Popular / Fundação Perseu Abramo, 2015.

SOUSA, Andreyna Karollayne Saraiva de. **Maternidade solo no Brasil: determinantes sociais da divisão desigual das responsabilidades parentais**. 2025. 40 f. Trabalho de Conclusão de Curso (Graduação em Serviço Social) – Centro de Ciências Sociais Aplicadas, Universidade Federal do Rio Grande do Norte, Natal, 2025.

SOUZA, Beatriz Duarte de; JANUÁRIO, Laila Siqueira Ribeiro; LIMA, João Pedro de Amorim Lucena; TEIXEIRA, Keuler Hissa. **Mães solo e desigualdades sociais: uma análise regional e educacional no Brasil**. 2024. Trabalho de Conclusão de Curso (Graduação em Ciências Econômicas) – Faculdade de Economia, Administração e Contabilidade, Universidade Federal de Alagoas, Maceió, 2024.

ZANELLO, Valeska. **Saúde mental, gênero e dispositivos: cultura e processos de subjetivação**. Curitiba: Editora Appris, 2020.

