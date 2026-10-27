# Documentação — EloMaterno

Rede digital solidária de apoio a mães solo (IFPI — Campus Parnaíba). Este diretório consolida a documentação de engenharia derivada do [README principal](../README.md).

## Índice

| Documento                                                                     | Conteúdo                                                                          |
| :---------------------------------------------------------------------------- | :-------------------------------------------------------------------------------- |
| [Requisitos Funcionais](requisitos/requisitos-funcionais.md)                  | RF-01 … RF-27, agrupados por módulo e sprint                                      |
| [Requisitos Não Funcionais](requisitos/requisitos-nao-funcionais.md)          | RNF-01 … RNF-25, por atributo de qualidade                                        |
| [ADRs](adr/README.md)                                                         | Registros de Decisões Arquiteturais (ADR-0001 … ADR-0013)                         |
| [Mapeamento Teórico-Tecnológico](../artigos/MAPEAMENTO_TEORICO_REQUISITOS.md) | Articulação entre literatura científica (artigos em PDF) e requisitos/ADRs (ABNT) |

## Convenções

- **Origem:** `README §N` = explícito no README; `Inferido` = deduzido do DER, do roadmap ou de boas práticas, a validar com o orientador.
- **Prioridade (MoSCoW):** `Must` (MVP), `Should`, `Could`, `Won't` (fora do MVP).
- **Perfis:** `MAE_SOLO`, `DOADOR`, `VOLUNTARIO`, `ADMIN` (enum `USUARIO.perfil`).
- **Rastreabilidade:** cada RF/RNF indica a sprint (organizadas em 6 sprints de duas semanas) e, quando aplicável, o ADR que o fundamenta.
