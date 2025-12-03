# 04 — Data Flow Diagram (DFD)  
## BlueShark Cognitive Platform

Este documento descreve o **Fluxo de Dados Completo** da plataforma BlueShark Cognitive Platform — cobrindo desde a entrada de dados pelos usuários (field, consultores, gestores, governo e cidadãos) até o processamento via RAG, agentes cognitivos e camadas de governança.

Inclui:

- visão macro do fluxo de dados  
- fluxos por camada  
- fluxos entre Copilots  
- fluxos entre Mobile, Academy, GovTech e Citizen  
- diagrama completo (Mermaid)  
- lista de entidades e transformações  
- requisitos de segurança e governança  

---

# 1. Objetivo do Fluxo de Dados

Este DFD garante:

✔ rastreabilidade completa  
✔ consistência entre módulos  
✔ integridade da informação  
✔ lógica clara entre entradas/saídas  
✔ mapeamento auditável do RAG  
✔ governança centralizada  
✔ preparação para multi-país / multi-norma  

---

# 2. Visão Geral do Fluxo de Dados

A plataforma BlueShark recebe dados de 5 grandes fontes:

1) **Usuários operacionais**  
   - auditores  
   - consultores  
   - hotéis / restaurantes  
   - pescadores / processadores  

2) **Aplicativos Mobile**  
   - Academy  
   - Implementation Hub  
   - Mobile & IA (ColdChain, BestFood, ESG, SafeStay, CX)  

3) **GovTech Suite**  
   - inspeções  
   - autos  
   - incidentes  
   - penalidades  
   - Citizen Reporter  

4) **Sensores & IoT**  
   - temperaturas  
   - trilhas HACCP  
   - rota de transporte  
   - integridade da cadeia de frio  

5) **Base de Conhecimento**  
   - leis  
   - decretos  
   - ISO  
   - HACCP  
   - APCC  
   - checklists  
   - manuais  
   - diretrizes governamentais  

Todos passam por:

- Camada de Ingestão  
- Normalização  
- RAG Pipeline  
- Agente Orquestrador  
- Copilots  
- Logs + Auditoria  
- Dashboards  

---

# 3. Diagrama de Fluxo Macro (DFD Nível 0)

