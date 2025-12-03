# 03 — Agents Orchestration  
## BlueShark Cognitive Platform

Este documento descreve como todos os **Copilots** da plataforma BlueShark interagem entre si, compartilham conhecimento e são orquestrados de forma segura, auditável e escalável.

Ele define:

- a estrutura dos agentes  
- o mecanismo de coordenação  
- limites e responsabilidades  
- o fluxo completo de execução  
- como garantir governança e segurança  
- como cada agente acessa o RAG  
- como interoperam com o Mobile & IA e GovTech  

---

# 1. Por que existe uma Orquestração?

Sem orquestração, Copilots seriam:

❌ isolados  
❌ redundantes  
❌ inconsistentes  
❌ difíceis de auditar  
❌ difíceis de gerenciar  
❌ caros de escalar  

Com orquestração:

✅ um único cérebro regula tudo  
✅ cada Copilot sabe exatamente seu papel  
✅ compartilhamento seguro do RAG  
✅ consistência entre módulos  
✅ governança e auditoria unificadas  
✅ capacidade de adicionar novos Copilots sem refazer arquitetura  
✅ alinhamento com normas e leis locais  

---

# 2. Modelo Geral de Orquestração

A BlueShark utiliza um sistema de **Agente Central Orquestrador**, responsável por:

1. Receber a intenção do usuário  
2. Identificar o Copilot apropriado  
3. Carregar o Context Pack específico  
4. Executar o fluxo RAG  
5. Gerar a resposta final com citações  
6. Registrar logs e auditoria  

### 2.1 Visão Macro

- 1 Orquestrador Principal  
- 11 Copilots especializados  
- 1 Pipeline RAG centralizado  
- 1 Sistema de Governança  
- 1 Base de Conhecimento Multi-País  

---

# 3. Diagrama da Orquestração (Mermaid)

