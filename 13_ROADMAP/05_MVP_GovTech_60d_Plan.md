# 05_MVP_GovTech_60d_Plan  
BlueShark GovTech Suite — Plano Técnico 60 dias (com IA)  
(BeSafe Digital — Versão 2025)

> Foco: **Arquitetura A (unificada)**, sem obrigatoriedade de evoluir para Arquitetura C.  
> Entrega principal: **MVP GovTech** sólido para demonstração oficial em ~60 dias,  
> com **Academy Básico** já integrado o suficiente para provar o conceito.

---

## 1. Objetivo do Plano

Entregar, em até **60 dias**, um MVP funcional que permita:

1. **GovTech Suite (núcleo)**  
   - Login multi-instituto (ITCV, IGAE, INSP, IGQPI, ERIS)  
   - Dashboard com **heatmap de risco por concelho**  
   - Lista de inspeções + detalhe de inspeção  
   - Registro de inspeções com checklist + evidências (foto, texto)  
   - Registro e visualização de incidentes (Citizen + internos)  
   - Exportação simples de relatórios (PDF/Excel)  
   - **GovTech Copilot (IA)** para apoiar análise de casos

2. **Academy Básico (mínimo viável ligado ao GovTech)**  
   - Trilhas básicas para inspetores e gestores  
   - Cadastro de cursos / aulas (mesmo que manual/simples)  
   - Registro de conclusão (mesmo sem player avançado)  
   - Integração simples GovTech → Academy:
     - % de inspetores formados  
     - % de gestores formados

3. Mostrar **uso real de IA no desenvolvimento**:
   - GitHub Copilot / Codeium / ChatGPT (para código)  
   - Ferramentas de geração de UI (Figma + plugins IA)  
   - IA para geração de testes, documentação, migrações etc.

---

## 2. Premissas

- 1 dev sênior (Ricardo) + você como **PO/BA/Arquiteto funcional**.  
- Uso intensivo de:
  - **GitHub Copilot** (ou equivalente) no VSCode  
  - **ChatGPT / OpenAI API** para scaffolding, rotinas e refactor  
  - **Figma** com plugins de IA para layout inicial  
- Arquitetura A:
  - **Next.js** (front web)  
  - **Node.js/NestJS** para backend (API + BFF no mesmo código, se necessário)  
  - **PostgreSQL** como DB  
  - Implantação em um único cluster (ECS/Fargate ou similar)  
- Segurança em nível MVP:
  - JWT simples  
  - RBAC básico (admin, inspetor, diretor, analista)  

---

## 3. Visão Geral do Roadmap (Semana a Semana)

| Semana | Foco Principal                                     | Entregáveis-chave                                                                 |
|--------|----------------------------------------------------|-----------------------------------------------------------------------------------|
| 1      | Setup, arquitetura mínima, repositórios            | Monorepo, CI simples, skeleton backend + front, auth básico                      |
| 2      | Modelo de dados + GovTech core                     | Tabelas principais (inspections, incidents, orgs), seed data, CRUD inicial       |
| 3      | Dashboards iniciais + Heatmap (Mapa de risco)      | Heatmap com dados fake, cards por instituto, KPIs iniciais                       |
| 4      | Fluxo de inspeção completo                         | Tela de inspeção, checklists, upload de evidência, gravação completa             |
| 5      | Incidentes + Citizen Reporter + ligação com risco  | Registro de incidentes, triagem simples, impacto no heatmap e dashboards         |
| 6      | MVP Academy Básico + integração GovTech ↔ Academy  | Trilhas para inspetores, % concluído, indicador nos dashboards GovTech           |
| 7      | GovTech Copilot (IA) + refino UX/UI + relatórios   | IA assistindo inspeções/relatórios, PDFs simples, polimento para demo            |
| 8      | Hardening, demo script, ajustes de produção        | Script da apresentação, testes finais, correções críticas, estabilização         |

> Observação: 60 dias ~ 8–9 semanas úteis.  
> Este plano considera **8 semanas intensivas**.

---

## 4. Detalhamento Semana a Semana (Com IA)

### Semana 1 — Setup & Arquitetura Básica

**Objetivos:**

- Colocar a “espinha dorsal” no ar: repos, build, deploy simples.  
- Preparar o ambiente para acelerar com IA sem travar depois.

**Atividades técnicas:**

1. **Repositório & Monorepo**
   - Criar repositório `blueshark-govtech-mvp` (privado).
   - Estrutura monorepo (Turborepo ou Nx ou simples `apps/` + `packages/`):
     - `/apps/govtech-web` (Next.js)  
     - `/apps/govtech-api` (NestJS ou Express bem estruturado)  
     - `/packages/shared` (tipos, utils)  

