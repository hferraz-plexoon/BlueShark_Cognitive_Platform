# 02 — Copilots Endpoints Specification  
BlueShark Cognitive Platform – API Layer  
Versão 2025

---

## 1. Objetivo do Documento
Este documento descreve as **APIs dos agentes cognitivos (Copilots)** da BlueShark Cognitive Platform, incluindo:

- Estrutura padrão de endpoints  
- Formatos de request/response  
- Modelos de validação  
- Políticas de contexto, memória e RAG  
- Integração com o módulo GovTech e Academy  
- Interfaces REST e WebSocket  

O objetivo é padronizar a integração entre front-end, back-end e serviços de IA.

---

## 2. Lista de Copilots (Escopo Oficial)

| Copilot | Domínio | Descrição |
|--------|---------|-----------|
| Academy Copilot | Educação | Tutor, explicação, reforço, quizzes |
| Implementation Copilot | Implantação | Auxílio em evidências, planos, PDCA |
| ColdChain Copilot | Pesca | Cadeia de frio, temperaturas, lotes |
| BestFood Copilot | HACCP | Segurança alimentar, POPs, PCCs |
| ESG Copilot | Sustentabilidade | Indicadores ESG + ações |
| SafeStay Copilot | Higiene/SSO | Biossegurança, housekeeping |
| GuestExperience Copilot | Turista | NPS, atendimento, acessibilidade |
| Audit Copilot | Auditoria | Cruzamento de normas e NCs |
| GovTech Copilot | Governo | Leis, decretos, fiscalização |
| CitizenSafety Copilot | População | Classificação de denúncias |
| GlobalStandards Copilot | Normas ISO | ISO, FAO, OMS, Codex Alimentarius |

---

## 3. Estrutura Geral dos Endpoints

Todos os Copilots seguem:

```
POST /api/v1/copilot/{name}/ask
POST /api/v1/copilot/{name}/analyze
POST /api/v1/copilot/{name}/suggest
POST /api/v1/copilot/{name}/rag
WS  /ws/copilot/{name}
```

### 3.1. Convenções
- **name** sempre em lowercase  
  Ex.: `academy`, `govtech`, `coldchain`
- **Content-Type:** `application/json`
- **Auth:** Bearer Token (JWT)  
- **Tenant-Header:** `X-Tenant-ID`
- **Country-Header:** `X-Country-Code` (CV, BR, AO, MZ, PT)

---

## 4. Estrutura Padrão de Payload

### 4.1. Entrada (Request)

```json
{
  "message": "Como aplico o PCC 01 no lote 2025-118?",
  "context": {
    "user_id": "u123",
    "role": "auditor",
    "organization_id": "rest001",
    "module": "bestfood",
    "language": "pt",
    "country": "CV"
  },
  "attachments": [
    {
      "type": "image",
      "url": "https://cdn.blueshark.cv/evidence/1234.png"
    }
  ]
}
```

### 4.2. Saída (Response)

```json
{
  "answer": "...",
  "sources": [
    { "type": "law", "ref": "DL 04/2009" },
    { "type": "iso", "ref": "ISO 22000:2018" }
  ],
  "actions": [
    "Registrar temperatura correta",
    "Corrigir fluxo de manipulação"
  ],
  "confidence": 0.92
}
```

---

## 5. Endpoints por Copilot

---

# 5.1 — Academy Copilot

### `POST /api/v1/copilot/academy/ask`
Explicações, reforço pedagógico.

### `POST /api/v1/copilot/academy/quiz`
Geração automática de exercícios.

### `POST /api/v1/copilot/academy/summary`
Resumo de aulas, PDFs e vídeo.

---

# 5.2 — Implementation Copilot

### `POST /api/v1/copilot/implementation/analyze-evidence`
Avalia fotos, vídeos, PDFs e gera NCs.

### `POST /api/v1/copilot/implementation/plan`
Gera plano PDCA automático.

---

# 5.3 — ColdChain Copilot

### `POST /api/v1/copilot/coldchain/check-temperature`
Classificação de risco térmico.

### `POST /api/v1/copilot/coldchain/traceability`
Explica cadeia de custódia do lote.

---

# 5.4 — BestFood Copilot

### `POST /api/v1/copilot/bestfood/pcc`
Aplicação de PCCs e POPs.

### `POST /api/v1/copilot/bestfood/haccp-diagnosis`
Classificação de NCs HACCP.

---

# 5.5 — ESG Copilot

### `POST /api/v1/copilot/esg/diagnose`
Análise de indicadores ambientais.

### `POST /api/v1/copilot/esg/actions`
Sugestões de ações ESG.

---

# 5.6 — SafeStay Copilot

### `POST /api/v1/copilot/safestay/hygiene`
Análise de limpeza e riscos.

---

# 5.7 — GuestExperience Copilot

### `POST /api/v1/copilot/guestexperience/nps`
Análise de NPS + recomendações.

---

# 5.8 — Audit Copilot

### `POST /api/v1/copilot/audit/check`
Auditoria cruzando leis + ISO + cheklists.

### `POST /api/v1/copilot/audit/report`
Geração de relatório automático.

---

# 5.9 — GovTech Copilot

### `POST /api/v1/copilot/govtech/law-lookup`
Busca e interpretação de leis/diplomas.

### `POST /api/v1/copilot/govtech/inspection`
Auxílio ao inspetor (IGAE/INSP/ERIS/IGQPI).

### `POST /api/v1/copilot/govtech/scenario`
Análise de risco nacional por ilha/região.

---

# 5.10 — CitizenSafety Copilot

### `POST /api/v1/copilot/citizensafety/classify`
Classificação de denúncias (gravidade + tipo).

---

# 5.11 — Global Standards Copilot

### `POST /api/v1/copilot/globalstandards/iso`
Explicações sobre normas ISO/FAO/OMS.

---

## 6. WebSocket Live Interaction

### Endpoint
```
/ws/copilot/{name}
```

### Tipos de Mensagens
- `stream.answer`  
- `stream.suggestion`  
- `stream.source`  
- `stream.alert`

---

## 7. Rate Limits (recomendado)

| Plano | Limite | Janela |
|-------|--------|---------|
| Governo | 500 req/min | 1 min |
| Empresas | 120 req/min | 1 min |
| Cidadão | 20 req/min | 1 min |

---

## 8. Logs & Auditoria

Todos os Copilots devem registrar:

- timestamp  
- usuário  
- tipo de pergunta  
- módulos usados  
- fontes consultadas (RAG)  
- score de segurança  
- score de confiabilidade  

---

## 9. Conclusão

Este documento define **toda a padronização dos endpoints dos Copilots**, garantindo:

- uniformidade da plataforma  
- escalabilidade para CPLP  
- auditabilidade regulatória  
- integração simples via REST e WebSocket  

Pronto para subir no `/08_API/02_Copilots_Endpoints.md`.

