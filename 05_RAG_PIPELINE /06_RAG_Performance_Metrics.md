# 06 — RAG Performance Metrics  
## BlueShark Cognitive Platform — BeSafe Digital (2025)

Este documento define **como avaliar a performance do pipeline RAG** em todos os Copilots BlueShark, garantindo:

- precisão regulatória  
- respostas consistentes  
- confiabilidade técnica  
- explicabilidade  
- controle governamental  
- prevenção de hallucinations  

Ele é obrigatório para todos os times de IA da BeSafe Digital.

---

# 🎯 1. Objetivos dos Métricos de Desempenho

As métricas existem para:

1. Garantir que os Copilots sejam **seguro-primários**.  
2. Reduzir riscos legais e operacionais.  
3. Avaliar precisão em compliance (ISO + leis + regulamentos CV).  
4. Otimizar o pipeline RAG continuamente.  
5. Automatizar Evals e testes para homologação.

---

# 🧪 2. Tipos de Métricas Avaliadas

Existem **5 grupos principais**:

| Grupo | Objetivo |
|-------|----------|
| **Retrieval Quality** | Avaliar se a busca trouxe o documento correto |
| **Grounding Accuracy** | Garantir que a resposta está baseada nas evidências |
| **Reasoning Quality** | Verificar se o raciocínio segue normas e fatos |
| **Safety & Compliance** | Checar violações, vieses, riscos legais |
| **User Experience** | Clareza, relevância e velocidade |

---

# 📊 3. Retrieval Quality Metrics

Avaliam a qualidade da recuperação de documentos (ElasticSearch + ChromaDB).

### 3.1. Recall@K
- Percentual de vezes que o documento correto aparece entre os top-K resultados.

Valores recomendados:
- **ColdChain / BestFood:** Recall@3 ≥ 0.85  
- **GovTech:** Recall@5 ≥ 0.95  

### 3.2. Precision@K
- Percentual de documentos relevantes entre os top-K.

Meta geral:
- **Precision@3 ≥ 0.90**

### 3.3. MMR Score (Diversity)
- Garantir que o conjunto recuperado não é redundante.

Meta:
- **MMR ≥ 0.65**

---

# 🧬 4. Grounding Accuracy Metrics

Avaliam se a resposta do agente está baseada *exclusivamente* na legislação, normas, checklists e manuais.

### 4.1. Groundedness Score
Análise automática:

- A resposta está 100% ancorada nos documentos?
- Existem afirmações não suportadas?

Meta:
- **≥ 0.92** para GovTech  
- **≥ 0.85** para Academy  

### 4.2. Faithfulness
Garante que o modelo **não alterou** ou **reinterpetou** normas.

Meta:
- **≥ 0.98** para agentes regulatórios

---

# 🧠 5. Reasoning Quality Metrics

### 5.1. Logical Chain Check
Avalia:

- coerência da cadeia de raciocínio  
- consistência com normas  
- explicabilidade  

Meta:
- **≥ 0.90**

### 5.2. Step-by-Step Accuracy
O modelo toma decisões coerentes em cada etapa?

Meta:
- **≥ 0.85**

---

# 🛡️ 6. Safety & Compliance Metrics

### 6.1. Hallucination Rate (HLR)
Proporção de respostas contendo trechos não suportados por fonte.

Meta:
- **HLR ≤ 2%**

### 6.2. Regulatory Violation Score
- Alguma resposta violou diretrizes legais?

Meta:
- **0 → sempre**

### 6.3. Risk Category Alignment
- Classificação de risco condiz com a legislação CV?

Meta:
- **≥ 0.95**

---

# 👥 7. User Experience Metrics

### 7.1. Response Relevancy Score
O usuário marcou como útil?

Meta:
- **≥ 4.5/5**

### 7.2. Latência
Tempo entre pergunta → resposta final.

Metas:
- Mobile & IA Copilots → **≤ 3.5s**  
- GovTech → **≤ 4.5s**  
- Citizen Reporter → **≤ 2.0s**  

---

# 🔁 8. Evals Automáticos

Cada commit no repositório executa:

- **RAG Recall Tests**
- **Grounding Tests**
- **Safety Tests**
- **Hallucination Tests**
- **Normative Alignment Tests**

Critérios de aprovação:

| Módulo | Evals necessários |
|--------|--------------------|
| Academy | Grounding + UX |
| Mobile & IA | Safety + Reasoning |
| GovTech | Grounding + Safety + Risco |
| Citizen | Latência + Segurança |
| Copilots | Todos acima |

---

# 🧩 9. Dashboards de Performance

A plataforma terá dashboards internos com:

- métricas por agente  
- regressão vs releases  
- alertas de queda de precisão  
- tracking por país/tenant  
- performance normativa  
- risco residual  

Esses dashboards alimentam o **Governance Board** da BeSafe Digital.

---

# 🧾 10. Conclusão

As métricas de performance garantem que:

- todos os agentes cognitivos do BlueShark sejam **confiáveis**  
- conformidade técnica e jurídica seja preservada  
- o GovTech tenha segurança máxima  
- o Academy seja consistente e pedagógico  
- a plataforma seja globalmente escalável  

Este é um documento normativo e obrigatório para QA, Dev, IA e Governança.

