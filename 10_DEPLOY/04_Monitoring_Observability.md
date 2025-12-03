# 04 — Monitoring & Observability  
BlueShark Cognitive Platform — BeSafe Digital  
Versão 1.0 — 2025

Este documento define o **modelo de monitoramento e observabilidade** para toda a BlueShark Cognitive Platform, cobrindo:

- Academy  
- Implementation Hub  
- Mobile Lite  
- GovTech Suite  
- Copilots (AI Agents)  
- RAG Engine  
- Pipelines de IA  
- Multi-país (CV, BR, AO, MZ, PT)  

A plataforma segue os princípios modernos de observabilidade:  
**Logs + Métricas + Traces + Evals de IA + Auditoria Regulamentar.**

---

# 1. Objetivos do Monitoramento

O sistema de monitoramento foi projetado para:

✔ Detectar falhas antes dos usuários  
✔ Monitorar Copilots e IA (qualidade, drift, erros)  
✔ Garantir conformidade legal e regulatória  
✔ Auditar ações sensíveis (GovTech, inspeções, certificações)  
✔ Fornecer métricas para decisões de produto  
✔ Proteger governança nacional (ITCV, IGAE, INSP, ERIS, IGQPI)  
✔ Operar em múltiplos países simultaneamente  

---

# 2. Arquitetura de Observabilidade

```
Application → OpenTelemetry SDK → Collector → CloudWatch / Grafana / S3
                               → OpenSearch (Logs)
                               → Prometheus (metrics)
                               → Jaeger (tracing)
                               → AI Eval Monitoring
```

Componentes:

| Componente | Função |
|-----------|--------|
| **OpenTelemetry (OTel)** | Coleta unificada de logs/metrics/traces |
| **CloudWatch** | Monitoramento AWS nativo |
| **OpenSearch** | Repositório de logs estruturados |
| **Prometheus** | Métricas customizadas |
| **Grafana** | Dashboards centralizados |
| **Jaeger** | Distributed tracing |
| **AI Eval Monitor** | Métricas de IA, RAG, prompts, precisão |
| **S3 Cold Storage** | Arquivo de logs regulatórios (10 anos) |

---

# 3. Tipos de Monitoramento

A observabilidade cobre 5 grandes domínios:

## 3.1. Monitoramento Técnico
- Disponibilidade de APIs  
- Latência por endpoint  
- Erros 4xx e 5xx  
- Performance de banco (RDS/Postgres)  
- Consumo de RAM/CPU (ECS Tasks)  
- Falhas de deploy  
- Filas SQS atrasadas  
- Eventos IoT perdidos  

## 3.2. Monitoramento Operacional
- Taxa de conclusão de treinamentos  
- Taxa de envio de evidências  
- Tempo de resolução de NCs  
- Taxa de implantações concluídas  
- Health do GovTech Dashboards  

## 3.3. Monitoramento de AI / RAG
- Precisão do RAG (RAG Score)  
- Drift de embeddings  
- Erros de chain-of-thought  
- Estabilidade de prompts  
- Toxicidade e vieses  
- Relevância das citações  
- Aderência às leis e normas  

## 3.4. Monitoramento de Segurança
- Tentativas de login inválidas  
- Ataques (SQL injection, brute force)  
- Acesso indevido à API  
- Alterações em normas/regulamentos  
- Manipulação de inspeções governamentais  
- Anomalias de acesso por país  

## 3.5. Monitoramento Regulatório (Obrigatório)
Para atender ITCV + INSP + ERIS + IGAE + IGQPI:

- Histórico de inspeções  
- Alterações de certificações  
- Alterações de listas de risco  
- Edições de dados sensíveis  
- Auditoria completa dos Copilots  
- Justificativas da IA em decisões críticas  

---

# 4. Dashboards Oficiais

A plataforma tem dashboards dedicados, entregues via **Grafana + CloudWatch Metrics**.

## 4.1. Dashboard Técnico (DevOps/SRE)
Contém:

- Latência p95  
- Erros por serviço  
- Saúde do cluster ECS  
- Métricas de container  
- Falhas de deploy  
- Filas lentas  

## 4.2. Dashboard de Produtos (Academy/Hub)
- Progresso por trilha  
- Aderência (%)  
- Tempo médio de conclusão  
- Taxa de reprovação  
- Engajamento  

## 4.3. Dashboard GovTech
- Risco por ilha/concelho  
- Inspeções abertas  
- Certificações emitidas  
- Incidentes críticos  
- Heatmaps de risco  

## 4.4. Dashboard RAG/IA
- Score RAG por módulo  
- Drift de embeddings (diário)  
- Tensões regulatórias (erros em leis)  
- Segurança de IA  

---

# 5. Logs

Toda a plataforma utiliza **logs estruturados em JSON** com:

```
timestamp
service_name
user_id
tenant_id
country
action
severity
trace_id
raw_payload
```

### Níveis:

- INFO  
- WARNING  
- ERROR  
- CRITICAL  
- AUDIT  

### Regras:
- Logs sensíveis criptografados  
- Armazenamento regulatório por 10 anos  
- Leis de proteção: GDPR + Lei de Proteção de Dados de Cabo Verde  

---

# 6. Métricas

Exemplos de métricas personalizadas:

| Serviço | Métrica | Significado |
|--------|---------|-------------|
| Academy | `academy.lesson.completed` | Conclusões por minuto |
| Hub | `hub.evidence.uploaded` | Número de evidências |
| GovTech | `gov.inspections.active` | Inspeções simultâneas |
| Copilot | `ai.rag.precision` | Precisão atual |
| Copilot | `ai.prompt.stability` | Estabilidade por agente |

---

# 7. Tracing (Jaeger)

Exemplo de trace:

```
academy-api → auth-service → db → ai-tutor → cache → response
```

Traces permitem:

- identificar gargalos  
- detectar loops de chamadas  
- validar performance  

---

# 8. Alerting

Sistema de alertas via:

- Slack  
- WhatsApp Business  
- Email  
- PagerDuty  

### Alertas críticos:
- IA com drift acima do limite  
- Falha em GovTech Dashboards  
- Falha no pipeline RAG  
- Cluster ECS instável  
- API sem resposta > 60 segundos  
- Aumento de incidentes críticos  

---

# 9. Política: Zero Silêncio Operacional

Toda falha deve gerar:

1. Incidente  
2. Responsável  
3. SLA  
4. Resolução  
5. Postmortem  

---

# 10. Auditoria Governamental (Obrigatória)

Conforme políticas BeSafe Digital:

- Histórico imutável (S3 + Glacier)  
- Ações do usuário assinadas digitalmente  
- IA justificando recomendações críticas  
- Log de inspeção vinculado a GPS + timestamp  
- Certificações rastreáveis com hash  

---

# 11. Multi-país Observability

Cada país possui **namespace próprio**:

```
cv.academy.*
cv.govtech.*
br.hub.*
ao.api.*
mz.ai.*
```

Permite:

- isolamento  
- auditoria individual  
- métricas independentes  
- deploy seguro  

---

# 12. Conclusão

Este modelo garante:

✔ Operação contínua e confiável  
✔ Segurança e transparência total  
✔ Inteligência para governo e direção  
✔ Monitoramento avançado da IA  
✔ Suporte para multi-país  
✔ Conformidade com ISO + FAO + OMS  
✔ Capacidade de escalar a BeSafe Digital globalmente  

