# 04_Architecture  
BlueShark Cognitive Platform  
(BeSafe Digital — Versão 2025)

Este documento descreve a **arquitetura técnica unificada (Opção A)** da  
**BlueShark Cognitive Platform**, já preparada para evoluir, em fases,  
para uma **arquitetura multi-agent distribuída (Opção C)**.

---

## 1. Objetivos da Arquitetura

1. Permitir entregar, em até **60 dias**, um MVP robusto de:
   - **GovTech Suite (MVP)** – dashboards + inspeção + IA assistida  
   - **Academy (MVP)** – trilhas básicas + certificação + IA tutor  

2. Manter uma base sólida para futura expansão:
   - Integração com **BlueShark Mobile & IA**  
   - Inclusão de **Citizen Safety Reporter**  
   - Adoção de **Agentes Cognitivos Especializados (Copilots)**  

3. Garantir:
   - **Multi-tenant** (país, instituto, empresa)  
   - **Multi-country** (Cabo Verde hoje, CPLP depois)  
   - **Multi-idioma** (PT, EN, Crioulo inicialmente)  
   - **IA regulada via RAG** (base normativa: leis Cabo Verde + ISO + políticas)  

---

## 2. Visão de Alto Nível

A arquitetura unificada (Opção A) é organizada em **5 camadas principais**:

1. **Camada de Experiência (UX Layer)**  
   - Portais Web (GovTech, Academy, Admin)  
   - Aplicativos Mobile (Inspect App, Learner App — fase posterior)  

2. **Camada de Orquestração & API (API Gateway / BFF)**  
   - Gateway único de entrada (REST/GraphQL)  
   - BFF (Backend for Frontend) por tipo de cliente (web gov, web academy, mobile)  

3. **Camada de Serviços de Negócio (Core Services)**  
   - Serviços lógicos independentes por domínio, mas **no mesmo cluster/backend**  
   - Cada serviço com seu modelo de dados, compartilhando:
     - auth  
     - tenants  
     - logging  
     - eventos internos  

4. **Camada de Dados (Data Layer)**  
   - Banco relacional principal (PostgreSQL)  
   - Armazenamento de arquivos (S3 compatível)  
   - Data Warehouse / Lake para analytics (fase 2)  
   - Event Store / fila (para futuro modelo C)  

5. **Camada de IA & RAG (AI Layer)**  
   - RAG Engine (com índices por domínio: Academy, GovTech, Mobile)  
   - Orquestrador de LLMs  
   - Visão Computacional (VC) para evidências  
   - Guardrails, logging de prompts, observabilidade de IA  

---

## 3. Componentes Principais

### 3.1. Camada de Experiência (UX Layer)

#### 3.1.1. Portais Web

**GovTech Web Portal**

- Perfil: diretores, inspetores, analistas de políticas públicas  
- Funcionalidades:
  - mapas de risco (heatmap Cabo Verde)  
  - dashboards por instituto (ITCV, IGAE, INSP, IGQPI, ERIS)  
  - listas de inspeções, autos, incidentes  
  - acesso ao GovTech Copilot (IA)  
  - exportação de relatórios (PDF/Excel)  

**Academy Web Portal**

- Perfil: alunos, gestores de RH, coordenadores de treinamento  
- Funcionalidades:
  - catálogo de trilhas  
  - player de aulas  
  - quizzes e avaliações  
  - certificados digitais  
  - dashboards de progresso  

**Admin / BeSafe Digital Portal**

- Perfil: BeSafe Digital & Social  
- Funcionalidades:
  - gestão de tenants e contratos  
  - criação de trilhas  
  - publicação de conteúdos  
  - parametrização de regras (mínimo de aprovação etc.)  
  - supervisão de IA e dados  

#### 3.1.2. Aplicativos Mobile (fase 2+)

**Inspector Mobile App (GovTech Inspect)**

- checklists oficiais  
- fotos, vídeos, OCR  
- geolocalização  
- sincronização offline → online  

**Learner Mobile App (Academy)**

- consumo de aulas  
- resolução de quizzes  
- notificações de prazos  
- IA Tutor no celular  

> MVP em 60 dias pode ser **Web-first responsivo**, com mobile vindo na fase seguinte.

---

### 3.2. API Gateway & BFFs

**API Gateway**

- Autenticação JWT / OAuth2  
- Rate limiting  
- Observabilidade (tracing, logs, métricas)  
- Roteamento para serviços internos  

**BFF – GovTech**

- Endpoints adaptados à experiência:
  - `GET /govtech/dashboards`  
  - `GET /govtech/heatmap`  
  - `GET /govtech/inspections`  
  - `GET /govtech/incidents`  
  - `POST /govtech/copilot/query`  

