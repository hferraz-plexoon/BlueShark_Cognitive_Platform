# 05 — Multi-Country Deployment & Operation Model  
BlueShark Cognitive Platform — BeSafe Digital  
Versão 1.0 — 2025

Este documento define o **modelo completo de operação, implantação e governança multi-país** da BlueShark Cognitive Platform, cobrindo:

- Cabo Verde (país origem)  
- Brasil  
- Angola  
- Moçambique  
- Portugal  
- Países adicionais da CPLP, Caribe e África Ocidental  

A arquitetura foi desenhada desde o início para operar em **ambientes regulatórios diferentes**, com **bases legais distintas**, múltiplos idiomas e distintos órgãos governamentais.

---

# 1. Objetivos do Modelo Multi-Country

✔ Garantir que a plataforma escale para qualquer país da CPLP  
✔ Preservar diferenças regulatórias (leis, normas, decretos)  
✔ Manter o core único, sem duplicar código  
✔ Suportar multi-tenant para empresas, consultorias e ministérios  
✔ Permitir customização de IA, checklists e certificações por país  
✔ Isolar dados conforme exigências legais (LGPD, GDPR, Lei CV)  
✔ Oferecer governança local para reguladores  

---

# 2. Arquitetura Multi-Country — Visão Geral

```
                 +-----------------------------+
                 |   Global Core (BeSafe Cloud) |
                 +-----------------------------+
                    | APIs / RAG / AI / Identity
                    v
+-----------------------------------------------+
|       Country Layer (CV / BR / AO / MZ / PT)  |
|   - Normas locais                              |
|   - Bases legais                               |
|   - Checklists                                 |
|   - Copilots especializados                    |
|   - Certificações                               |
+-----------------------------------------------+
       | Multi-tenant por país / cliente
       v
+-----------------------------------------------+
|     Organizations Layer (empresas / gov)      |
|   - Restaurantes / Hotéis / Processadores     |
|   - Ministérios / Institutos Governamentais   |
|   - Consultorias locais                        |
+-----------------------------------------------+
```

Camadas:

| Camada | Função |
|--------|--------|
| **Global Core** | Motor central da plataforma (AI, RAG, IA Security, dashboards globais, pipelines universais) |
| **Country Layer** | Adaptação por país: normas, leis, Copilots especializados, trilhas Academy regionais |
| **Organization Layer** | Empresas, hotéis, embarcações, processadores, institutos, consultorias |

---

# 3. Isolamento por País (Namespaces)

Cada país possui **namespace próprio**, separando:  
- banco de dados  
- logs  
- métricas  
- dashboards  
- AI embeddings  
- políticas de segurança  

Formato dos namespaces:

```
cv.*   → Cabo Verde  
br.*   → Brasil  
ao.*   → Angola  
mz.*   → Moçambique  
pt.*   → Portugal
```

Exemplo:

```
cv.govtech.inspections
br.academy.trails
ao.ai.embeddings
mz.coldchain.events
pt.esg.metrics
```

---

# 4. Multi-Tenant (País → Setor → Empresa)

Modelo multi-tenant hierárquico:

```
Tenant 1 (CV)
 ├─ Hotéis
 ├─ Restaurantes
 ├─ Processadores
 ├─ Ministérios
 └─ Consultorias

Tenant 2 (BR)
 ├─ Hotéis
 ├─ Food Service
 ├─ Indústria Pesqueira
 └─ Órgãos Reguladores
```

Cada tenant possui:

- regras próprias  
- conteúdo próprio  
- Copilots próprios  
- banco de dados isolado  
- auditoria isolada  

---

# 5. Idiomas e Localização

A plataforma suporta nativamente:

| Idioma | Status |
|--------|--------|
| Português (PT-BR / PT-PT) | ✔ |
| Crioulo Cabo-verdiano | ✔ |
| Inglês | ✔ |
| Francês | previsto |
| Espanhol | previsto |

Suporte automático:

- interface  
- conteúdo (Academy)  
- prompts de IA  
- relatórios  
- certificados  
- checklists  

---

# 6. Customização dos Copilots por País

Cada país tem **seu próprio conjunto de normas e leis**.

Os Copilots são ajustados via:

### 6.1. Policy Packs (por país)
```
cv_norms/
br_norms/
ao_norms/
mz_norms/
pt_norms/
```

Conteúdos:

- legislações  
- decretos  
- normas sanitárias  
- normas de pesca  
- normas de hospitalidade  
- padrões ESG  
- requisitos do turismo local  

### 6.2. Prompt Packs
Por exemplo:

```
cv_prompts/govtech.md
br_prompts/esg.md
ao_prompts/coldchain.md
```

### 6.3. RAG Stores por país
Cada país tem sua própria base vetorial.

---

# 7. Multi-Country Pipelines de Deploy (CI/CD)

Deploy segregado:

| País | Ambiente | Frequência |
|------|----------|------------|
| Cabo Verde | Produção principal | diário |
| Brasil | Beta | semanal |
| Angola | Staging | sob demanda |
| Moçambique | Beta futuro | sob demanda |
| Portugal | Staging | sob demanda |

Fluxo CI/CD:

```
Git Push →
Quality Gates →
IA Tests →
Security Scans →
Country Split Build →
Deployment por tenant →
Smoke Tests →
Country Release Approval
```

---

# 8. Multi-Country Observability

Cada país possui dashboards independentes:

```
Grafana:
 - cv_dashboard.json
 - br_dashboard.json
 - ao_dashboard.json
 - mz_dashboard.json
 - pt_dashboard.json
```

Logs separados por país em OpenSearch:

```
logs/cv/...
logs/br/...
...
```

---

# 9. Segurança Multi-País

Regras especiais:

- Dados não podem cruzar fronteiras  
- Certificações são assinadas digitalmente por país  
- Auditores governamentais só veem seu país  
- Copilots não misturam legislação entre países  
- S3 com buckets separados por país  
- API com acesso Geo-restricted  

Leis atendidas:

- Lei Cabo Verde de Proteção de Dados  
- LGPD (Brasil)  
- GDPR (Portugal / UE)  

---

# 10. Governança Multi-País

Modelo de governança:

| Papel | País | Permissões |
|-------|-------|-------------|
| **Admin Global (BeSafe Digital)** | Global | Core, AI, pipelines |
| **Country Admin** | CV/BR/AO/MZ/PT | Normas, legislação, auditoria |
| **Consultoria Local** | por país | Implantação e suporte |
| **Institutos Governamentais** | por país | Dashboards, inspeções |
| **Empresas** | por país | Operação diária |

---

# 11. Fluxo de Abertura de Novo País

1. Criar tenant  
2. Criar namespace  
3. Criar cluster isolado (opcional)  
4. Importar normas e decretos  
5. Treinar Copilots com leis locais  
6. Criar trilhas Academy específicas  
7. Conectar consultorias locais  
8. Ativar dashboards governamentais  
9. Configurar multi-idioma  
10. Publicar versão  

Tempo estimado: **21 a 30 dias** por país.

---

# 12. Conclusão

O modelo multi-country permite que a BeSafe Digital:

✔ escale globalmente  
✔ respeite legislações locais  
✔ mantenha segurança e isolamento  
✔ ofereça Copilots especializados por país  
✔ replique o modelo Cabo Verde → CPLP → Caribe  
✔ suporte expansão internacional com custo marginal baixo  

Este é o alicerce da internacionalização do **BlueShark Program**.