2. **Infra Dev (local & cloud)**
   - Docker Compose simples:
     - `api`  
     - `web`  
     - `postgres`
   - Configurar `.env` com variáveis sensíveis.

3. **Autenticação Básica (sem SSO ainda)**
   - Modelos iniciais: `User`, `Role`, `Institute`.
   - Implementar login simples (email + senha hash) com JWT.
   - Seed de usuários:
     - admin global  
     - diretor ITCV  
     - inspetor IGAE

4. **CI/CD inicial**
   - GitHub Actions:
     - build web  
     - build API  
     - rodar testes básicos  
   - Deploy automatizado em ambiente de **staging** (ou manual via Docker, se preferir).

**Uso de IA:**

- Pedir ao **ChatGPT**:
  - Scaffold inicial do monorepo  
  - Modelo de tabelas básicas (User, Institute, Role)  
  - Config inicial do NestJS + Postgres  
- Usar **GitHub Copilot**:
  - Para gerar boa parte dos boilerplates (controllers, DTOs, services).

---

### Semana 2 — Modelo de Dados + GovTech Core

**Objetivos:**

- Fechar o **modelo de dados mínimo** para MVP GovTech.  
- Expor CRUDs básicos via API.

**Domínios a modelar (mínimo):**

- `Institute` (ITCV, IGAE, INSP, IGQPI, ERIS, Ministério)  
- `Municipality/County` (ilhas, concelhos)  
- `Establishment` (hotel, restaurante, processador, embarcação — para o MVP, pelo menos hotéis/restaurantes)  
- `Inspection` (visitas, tipo, status, score)  
- `Incident` (denúncias, origem, gravidade)  

**Atividades técnicas:**

1. **Modelagem com IA:**
   - Você e Ricardo definem campos em alto nível.
   - Pedir ao ChatGPT:
     - Sugestão de schema SQL para Postgres.
     - Scripts de migração (TypeORM/Prisma, etc).

2. **Implementar `GovTech Service` (MVP)**
   - Endpoints:
     - `GET /institutes`  
     - `GET /municipalities`  
     - `GET /establishments`  
     - `GET /inspections`  
     - `POST /inspections` (básico)  
     - `GET /incidents`  
     - `POST /incidents` (básico)  

3. **Seed de Dados**
   - Carga fake de:
     - 22 concelhos (Cabo Verde)  
     - alguns hotéis e restaurantes por concelho  
     - algumas inspeções e incidentes de exemplo  

**Uso de IA:**

- ChatGPT/GitHub Copilot:
  - gerar DTOs, models, migrations, seeds.
- IA para gerar dados fake coerentes para teste/demo.

---

### Semana 3 — Dashboards + Heatmap

**Objetivos:**

- Ter um **Dashboard Governamental inicial** já navegável.  
- Mostrar o **Mapa de Calor (Cabo Verde)** com risco por concelho.

**Atividades técnicas:**

1. **Heatmap (Frontend)**
   - Next.js + React + biblioteca de mapas (Leaflet, Mapbox GL ou Google Maps).  
   - Implementar:
     - mapa de Cabo Verde  
     - coloração por concelho:
       - verde → risco baixo  
       - amarelo → intermediário  
       - vermelho → alto  
     - **On click**: abrir painel lateral com:
       - Nº de estabelecimentos  
       - Nº de inspeções  
       - Nº de incidentes (últimos X dias)

2. **API para Heatmap**
   - Endpoint: `GET /govtech/heatmap-summary`:
     - Por concelho:
       - `count_establishments`  
       - `count_inspections`  
       - `count_incidents`  
       - `risk_score` calculado (fórmula simples em MVP)

3. **Dashboard Cards**
   - Cards no topo:
     - Total de inspeções (30 dias)  
     - Incidentes críticos  
     - % concelhos “verdes” vs “vermelhos”  
     - Ranking de concelhos mais críticos  

**Uso de IA:**

- ChatGPT:
  - gerar código base do Heatmap em React (já fizemos parte disso em outro trecho).  
- Copilot:
  - completar componentes, hooks, funções de agregação.  
- IA para ajudar na escolha de fórmula inicial de `risk_score`.

---

### Semana 4 — Fluxo Completo de Inspeção

**Objetivos:**

- Permitir que um inspetor execute uma inspeção **do início ao fim**.

**Atividades técnicas:**

