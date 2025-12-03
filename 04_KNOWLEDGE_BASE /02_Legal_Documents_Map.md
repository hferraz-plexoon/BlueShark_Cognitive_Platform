# 02 — Legal Documents Map  
## BlueShark Cognitive Platform  
### Mapeamento Jurídico e Regulatório (Global + Países)

---

# 1. Objetivo do Documento

Este arquivo apresenta o **mapa completo de documentos legais**, decretos, normas sanitárias, regulamentos turísticos, diretrizes técnicas e referenciais internacionais que compõem a base jurídica utilizada pelo:

- RAG normativo  
- Copilots  
- GovTech Suite  
- Academy & Implementation Hub  
- Auditoria e Certificação BlueShark  

É o inventário que organiza **onde cada lei está**, **como é versionada** e **qual módulo BlueShark ela influencia**.

---

# 2. Estrutura Geral

A base legal é organizada por:

/knowledge-base/
/global/
/country/
/<pais>/


Cada país possui:

- Leis  
- Decretos  
- Resoluções  
- Guias técnicos  
- Checklists oficiais  
- Normas complementares  
- Documentos de inspeção  

---

# 3. Normas Globais (Usadas por todos os países)

/knowledge-base/global/


### 3.1 Segurança Alimentar
| Norma / Guia | Organização | Escopo |
|--------------|-------------|--------|
| Codex Alimentarius – HACCP | FAO/OMS | Base global de segurança alimentar |
| General Principles of Food Hygiene | FAO/OMS | Higiene, manipulação, PCCs |
| Guidelines for Fish and Fishery Products | FAO | Regras globais para pescado |
| One Health & Food Safety Guidelines | WHO | Saúde pública + alimentos |

---

### 3.2 Certificação ISO
| Norma | Escopo |
|-------|---------|
| **ISO 22000** | Segurança Alimentar |
| **ISO 9001** | Gestão da Qualidade |
| **ISO 14001** | Gestão Ambiental |
| **ISO 45001** | Segurança do Trabalho |
| **ISO 21401** | Sustentabilidade no Turismo |
| **ISO 17065** | Certificação de Produtos |

---

### 3.3 Turismo & Hospitalidade
| Documento | Organização | Escopo |
|-----------|-------------|--------|
| UNWTO Global Code of Ethics | UNWTO | Ética e padrões turísticos |
| UNWTO Quality Standards | UNWTO | Qualidade do turismo |
| WHO Tourism & Hygiene Guidelines | WHO | Higiene, prevenção, saúde pública |

---

### 3.4 ESG & Sustentabilidade
| Framework | Escopo |
|----------|---------|
| UN SDGs | Objetivos de Desenvolvimento Sustentável |
| GRI Standards | Relatórios ESG |
| SASB | Indicadores ESG por setor |

---

# 4. Cabo Verde — Mapas Legais

Diretório:
/knowledge-base/country/cabo-verde/


---

## 4.1 — Segurança Alimentar (BestFood)

| Documento | Código | Aplicação |
|----------|--------|-----------|
| **Regime Jurídico da Segurança Alimentar** | DL 04/2009 | Base legal principal |
| Regulamento de Higiene de Géneros Alimentícios | — | Hotéis, restaurantes, cozinhas |
| Procedimentos Oficiais de Inspeção | INSP/ERIS | Auditoria governamental |
| Manual de Boas Práticas para Manipuladores | INSP | Formação básica obrigatória |

---

## 4.2 — Pesca & Cadeia de Frio (ColdChain)

| Documento | Código | Aplicação |
|----------|--------|-----------|
| **Lei da Pesca & Recursos Marinhos** | — | Atividades pesqueiras |
| Regulamento de Transporte de Pescado | — | Cadeia de frio |
| Normas Sanitárias para Pescado | INDP/INSP | Qualidade e frescor |
| Regras de Desembarque e Inspeção | INDP | Portos e lotas |

---

## 4.3 — Turismo (SafeStay / GuestExperience)

| Documento | Órgão | Aplicação |
|----------|--------|-----------|
| **Normas de Qualidade Turística** | ITCV | Hotéis, alojamentos |
| Guias de Higiene e Housekeeping | ITCV | SafeStay |
| Standards de Atendimento & Experiência | ITCV | GuestExperience |
| Regulamento de Alojamento Turístico | Governo | Classificação e requisitos |

---

## 4.4 — Saúde Pública & Vigilância (GovTech)

| Documento | Órgão | Aplicação |
|----------|--------|-----------|
| Programas de Vigilância Sanitária | INSP | Inspeções |
| Protocolos de Investigação de Intoxicação | INSP/ERIS | Incidentes alimentares |
| Procedimentos de Notificação Obrigatória | ERIS | Citizen Safety Reporter |
| Normas de Interdição & Autos | IGAE | Fiscalização econômica |

---

## 4.5 — Qualidade & Certificação (IGQPI)

| Documento | Escopo |
|----------|---------|
| Padrões de Certificação Nacional | Certificação de hotéis, restaurantes |
| Regras de Conformidade de Produtos | Cadeia de produção |
| Normas Complementares de Qualidade | Auditoria |

---

# 5. Brasil  
*(usado para expansão futura e treinar Copilots na CPLP)*

Diretório:
/knowledge-base/country/brazil/

Inclui:

- RDCs da ANVISA  
- Portarias MAPA  
- Legislação de pesca  
- Normas ABNT relacionadas  
- Regras de ESG e certificações  

---

# 6. Portugal

Diretório:
/knowledge-base/country/portugal/

Inclui:

- Regulamento Europeu de Higiene  
- Padrões HACCP obrigatórios  
- Regras de turismo (Turismo de Portugal)  
- Marés & pesca  
- ESG europeu (CSRD, ESRS)  

---

# 7. Angola

Diretório:
/knowledge-base/country/angola/

Inclui:

- Regras sanitárias nacionais  
- Normas de pesca  
- Legislação alimentar  
- Turismo & hotelaria  

---

# 8. Moçambique

Diretório:
/knowledge-base/country/mozambique/

Inclui:

- Regulamento sanitário  
- Segurança alimentar  
- Turismo (MITUR)  
- Pesca & cadeia de frio  

---

# 9. Como os Copilots Usam o Mapa Legal

Tabela de uso por Copilot:

| Copilot | Fontes Legais Usadas |
|---------|------------------------|
| Academy | global + país |
| Implementation | normas técnicas + inspeções |
| ColdChain | pesca + cadeia de frio |
| BestFood | HACCP + ISO22000 + DL04/2009 |
| ESG | ISO14001 + SDGs |
| SafeStay | turismo + higiene |
| GuestExperience | turismo + atendimento |
| Audit Copilot | todas |
| GovTech Copilot | leis do país + normas globais |
| Citizen Safety | leis de notificação + INSP/ERIS |

---

# 10. Governança da Base Legal

A atualização segue:
1. Submissão
2. Validação técnica (2 revisores)
3. Controle jurídico
4. Versionamento
5. Publicação no RAG


A Equipe responsável:

- BeSafe Digital (Cabo Verde + Brasil)  
- Núcleo jurídico  
- Equipe regulatória  
- Equipe IA (RAG Pipeline)  

---

# 11. Conclusão
Este documento é o **inventário jurídico oficial** da BlueShark Cognitive Platform. Ele garante:

- precisão legal  
- rastreabilidade  
- explicabilidade para IA  
- segurança jurídica  
- padronização internacional  

É uma peça crítica para o funcionamento do RAG, dos Copilots e da camada GovTech.