**BFF – Academy**

- Endpoints:
  - `GET /academy/tracks`  
  - `GET /academy/enrollments`  
  - `GET /academy/progress`  
  - `GET /academy/certificates`  
  - `POST /academy/tutor/query`  

**BFF – Admin**

- Endpoints:
  - `GET /admin/tenants`  
  - `POST /admin/content`  
  - `POST /admin/normatives`  
  - `GET /admin/ai/monitoring`  

> Mesmo em arquitetura unificada, os BFFs já preparam a transição  
> para uma arquitetura mais modular/multi-service no futuro.

---

### 3.3. Core Services (Domínios de Negócio)

#### 3.3.1. Auth & Identity Service

Responsável por:

- autenticação (e-mail/senha, SSO futuro)  
- gestão de perfis:
  - governo (institutos)  
  - empresas (hotéis, restaurantes, processadores)  
  - consultores  
  - alunos  
- RBAC/ABAC:
  - roles por perfil  
  - escopos por tenant (país, instituto, empresa)  
  - permissões por módulo (Academy, GovTech, Mobile&IA)  

---

#### 3.3.2. Tenant & Org Registry Service

- Cadastro de:
  - países  
  - institutos governamentais  
  - empresas  
  - unidades operacionais  
- Metadados:
  - ilhas, concelhos  
  - categorias de risco  
  - vínculos com módulos habilitados  

---

#### 3.3.3. Academy Service

Responsável por toda lógica de:

- trilhas de aprendizado  
- cursos, aulas, quizzes  
- matrículas  
- progresso  
- notas  
- certificação automática  
- regras de conclusão (ex: 80% acertos + 100% módulos críticos)  

Integrações importantes:

- com **AI Tutor Service** (explicar, gerar exercícios, tirar dúvidas)  
- com **GovTech** (indicadores de % da força de trabalho qualificada)  

---

#### 3.3.4. Implementation Hub Service (Futuro / Fase 2+)

Mesmo estando no mesmo backend, é um serviço separado:

- projetos de implantação  
- checklists de implantação  
- evidências (foto, vídeo, PDF)  
- plano de ação  
- auditorias da BeSafe Digital  

> No MVP em 60 dias, este serviço pode estar **parcialmente implementado**  
> ou apenas preparado na arquitetura, focando GovTech + Academy.

---

#### 3.3.5. GovTech Service

Domínio central do MVP:

- gestão de inspeções  
- gestão de incidentes  
- vinculação com normas/leis  
- regra de decisão para:
  - auto de infração  
  - advertência  
  - recomendação  
  - interdição  

Integra com:

- **Heatmap Engine** (por concelho/região)  
- **Incident Service**  
- **AI Copilot (GovTech Copilot)** para:
  - sugerir enquadramento legal  
  - propor plano de ação  
  - analisar histórico da empresa  

---

#### 3.3.6. Incident & Citizen Reporter Service

- registros de incidentes:
  - intoxicação alimentar  
  - má higiene  
  - péssimo atendimento  
- relatórios por:
  - cidadão  
  - turista  
  - empresa  
  - governo  
- classificação por IA:
  - gravidade  
  - tipo  
  - urgência  
  - instituto competente (ERIS, INSP, ITCV, IGAE etc.)  

---

#### 3.3.7. Notification Service

- envio de e-mails e push  
- templates por tipo de alerta:
  - certificado emitido  
  - trilha atrasada  
  - risco crítico  
  - nova inspeção marcada  
  - incidente grave  

---

### 3.4. Data Layer

#### 3.4.1. Banco de Dados Operacional

- **PostgreSQL**
  - schemas segmentados:
    - `core` (auth, tenant, org)  
    - `academy`  
    - `govtech`  
    - `incidents`  
  - cada tenant com isolamento lógico (linha + coluna com `tenant_id`)  

#### 3.4.2. Armazenamento de Arquivos

- S3 compatível:
  - evidências de inspeção (foto, vídeo)  
  - documentos PDF  
  - anexos de normas  

#### 3.4.3. Data Warehouse / Analytics (fase 2+)

- Redshift / BigQuery / Snowflake (decisão posterior)  
- Alimentado por ETL/ELT noturno ou near-real time  
- Base dos dashboards analíticos avançados  

---

### 3.5. AI Layer (RAG + Reasoning)

Mesmo na arquitetura unificada, a IA é construída como **serviços desacoplados**,  
já pensando na migração para **Arquitetura C (multi-agents)**.

#### 3.5.1. RAG Engine

- Índices por domínio:
  - `academy_normatives`  
  - `govtech_normatives`  
  - `mobile_ia_normatives`  
- Fontes:
  - leis de Cabo Verde  
  - decretos  
  - normas ISO (22000, 14001, 45001, 21401 etc.)  
  - políticas internas BeSafe Digital  
