# 03 — Contextual Retrieval Strategy  
## BlueShark Cognitive Platform — BeSafe Digital (2025)

Este documento descreve a estratégia oficial de **Contextual Retrieval** utilizada por todos os Copilots da BlueShark, incluindo GovTech, Academy, Implementation Hub, ColdChain, BestFood, SafeStay, ESG e Citizen Safety.

O objetivo é garantir que cada agente obtenha **contexto normativo, pedagógico e operacional** com precisão, segurança e explicabilidade.

---

# 🎯 1. Objetivos do Contextual Retrieval

A estratégia deve:

1. **Identificar corretamente o módulo** (ColdChain, BestFood, ESG etc.).
2. **Aplicar filtros normativos obrigatórios** por país.
3. **Incorporar contexto dinâmico:**
   - perfil do usuário  
   - nível de certificação  
   - risco atual  
   - localização (ilha/concelho)  
   - tipo de estabelecimento  

4. **Retornar chunks relevantes com explicabilidade.**
5. **Minimizar alucinação (<2%)**.
6. **Suportar GovTech**, incluindo inspeção, penalidades e autos.

---

# 🧩 2. Modelo de Contexto (Context Envelope)

Cada requisição passa por um "envelope" padronizado:

```json
{
  "user_context": {
    "role": "auditor | consultor | pescador | cozinheiro | gestor | cidadão | inspetor",
    "country": "CV",
    "region": "Santiago / Praia",
    "organization_type": "hotel | restaurante | embarcação | armazém | governo"
  },
  "module_context": {
    "module": "BestFood",
    "submodule": "HACCP",
    "risk_level": "medium",
    "checklist_stage": "PCC",
    "norm": "ISO 22000"
  },
  "query_context": {
    "original_query": "...",
    "expanded_keywords": ["HACCP", "temperatura", "ponto crítico"],
    "task_type": "explicação | auditoria | diagnóstico | ação corretiva"
  }
}
````

---

# 🧠 3. Tipos de Recuperação (Retrieval Modes)

A plataforma usa três modos oficiais.

## 3.1 Retrieval Normativo (Legal & ISO/HACCP)

Prioridade Máxima
Usado em:
- inspeção
- auditoria
- explicação de normas
- autos e penalidades
- GovTech e Citizen Reporter
Critérios:
- país correto
- versão da norma
- nível de risco
- módulo aplicável

---

## 3.2 Retrieval Operacional (Checklists & POPs)

Usado em:
- Academy
- Implementation Hub
- consultores
- treinamento prático

Exemplos:
- POP de Higiene
- PCC de temperatura
- Checklist de pragas
- Plano APPCC

---

## 3.3 Retrieval Educacional (Academy)

Usado em:
- IA Tutor
- quizzes
- simuladores
- explicação didática

Inclui:
- transcrição de aulas
- PDFs explicados
- microlearning
- estudos de caso

---

# ⚙️ 4. Hybrid Retrieval Pipeline

A BlueShark adota um pipeline híbrido:
Query → Expansion → Hybrid Search → Re-ranking → Context Injection → Prompt Final

---

## 4.1 Query Expansion

O sistema expande automaticamente a consulta:
- sinônimos
- termos técnicos
- termos normativos
- termos locais (Crioulo)

Exemplo:
"carne mal acondicionada" →
["temperatura", "armazenamento", "PCC", "HACCP", "risco biológico"]

---

## 4.2 Hybrid Search (Regra Oficial)

Combinação obrigatória:
🔹 Similaridade vetorial
🔹 BM25
🔹 Filtros normativos
🔹 Repriorização por risco

---

## 4.3 Re-ranking (Cross-Encoder)

O sistema reordena por:
- risco do chunk
- precisão normativa
- relevância contextual
- histórico do usuário

---

# 📦 5. Estratégias por Módulo (Módulo-Specific Retrieval)

Cada módulo possui regras específicas.

## 5.1 ColdChain Retrieval Rules

Priorizar:
1. temperatura
2. telemetria
3. rastreabilidade
4. embarcação
5. APPCC da pesca
6. contaminação cruzada
7. legislação de pesca (INPS/IGAE)

---

## 5.2 BestFood Retrieval Rules

Priorizar:
1. POPs
2. PCCs críticos
3. Boas práticas
4. legislação sanitária
5. ISO 22000
6. evidências de higiene

---

## 5.3 ESG Retrieval Rules

Priorizar:
1. emissão
2. resíduos
3. água e energia
4. políticas sociais
5. indicadores globais
6. metas ESG nacionais

---

## 5.4 SafeStay Retrieval Rules

Priorizar:
- higiene de quartos
- pragas
- primeiros socorros
- risco ao hóspede
- inspeção do ITCV

---

## 5.5 Customer Experience Retrieval Rules

1. NPS
2. Reclamações
3. Insights comportamentais
4. Padrões de hospitalidade
5. ISO 10004 (Satisfação do Cliente)

---

## 5.6 GovTech Retrieval Rules (crítico)

1. legislação
2. autos e penalidades
3. riscos críticos
4. padrões de inspeção
5. relatórios de incidente
6. Citizen Reporter
7. decisões IA explicáveis

---

# 🗺 6. Geo-Context Retrieval (GovTech)

Quando o usuário está em Cabo Verde:
- filtro automático por concelho/ilha
- risco local
- histórico de incidentes
- padrões de não conformidade locais
- alertas EPID

O chunk recebe metadados:
{
  "geo": "Santiago.Praia",
  "risk_cluster": "sanitary-hotspot",
  "last_incident": "2025-02-03"
}

---

# 🧪 7. Evals de Recuperação

Testes obrigatórios:
- precisão por módulo
- recall normativo por país
- regressão a cada atualização
- validação com auditores BeSafe
- validação com inspetores GovTech

---

# 🧩 8. Context Injection (Prompt Final)

Depois da busca, o contexto é injetado no prompt:

Você é um agente oficial do módulo {BestFood}.
Use apenas normas válidas de {Cabo Verde}.
O estabelecimento está classificado como {risco médio}.
O inspetor está em {Praia, Santiago}.

---

# 🧲 9. Output Final com Explicabilidade

Todo Copilot deve responder assim:

1. Resposta curta
2. Fundamento normativo
3. Evidência necessária
4. Ação recomendada
5. Citação da fonte normativa

E opcionalmente:
6. Estrutura para auditoria

---

# 🧩 10. Conclusão

A estratégia de contextual retrieval garante:
- precisão regulatória
- recuperações seguras
- respostas auditáveis
- integração GovTech
- suporte total à BlueShark Mobile & IA
- aderência às normas ISO + legislação de Cabo Verde

Este documento é usado em conjunto com:
01_RAG_Pipeline_Overview.md
02_Embedding_Strategy.md
04_Prompt_Chains.md
05_Memory_Policies.md
