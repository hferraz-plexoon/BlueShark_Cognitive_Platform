# 05 — Update Governance  
## BlueShark Cognitive Platform  
### Governança de Atualização, Versionamento e Auditoria da Base Normativa (Global + País)

---

# 1. Objetivo do Documento

Este documento define **como normas, leis, decretos, checklists e conteúdos regulatórios** são:

- recebidos  
- validados  
- ingeridos  
- versionados  
- atualizados  
- auditados  

Ele garante que toda a BlueShark Cognitive Platform (Academy, Implementation Hub, Mobile & IA, GovTech e Copilots) opere sempre com **a norma correta**, evitando:

- conteúdo desatualizado  
- erros legais  
- inconsistências por país  
- interpretações incorretas de IA  

Este é um documento **criticamente sensível** para garantir segurança jurídica, auditoria e governança pública.

---

# 2. O que faz parte da Base Normativa?

A base normativa inclui:

## 2.1 Normas Internacionais
- ISO 22000  
- ISO 21401  
- ISO 14001  
- ISO 9001  
- ISO 26000  
- WCAG 2.2  
- Codex Alimentarius  
- GRI Standards  
- WHO/FAO Guidelines  

---

## 2.2 Legislação de Cabo Verde
- DL 04/2009 — Segurança Alimentar  
- Regulamentações do ITCV  
- Normas do INSP  
- Guias do IGAE  
- Protocolos de Turismo Sustentável  

---

## 2.3 Documentos Operacionais
- Checklists por módulo  
- Protocolos de inspeção  
- Manuais BeSafe  
- Materiais técnicos  
- Critérios de auditoria  
- Procedimentos de certificação  

---

# 3. Princípios de Governança

A base normativa adota os seguintes princípios:

### **FP-01 — Single Source of Truth (SoT)**
Existe **apenas uma fonte oficial** para cada norma, alojada no repositório:
/04_KNOWLEDGE_BASE/normas/


### **FP-02 — Versionamento Semantic (SemVer)**
Toda norma segue:

MAJOR.MINOR.PATCH

makefile
Copiar código

Exemplo:
ISO22000_CV_v1.2.4

yaml
Copiar código

### **FP-03 — Multi-país com Overrides**
A norma global é base.
Cada país adiciona exceções (“overrides”).

### **FP-04 — Histórico Imutável**
Nenhuma versão é apagada.
Todas são arquivadas.

### **FP-05 — AI-Safe Updates**
A IA só consulta normas aprovadas e validadas.

---

# 4. Estrutura de Diretórios

A estrutura normativa no repositório segue:

/04_KNOWLEDGE_BASE/
/normas/
/global/
ISO22000/
HACCP/
ISO21401/
...
/cabo-verde/
DL04_2009/
ITCV/
INSP/
...
/angola/
/brasil/
/portugal/
...
/metadata/
/embedding/
/change_log/

yaml
Copiar código

---

# 5. Processo de Atualização Normativa (Governança Completa)

## Fase 1 — Submissão
Um novo documento pode ser submetido por:
- BeSafe Digital & Social  
- Institutos governamentais  
- Especialistas técnicos  
- Consultores BlueShark  

Formato aceito:
- PDF  
- Word  
- URL  
- DOC digitalizado  
- Dados oficiais  

Cada submissão gera automaticamente:

submission_id
timestamp
usuario
pais
tipo_documento

yaml
Copiar código

---

## Fase 2 — Validação

A validação deve responder:

1. O documento é oficial?  
2. É uma versão mais recente?  
3. Está completo?  
4. É aplicável ao módulo certo?  
5. Afeta outras normas?  

Papéis envolvidos:

| Papel | Responsabilidade |
|-------|------------------|
| **Normative Curator** | validação técnica |
| **Legal Reviewer** | conformidade jurídica |
| **BeSafe Digital QA** | qualidade + padronização |
| **BlueShark RAG Engineer** | indexação + embeddings |

A atualização só segue após **dupla aprovação**.

---

## Fase 3 — Normalização

O documento é transformado em:

- texto limpo  
- chunks alinhados com tokenização  
- metadados  
- estrutura YAML  

Formato:

id: ISO_22000_1.2.4
lang: pt
country: global
module: BestFood
tokens: 2456
chapter: 7.3
tags: ["controle de temperatura", "PCC"]

---

## Fase 4 — Versionamento

As regras:

### 🔹 PATCH  
Correções pequenas (erro ortográfico, metadados).

### 🔹 MINOR  
Mudanças moderadas (novos capítulos, ajustes).

### 🔹 MAJOR  
Mudanças estruturais, novas versões legais.

---

## Fase 5 — Embeddings

Novos embeddings são gerados para:

- busca semântica  
- contexto do RAG  
- copilots  

Os embeddings antigos **nunca são apagados** — apenas marcados como deprecated.

---

## Fase 6 — Publicação

A publicação torna a norma disponível em:

- RAG pipeline  
- Copilots  
- Academy  
- Checklists  
- GovTech  

Estrutura:

release_notes/
ISO21401_v1.1.0.md

---

# 6. Política de Atualização por País

Cada país possui arquivo:
country_overrides.yaml

Exemplo:

```yaml
base_norm: ISO22000
country: cabo-verde
overrides:
  - cap_4: "Adicionar limite microbiológico para pescados frescos (INSP 2022)"
  - cap_7: "Temperatura máxima de conservação ajustada para 6°C"

````

--- 

# 7. Auditoria & Conformidade Interna

Todo update gera:
- histórico
- autor
- motivação
- impacto nos módulos
- impacto nos copilots
- impacto nas trilhas do Academy

Auditorias ocorrem:
- trimestralmente
- antes de grandes releases
- antes de expansão CPLP

---

# 8. Segurança e Controle de Acesso
Níveis:

Nível	Permissões
Admin	tudo
Curator	editar normas
Legal	aprovar normas
Engineer	embeddings
Viewer	leitura

---

9. Indicadores-chave (KPIs)
- tempo médio para atualizar norma
- % de normas validadas
- % de normas com override por país
- nº de releases por trimestre
- nº de inconsistências encontradas pela IA

---

# 10. Conclusão
Este documento garante:
- conformidade internacional
- rigor legal
- consistência entre países
- IA segura e auditável
- governança pública robusta
- atualizações transparentes e controladas

É a base da integridade regulatória da BlueShark Cognitive Platform.