1. **Tela de Lista de Inspeções**
   - Filtros por:
     - data  
     - concelho  
     - situação (`agendada`, `em andamento`, `concluída`)  
   - Ordenação por risco, data.

2. **Tela de Detalhe da Inspeção**
   - Dados do estabelecimento  
   - Checklist:
     - perguntas básicas (MVP)  
     - campos: conforme sim/não/não se aplica  
   - Registro de evidências:
     - upload de fotos (1–3 fotos)  
     - observações do inspetor

3. **Persistência**
   - API:
     - `POST /inspections/{id}/answers`  
     - `POST /inspections/{id}/attachments`  
   - Atualizar `risk_score` do estabelecimento e concelho após conclusão.

4. **UX mínima agradável**
   - Barra de progresso da inspeção  
   - Indicação visual de itens críticos  
   - Alertas simples (“faltam X itens críticos sem resposta”).

**Uso de IA:**

- ChatGPT:
  - gerar modelo inicial de checklist + código do form.  
- Copilot:
  - acelerar implementação dos formulários, validações, uploads.  

---

### Semana 5 — Incidentes + Citizen Reporter (Mínimo)

**Objetivos:**

- Permitir registrar incidentes e vê-los impactando a visão de risco.

**Atividades técnicas:**

1. **Registro de Incident (Backoffice)**
   - Tela para inspetor / diretor registrar incidentes:
     - tipo (intoxicação, má higiene, reclamação grave etc.)  
     - descrição  
     - estabelecimento  
     - data  
     - gravidade (1–5)

2. **Endpoint de Citizen Reporter (API externa)**
   - `POST /public/incidents/report` (para uso futuro por app citizen/web)  
   - Campos mínimos:
     - localização aproximada  
     - tipo de problema  
     - descrição  
     - opcional: foto

3. **Impacto no Heatmap**
   - Regra simples:
     - incidentes recentes (30 dias) com gravidade alta  
       → aumentam `risk_score` do concelho.  

4. **Lista de Incidentes**
   - Tela no GovTech:
     - Filtros por:
       - concelho  
       - gravidade  
       - status de tratamento (aberto/em tratamento/fechado)

**Uso de IA:**

- ChatGPT:
  - sugerir categorias padrão de incidentes  
  - desenhar modelo de dados para `Incident`  
- Copilot:
  - gerar rapidamente os handlers de API, queries, UI.

---

### Semana 6 — MVP Academy Básico + Integração

**Objetivos:**

- Colocar **Academy Básico** no ar:
  - trilhas mínimas para inspetores e diretores  
  - registrar conclusão  
- Conectar com o GovTech (indicador de % equipe treinada).

**Atividades técnicas:**

1. **Academy — Domínio mínimo**
   - Modelo:
     - `Track` (trilha)  
     - `Lesson` (aula/unidade)  
     - `Enrollment` (matrícula)  
     - `Progress` (progresso)  
   - API:
     - `GET /academy/tracks`  
     - `POST /academy/enroll`  
     - `POST /academy/complete-lesson`  
     - `GET /academy/summary-by-institute`

2. **Tela simples de Academy**
   - Na mesma aplicação Next.js (área “Academy” no menu):
     - Lista de trilhas (ex: “Formação Básica Inspetor GovTech”)  
     - Botão de marcar aula concluída (MVP sem player avançado)  

3. **Integração com GovTech Dashboard**
   - Para cada instituto:
     - `% de inspetores com trilha básica concluída`  
   - Exibir no dashboard:
     - “Capacitação Inspetores ITCV: 72%” etc.

4. **IA Tutor (versão super simples)**
   - Uma caixa de chat:
     - `POST /ai/academy/tutor`  
   - MVP:
     - integra com ChatGPT com **prompt fixo** + base normativa inicial.  

**Uso de IA:**

- ChatGPT:
  - gerar scaffolding do domínio Academy (modelos, APIs, telas).  
- Copilot:
  - completar implementações repetitivas.  
- IA para preparar alguns textos de aula (conteúdo) em paralelo.

---

### Semana 7 — GovTech Copilot + Relatórios + Refinos

**Objetivos:**

- Entregar um **GovTech Copilot funcional para demo**.  
- Ter **PDF de relatório simples** para inspeções.  
- Polir UX para apresentação.

**Atividades técnicas:**

1. **GovTech Copilot (Backend)**
   - Endpoint:
     - `POST /ai/govtech/copilot`
   - Entrada:
     - contexto da inspeção (respostas, fotos **(somente metadados)**)  
     - histórico do estabelecimento  
     - tipo de incidente (se houver)  
   - Saída:
     - resumo da situação  
     - sugestão de enquadramento legal (texto livre, com disclaimer)  
     - sugestão de plano de ação (curto prazo, longo prazo)

