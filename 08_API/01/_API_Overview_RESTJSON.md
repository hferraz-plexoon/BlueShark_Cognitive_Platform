# 01_API_Overview.md  
## BlueShark Cognitive Platform — API Overview (Opção A – REST/JSON)

Este documento descreve a **visão geral da API REST/JSON** da **BlueShark Cognitive Platform**, utilizada para:

- Integrar os **Copilots de IA** (GovTech, BestFood, ColdChain, Academy etc.)
- Conectar **sistemas externos** (portais governamentais, ERPs, LMS, apps móveis)
- Permitir consultas a **RAG normativo** (leis, normas, checklists, políticas)
- Expôr dados para **dashboards**, **GovTech Suite** e **Academy**

> Modelo: **REST + JSON**, com possibilidade de **GraphQL** em uma fase futura.  
> Segurança: **HTTPS + JWT + API Keys + RBAC**.

---

## 1. Objetivos da API

1. **Unificar acesso** aos Copilots e à base de conhecimento BlueShark.  
2. **Permitir integração simples** com sistemas públicos e privados (Ministérios, ITCV, IGAE, INSP, IGQPI, ERIS, hotéis, restaurantes, consultorias).  
3. **Padronizar entradas e saídas** (payloads JSON estáveis, versionados).  
4. **Garantir segurança e rastreabilidade**, com logs adequados para auditoria.  
5. **Facilitar evolução futura** para um modelo de plataforma de agentes (multi-copilot, orquestração, plugins).

---

## 2. Princípios de Design

- **RESTful e previsível**  
  - Recursos, verbos HTTP e códigos de status consistentes.

- **JSON-first**  
  - Todas as respostas e requests em JSON UTF-8; exceções apenas para arquivos binários.

- **Versionamento explícito**  
  - Versão na URL: `/api/v1/...`  
  - Políticas detalhadas em `04_Versioning_Guidelines.md`.

- **Segurança por padrão**  
  - HTTPS obrigatório  
  - JWT + API Key + roles (RBAC)  
  - Trilha de auditoria para chamadas sensíveis.

- **Idempotência em operações críticas**  
  - Uso opcional de `Idempotency-Key` em headers para operações que criam registros relevantes (incidentes, inspeções, ações corretivas).

- **Observabilidade integrada**  
  - Logs estruturados de request/response (metadados)  
  - Correlation ID (`X-Request-Id`) para rastreio ponta a ponta.

---

## 3. Estrutura Geral da API

### 3.1. Base URLs (placeholders)

Ambientes típicos (a ajustar conforme DevOps):

- **Produção (Cabo Verde)**  
  `https://api.blueshark.cv/api/v1/`

- **Homologação / Sandbox**  
  `https://sandbox.api.blueshark.cv/api/v1/`

- **Desenvolvimento interno**  
  `https://dev.api.blueshark.local/api/v1/`

> Observação: nomes de domínio são sugestivos; definidos pela BeSafe Digital na fase de DevOps.

---

### 3.2. Grupos de Endpoints (Visão Macro)

A API é organizada em **grupos funcionais**:

1. **Auth & Identity**  
   - `/auth/login`  
   - `/auth/refresh`  
   - `/auth/logout`  
   - `/auth/me`

2. **Copilots de IA (Cognitivos)**  
   - `/copilots/query` — endpoint genérico multi-copilot  
   - `/copilots/{copilotId}/query` — endpoint específico por agente  
   - `/copilots/{copilotId}/sessions` — histórico de sessões  

3. **Knowledge Base & RAG**  
   - `/knowledge/documents` — cadastro e gestão de documentos  
   - `/knowledge/search` — busca contextual (RAG)  
   - `/knowledge/tags` — taxonomias e categorias  

4. **GovTech & Incidentes**  
   - `/govtech/incidents` — registro de casos (intoxicações, denúncias)  
   - `/govtech/inspections` — inspeções e autos digitais  
   - `/govtech/risk-maps` — dados para heatmaps e dashboards  
   - `/govtech/institutes` — ITCV, IGAE, INSP, IGQPI, ERIS etc.

5. **Academy & Treinamentos**  
   - `/academy/courses` — cursos e trilhas  
   - `/academy/enrollments` — matrículas  
   - `/academy/progress` — progresso por aluno/unidade  
   - `/academy/certificates` — certificados digitais  

6. **Checklists & Auditorias**  
   - `/audits/checklists`  
   - `/audits/runs`  
   - `/audits/findings`  
   - `/audits/actions`  

7. **Admin & Configuração**  
   - `/admin/tenants` — multi-tenant  
   - `/admin/organizations`  
   - `/admin/users`  
   - `/admin/roles`  

Cada grupo será detalhado em **02_Copilots_Endpoints.md** e, futuramente, em arquivos específicos adicionais, se necessário.

---

## 4. Modelo de Autenticação e Autorização (Resumo)

> Detalhes completos em `03_Authorization_Model.md`.

- Autenticação primária via **JWT**:
  - Bearer token no header:  
    `Authorization: Bearer <jwt-token>`
- Possibilidade de **API Keys** para integrações máquina-a-máquina (gov, ERPs).
- **RBAC (Role-Based Access Control)**:
  - Roles como: `GOV_INSPECTOR`, `GOV_DIRECTOR`, `CONSULTANT`, `HOTEL_MANAGER`, `RESTAURANT_MANAGER`, `ACADEMY_TUTOR`, `ACADEMY_LEARNER`.
