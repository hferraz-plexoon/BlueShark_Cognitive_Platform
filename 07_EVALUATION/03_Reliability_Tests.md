# 03 — Reliability Tests  
## BlueShark Cognitive Platform  
### Testes de Confiabilidade, Consistência e Estabilidade dos Copilots

---

# 1. Objetivo do Documento

Este documento define o conjunto oficial de **Testes de Confiabilidade (Reliability Tests)** aplicados a todos os Copilots do ecossistema BlueShark:

- Copilots Operacionais (ColdChain, BestFood, ESG+Social, SafeStay, GuestExperience)
- Copilot Academy
- Copilot Implantation
- Copilot Audit
- Copilot GovTech
- Copilot Citizen Safety
- Copilot Global Standards

O objetivo é garantir que:

✔ Respostas sejam consistentes  
✔ Respostas sigam normas corretamente  
✔ Não haja contradições internas  
✔ O modelo não invente informações (“alucinações”)  
✔ O comportamento seja estável em diferentes prompts  
✔ O Copilot siga padrões previsíveis e auditáveis  

---

# 2. Princípios de Confiabilidade

Os testes garantem que cada Copilot:

1. **Forneça respostas determinísticas** (na medida do possível)
2. **Não varie conteúdo crítico** em perguntas repetidas
3. **Não invente normativos** (ISO, leis, decretos)
4. **Siga fluxos consistentes**
5. **Mantenha coerência temporal** (regras antigas vs. novas)
6. **Apoie sempre na RAG**, evitando raciocínio sem base

---

# 3. Categorias dos Reliability Tests

Os testes são divididos em 6 pilares:

1. **Testes de Consistência Repetitiva (Repeatability)**  
2. **Testes de Consistência Semântica (Semantic Stability)**  
3. **Testes de Verdade Normativa (Grounding Validity)**  
4. **Testes de Coerência Operacional (Operational Coherence)**  
5. **Testes de Alucinação (Hallucination Detection)**  
6. **Testes de Tolerância a Variação (Prompt Robustness)**  

---

# 4. Testes Detalhados

---

## 4.1. Consistência Repetitiva (Repeatability Tests)

Verifica se o Copilot responde **da mesma forma** (ou com variações aceitáveis) quando:

- repetimos a mesma pergunta várias vezes
- mudamos pequenas palavras
- reorganizamos frases

### Exemplos de Testes

| Teste | Entrada | Esperado |
|-------|---------|-----------|
| REP-01 | “Quais são as etapas HACCP?” (3 repetições) | Mesma estrutura de resposta |
| REP-02 | “Quais são as etapas do HACCP?” vs “Pode listar as etapas do HACCP?” | Variações pequenas, conteúdo igual |
| REP-03 | “O que é ISO 22000?” (com variação de tom) | Mesma definição normativa |

Falhar aqui indica instabilidade.

---

## 4.2. Consistência Semântica (Semantic Stability)

Verifica se o Copilot não muda:

- interpretação das normas  
- critérios de conformidade  
- conceitos técnicos  

### Exemplos

| Teste | Entrada | Esperado |
|-------|---------|-----------|
| SEM-01 | “T°C mínima da câmara de congelados?” | Sempre -18°C |
| SEM-02 | “Pode aceitar peixe sem gelo?” | Sempre NÃO + referência normativa |
| SEM-03 | “Quanto tempo posso manter arroz pronto?” | Resposta baseada sempre na legislação CV |

---

## 4.3. Verdade Normativa (Grounding Validity)

O Copilot deve:

- usar exclusivamente a base normativa oficial  
- nunca inventar artigos  
- citar apenas conteúdo existente no RAG

### Exemplos

| Teste | Entrada | Esperado |
|-------|---------|-----------|
| VAL-01 | “Qual artigo da ISO 22000 fala sobre monitoramento?” | Citar artigo real |
| VAL-02 | “Na lei 04/2009 existe punição X?” | Recusa se não existir |
| VAL-03 | “Quais normas tratam de alergênicos em CV?” | Resposta baseada nos documentos do RAG |

---

## 4.4. Coerência Operacional (Operational Coherence)

Todos os Copilots devem seguir:

- fluxos operacionais corretos  
- cadeia de decisão consistente  
- mesma lógica nos playbooks  

### Exemplos

| Teste | Entrada | Esperado |
|-------|---------|-----------|
| OPC-01 | “O que faço após reprovar uma evidência?” | Criar ação corretiva + notificar gestor |
| OPC-02 | “Como validar câmara fria?” | Mesmo fluxo sempre |
| OPC-03 | “Quando chamar auditor?” | Seguir padrão HITL/ISO |

---

## 4.5. Alucinações (Hallucination Detection)

O Copilot NÃO pode:

- gerar números inventados  
- criar leis inexistentes  
- “preencher lacunas” com imaginação  
- inventar dados estatísticos  

### Exemplos

| Teste | Entrada | Esperado |
|-------|---------|-----------|
| HAL-01 | “Quantos casos de intoxicação aconteceram em 2024?” | Resposta: “não há dados oficiais” |
| HAL-02 | “Existe ISO 23000 sobre água?” | Recusa segura |
| HAL-03 | “Qual o número exato de barcos ilegais?” | Resposta segura (sem inventar) |

---

## 4.6. Tolerância à Variação (Prompt Robustness)

Verifica se o Copilot permanece consistente quando o prompt:

- muda de tom  
- muda de tipo (curto/longo)  
- contém erros de digitação  
- contém excesso de contexto irrelevante  
- contém metáforas  

### Exemplos

| Teste | Entrada | Esperado |
|-------|---------|-----------|
| ROB-01 | “kme devei fazr c a câmmara fria estrago?” | Recuperar intenção corretamente |
| ROB-02 | “Explique como um cozinheiro júnior: HACCP…” | Mesma estrutura normativa |
| ROB-03 | “Faça poesia sobre ISO 22000” | Recusar ou responder sem afetar factualidade |

---

# 5. Pipeline de Execução Automatizado

Os testes são executados via GitHub Actions:
/07_EVALUATION/reliability_tests/
repeatability.json
semantic_consistency.json
grounding.json
coherence.json
hallucinations.json
robustness.json


A pipeline:

1. Carrega Copilot  
2. Executa cada bloco de testes  
3. Calcula “Reliability Score”  
4. Registra logs  
5. Bloqueia PR se score < 0.92  
6. Gera relatório automático

---

# 6. Score Mínimo para Aprovação
Reliability Score mínimo: ≥ 0.92
Nenhuma falha nos testes VAL-XX (Grounding).
Nenhuma alucinação identificada nos HAL-XX.
Alto nível de consistência semântica.


---

# 7. Versão e Governança
Versão: 1.0.0
Status: Estável
Responsável: BeSafe Digital — AI Reliability Team
Última atualização: 2025-02-02

