# 01 — Normative Structure  
## BlueShark Cognitive Platform  
### Estrutura Normativa Global para IA Regulada, RAG e Certificação Multipaís

---

# 1. Objetivo do Documento

Este documento define como é organizada toda a **base normativa oficial** utilizada pelos Copilots, RAG e GovTech da BlueShark Cognitive Platform.

Ele descreve:

- a estrutura de diretórios da base normativa  
- normas globais suportadas  
- legislações por país  
- taxonomias e ontologias normativas  
- políticas de atualização  
- requisitos de versionamento  
- vinculação entre normas e módulos (ColdChain, BestFood, ESG, etc.)

---

# 2. Estrutura Geral da Base Normativa (RAG)

A Knowledge Base é organizada em duas macro-camadas:

/knowledge-base/
/global/
/country/


### 2.1. Diretório “global”  
Contém normas universais, como:

- ISO  
- Codex Alimentarius  
- WHO/OMS  
- UNWTO  
- ESG global frameworks  
- Regras internacionais de cadeia de frio  
- Tourism & Hospitality Standards  

### 2.2. Diretório “country”  
Normas específicas por país:

- leis sanitárias  
- decretos de fiscalização  
- normas de pesca, turismo e qualidade  
- resoluções específicas  
- procedimentos oficiais  

---

# 3. Estrutura Completa de Diretórios

Abaixo, a **árvore oficial** adotada pela BlueShark:

/knowledge-base/
│
├── global/
│ ├── HACCP/
│ │ ├── Codex_Principles.md
│ │ ├── HACCP_7Steps.md
│ │ ├── HACCP_PRP_PPRO.md
│ │ └── Glossary.md
│ │
│ ├── ISO/
│ │ ├── ISO_22000/
│ │ │ ├── Clauses.md
│ │ │ ├── Requirements.md
│ │ │ ├── Audit_Guide.md
│ │ │ └── CCP_vs_OPRP.md
│ │ ├── ISO_14001/
│ │ ├── ISO_9001/
│ │ └── ISO_21401/
│ │
│ ├── ESG/
│ │ ├── SDGs_UN.md
│ │ ├── Environmental_Indicators.md
│ │ ├── Social_Indicators.md
│ │ └── Governance_Principles.md
│ │
│ ├── ColdChain/
│ │ ├── WHO_Temperature_Guide.md
│ │ ├── Fishing_Standards_FAO.md
│ │ └── Transport_Requirements.md
│ │
│ ├── Tourism/
│ │ ├── UNWTO_Quality_Guide.md
│ │ ├── Hygiene_Standards.md
│ │ └── Accessibility_Guide.md
│ │
│ └── Safety/
│ ├── WHO_Sanitation_Guide.md
│ └── Occupational_Safety.md
│
└── country/
├── cabo-verde/
│ ├── FoodSafety/
│ │ ├── DL_04_2009.md
│ │ ├── Hygienic_Guidelines.md
│ │ └── Inspection_Checklists.md
│ ├── Fisheries/
│ │ ├── Fishing_Law.md
│ │ ├── Maritime_Standards.md
│ │ └── ColdChain_Regulation.md
│ ├── Tourism/
│ │ ├── ITCV_Standards.md
│ │ ├── Tourist_Safety.md
│ │ └── Hotel_Certification.md
│ ├── Quality/
│ │ └── IGQPI_Requirements.md
│ └── PublicHealth/
│ ├── INSP_Guidelines.md
│ ├── ERIS_Regulations.md
│ └── Incident_Reporting.md
│
├── brazil/
├── portugal/
├── angola/
└── mozambique/


---

# 4. Taxonomia Normativa (Ontologia)

Para interpretação correta via IA, toda norma é categorizada em:
Domain -> Subdomain -> Category -> Requirement -> Clause

Exemplo para segurança alimentar:
FoodSafety
└── HACCP
└── PRP
└── PersonalHygiene
└── Requirement: "Uso obrigatório de EPI"


---

# 5. Tipos de Documentos Suportados

Cada item da Knowledge Base pode conter:

- **Texto estruturado** (markdown)  
- **Tabelas normativas**  
- **Exemplos aplicados**  
- **Casos de uso**  
- **Checklists oficiais**  
- **Modelos PDF convertidos**  
- **Imagens (para visão computacional)**  

---

# 6. Como a IA Utiliza a Estrutura Normativa

O pipeline RAG usa:

### 6.1. Embeddings separados
- embeddings por norma  
- embeddings por país  
- embeddings por checklist  

### 6.2. Camadas de contexto
- tipo de estabelecimento  
- módulo BlueShark (ColdChain, BestFood, etc.)  
- país/região/ilha  
- atividade do usuário  
- nível profissional  

### 6.3. Reasoning jurídico-técnico
O copiloto:

- cita normas  
- explica item por item  
- compara ISO × Codex × leis nacionais  
- gera recomendações baseadas nas cláusulas corretas  

---

# 7. Governança de Atualização

## 7.1. Perfis que podem atualizar normas
- BeSafe Digital — Núcleo técnico  
- Consultores especialistas  
- Equipe jurídica  
- Equipe de IA da plataforma  

## 7.2. Processo de atualização
1. Submissão de nova norma
2. Revisão técnica
3. Aprovação (2 revisores mínimos)
4. Versionamento
5. Publicação no repositório RAG


---

# 8. Versionamento Normativo

A versão segue o padrão:
ISO22000-v1.3-2025
CV-DL04-2009-v2.0-2025
UNWTO-Guide-v1.1-2024


---

# 9. Regras por Módulo BlueShark

### 9.1 ColdChain  
- WHO  
- FAO Fishing Standards  
- Cabo Verde ColdChain laws  

### 9.2 BestFood  
- ISO 22000  
- HACCP Codex  
- Cabo Verde DL 04/2009  

### 9.3 ESG  
- ISO 14001  
- SDGs  
- Regras locais ambientais  

### 9.4 SafeStay  
- UNWTO Hygiene  
- WHO Public Health  
- ITCV/INSP normas turísticas  

### 9.5 GuestExperience  
- Normas UNWTO  
- Acessibilidade ADA/WCAG  
- ITCV padrões de qualidade  

---

# 10. Relação com os Copilots

O Copilot Global Standards usa toda a base.

Cada Copilot setorial usa um subconjunto:

| Copilot | Diretórios usados |
|--------|--------------------|
| Academy | global + country |
| ColdChain | ColdChain + Fisheries |
| BestFood | HACCP + ISO22000 |
| ESG | ESG + ISO14001 |
| SafeStay | Tourism + Safety |
| GuestExperience | Tourism + Accessibility |
| GovTech | country + global |
| Auditor | todos |

---

# 11. Conclusão

Esta estrutura normativa garante:

- consistência  
- padronização  
- escalabilidade internacional  
- precisão técnica  
- rastreabilidade jurídica  
- interoperabilidade entre módulos  

É o “cérebro normativo” que alimenta toda a inteligência regulatória da BlueShark Cognitive Platform.



