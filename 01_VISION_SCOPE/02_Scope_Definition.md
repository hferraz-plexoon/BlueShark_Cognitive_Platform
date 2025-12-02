# 02 — Scope Definition  
## BlueShark Cognitive Platform  
### BeSafe Digital — Unidade de IA & Engenharia

---

# 🎯 1. Objetivo do Documento

Este documento define de forma clara e objetiva **todo o escopo funcional, técnico e operacional** da **BlueShark Cognitive Platform**, delimitando:

- O que está incluído  
- O que está excluído  
- Interfaces com outras plataformas  
- Limitações e fronteiras do sistema  
- Escopo por módulo (Academy, Mobile & IA, GovTech, Citizen Reporter)  
- Escopo por Copilot

É a referência oficial para engenharia, produto, governança e auditoria técnica.

---

# 📦 2. Escopo Geral da Cognitive Platform

A Cognitive Platform é composta por:

### ✔ Núcleo de Inteligência (Core AI Engine)
- RAG (Retrieval-Augmented Generation)
- Reasoning multietapas
- Classificação automática
- Interpretação normativa
- Análise de evidências (VC)
- Preditivo e alerta antecipado

### ✔ Agentes Cognitivos (Copilots)
Um conjunto de agentes especializados, cada um com função específica:

- Academy Copilots  
- Operational Copilots  
- Auditoria & Consultoria  
- GovTech Copilots  
- Citizen Safety Copilot  

### ✔ Knowledge Base (Base de Conhecimento)
- Normas ISO  
- Leis de Cabo Verde  
- Decretos e regulamentos  
- Checklists oficiais  
- Procedimentos e POPs  
- Documentação do BlueShark Program  

### ✔ Componentes Técnicos
- Indexação e embeddings  
- Vetorização normativa  
- Guardrails  
- Sistemas de contexto longo  
- Observabilidade  
- Segurança e governança  

---

# 🧭 3. Escopo por Plataforma

A Cognitive Platform atende simultaneamente 4 sistemas do ecossistema BlueShark:

---

## **3.1. BlueShark Academy & Implementation Hub**
**INCLUSO:**
- IA Tutor (explicação)  
- IA Avaliador (provas e exercícios)  
- IA de recomendação de trilhas  
- Geração de exercícios  
- Geração de conteúdos complementares  
- Explicação normativa contextual  
- Copilot para consultores

**NÃO INCLUSO:**
- Motor de cursos  
- Player SCORM  
- Infraestrutura pedagógica  
(→ isso pertence ao repositório Academy)  

---

## **3.2. BlueShark Mobile & IA**
**INCLUSO:**
- Cálculo automático de riscos  
- Análise de checklists por IA  
- Validação de evidências críticas  
- Geração de planos de ação  
- Copilots operacionais por módulo  
  - ColdChain  
  - BestFood  
  - ESG  
  - SafeStay  
  - GuestExperience  

**NÃO INCLUSO:**
- App mobile  
- Módulo de checklists  
- IoT  
(→ pertence ao Mobile & IA repo)

---

## **3.3. BlueShark GovTech Suite**
**INCLUSO:**
- Copilots governamentais (ITCV, IGAE, INSP, IGQPI, ERIS)  
- Interpretação legal automatizada  
- Cruzamento leis × evidências  
- Auxílio na emissão de autos  
- Suporte ao dashboard regulatório  
- Classificação de denúncias  
- Previsão de clusters de risco  

**NÃO INCLUSO:**
- App de inspeção  
- Dashboards  
(→ desenvolvido no repositório GovTech)

---

## **3.4. Citizen Reporter**
**INCLUSO:**
- Classificação automática  
- Triagem por gravidade  
- IA para determinar risco sanitário  
- Cruzamento automático com módulos  
- Envio de alertas para institutos  

**NÃO INCLUSO:**
- Interface do app  
- Mapa e dashboard públicos  

---

# 🧩 4. Escopo por Copilot

A Cognitive Platform contém **11 Copilots oficiais**, divididos em 5 categorias.

---

## **4.1. Academy Copilots**
- Learning Copilot  
- Exam Copilot  
- Content Builder Copilot  

Escopo:
- Explicações  
- Avaliação  
- Geração de conteúdo  
- Correção automática  

---

## **4.2. Operational Copilots (Mobile & IA)**  
- ColdChain Copilot  
- BestFood Copilot  
- ESG Copilot  
- SafeStay Copilot  
- GuestExperience Copilot  

Escopo:
- Diagnósticos operacionais  
- Riscos  
- Conformidade  
- Planos de ação  

---

## **4.3. Audit & Consulting Copilots**
- Implementation Copilot  
- Audit Copilot  
- Evidence/VC Copilot  

Escopo:
- Apoio a consultores  
- Auditorias internas  
- Análise de evidências  

---

## **4.4. GovTech Copilots**
- ITCV Copilot  
- IGAE Copilot  
- IGQPI Copilot  
- INSP Copilot  
- ERIS Copilot  
- Ministério da Economia Copilot  

Escopo:
- Interpretação legal  
- Riscos regulatórios  
- Autos assistidos  
- Ranking governamental  
- Políticas públicas  

---

## **4.5. Citizen Safety Copilot**
Escopo:
- Classificação de denúncias  
- Avaliação de risco sanitário  
- Surtos previsíveis  
- Dados para ERIS / INSP  

---

# 🛑 5. O que NÃO está no escopo da Cognitive Platform

Estas atividades pertencem a outros repositórios:

### ❌ Aplicativos Mobile (Mobile & IA e Academy)
### ❌ Dashboards Web
### ❌ Infraestrutura IoT
### ❌ Banco de dados de produção
### ❌ DevOps completo
### ❌ Certificação Blockchain (futuro)
### ❌ Hospedagem de conteúdo multimídia

A Cognitive Platform só fornece **inteligência**.

---

# 🏗️ 6. Interfaces e Dependências

A Cognitive Platform depende de:

- APIs do Academy  
- APIs do Mobile & IA  
- APIs do GovTech  
- Base normativa (Knowledge Base repo)  
- Pipelines de ingestão documental  
- Rotinas de atualização legal  
- Sistema de autenticação (IAM unificado no BlueShark Program)

E fornece:

- respostas com reasoning  
- diagnósticos  
- recomendações  
- classificações  
- resumos normativos  
- relatórios automáticos  
- execuções multiagente  

---

# 🧱 7. Limitações Técnicas

- A IA não substitui decisão humana (HITL obrigatório)  
- Não executa ações diretas nos módulos operacionais  
- Não altera dados de produção diretamente  
- Não gera documentos legais oficiais sem validação humana  
- Depende da atualização constante da base normativa  

---

# 📌 8. Conclusão

Este documento define o **escopo oficial, estável e aprovado** da BlueShark Cognitive Platform.

Ele garante:

- clareza para engenharia  
- segurança jurídica  
- governança de IA  
- escopo fechado para contratação  
- base para todos os demais documentos do repositório

