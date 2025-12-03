# 04 — RAG Precision Tests  
## BlueShark Cognitive Platform  
### Avaliação de Precisão da Recuperação (Retrieval) e Qualidade do Grounding

---

# 1. Objetivo do Documento

Este documento define o conjunto oficial de **RAG Precision Tests**, aplicados para validar:

- se o sistema de recuperação (retriever) encontra o documento correto  
- se o Copilot utiliza fielmente o conteúdo recuperado  
- se NÃO usa informações fora da base oficial  
- se evita alucinações mesmo após o retrieval  
- se a resposta final segue estritamente o texto normativo original  

Ele é obrigatório para:

- todos os Copilots operacionais  
- Copilots de compliance  
- Copilot GovTech  
- Copilot Citizen Safety  
- Copilot Audit  
- Copilot Academy (normativos de estudo)  

---

# 2. Métricas Oficiais Avaliadas

A avaliação utiliza 5 KPIs obrigatórios:

### **1. Precision@k**  
Percentual de vezes em que o documento relevante aparece no top-k resultados.

### **2. Recall@k**  
Percentual de documentos relevantes encontrados entre todos os corretos.

### **3. Grounding Accuracy**  
Percentual da resposta final do Copilot que está **exatamente** baseado no conteúdo real do RAG.

### **4. Citation Coverage**  
Percentual de respostas que citam corretamente o documento normativo correspondente.

### **5. Hallucination Rate**  
Percentual de respostas que introduzem informações inexistentes no RAG.

> Meta do programa BlueShark:  
> - Precision@5 ≥ 0.85  
> - Grounding Accuracy ≥ 0.90  
> - Hallucination Rate ≤ 0.03  
> - Citation Coverage ≥ 0.95  

---

# 3. Conjunto de Testes RAG

Os testes são organizados em 6 categorias principais.

---

## 3.1. Normative Retrieval Tests (NRT)

Testam se o RAG encontra corretamente:

- leis  
- decretos  
- normas ISO  
- manuais operacionais  
- checklists  
- pacotes normativos por país  

### Exemplos

| ID | Pergunta | Documento esperado |
|-----|----------|----------------------|
| NRT-01 | “Quais são os requisitos da ISO 22000 para monitoramento?” | ISO 22000 — Seção 8 |
| NRT-02 | “O Decreto-Lei 04/2009 define o que sobre higiene?” | DL 04/2009 Art. 6–9 |
| NRT-03 | “Quais registros HACCP são obrigatórios?” | HACCP — Codex Alimentarius |

**Critério de aprovação:**  
Precision@3 ≥ 0.90 para o corpus de Cabo Verde.

---

## 3.2. Cross-document Disambiguation Tests (CDT)

Testam se o sistema seleciona o documento correto quando há múltiplos documentos parecidos.

### Exemplos

| ID | Situação | Esperado |
|-----|----------|-----------|
| CDT-01 | ISO 22000 vs. ISO 22002-1 | Contexto industrial corretamente identificado |
| CDT-02 | HACCP genérico vs. HACCP peixe | Selecionar o específico |
| CDT-03 | Decreto-Lei 04/2009 vs. Portarias posteriores | Selecionar a fonte mais relevante |

---

## 3.3. Multi-country RAG Tests (MCT)

Fundamental porque o BlueShark opera em:

- Cabo Verde  
- Brasil  
- Angola  
- Moçambique  
- Portugal  
- Ilhas do Caribe (próxima expansão)  

### Exemplos

| ID | Entrada | Esperado |
|-----|----------|-----------|
| MCT-01 | “Qual temperatura de transporte de pescado?”– sem país informado | Perguntar país antes de responder |
| MCT-02 | “Checklist de alergênicos — Brasil x CV” | Recuperar tabelas corretas para cada país |
| MCT-03 | “O que exige a vigilância sanitária?” | Buscar normas **do país correto** |

**Critério de aprovação:**  
Recall@5 ≥ 0.85  
Zero contaminação cruzada entre países.

---

## 3.4. Context Window Stress Tests (CST)

Testam a habilidade do retriever + LLM de:

- usar contextos longos  
- ignorar material irrelevante  
- manter foco em requisitos críticos  

### Exemplos

| ID | Entrada | Testado |
|-----|----------|-----------|
| CST-01 | Pergunta simples + 3 páginas irrelevantes | O sistema ignora ruído |
| CST-02 | Pergunta com texto muito longo | O sistema recupera apenas seções relevantes |
| CST-03 | Pergunta sobre item específico | LLM seleciona trecho correto |

---

## 3.5. Deep Grounding Tests (DGT)

Validam a capacidade do LLM de:

- citar exatamente a norma  
- usar o trecho original  
- não interpretar equivocadamente  

### Exemplo

Pergunta:  
“Quais são os requisitos de controle operacional segundo ISO 22000?”

A resposta deve incluir:  

- texto normativo fiel  
- referência exata (capítulo, item)  
- sem invenções  

**Meta:**  
Grounding Accuracy ≥ 0.92

---

## 3.6. Error Rejection Tests (ERT)

Simulam erros do usuário:

- normas inexistentes  
- leis inventadas  
- números de artigos errados  

### Exemplos

| ID | Entrada | Resposta esperada |
|-----|----------|-------------------|
| ERT-01 | “ISO 22700” | Recusar e corrigir |
| ERT-02 | “Lei 123/2021 CV sobre comida” | Informar que não existe |
| ERT-03 | “Artigo 28 da ISO 22000” | Corrigir com número real |

---

# 4. Pipeline de Execução
/07_EVALUATION/rag_precision_tests/
normative_retrieval.json
disambiguation.json
multi_country.json
context_stress.json
deep_grounding.json
error_rejection.json


Pipeline:

1. Carrega dataset de perguntas  
2. Executa consultas RAG  
3. Avalia métricas (Precision, Recall, GA, HC)  
4. Gera relatório  
5. Bloqueia PR se Precision@5 < 0.85  
6. Exporta relatório em JSON + Markdown  

---

# 5. Scoring e Critérios de Aprovação

### Matriz oficial:

| Métrica | Mínimo | Ideal |
|---------|----------|--------|
| Precision@5 | ≥ 0.85 | ≥ 0.92 |
| Recall@5 | ≥ 0.80 | ≥ 0.90 |
| Grounding Accuracy | ≥ 0.90 | ≥ 0.95 |
| Hallucination Rate | ≤ 0.03 | ≤ 0.01 |
| Citation Coverage | ≥ 0.95 | ≥ 0.98 |

Se qualquer Copilot ficar abaixo → bloqueio de release.

---

# 6. Governança e Revisões
Versão: 1.0.0
Responsável: BeSafe Digital — RAG Engineering Team
Revisão: Mensal
Última atualização: 2025-02-02
Status: Estável
A execução é totalmente automatizada via GitHub Actions:

