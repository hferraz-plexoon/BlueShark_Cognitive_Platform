# 01 — Deployment Guide  
BlueShark Cognitive Platform – 2025  
Versão 1.0

Este documento descreve **como implantar, atualizar e manter** a BlueShark Cognitive Platform  
(Academy + Implementation Hub + Mobile/IA + GovTech + Copilots) em ambiente cloud, seguindo padrões de:

- segurança (ISO + OWASP)
- escalabilidade
- multi-país
- modularidade
- padronização DevOps

---

# 1. Objetivos da Implantação

Garantir que:

- o sistema suba em minutos, não horas  
- ambientes possam ser replicados para novos países  
- a AI opere com segurança, guardrails e rastreabilidade  
- seja possível monitorar e auditar tudo  
- múltiplos módulos funcionem de forma desacoplada  
- serviços possam ser atualizados sem downtime  

---

# 2. Estrutura de Ambientes

A plataforma utiliza **quatro ambientes**:

| Ambiente | Objetivo | Acesso |
|---------|----------|--------|
| **DEV** | Desenvolvimento e testes rápidos | Dev Team |
| **STAGING** | Testes integrados, QA e avaliações de IA | Dev + QA |
| **UAT (User Acceptance Testing)** | Testes com BeSafe Digital + Institutos | BeSafe + Governo |
| **PROD** | Ambiente oficial nacional | Governo + BeSafe |

Cada país futuro possui seu **próprio tenant isolado** dentro do mesmo cluster.

---

# 3. Orquestração Geral

A arquitetura de implantação é baseada em:

- AWS ECS / Fargate (ou Kubernetes EKS em evolução)
- API Gateway
- Load Balancers
- RDS PostgreSQL
- Elasticache Redis
- S3 buckets versionados
- OpenSearch (Busca + logs)
- CloudFront (assets globais)

---

# 4. Pipeline CI/CD

A cadeia de automação usa:

- **GitHub Actions** (CI)
- **GitHub Packages / ECR** (artefatos)
- **Terraform** (IaC)
- **AWS CodeDeploy** (CD)
- **OpenTelemetry** (observabilidade)

### 4.1. Fluxo completo

1. Desenvolvedor cria branch → Pull Request  
2. Testes automatizados (lint, unit, RAG evals)  
3. Build + Containerização (Docker)  
4. Push para ECR  
5. Terraform aplica infraestrutura (se necessário)  
6. Deploy automático → DEV  
7. Deploy manual → STAGING  
8. Aprovação BeSafe/Governo → UAT  
9. Deploy final → PROD  

Nenhuma fase é feita manualmente fora de UAT → PROD.

---

# 5. Estrutura dos Serviços Implantados

A plataforma é dividida em 6 componentes:

1. **API Core** – autenticação, RBAC, multi-tenant  
2. **Academy Service** – cursos, trilhas, certificação  
3. **Implementation Hub Service** – projetos, evidências, auditorias  
4. **GovTech Service** – dashboards, inspeções, Citizen Reporter  
5. **AI Copilot Engine** – RAG + Reasoning + Guardrails  
6. **Frontend** – Next.js (GovTech), React (Academy/Hub)

Cada serviço sobe como container isolado.

---

# 6. Infraestrutura como Código (IaC)

Todo o ambiente é criado via:

```
/infra
   /terraform
   /modules
   /environments
```

Itens provisionados:

- VPC + Subnets  
- NAT Gateways  
- Security Groups  
- ECS Cluster / EKS Cluster  
- RDS PostgreSQL  
- S3 buckets  
- Redis cache  
- OpenSearch cluster  
- IAM roles (mínimo privilégio)  

Cada mudança é versionada automaticamente.

---

# 7. Deploy do RAG (Retrieval-Augmented Generation)

Os agentes cognitivos exigem um pipeline separado:

### 7.1. Estrutura

- Embeddings indexados em OpenSearch  
- Normalização automática via ETL  
- Versionamento de bases normativas  
- Deploy do modelo de prompts via Git  

### 7.2. Fluxo

1. Novo documento legal ou norma ISO é adicionado no `/04_KNOWLEDGE_BASE`
2. Pipeline de ETL converte → limpa → indexa
3. Vetores são gerados e armazenados
4. RAG passa por testes automáticos (evals)
5. Publicação é acionada em produção

Nada vai para produção sem:

- aprovação manual + logs
- testes de segurança semântica
- testes de precisão RAG

---

# 8. Estratégia de Zero Downtime

A plataforma usa:

- blue/green deployment  
- health checks no load balancer  
- rollback automático  
- migrações de banco backward-safe  

Atualizações críticas acontecem via:

- feature flags  
- dark launches  
- canary releases  

---

# 9. Backups e Recuperação

### 9.1. Backups Automáticos

- RDS: snapshots diários (7–30 dias)  
- S3: versionamento total + replicação  
- Redis: backup a cada 15 min  
- OpenSearch: snapshots diários  

### 9.2. Plano de Restauração

- RDS → restauração point-in-time  
- S3 → restauração de versões  
- Containers → reimplantação do artefato  
- Logs → retidos por 12 meses  

---

# 10. Multi-Country Deployment

Quando um novo país entra no programa, o deploy cria:

- tenant isolado (segurança)  
- normas e checklists locais  
- agente cognitivo local  
- dashboards adaptados  
- configurações de moeda, fuso, idioma  

A replicação é automatizada em menos de 3 horas.

---

# 11. Operações e Monitoramento

Ferramentas:

- CloudWatch (métricas)  
- OpenTelemetry (tracing distribuído)  
- Sentry (erros)  
- Kibana (logs)  
- Grafana (dashboards)  

Monitoramento inclui:

- Latência por módulo  
- Falhas do RAG  
- Taxa de erro de Copilots  
- Performance de embeddings  
- Uso por ilha/país  

---

# 12. Conclusão

Este guia permite que:

✔ A BeSafe Digital opere a plataforma sem dependências externas  
✔ O Governo tenha estabilidade e alta disponibilidade  
✔ O sistema escale para vários países da CPLP  
✔ Mantenhamos segurança, auditoria e confiabilidade total  
✔ Os Copilots funcionem com conformidade legal e padronização  