- **Scopes** adicionais para restringir ações sensíveis, por exemplo:
  - `govtech:incidents:read`
  - `govtech:incidents:write`
  - `copilots:govtech:query`
  - `academy:certificates:issue`

---

## 5. Convenções de Requests & Responses

### 5.1. Headers

Recomendação padrão:

```http
Authorization: Bearer <jwt-token>
Content-Type: application/json
Accept: application/json


X-Request-Id: <uuid-gerado-pelo-cliente-ou-servidor>
Idempotency-Key: <uuid-para-operações-não-repetíveis>  # opcional
````

---

### 5.2. Sucesso — Envelope de Resposta

{
  "success": true,
  "data": { ... },
  "meta": {
    "requestId": "a3d5-...",
    "timestamp": "2025-12-03T10:15:30Z",
    "version": "v1"
  }
}

---

### 5.3. Erro — Envelope de Resposta

Todas as respostas de sucesso seguem formato:

{
  "success": false,
  "error": {
    "code": "INVALID_INPUT",
    "message": "Campo 'copilotId' é obrigatório.",
    "details": {
      "field": "copilotId"
    }
  },
  "meta": {
    "requestId": "a3d5-...",
    "timestamp": "2025-12-03T10:16:01Z",
    "version": "v1"
  }
}

Códigos de erro típicos:
- UNAUTHORIZED
- FORBIDDEN
- NOT_FOUND
- INVALID_INPUT
- CONFLICT
- RATE_LIMITED
- INTERNAL_ERROR

---

## 6. Exemplos de Fluxos Típicos

### 6.1. Fluxo — GovTech Copilot para Investigação de Surto

1. Inspetor ou analista de saúde pública autentica no sistema.

2. Sistema (ou UI) chama:
POST /api/v1/copilots/govtech/query
{
  "question": "Quais restaurantes na Ilha do Sal tiveram incidentes de intoxicação nos últimos 30 dias?",
  "context": {
    "region": "Ilha do Sal",
    "timeWindowDays": 30
  }
}

3. O backend:
- usa RAG para buscar incidentes, inspeções, evidências,
- roda o modelo de IA (GovTech Copilot),
- gera resposta estruturada + insights.

Retorno:
{
  "success": true,
  "data": {
    "answer": "Foram registrados 3 incidentes relevantes...",
    "incidents": [ ... ],
    "recommendedActions": [ ... ]
  }
}

---

### 6.2. Fluxo — Academy Copilot (Tutor para Aluno)

1. Aluno acessa aula no app Academy.

2. Ao clicar em “Perguntar à IA”, o app chama:
POST /api/v1/copilots/academy-tutor/query

{
  "userId": "user_123",
  "courseId": "course_haccp_basic",
  "lessonId": "lesson_05_ccp",
  "question": "Explique de novo o que é um PCC em HACCP com um exemplo simples."
}

O Academy Copilot usa:
- trilha do aluno,
- conteúdo oficial do curso,
- base normativa HACCP.

Resposta é enviada com explicação didática + exemplos.

---

### 6.3. Fluxo — Registro de Incidente pelo GovTech

1. Sistema de Citizen Safety Reporter ou outro front chama:
POST /api/v1/govtech/incidents

{
  "source": "citizen_reporter",
  "type": "food_poisoning",
  "location": {
    "latitude": 16.7412,
    "longitude": -22.9491,
    "region": "Praia",
    "island": "Santiago"
  },
  "description": "Grupo de turistas com sintomas após jantar em restaurante X.",
  "reportedAt": "2025-12-03T09:00:00Z",
  "metadata": {
    "suspectedEstablishmentId": "rest_789"
  }
}

Backend:
- valida,
- grava na base,
- dispara fila para IA de triagem,
- notifica INSP + ERIS se gravidade alta.

Retorno:
{
  "success": true,
  "data": {
    "incidentId": "inc_abc123",
    "status": "UNDER_ANALYSIS"
  }
}

---

7. Não Funcionais (NFRs) da API

- Desempenho
  - 95% das requisições simples (GET) ≤ 300 ms.
  - Chamada de Copilot (com IA) ≤ 3–6 segundos em média.

- Escalabilidade
  - Projetada para escalar horizontalmente via containers/Kubernetes.
  - Rate limiting configurável por tenant e por chave de API.

- Resiliência
  - Circuit breaker para dependências externas (LLMs, bancos, motores de busca).
  - Requisições críticas com retries com backoff exponencial.

Auditoria
- Log de:
  - quem chamou
  - qual recurso
  - qual tenant
  - data/hora
  - resultado (sucesso/erro)

- Sem logar conteúdo sensível de payloads (apenas metadados ou conteúdo mascarado).

---

## 8. Relacionamento com Outros Documentos

- 02_Copilots_Endpoints.md
  → Define em detalhe os endpoints por Copilot (GovTech, Academy, BestFood, ColdChain, ESG etc.).

- 03_Authorization_Model.md
  → Especifica JWT, roles, scopes, multi-tenant e regras de acesso.

- 04_Versioning_Guidelines.md
  → Define como serão gerenciadas versões da API, depreciação e compatibilidade.

---

## 9. Conclusão

Este documento define a espinha dorsal da API do BlueShark Cognitive Platform:
- REST/JSON
- versionada (/api/v1)
- segura (JWT + API Keys + RBAC)
- preparada para GovTech, Academy, Copilots setoriais e expansão CPLP.

Os próximos arquivos da pasta 08_API detalham os endpoints específicos, o modelo de autorização e a estratégia de versionamento para garantir estabilidade, governança e evolução segura da plataforma.
