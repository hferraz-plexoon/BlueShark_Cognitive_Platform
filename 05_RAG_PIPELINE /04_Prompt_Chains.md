# 04 — Prompt Chains  
## BlueShark Cognitive Platform — BeSafe Digital (2025)

Este documento descreve a arquitetura oficial de **Prompt Chains** utilizada pelos agentes cognitivos da BlueShark.  
As cadeias de prompts padronizam a estrutura de raciocínio dos Copilots, garantindo:

- consistência  
- explicabilidade  
- segurança  
- reprodutibilidade  
- precisão normativa  
- auditoria governamental  

---

# 🎯 1. Objetivos das Prompt Chains

As Prompt Chains devem:

1. estruturar respostas com multi-passos (chain-of-thought supervisionado)
2. separar etapas de raciocínio:
   - busca
   - interpretação
   - normativo
   - verificação
   - decisão
   - plano de ação
3. aplicar restrições normativas (ISO + legislação Cabo Verde)
4. reduzir alucinações
5. garantir outputs consistentes com GovTech, Academy e Mobile & IA
6. fornecer explicabilidade para auditores e governos

---

# 🧩 2. Tipos de Prompt Chains

A plataforma usa **seis tipos oficiais**:

1. **Retrieval Chain**  
2. **Understanding Chain**  
3. **Normative Reasoning Chain**  
4. **Diagnostic Chain**  
5. **Action Chain (Planos do PDCA)**  
6. **Audit Chain (GovTech + Certificação)**

---

# 3. Estrutura Geral da Prompt Chain (Blueprint Oficial)

Todas seguem o formato:
[1] System Prompt
[2] Context Injection
[3] User Intent Classifier
[4] Retrieval Query Generator
[5] Evidence Interpreter
[6] Normative Matching Layer
[7] Risk Scoring
[8] Recommendation Engine
[9] Output Formatter

---

# 🔷 4. Prompt Chains — Detalhamento

---

## 4.1 Retrieval Chain  
*Objetivo: Encontrar o contexto certo com precisão jurídica e técnica.*

Etapas:

1. detectar módulo
2. analisar query
3. aplicar expansão semântica
4. gerar busca híbrida
5. re-ranking normativo
6. retornar chunks explicáveis

Prompt principal:
Você é um agente BlueShark especializado em {Módulo}.
Gere termos de busca, sinônimos, siglas normativas e palavras críticas.
Use legislação aplicável: {País}, {Normas ISO}, {Legislação setorial}.
NUNCA invente normas.

---

## 4.2 Understanding Chain  
*Objetivo: transformar texto do usuário em intenção clara.*

Exemplo de classificação:

- dúvida pedagógica  
- diagnóstico de risco  
- auditoria  
- penalidade  
- ação corretiva  
- consulta normativa  
- explicação técnica  

Prompt-base:
Classifique a intenção do usuário em:
[treinamento] [auditoria] [norma] [risco] [diagnóstico] [ação] [relatório].

Se múltipla, priorize auditoria > risco > norma.

---

## 4.3 Normative Reasoning Chain  
*O coração da precisão jurídica do sistema.*

Usado para:

- autos de infração
- interpretação de legislação
- cruzamento ISO com leis
- explicação de APPCC
- justificativas GovTech

Prompt:
Aplique a seguinte hierarquia normativa:
1. Legislação nacional (Cabo Verde)
2. Regulamentos complementares
3. Normas internacionais (ISO, CAC, FAO)
4. Boas práticas reconhecidas

Explique como a norma se aplica ao caso.
Nunca extrapole além do texto normativo.

---

## 4.4 Diagnostic Chain  
*Usado por consultores, inspetores e Copilots operacionais.*

Diagnostica:

- não conformidades
- riscos de higiene
- falhas em PCCs
- erro em cadeia de frio
- risco ao hóspede
- falhas ESG

Prompt:
Identifique o problema.
Classifique em: crítica, maior, menor.
Justifique usando normas e evidências.
Indique impacto sanitário, legal e turístico.

---

## 4.5 Action Chain (PDCA Generator)

Entrega ações corretivas:

- imediatas  
- de curto prazo  
- preventivas  

Sempre seguindo a metodologia oficial BlueShark.

Prompt:
Gere ações em formato PDCA:
- Ação imediata
- Correção
- Prevenção
- Responsável
- Prazo
- Evidências necessárias
Aplique somente ações tecnicamente possíveis.

---

## 4.6 Audit Chain (GovTech + Certificação)

Usado para:
- relatórios automáticos
- autos de infração
- scoring
- inspeções multi-instituto

Prompt oficial:
Gere um relatório auditável contendo:
- Resumo
- Achados
- Fundamentação legal
- Criticidade
- Penalidade cabível
- Ação imediata
- Evidência necessária
- Registro para GovTech
Respeite a legislação de Cabo Verde.


---

# 🔒 5. Guardrails da Prompt Chain

Obrigatórios:

- Sem alucinação normativa
- Sem inventar penalidades
- Sem criar valores de temperatura inexistentes
- Sem flexibilizar riscos sanitários
- Sem alterar normas ISO
- Sem dar instruções inseguras
- Sem sugerir manipulação política/institucional
- Sem ações que violem padrões da BeSafe Digital

---

# 🧪 6. Testing Protocol (Prompt Evals)

Cada cadeia tem testes:

| Tipo | Frequência | Responsável |
|------|------------|-------------|
| Factual | diário | IA/ML |
| Normativo | semanal | Auditores BeSafe |
| Risco Sanitário | semanal | INSP/ERIS via GovTech |
| Risco Turístico | mensal | ITCV |
| Explicabilidade | contínua | QA |

---

# 🧩 7. Versionamento das Prompt Chains

As Prompt Chains seguem versionamento semântico:
vMAJOR.MINOR.PATCH

MAJOR = mudança de arquitetura
MINOR = novas regras normativas
PATCH = otimização ou fix

Exemplo:

- GovTech Audit Chain v2.1.0
- ColdChain Diagnostic Chain v1.3.4

---

# 📘 8. Conclusão

Esta especificação garante:

- uma base sólida para todos os Copilots BlueShark  
- rastreabilidade para o governo  
- consistência pedagógica  
- precisão jurídica  
- suporte total ao Mobile & IA  
- alinhamento com a estratégia da BeSafe Digital  

Este documento deve ser usado junto com:

- 01_RAG_Pipeline_Overview.md  
- 02_Embedding_Strategy.md  
- 03_Contextual_Retrieval.md  
- 05_Memory_Policies.md  

