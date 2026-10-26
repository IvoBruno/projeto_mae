# ADR-0011: Deploy em Vercel (Frontend), Render (API) e Supabase/Neon (PostgreSQL com PostGIS)

- **Status:** Aceito
- **Data:** 2026-10-13 (atualizado conforme resolução Q-05)
- **Requisitos relacionados:** RNF-08, RNF-21, RNF-24

## Contexto

O projeto acadêmico precisa de esteira de integração e entrega contínua (CI/CD) automatizada, certificado SSL/HTTPS provido sem custos e suporte estável à extensão espacial **PostGIS**, operando com custo zero durante a fase de validação e avaliação do TCC ([Q-05](../historico-deliberacoes.md)).

## Decisão

Consolidar a arquitetura de implantação em nuvem com a seguinte divisão de serviços:

1. **Frontend (SPA React / Vite):** Hospedado na **Vercel**, configurada para deploy contínuo automático acionado por *push* no branch principal do GitHub e geração de URLs de *preview* a cada Pull Request.
2. **Backend (API Spring Boot):** Hospedado no **Render** executando um container Docker com build multi-stage (Maven + JDK 17 slim), configurado para deploy automático a partir do repositório.
3. **Banco de Dados Relacional com PostGIS:** Hospedado no **Supabase** ou **Neon**, instâncias gerenciadas de PostgreSQL 15+ com a extensão PostGIS instalada e ativa por padrão, sem custos e com limites generosos para o volume de dados do MVP.
4. **Segurança e Comunicação:**
   - HTTPS obrigatório provido automaticamente por certificados emitidos pelas plataformas.
   - CORS no Spring Boot restrito ao domínio de produção da Vercel (`*.vercel.app`) e ao ambiente local (`http://localhost:5173`).
   - Variáveis de ambiente (`SPRING_DATASOURCE_URL`, `JWT_SECRET`, credenciais do Cloudinary) configuradas diretamente no painel do Render.

## Alternativas consideradas

- **Railway (Backend + Banco integrado):** Oferece boa experiência de uso, porém o plano gratuito baseado em créditos de teste ($5) expira em 30 dias ou com uso continuado, inviabilizando o ciclo de 12 semanas (6 sprints) do projeto sem cartão de crédito ativo.
- **Render PostgreSQL gratuito:** Possui expiração do banco de dados a cada 30 ou 90 dias, o que arriscaria a perda de dados durante as bancas de avaliação. O Supabase/Neon oferece retenção permanente e suporte nativo ao PostGIS.
- **VPS Autogerenciada (Oracle Cloud / AWS EC2):** Maior controle, porém exige configuração manual de firewall, TLS/Certbot, Nginx e manutenção do sistema operacional, incompatível com a restrição de tempo do desenvolvedor solo.

## Consequências

- **Positivas:**
  - Custo operacional R$ 0 durante toda a execução e avaliação do TCC.
  - Deploy contínuo por `git push` no frontend e backend.
  - PostgreSQL com PostGIS nativo e estável, sem risco de perda de migrations ou expiração precoce.
- **Negativas / Riscos:**
  - O container gratuito da API no Render entra em hibernação após 15 minutos de inatividade, gerando *cold start* de aproximadamente 30 a 50 segundos na primeira requisição após o repouso. Esse comportamento é documentado na avaliação acadêmica e não invalida o [RNF-01], cuja medição deve ocorrer em regime aquecido (*warm start*).
