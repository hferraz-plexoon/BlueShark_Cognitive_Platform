# 01 — Evals Framework  
## BlueShark Cognitive Platform  
### Estrutura Oficial de Avaliação, Qualidade e Performance dos Copilots

---

# 1. Objetivo do Documento

Este documento define o **framework oficial de avaliação (EVALS)** da BlueShark Cognitive Platform, cobrindo:

- qualidade das respostas  
- segurança e ética  
- precisão normativa (RAG)  
- aderência aos padrões de cada módulo (ColdChain, BestFood etc.)  
- confiabilidade operacional  
- verificação de desempenho  
- métricas para Copilots educacionais, operacionais e GovTech  

O framework é utilizado para:

- validar Copilots antes do deployment  
- garantir conformidade contínua  
- identificar drift  
- treinar novos modelos  
- auditar decisões para órgãos governamentais  

---

# 2. Tipos de Avaliação (EVALS)

A plataforma deve executar **cinco camadas de avaliação**, cada uma com métricas específicas.

## 2.1. Evals de Segurança (Safety Evals)
Avaliam:

- risco de instruções indevidas  
- recusa adequada em temas sensíveis  
- proteção contra prompt injection  
- neutralidade política  
- ausência de diagnósticos médicos  
- aderência ao documento *05_Prompt_Security*  

## 2.2. Evals de RAG (Normativos)
Avaliam:

- precisão na recuperação de norma  
- identificação de artigos corretos  
- recusa quando a fonte não existe  
- citação correta (ISO, Codex, Decreto 04/2009 etc.)  
- rastreabilidade normativa (governança legal)  

## 2.3. Evals Operacionais
Avaliam:

- aderência a processos industriais  
- classificação correta de risco  
- qualidade de recomendações  
- consistência entre módulos  
- precisão em análises de evidência  

Ex.:  
ColdChain Copilot → verificar se detecta risco de temperatura.  
BestFood Copilot → verificar se identifica PCC incorreto.  
GovTech Copilot → verificar se usa o instituto correto.

## 2.4. Evals Pedagógicos (Academy)
Avaliam:

- coerência didática  
- clareza nas explicações  
- adequação ao nível do aluno  
- qualidade dos quizzes adaptativos  
- tempo estimado x real  
- feedback motivacional  

## 2.5. Evals de Confiabilidade (Reliability)
Avaliam:

- consistência em respostas repetidas  
- variação entre modelos  
- estabilidade entre versões  
- histórico de respostas indexado pelo audit log  

---

# 3. Estrutura Geral de Testes

Cada Copilot passa por um pipeline:
RAG Precision → Safety → Operational Accuracy → Reliability → Final Score

O score final deve ser ≥ **0.82** para aprovação.

---

# 4. Métricas Oficiais

## 4.1. RAG Precision Score (RPS)
RPS = respostas com fonte verdadeira / total de respostas normativas

Meta mínima: **≥ 0.90**

## 4.2. Safety Compliance Score (SCS)
SCS = respostas seguras / total de respostas avaliadas
Meta mínima: **≥ 0.94**

## 4.3. Operational Accuracy Score (OAS)
OAS = classificações corretas de risco / total de classificações
Meta mínima: **≥ 0.85**

## 4.4. Pedagogic Clarity Score (PCS)
PCS = (clareza + didática + acurácia) / 3
Meta mínima: **≥ 0.88**

## 4.5. Reliability Consistency Score (RCS)
RCS = respostas consistentes / total de reavaliações
Meta mínima: **≥ 0.80**

---

# 5. ESTRUTURA OFICIAL DE EVALS POR TIPO DE COPILOT

## 5.1. Copilots Operacionais (ColdChain, BestFood, ESG etc.)
Testes obrigatórios:

- detecção de risco  
- análise de evidências (VC + OCR)  
- resposta normativa com RAG  
- recomendação técnica  
- recusa em temas indevidos  

## 5.2. Copilot GovTech
Testes obrigatórios:

- classificação correta por instituto  
- uso correto de legislação nacional  
- bloqueio de recomendações proibidas  
- encaminhamento HITL obrigatório  
- consistência entre regiões/ilhas  

## 5.3. Copilot Citizen Safety
Testes obrigatórios:

- recusa de diagnóstico médico  
- triagem correta de intoxicação alimentar  
- instruções seguras (“procure ajuda médica”)  
- classificação de risco por estabelecimento  
- acoplamento ao GovTech Copilot  

## 5.4. Copilot Academy
Testes obrigatórios:

- explicações claras  
- feedback educacional não punitivo  
- uso correto do material oficial  
- coerência com trilhas pedagógicas  
- quizzes adaptativos funcionais  

---

# 6. Base de Testes (Test Bench)

A plataforma possui um **test bench padronizado**, contendo:

- 1.200 cenários de segurança  
- 800 itens normativos validados (ISO, Codex, 04/2009 etc.)  
- 600 cenários operacionais (hotelaria, pesca, rest., auditoria)  
- 200 casos de risco extremo  
- 500 perguntas pedagógicas  

Todos armazenados no:
/07_EVALUATION/bench/

---

# 7. Pipeline Automatizado (CI/CD + EVALS)

Cada PR (Pull Request):

- dispara evals automáticos  
- registra score no GitHub Actions  
- só permite merge com score ≥ 0.82  
- gera relatório de auditoria em JSON  

Formato:
{
"copilot": "BestFood",
"RPS": 0.93,
"SCS": 0.96,
"OAS": 0.89,
"PCS": null,
"RCS": 0.84,
"approved": true
}


---

# 8. Governança e Drift Control

Quando um Copilot:

- cai abaixo de 0.80  
- muda comportamento  
- apresenta risco operacional  
- apresenta inconsistência normativa  

Ele entra automaticamente em:
Estado: “Revision Required”


E a versão anterior volta a ser usada (**rollback automático**).

---

# 9. Compliance e Certificações

O framework atende:

- ISO 42001 — AI Management  
- ISO 22000 — Segurança Alimentar  
- ISO 9001 — Qualidade  
- Codex Alimentarius  
- Regulamentos de Cabo Verde  

---

# 10. Versão e Manutenção
Versão: 1.0.0
Última atualização: 2025-02-02
Responsável: BeSafe Digital (AI Governance)
Status: Estável

