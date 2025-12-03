# 03 — CI/CD Pipeline  
BlueShark Cognitive Platform – BeSafe Digital  
Versão 1.0 — 2025

Este documento define o **pipeline completo de CI/CD** da BlueShark Cognitive Platform,
abrangendo:

- Academy  
- Implementation Hub  
- GovTech Suite  
- Copilots (AI Agents)  
- Pipelines de RAG  
- Infraestrutura multi-país  
- Web & Mobile (Lite)  

O pipeline segue o padrão **GitHub Actions**, com alta automação, segurança, auditoria e
rastreamento.

---

# 1. Objetivos do Pipeline

O CI/CD foi projetado para:

✔ Entregar mudanças rapidamente  
✔ Garantir segurança e governança  
✔ Validar AI (RAG, prompts, chains, embeddings)  
✔ Implantar multi-país automaticamente  
✔ Garantir rastreabilidade para governo e auditoria  
✔ Reduzir custo operacional  
✔ Minimizar erros humanos  

---

# 2. Arquitetura Geral do Pipeline

```
Developer → GitHub → Actions → Build → Test → AI Evals → Security Scan
           → Artifact Registry → Deploy (Dev/Staging/Prod)
           → Multi-country Deploy (CV, BR, AO, MZ)
```

Componentes principais:

1. **CI** — Build + Test + Lint + AI Evals  
2. **Security** — SAST + Secrets Scan + Container Scan  
3. **CD** — Deploy automatizado com aprovação  
4. **AI Pipeline** — validação de RAG e prompts  
5. **Multi-country Pipeline** — replicação automatizada  
6. **Infra Pipeline (Terraform)** — IaC validado  
7. **Rollback inteligente** — revert automatic  

---

# 3. Branch Strategy

```
main        → Produção
staging     → Ambiente de testes integrados
dev         → Desenvolvimento ativo
feature/*   → Features novas
hotfix/*    → Correções imediatas
```

Políticas:

- PR obrigatório  
- Revisão mínima por 1 engenheiro  
- Testes obrigatórios  
- Evals de IA obrigatórios para módulos com Copilots  

---

# 4. GitHub Actions — Estrutura

Diretório:

```
.github/workflows/
   ci.yml
   cd.yml
   ai-evals.yml
   security.yml
   migrations.yml
   rag-indexer.yml
   terraform.yml
```

---

# 5. CI Pipeline (ci.yml)

O pipeline roda:

### 5.1. Linting
- ESLint (Node.js / Next.js)
- Flutter Analyzer (Mobile Lite)
- Markdown Linter (documentação)

### 5.2. Unit Tests
- Jest (APIs)
- Vitest (frontend)
- PyTest (AI Engine)

### 5.3. Build
- Next.js build
- Docker BuildKit (APIs)
- Flutter build (artefatos dev)

### 5.4. Code Coverage
- Enforce >= 80%  

### 5.5. Notifications
- Slack / WhatsApp (opcional)

---

# 6. Security Pipeline (security.yml)

Execução automática de:

### 6.1. SAST (Static Analysis)
- CodeQL  
- SonarCloud  

### 6.2. Secrets Detector
- Gitleaks  
- Trufflehog  

### 6.3. Dependency Scan
- npm audit  
- pip-audit  
- Docker image scan (Trivy)  

### 6.4. Compliance Rules
- OWASP Top 10  
- GDPR/ISO flags  

---

# 7. AI Evals Pipeline (ai-evals.yml)

**Crítico para Copilots e GovTech.**

Executa:

### 7.1. RAG Precision Tests
- Recall@k  
- MRR (Mean Reciprocal Rank)  
- Relevância normativa  

### 7.2. Prompt Regression Tests
- Estabilidade do output  
- Verificação de vieses  
- Políticas de segurança da plataforma  

### 7.3. Reasoning Tests
- Cadeias lógicas  
- Qualidade do plano de ação  
- Aderência às normas ISO e leis de Cabo Verde  

### 7.4. Aprovação Automática
Mudanças só são aceitas se:

```
RAG score > 0.75
Factfulness > 0.90
Stability >= 85%
```

---

# 8. CD Pipeline (cd.yml)

Fluxo:

```
main push → Build → Test → AI Evals → Deploy → Smoke Tests → Notificação
```

Ambientes:

### Dev
- Deploy automático
- Sem aprovação

### Staging
- Deploy automático após PR aprovado
- Testes integrados
- Evals adicionais

### Production
- Deploy com aprovação de Helder ou CTO
- Janela segura

---

# 9. Multi-Country Deployment

A plataforma é multi-país.

O deploy replica automaticamente para:

```
cv → Cabo Verde
br → Brasil
ao → Angola
mz → Moçambique
pt → Portugal (futuro)
```

Automation:

- Criação automática de schemas RDS  
- Criação de buckets S3 independentes  
- Provisionamento de OpenSearch por país  
- Configuração de normas locais  
- Geração de embeddings específicos  

---

# 10. RAG Indexer Pipeline (rag-indexer.yml)

Processos:

### 10.1. Extração
PDF → OCR → limpeza

### 10.2. Chunking inteligente
Por:

- seção
- norma
- cláusula legal
- módulo (ColdChain, BestFood etc.)

### 10.3. Embeddings
OpenAI Embeddings (ou modelo local futuro)

### 10.4. Indexação OpenSearch
Criação de:

```
/vectors/cv/iso
/vectors/cv/leis
/vectors/esg
/vectors/haccp
```

### 10.5. Validação com AI Evals

---

# 11. IaC Pipeline (terraform.yml)

Infraestrutura versionada:

- VPC  
- RDS  
- ECS Fargate  
- OpenSearch  
- Redis  
- CloudFront  
- IAM Roles  
- Buckets S3  
- WAF  

Fluxo:

1. `terraform plan`  
2. aprovação manual  
3. `terraform apply`

---

# 12. Rollback Automático

Deploy monitora:

- latência
- erros 5xx
- falha de Evals AI
- falha de RAG
- healthcheck da API

Se falhar → rollback automático para:

```
latest-stable-prod-tag
```

---

# 13. Auditoria (obrigatório)

Toda mudança gera:

- hash da versão
- autor
- data/hora
- país impactado
- logs dos testes
- logs de AI Evals
- commit vinculado

---

# 14. Conclusão

O pipeline CI/CD entrega:

✔ Deploy rápido e seguro  
✔ Governança auditável  
✔ AI validada e confiável  
✔ Redução de riscos regulatórios  
✔ Suporte multi-país  
✔ Padronização global da BeSafe Digital  
✔ Total alinhamento com Mobile & IA + GovTech  

Este pipeline será uma das fortalezas técnicas do BlueShark Program.