```mermaid
flowchart LR
    U[Usuário / Auditor / Consultor] --> APP[Aplicativos Mobile]
    U2[Gestores / Governo] --> WEB[Portal Web]

    APP --> ING[Ingestão de Dados]
    WEB --> ING
    IOT[Sensores IoT] --> ING
    CIT[Citizen Reporter] --> ING

    ING --> NORM[Normalização & Validação]
    NORM --> DB[(BD Operacional)]
    NORM --> KB[(Base de Conhecimento)]

    DB --> RAG[RAG Pipeline]
    KB --> RAG

    RAG --> ORCH[Agente Orquestrador]

    ORCH --> CP1[Copilot Academy]
    ORCH --> CP2[Copilot Implementation]
    ORCH --> CP3[Copilot BestFood]
    ORCH --> CP4[Copilot ColdChain]
    ORCH --> CP5[Copilot ESG]
    ORCH --> CP6[Copilot SafeStay]
    ORCH --> CP7[Copilot GuestExperience]
    ORCH --> CP8[Copilot Auditor]
    ORCH --> CP9[Copilot GovTech]
    ORCH --> CP10[Copilot CitizenSafety]
    ORCH --> CP11[Copilot Global Standards]

    CP1 --> ORCH
    CP2 --> ORCH
    CP3 --> ORCH
    CP4 --> ORCH
    CP5 --> ORCH
    CP6 --> ORCH
    CP7 --> ORCH
    CP8 --> ORCH
    CP9 --> ORCH
    CP10 --> ORCH
    CP11 --> ORCH

    ORCH --> RESP[Resposta ao Usuário]
    ORCH --> AUD[Auditoria & Logs]
````

# 4. Fluxo de Dados por Camada
## 4.1 Camada de Entrada (Input Layer)

| Fonte              | Tipo                                 | Observações                         |
| ------------------ | ------------------------------------ | ----------------------------------- |
| Mobile Academy     | Progresso, quizzes, vídeos, provas   | IA avalia automaticamente           |
| Implementation Hub | Evidências, fotos, PDFs, vídeos      | Passa por OCR + visão computacional |
| Mobile & IA        | HACCP, segurança, ESG, temperaturas  | Fluxo crítico                       |
| GovTech            | inspeções, autos, não conformidades  | Dados sensíveis                     |
| Citizen Reporter   | denúncias, fotos, geolocalização     | Alto volume, risco moderado         |
| IoT                | telemetria, temperatura, localização | Ingestão contínua                   |

---

## 4.2 Camada de Normalização
Processos:
- validação estrutural
- extração de metadados
- anonimização (quando necessário)
- classificação automática
- enriquecimento contextual (ilha, concelho, setor, risco)
- transformação HACCP / ColdChain
- limpeza e padronização de linguagem

## 4.3 Camada de Armazenamento
Dois bancos:
### Banco Operacional (Postgres / Timescale)
- dados dinâmicos
- evidências
- auditorias
- trilhas HACCP
- telemetria IoT
### Base de Conhecimento (RAG Store)
- ISO 22000
- HACCP
- Segurança Alimentar
- ESG e Sustentabilidade
- Turismo
- SafeStay
- legislações CV
- decretos
- manuais de inspeção

## 4.4 Camada RAG
Pipeline:
- Embedding
- Recuperação contextual
- Filtragem por país/setor
- Seleção normativa
- Montagem de contexto
- Envio para LLM
Garantias:
- citações obrigatórias
- chunk toxicity filter
- filtros por nível crítico

## 4.5 Camada dos Copilots
Cada Copilot:
- recebe contexto refinado
- aplica prompts especializados
- invoca sub-agentes (OCR, Risk Analyzer, Vision, Checklist Validator)
- devolve saída para o Orquestrador

## 4.6 Saída
Entregas:
- recomendações
- alertas
- ações corretivas
- diagnósticos
- análises de risco
- relatórios
- certificados
- notificações a governo

---

# 5. DFD Nível 1 – Detalhado (Mermaid)

flowchart TD

    %% NÍVEL 1 - INTEGRAÇÃO COMPLETA

    subgraph INPUTS[Camada de Entrada]
        A1[Mobile Academy]
        A2[Mobile Implementation]
        A3[Mobile HACCP/ColdChain]
        A4[GovTech Inspeções]
        A5[Citizen Reporter]
        A6[Sensores IoT]
    end

    subgraph ING[Ingestão & Pré-processamento]
        B1[Validação]
        B2[OCR / Visão]
        B3[Normalização]
        B4[Classificação]
        B5[Enriquecimento]
    end

    subgraph STORAGE[Armazenamento]
        C1[(BD Operacional)]
        C2[(Base RAG Multi-País)]
    end

    subgraph RAG[RAG Pipeline]
        D1[Embedding]
        D2[Retriever]
        D3[Context Filter]
        D4[LLM Context Builder]
    end

    subgraph ORCH[Agente Orquestrador]
        E1[Intenção]
        E2[Seleção de Copilot]
        E3[Governança & Regras]
        E4[Fusão de Respostas]
    end

    subgraph CP[Copilots]
        F1[Academy]
        F2[Implementation]
        F3[ColdChain]
        F4[BestFood]
        F5[ESG]
        F6[SafeStay]
        F7[GuestExperience]
        F8[Audit]
        F9[GovTech]
        F10[Citizen Safety]
        F11[Global Standards]
    end

    subgraph OUTPUTS[Saída]
        G1[Web Dashboard]
        G2[Mobile Response]
        G3[Gov Reports]
        G4[Logs & Auditoria]
    end

    INPUTS --> ING
    ING --> STORAGE
    STORAGE --> RAG
    RAG --> ORCH
    ORCH --> CP
    CP --> ORCH
    ORCH --> OUTPUTS

/````

---

# 6. Entidades e Transformações
## 6.1 Entidades Principais
- Usuário
- Auditor
- Inspector
- Empresa
- Embarcação
- Lote de Peixe
- Checklist
- Evidência
- Ação Corretiva
- Treinamento
- Trilha
- Certificação
- Incidente
- Risco

---

# 7. Requisitos de Governança do Fluxo de Dados
Obrigatórios:

✔ log imutável
✔ assinatura das evidências
✔ versionamento de normas
✔ segregação por país
✔ segregação por setor
✔ regras ABAC (atributos)
✔ relação ilhas → concelhos → empresas
✔ trilha de auditoria LLM

Proibidos:

❌ respostas sem fonte
❌ mistura de normas de países distintos
❌ ações corretivas sem explicação
❌ decisões automáticas sem HITL

---

# 8. Conclusão

Este Data Flow Diagram estabelece:

✔ o fluxo oficial da BlueShark Cognitive Platform
✔ alinhamento entre Academy, Mobile, GovTech e Citizen
✔ segurança normativa e regulatória
✔ rastreabilidade multi-país
✔ mecanismo auditável para agentes cognitivos

É a base técnica para:
- arquitetura
- AI Copilots
- API
- RAG
- segurança
- auditoria
- certificação governamental