2. **GovTech Copilot (Frontend)**
   - Na tela de inspeção concluída:
     - botão “Pedir análise da IA”  
   - Exibir resposta formatada:
     - bloco de texto  
     - bullets de ações sugeridas  

3. **Relatório PDF**
   - Endpoint:
     - `GET /inspections/{id}/report.pdf`
   - Conteúdo:
     - dados do estabelecimento  
     - itens do checklist  
     - evidências listadas  
     - resumo da IA (GovTech Copilot) incorporado no PDF  

4. **Refino UX/UI**
   - Ajuste de cores, ícones, tipografia.  
   - Ajustar textos para português claro e executivo.

**Uso de IA:**

- ChatGPT:
  - prompt design do GovTech Copilot (definir instruções, tom de voz, disclaimers).  
- IA para exportar template de relatório em HTML → PDF (ex: sugestão de libs, estrutura).  

---

### Semana 8 — Hardening, Demonstração e Ajustes

**Objetivos:**

- Garantir que tudo “aguente” a demo.  
- Fechar um **roteiro de demonstração** didático para as autoridades.

**Atividades técnicas:**

1. **Hardening**
   - Validar:
     - permissões de acesso  
     - autenticação  
     - integridade dos dados  
   - Carga de dados mais realista (seed de:
     - concelhos  
     - estabelecimentos  
     - inspeções históricas  
     - incidentes)

2. **Testes**
   - Roteiros manuais:
     - fluxo completo de inspeção  
     - registro de incidente  
     - impacto no heatmap  
     - fluxo Academy básico + reflexo no dashboard GovTech  
     - uso do GovTech Copilot

3. **Script de Demo**
   - Roteiro passo a passo para apresentação:
     1. Visão geral do dashboard nacional  
     2. Heatmap mostrando concelho crítico  
     3. Abrir concelho → lista de estabelecimentos  
     4. Mostrar inspeção recente + relatório  
     5. Pedir análise da IA (GovTech Copilot)  
     6. Mostrar incidente grave entrando no sistema  
     7. Ver mudança no risco  
     8. Mostrar que X% da equipa já está formada no Academy  

4. **Documentação Executiva para a Reunião**
   - 2–3 páginas técnicas resumidas:
     - arquitetura  
     - segurança  
     - escalabilidade  
   - 2–3 páginas de visão de futuro (como conectar Mobile & IA, Citizen app, etc.)

**Uso de IA:**

- ChatGPT:
  - ajudar a escrever script da demo  
  - revisar textos de UX e documentação executiva  
- Copilot:
  - pequenos ajustes finais no código.  

---

## 5. Escopo Fora do MVP (Mas Preparado na Arquitetura)

Para não explodir o esforço de 60 dias, ficam **explicitamente fora** do MVP:

- App mobile separado para inspetores (pode ser fase 2).  
- Player avançado do Academy (SCORM, vídeo com sync, simuladores IoT).  
- Multi-country completo (deixar pronto para “Country” como campo, mas focar em Cabo Verde).  
- Integrações com sistemas externos (ERPs, Booking, TripAdvisor etc.).  
- Orquestração multi-agent (Arquitetura C, event bus etc.).

A Arquitetura A **já suporta** adicionar isso depois **sem recomeçar do zero**.

---

## 6. Resumo Rápido para Explicar ao Ricardo na Reunião

- **Meta**: em 60 dias, ter um **GovTech MVP + Academy Básico** rodando, com:
  - mapas de risco  
  - inspeções registradas  
  - incidentes impactando dashboards  
  - trilhas básicas de formação  
  - um GovTech Copilot funcionando  

- **Arquitetura**:  
  - Next.js + NestJS + Postgres + S3  
  - tudo em uma arquitetura A unificada, simples de manter  
  - com camada de IA desacoplada via API (`/ai/...`)

- **Ferramentas de IA no desenvolvimento**:  
  - GitHub Copilot + ChatGPT para acelerar:
    - modelagem de dados  
    - geração de APIs  
    - formulários  
    - relatórios  
    - testes  
  - Figma + IA para montar rapidamente a interface GovTech.

- **Resultado**:  
  - MVP convincente para governo e parceiros  
  - Base técnica sólida para plugar depois:
    - Academy completo  
    - Mobile & IA  
    - Citizen App  
    - Arquitetura multi-agent, se algum dia fizer sentido.

