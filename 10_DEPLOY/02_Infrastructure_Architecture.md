# 02 — Infrastructure Architecture  
BlueShark Cognitive Platform – 2025  
Versão 1.0

Este documento descreve a **arquitetura completa de infraestrutura** usada pela  
BeSafe Digital para operar a BlueShark Cognitive Platform em produção nacional  
e multi-país (CPLP).

A arquitetura é baseada em cloud AWS, com padrões de segurança, resiliência,  
auditabilidade e escalabilidade para suportar:

- Academy  
- Implementation Hub  
- GovTech Suite  
- Mobile & IA (futuro na plataforma conjunta)  
- Copilots (AI Agents)  
- Aplicações Web e Mobile  
- Bases normativas legais  
- Dashboards governamentais  

---

# 1. Objetivos da Arquitetura

A infraestrutura foi desenhada para:

✔ Alta disponibilidade (HA)  
✔ Segurança forte (Zero Trust + IAM mínimo privilégio)  
✔ Escalabilidade horizontal automática  
✔ Multi-tenant (países, empresas, institutos)  
✔ Multi-país (dados isolados por país)  
✔ Suporte a AI em produção (RAG + LLMs + Guardrails)  
✔ Observabilidade completa  
✔ Custos otimizados  

---

# 2. Topologia Geral (Resumo)

A plataforma opera em **4 camadas principais**:

1. **Frontend Layer**  
   - Next.js (GovTech)  
   - React Web (Academy & Hub)  
   - CDN (CloudFront)  

2. **Application Layer (APIs e Serviços)**  
   - ECS Fargate / Kubernetes (EKS futuro)  
   - Microserviços isolados por módulo  
   - BFF (Backend-for-Frontend)  

3. **Data Layer**  
   - PostgreSQL (RDS)  
   - Redis (Elasticache)  
   - S3 (arquivos + evidências)  
   - OpenSearch (RAG + logs + busca)  

4. **AI Layer**  
   - Copilot Engine  
   - RAG Pipeline  
   - Vetores em OpenSearch  
   - Guardrails + Evaluations  
   - Orquestrador de prompts  

---

# 3. Infraestrutura em AWS (detalhada)

### 3.1. Rede (VPC)

- 1 VPC principal  
- 3 subnets públicas  
- 3 subnets privadas  
- Internet Gateway  
- NAT Gateways  
- NACLs isolando ambientes DEV/STAGING/UAT/PROD  

---

# 4. Compute Layer (ECS / Fargate)

Cada módulo sobe como serviço independente:

| Serviço | Função |
|---------|--------|
| **auth-service** | RBAC, ABAC, IAM interno |
| **academy-service** | Trilhas, cursos, certificações |
| **implementation-hub-service** | Projetos, auditorias, evidências |
| **govtech-service** | Dashboards, inspeções, Citizen Reporter |
| **copilot-engine** | RAG + Reasoning |
| **etl-indexer** | Indexação normativa |
| **frontend-academy** | Web App |
| **frontend-hub** | Web App |
| **frontend-govtech** | Next.js |

Cada serviço roda em:

- Containers Fargate  
- Auto Scaling  
- Load Balancers independentes  

---

# 5. Banco de Dados (RDS PostgreSQL)

Para cada país é criado um **database schema isolado**, garantindo:

- compliance legal  
- segregação de dados  
- auditoria por país  
- migrações controladas

Características:

- Multi-AZ  
- Backups diários  
- Criptografia em repouso (KMS)  
- Conexão via IAM  

---

# 6. Caching Layer (Redis)

Usada para:

- sessões  
- tokens temporários  
- throttling para Copilots  
- caching de normativos  
- caching de embeddings quentes  

---

# 7. Arquivos e Evidências (S3)

Buckets separados por país:

```
s3://blueshark-cv-prod
s3://blueshark-br-prod
s3://blueshark-ao-prod
```

Com:

- versionamento ativado  
- criptografia (AES-256)  
- política de retenção (governamental)  

---

# 8. OpenSearch (criticamente importante)

Funções:

- indexação dos embeddings normativos  
- indexação das bases legais  
- buscas rápidas  
- logs e auditoria  
- queries para Copilot Engine  

Estrutura:

```
/vectors/normatives
/vectors/iso
/vectors/haccp
/logs/application
/logs/audit
```

---

# 9. AI Layer (Copilot Engine)

Componentes:

### 9.1. RAG Subsystem
- PDF → extractor  
- chunking  
- embeddings  
- contextual search  
- score ranking  

### 9.2. Prompts Layer  
- templates  
- chains  
- system context  
- multi-agente  

### 9.3. Reasoning Layer  
- plano de ação  
- auditoria técnica  
- análise regulatória  

### 9.4. Guardrails  
- moderação semântica  
- verificação normativa  
- HITL (Human-In-The-Loop)  

---

# 10. Observabilidade

Ferramentas:

- CloudWatch  
- OpenTelemetry  
- Grafana  
- Kibana  
- Sentry  

Monitora:

- latência  
- falhas do RAG  
- custo por chamada de IA  
- throughput por módulo  
- erros por país  
- estabilidade dos serviços  
- métricas de auditoria  

---

# 11. Segurança

Pilares:

- Zero Trust  
- RBAC + ABAC  
- IAM com privilégio mínimo  
- TLS obrigatório  
- Regras OWASP  
- WAF + Rate limiting  
- Logs imutáveis de auditoria  
- criptografia ponta a ponta  

---

# 12. Multi-País (CPLP Ready)

Cada país tem:

- schema isolado  
- bucket isolado  
- normas próprias  
- Copilot com base normativa local  
- dashboards exclusivos  
- governança própria  

---

# 13. Custos Otimizados

A arquitetura reduz 40–60% usando:

- Fargate spot (módulos não críticos)  
- RDS com auto-scaling  
- OpenSearch warm tiers  
- CloudFront para assets  
- cache Redis agressivo  
- ETL noturno (não em horário de pico)  

---

# 14. Conclusão

Esta arquitetura garante:

✔ Operação nacional estável  
✔ Escala para vários países  
✔ Copilots seguros e auditáveis  
✔ Conformidade legal  
✔ Implantação automatizada  
✔ Custos reduzidos  
✔ Alto nível de segurança  

Ela foi desenhada para ser **a base principal da BeSafe Digital** para  
Cabo Verde, Brasil, Angola, Moçambique e Caribe.

