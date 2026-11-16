# EloMaterno: Rede Digital Solidária de Apoio a Mães Solo

Repositório de pesquisa e documentação do Trabalho de Conclusão de Curso (TCC) desenvolvido no Curso Superior de Tecnologia em Análise e Desenvolvimento de Sistemas do **Instituto Federal do Piauí (IFPI) - Campus Parnaíba**.

- **Autor:** Ivo Bruno Gomes Araujo
- **Orientador:** Prof. Me. Antonio Santos de Sousa
- **Licença do código-fonte:** MIT

---

## Sobre o Projeto

O **EloMaterno** é uma aplicação web responsiva voltada à formação de uma rede digital de apoio para mães solo em Parnaíba (PI). A proposta busca amenizar duas dificuldades recorrentes enfrentadas por mulheres que chefiam famílias monoparentais em situação de vulnerabilidade: a falta de suporte emocional ou informativo e o custo elevado de itens essenciais nos primeiros anos da criança.

A plataforma organiza-se em duas frentes principais:

1. **Fórum Comunitário:** espaço categorizado para troca de experiências, desabafos e esclarecimento de dúvidas com outras mães e com especialistas voluntários. Conta com validação no servidor para impedir a exposição acidental de dados pessoais sensíveis, como telefone, CPF e endereço residencial.
2. **Vitrine de Doações e Mural de Pedidos de Ajuda:** catálogo gratuito para oferta e solicitação de enxovais, fraldas, fórmulas, roupas e móveis infantis. A busca é filtrada por estado, município, bairro e zona a partir do CEP, sem armazenar logradouro ou coordenadas de GPS. O contato entre quem doa e quem recebe ocorre no WhatsApp somente após o aceite mútuo da doação.

No aspecto técnico, o sistema adota a **Arquitetura Hexagonal (*Ports and Adapters*)** no *back-end* (Java 17+ e Spring Boot 3) e uma interface *mobile-first* em React com Tailwind CSS no *front-end*. Essa separação protege as regras de negócio e as políticas de privacidade (*Privacy by Design* e conformidade com a LGPD) do banco de dados PostgreSQL e dos serviços externos de nuvem gratuita.

---

## Estrutura de Pastas e Navegação

O repositório está organizado nos seguintes diretórios:

```text
projeto_mae/
├── pre-projeto/               # Documento acadêmico do pré-projeto em LaTeX
│   ├── main.tex               # Arquivo principal de configuração e compilação
│   ├── main.pdf               # Versão compilada mais recente do pré-projeto
│   ├── dados.tex              # Metadados do trabalho (título, subtítulo, autor, orientador)
│   ├── bib/referencias.bib    # Base bibliográfica no padrão BibLaTeX/ABNT
│   └── estrutura/             # Seções pré-textuais, textuais (1 a 8) e pós-textuais
│
├── docs/                      # Documentação de engenharia de software e apoio
│   ├── README.md              # Índice geral da documentação técnica
│   ├── requisitos/            # Requisitos Funcionais (RF) e Não Funcionais (RNF) detalhados
│   ├── adr/                   # Registros de Decisões Arquiteturais (ADR-0001 a ADR-0013)
│   ├── feedbacks/             # Anotações de reuniões e devolutivas de orientação
│   └── ReferenciasExternas.md # Links das plataformas comparadas na justificativa
│
└── artigos/                   # Acervo de artigos científicos utilizados no referencial
    ├── Social/                # Estudos sobre maternidade solo, gênero e apoio social
    └── Tecnológico/           # Estudos sobre arquitetura de software, APIs REST e LGPD
```

### Atalhos Rápidos

- **Texto completo do Pré-Projeto (PDF):** [`pre-projeto/main.pdf`](pre-projeto/main.pdf)
- **Seções em LaTeX do Pré-Projeto:** [`pre-projeto/estrutura/2_textuais/`](pre-projeto/estrutura/2_textuais/)
- **Requisitos Funcionais:** [`docs/requisitos/requisitos-funcionais.md`](docs/requisitos/requisitos-funcionais.md)
- **Requisitos Não Funcionais:** [`docs/requisitos/requisitos-nao-funcionais.md`](docs/requisitos/requisitos-nao-funcionais.md)
- **Decisões Arquiteturais (ADRs):** [`docs/adr/README.md`](docs/adr/README.md)