\```mermaid
flowchart TD
    U[Usuário] --> I[Intenção Detectada]
    I --> O[Agente Orquestrador]

    O -->|Seleciona| C1[Copilot Academy]
    O -->|Seleciona| C2[Copilot Implementation]
    O -->|Seleciona| C3[Copilot ColdChain]
    O -->|Seleciona| C4[Copilot BestFood]
    O -->|Seleciona| C5[Copilot ESG]
    O -->|Seleciona| C6[Copilot SafeStay]
    O -->|Seleciona| C7[Copilot GuestExperience]
    O -->|Seleciona| C8[Copilot Auditor]
    O -->|Seleciona| C9[Copilot GovTech]
    O -->|Seleciona| C10[Copilot Citizen Safety]
    O -->|Seleciona| C11[Copilot Global Standards]

    C1 --> RAG[(RAG Pipeline)]
    C2 --> RAG
    C3 --> RAG
    C4 --> RAG
    C5 --> RAG
    C6 --> RAG
    C7 --> RAG
    C8 --> RAG
    C9 --> RAG
    C10 --> RAG
    C11 --> RAG

    RAG --> LLM[LLM / IA Generativa]
    LLM --> O
    O --> A[Resposta com Citações + Auditoria]
\```

---

# 4. Hierarquia dos Agentes

| Nível | Agente | Função |
|------|--------|---------|
| **N0** | **Orquestrador Central** | Comanda tudo |
| **N1** | Copilots especializados | Executam suas funções específicas |
| **N2** | Sub-agentes internos | Checklists, ações corretivas, análises, etc. |

---

# 5. O Agente Orquestrador (N0)

## 5.1 Funções Principais

- Classificação de intenção  
- Seleção de Copilot  
- Montagem do contexto  
- Supervisão do LLM  
- Geração da resposta final  
- Auditoria total  
- Segurança e guardrails  
- Encaminhamento entre Copilots  

## 5.2 Regras de Controle

1. Nenhum Copilot pode acessar conteúdo fora do seu domínio  
2. O Orquestrador aplica filtros por:
   - país  
   - módulo  
   - norma  
   - organização  
   - papel do usuário  
3. Toda resposta deve citar a fonte normativa  
4. O Orquestrador tem a palavra final sempre  

---

# 6. Copilots Especializados (N1)

## Lista Oficial (11 Copilots)

1. Academy Copilot  
2. Implementation Copilot  
3. ColdChain Copilot  
4. BestFood Copilot  
5. ESG+Social Copilot  
6. SafeStay Copilot  
7. GuestExperience Copilot  
8. Audit Copilot  
9. GovTech Copilot  
10. Citizen Safety Copilot  
11. Global Standards Copilot  

Cada Copilot possui:

- Prompt mestre  
- Context Pack próprio  
- Checklists e Regras  
- Regulamentos aplicáveis  
- Restrições de atuação  

---

# 7. Sub-Agentes Especializados (N2)

Cada Copilot pode acionar sub-agentes internos:

### Exemplos:

- **Evidence Analyzer** – análise de fotos, vídeos, documentos  
- **OCR Agent** – leitura e extração de texto  
- **Risks Agent** – detecção de riscos e recomendações  
- **Corrective Action Agent** – geração de ações corretivas  
- **Legal Checker Agent** – validação com normas  
- **Summarizer Agent** – sumarização de relatórios  
- **Checklist Validator** – validação de passos obrigatórios  

---

# 8. Fluxo Completo de Execução

## 8.1 Fase 1 — Intenção
O sistema detecta qual Copilot deve responder.

## 8.2 Fase 2 — Seleção de Context Pack
O Orquestrador carrega:

- Módulo  
- País  
- Norma/ISO  
- Perfil do usuário  

## 8.3 Fase 3 — Recuperação via RAG
Filtragem por:

- país  
- setor  
- módulo  
- nível crítico de evidência  

## 8.4 Fase 4 — Execução pelo Copilot

Ele:

- interpreta a pergunta  
- aplica regras  
- seleciona fontes  
- produz resposta técnica  

## 8.5 Fase 5 — Auditoria Automática
Cada resposta recebe:

- fontes citadas  
- ID das chunks  
- score de confiança  
- trilha de decisão  

---

# 9. Limites entre Copilots

### Academy Copilot
🎓 Só responde sobre treinamento, trilhas, certificação.

### Implementation Copilot
🛠 Só responde sobre implantação, playbooks, evidências.

### BestFood / ColdChain / ESG / SafeStay / GuestExperience
🍽️ 🧊 ♻️ 🧼 ⭐  
Focados nas normas específicas dos módulos governamentais (selos BlueShark).

### Audit Copilot
🔍 Focado em conformidade, checklists e auditorias.

### GovTech Copilot
🏛️ Exclusivo para:

- fiscalização  
- penalidades  
- autos  
- incidentes  
- inspeções públicas  

### Citizen Safety Copilot
📱 Responde denúncias e urgências leves.

---

# 10. Segurança e Garantias

## 10.1 Garantias do Orquestrador
- nunca extrapolar domínio  
- nunca responder sem base normativa  
- nunca fornecer recomendações ilegais  
- sempre citar as fontes  

## 10.2 Controles
- RBAC + ABAC  
- Logs imutáveis  
- Proteção contra jailbreak prompt  
- Limites de escopo por Copilot  

---

# 11. Versionamento e Deploy de Copilots

Cada Copilot é versionado individualmente:

- `Copilot_Academy_v1.4.2`  
- `Copilot_GovTech_v2.1.0`  
- etc.

Permite:

- rollback  
- testes independentes  
- evolução modular  

---

# 12. Conclusão

A orquestração é o coração da BlueShark Cognitive Platform — garantindo:

✔ Consistência  
✔ Segurança  
✔ Escalabilidade  
✔ Multi-país  
✔ Multi-norma  
✔ Governança  
✔ Explicabilidade  
✔ Auditorabilidade  

Com essa arquitetura, a BeSafe Digital pode adicionar novos Copilots rapidamente e evoluir para uma plataforma AI-first de padrão internacional.
