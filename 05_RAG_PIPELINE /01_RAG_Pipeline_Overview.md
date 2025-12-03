# 01 — RAG Pipeline Overview  
## BlueShark Cognitive Platform — BeSafe Digital (2025)

Este documento descreve o pipeline completo de **RAG (Retrieval-Augmented Generation)** utilizado por todos os Copilots da BlueShark Cognitive Platform, incluindo:

- Copilot Academy  
- Copilot Implementation  
- Copilot ColdChain  
- Copilot BestFood  
- Copilot ESG  
- Copilot SafeStay  
- Copilot GuestExperience  
- Copilot Audit  
- Copilot GovTech  
- Copilot CitizenSafety  

O objetivo é garantir **respostas auditáveis, normativas, alinhadas à legislação de Cabo Verde e padrões ISO**, além de escalabilidade para expansão CPLP.

---

# 🎯 1. Objetivos do RAG Pipeline

1. Garantir **respostas 100% baseadas em conhecimento verificável** (leis, normas, checklists, ISO, HACCP, legislação CV).  
2. Reduzir alucinação para níveis **< 2%**.  
3. Permitir **expansão multi-país** com bases normativas distintas.  
4. Criar um pipeline auditável para governo e certificadoras.  
5. Operar em baixa latência para uso em mobile & IA.  
6. Suportar **Copilots híbridos** (Academy + Operacional + Auditoria + GovTech).

---

# 🧠 2. Macro-Pipeline Geral
[User Input]
↓
[Pre-Processor & Intent Classifier]
↓
[Copilot Router / Orchestrator]
↓
[RAG Layer]
├─ Embedding Retrieval
├─ Semantic Search
├─ Normative Filters
├─ Context Builder
↓
[Reasoning Layer (LLM)]
↓
[Safety + Compliance Filters]
↓
[Output Generator]
↓
[Audit Log + Metadata]


---

# 🔍 3. Componentes do Pipeline

### ✔ 3.1 Pre-Processor
Responsável por:

- normalização do texto  
- language detection (PT-BR, PT-CV, EN, ES)  
- token cleaning  
- identificação de entidade (NER)  
- expansão de abreviações normativas (HACCP, APPCC, IGAE, ITCV etc.)  
- conversão de fala → texto (mobile)  

---

### ✔ 3.2 Intent Classifier
Classifica automaticamente qual Copilot deve responder:

coldchain, bestfood, esg, safestay, guestexp,
audit, academy, implementation, govtech, citizen

Modelos possíveis:
- FastText  
- BERT-base multilingual  
- LLM few-shot (quando necessário)

---

### ✔ 3.3 Copilot Orchestrator
Decide se a resposta exige:

- RAG apenas  
- RAG + Reasoning  
- Reasoning puro  
- Multi-copilot fusion  
- Modo “auditor” (resposta mais normativa)  
- Modo “academy tutor” (resposta pedagógica)  

---

### ✔ 3.4 RAG Layer
Camada mais crítica do pipeline.

Inclui:

- embeddings (OpenAI, Jina, VoyageAI ou OSS: bge-m3, instructor-xl)  
- semantic search híbrido (vetorial + BM25)  
- filtros por país / norma / módulo  
- anotação de cada chunk com metadados normativos  

Metadados típicos:
{
"norm": "ISO 22000:2018",
"country": "Cabo Verde",
"module": "BestFood",
"section": "HACCP",
"source": "Decreto-Lei 04/2009",
"validity": "2024-2030"
}


---

### ✔ 3.5 Context Builder
Responsável por montar o contexto final enviado ao LLM:

- top-k documentos  
- metadata prioritization  
- “normative highlighting”  
- filtros específicos por Copilot  
- limite seguro de tokens  

Também adiciona:

- resumo automático dos chunks  
- extração de normas com maior impacto  
- ordenação por confiabilidade  

---

### ✔ 3.6 Reasoning Layer
O LLM toma a decisão final, com regras:

- respostas estruturadas  
- cadeia de raciocínio interna, mas não exposta  
- justificativas sempre com base nas normas listadas  
- modo “normative strict” ativo para auditorias  
- modo “pedagógico” para Academy  

Modelos recomendados (2025):

- GPT-5.1 Reasoning  
- Claude 3.7 Sonnet  
- LLama 3.1 405B (self-hosted futuro)  

---

### ✔ 3.7 Safety, Ethics & Compliance Filters
Obrigatório para:

- GovTech  
- Auditoria  
- Ocorrências Cidadãs  
- Relatórios oficiais  

Inclui:

- Toxicity remover  
- Bias mitigator  
- Normative-only validation  
- Anti-alucination checker  
- Regra: “sem aconselhamento médico/biológico não permitido”

---

### ✔ 3.8 Output Generator
Gera:

- respostas normativas  
- tabelas  
- planos de ação  
- classificação de risco  
- recomendações HACCP e ISO  
- notificações para painel GovTech  
- respostas simplificadas para o cidadão (Citizen Safety)  

---

### ✔ 3.9 Audit Log Layer
Cada resposta gera:
- prompt do usuário
- copilots envolvidos
- documentos consultados (hash)
- modelo utilizado
- versão do embedding
- tempo de execução
- agente responsável
- score de precisão


Fundamental para certificações e auditorias futuras.

---

# 🌍 4. Suporte Multi-País

O pipeline já está preparado para:

- Cabo Verde  
- Brasil  
- Portugal  
- Angola  
- Moçambique  

Com separação:

/kb/country/CV/
/kb/country/BR/
/kb/country/PT/


E seleção automática através do metadado:

`metadata.country == user.country`

---

# 📚 5. Tipos de Documentos Suportados

- PDFs normativos  
- Decretos e leis  
- Manuais operacionais  
- Checklists de auditoria  
- Slides técnicos  
- Bases HACCP  
- ISO 22000, 9001, 14001, 21401  
- Relatórios de inspeção  
- Dados de IoT (sensorial)  
- Ocorrências ciudadãs  

---

# 🛡️ 6. Objetivos de Conformidade

- 100% de rastreabilidade  
- Zero respostas fora da norma  
- Auditoria independente  
- Validação por autoridades sanitárias  
- Base para certificação nacional BlueShark  

---

# 🧩 7. Conclusão

Este documento estabelece:

- o padrão oficial do pipeline RAG da plataforma  
- como cada Copilot usa o conhecimento normativo  
- como garantimos segurança e confiabilidade  
- como explicamos a arquitetura para governo e parceiros  

Serve como fundação para:

- 02_Embedding_Strategy.md  
- 03_Contextual_Retrieval.md  
- 04_Prompt_Chains.md  
- 05_Memory_Policies.md  