- Funções:
  - recuperar contexto relevante  
  - enriquecer prompts de copilots  
  - manter trilha de auditoria (o que foi usado como base)  

#### 3.5.2. Copilot Orchestrator

- Interface única usada pelos frontends:
  - `POST /ai/copilot/query`  
- Roteia para “personalidades”:
  - `academy_tutor`  
  - `govtech_inspector_assistant`  
  - `policy_analyst`  
  - `implementation_consultant`  
- Aplica:
  - prompt engineering  
  - guardrails  
  - logging de conversas  
  - anonimização quando necessário  

#### 3.5.3. Vision & Document AI

- Análise de:
  - fotos de cozinha, limpeza, embarcações  
  - documentos (PDF de relatórios, normas locais, laudos)  
- Usa:
  - OCR  
  - classificação de imagem  
  - detecção de padrões (EPI, limpeza, desorganização etc.)  

---

## 4. Segurança, Governança e Observabilidade

### 4.1. Segurança

- Autenticação: OAuth2 / OIDC  
- Autorização: RBAC + ABAC (por tenant, perfil, módulo)  
- Criptografia:
  - em trânsito: TLS 1.2+  
  - em repouso: KMS no banco de dados e S3  
- Logs de auditoria:
  - acessos  
  - mudanças de configuração  
  - decisões da IA em contextos críticos  

### 4.2. Observabilidade

- Logs estruturados (JSON)  
- Tracing distribuído (OpenTelemetry)  
- Métricas por serviço:
  - latência  
  - erro  
  - uso de IA  
  - consumo por tenant  

---

## 5. Deploy, Pipelines e Ambientes

### 5.1. Ambientes

- **DEV** – desenvolvimento contínuo  
- **STG** – homologação, testes com dados anonimizados  
- **PRD** – produção  

### 5.2. Deploy

- Containers (Docker)  
- Orquestração:
  - ECS/Fargate ou Kubernetes (a decidir)  
- Infra como código:
  - Terraform  

### 5.3. CI/CD

- GitHub Actions:
  - build  
  - testes  
  - segurança básica (lint, SCA)  
  - deploy automatizado por ambiente  

---

## 6. Estratégia de Evolução para Arquitetura C (Multi-Agent)

A arquitetura foi propositalmente desenhada para que, depois do MVP,  
a BeSafe Digital possa migrar progressivamente para a **Arquitetura C**, com agentes:

- **Academy Agent**  
- **GovTech Agent**  
- **Citizen Safety Agent**  
- **Inspector Agent**  
- **Implementation Agent**  
- **Policy & Normatives Agent**  

### 6.1. Etapas da Evolução

1. **Isolamento de Serviços**  
   - separar fisicamente alguns serviços do core:
     - AI Layer  
     - Incident Service  
     - Academy Service  
     - GovTech Service  

2. **Introdução de Event Bus**  
   - Kafka / RabbitMQ / SNS+SQS  
   - eventos:
     - `inspection.completed`  
     - `incident.reported`  
     - `course.completed`  
     - `certificate.issued`  
     - `risk.level.changed`  

3. **Transformação de Serviços em Agentes**  
   - cada serviço passa a:
     - consumir eventos  
     - tomar decisões (via IA)  
     - publicar novos eventos  
   - ex.:
     - `GovTech Agent` ouve `incident.reported` e decide:
       - agendar inspeção  
       - rebaixar risco da empresa  
       - alertar instituto  

4. **Orquestração Avançada**  
   - camada de **Orchestration Engine**:
     - define “playbooks” de reação  
     - compõe respostas de múltiplos agentes  

5. **Multi-Cloud / Multi-Region**  
   - replicação para novos países  
   - agentes específicos por jurisdição  

---

## 7. Conclusão

- A **Arquitetura Unificada (Opção A)**:
  - é suficiente para impressionar na reunião em 60 dias  
  - permite entregar um MVP sólido de **GovTech + Academy**  
  - não engessa o futuro  

- A forma como os domínios foram separados (core services + AI Layer)  
  já prepara a plataforma para se tornar, com o tempo, uma  
  **Arquitetura Multi-Agent (Opção C)**:

  - GovTech mais inteligente  
  - Academy hiper-personalizada  
  - Copilots especializados por módulo (ColdChain, BestFood, ESG, SafeStay, GuestExperience)  
  - Cidadãos e turistas como sensores em tempo real  

A BlueShark Cognitive Platform nasce como uma base unificada,  
mas com DNA preparado para se tornar uma **infraestrutura cognitiva nacional**  
de segurança alimentar, turismo e desenvolvimento social  
liderada pela **BeSafe Digital**.
