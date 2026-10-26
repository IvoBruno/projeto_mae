# ADR-0008: Armazenamento de mídia no Cloudinary (upload direto)

- **Status:** Aceito
- **Data:** 2026-10-13
- **Requisitos relacionados:** RF-15, RF-17, RNF-02

## Contexto

Os itens de doação têm fotos. Receber e processar imagens no backend consome banda, CPU e disco efêmero (PaaS gratuito). O README prevê upload direto via _unsigned presets_ e transformações na URL (§5).

## Decisão

- O frontend envia a imagem **direto ao Cloudinary** usando um _unsigned upload preset_ restrito (formatos e tamanho máximo, pasta fixa).
- O backend recebe e persiste apenas a **URL** em `item_doacao.foto_url`, validando que o host é o do Cloudinary.
- A exibição usa transformações na URL: `f_auto,q_auto,w_500`.
- O SDK Cloudinary no backend fica reservado para operações administrativas, como a remoção de imagens órfãs.

## Alternativas consideradas

- **Upload via backend (multipart) para disco/S3:** controle total, mas mais carga e infraestrutura.
- **AWS S3 + CloudFront:** escalável, mas exige mais configuração e não tem transformação de imagem embutida.
- **Armazenar em BLOB no PostgreSQL:** simples, mas incha o banco e prejudica o desempenho.

## Consequências

- **Positivas:** menos carga no backend; imagens otimizadas automaticamente; CDN.
- **Negativas / riscos:**
  - _Unsigned presets_ permitem uploads por terceiros que conheçam o preset. Mitigar com limites no preset e revisão de uso.
  - Dependência de serviço externo e do limite do plano gratuito.
  - Fotos podem conter metadados EXIF/GPS; configurar a remoção no preset (privacidade, [ADR-0009](0009-moderacao-pii-regex.md)).
