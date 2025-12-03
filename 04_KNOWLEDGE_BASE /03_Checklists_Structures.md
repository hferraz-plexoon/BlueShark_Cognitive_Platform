# 03 — Checklists Structures  
## BlueShark Cognitive Platform  
### Estrutura Oficial dos Checklists dos Módulos + Padrões RAG

---

# 1. Objetivo do Documento

Este documento define a **estrutura oficial dos checklists** utilizados em:

- BlueShark Mobile & IA  
- Academy (Simulados Práticos)  
- Implementation Hub  
- Auditorias internas e externas  
- GovTech (Inspeções Nacionais)  
- Copilots (IA explicativa e avaliadora)

Ele garante que todos os checklists:

- Sigam uma **estrutura padronizada**  
- Possam ser processados por IA (RAG + Reasoning + VC)  
- Sejam multi-país e multi-norma  
- Permitam auditoria contínua  
- Alimentem dashboards governamentais  

---

# 2. Estrutura Padrão de Qualquer Checklist

Todos os checklists seguem o mesmo modelo universal:
checklist_item:
id: string
titulo: string
descricao: string
categoria: string
subcategoria: string
criticidade: baixa | media | alta | critica
evidencias_requeridas:
- foto
- video
- documento
- sensor
- assinatura
responsavel: função / role
base_legal:
- <lei>
- <norma>
- <procedimento>
peso: 1–10
orientacao_ia: "mensagem explicativa para copilots"


Cada item deve ser:

- curto  
- auditável  
- vinculado à legislação  
- treinável  
- passível de análise por IA  

---

# 3. Estrutura de Pastas dos Checklists

/checklists/
/coldchain/
/bestfood/
/esg/
/safestay/
/guestexperience/
/audit/
/govtech/

Cada módulo contém:
01_base_checklist.yaml
02_country_overrides.yaml
03_inspection_flows.yaml
04_training_examples.yaml

---

# 4. Módulo ColdChain — Estrutura de Checklist

Diretório:

/checklists/coldchain/

Categorias padrão:

| Categoria | Descrição |
|----------|-----------|
| Embarcação | Higiene, estrutura, EPI |
| Captura | Método, espécie, horário |
| Armazenamento | Temperatura, gelo, embalagens |
| Transporte | Cadeia de frio |
| Documentação | Licenças, origem, lotes |

Exemplo de item:

id: CC-01
titulo: Temperatura da câmara de conservação
criticidade: critica
evidencias_requeridas: [foto, sensor]
base_legal: [Codex HACCP, DL04/2009]
orientacao_ia: "Verifique leitura do sensor e padrões globais FAO."

---

# 5. Módulo BestFood — Estrutura de Checklist

Diretório:

/checklists/bestfood/

Categorias:

- Manipulação  
- Higiene pessoal  
- Cozinha  
- Armazenamento  
- Temperaturas  
- PCCs  
- Controle de pragas  
- Contaminação cruzada  

Exemplo:

id: BF-12
titulo: Higienização das mãos antes da manipulação
criticidade: alta
evidencias_requeridas: [foto]
base_legal: [ISO22000, HACCP]

---

# 6. Módulo ESG — Estrutura de Checklist

Diretório:

/checklists/esg/

Categorias:

- Água  
- Energia  
- Resíduos  
- Inclusão social  
- Políticas de governança  
- Compras sustentáveis  

Exemplo:

id: ESG-07
titulo: Registo do consumo mensal de energia
criticidade: media
base_legal: [ISO14001]

---

# 7. Módulo SafeStay — Estrutura de Checklist

Diretório:

/checklists/safestay/

Categorias:

- Housekeeping  
- Áreas comuns  
- Manutenção  
- EPI  
- Primeiros socorros  
- Riscos ocupacionais  

Exemplo:

id: SS-05
titulo: Inspeção diária da limpeza dos quartos
criticidade: alta
evidencias_requeridas: [foto]
base_legal: [ITCV guidelines]

---

# 8. Módulo GuestExperience — Estrutura de Checklist

Diretório:
/checklists/guestexperience/

Categorias:

- Atendimento  
- Acessibilidade  
- Conforto  
- Infraestrutura  
- Reclamações  

Exemplo:

id: GX-03
titulo: Acessibilidade adequada nas áreas comuns
criticidade: media
base_legal: [WCAG, ITCV]

---

# 9. Módulo Audit (Auditorias Assistidas por IA)

Diretório:
/checklists/audit/

diff
Copiar código

Uso:
- Consultores  
- Auditores BestFood, SafeStay, ColdChain  

Fluxos:

pré-auditoria → auditoria → plano de ação → verificação → certificação

Tem orientações especiais para Copilots:

orientacao_ia: "Se criticidade = alta e repetir >2x, sugerir auto de infração preventiva."

---

# 10. Módulo GovTech — Checklists para Inspeções

Diretório:

/checklists/govtech/

Institutos:

- IGAE  
- INSP  
- ERIS  
- IGQPI  
- ITCV  

Itens incluem:

- Autos  
- Violações legais  
- Riscos sanitários  
- Procedimentos de interdição  
- Coerência com Citizen Safety Reports  

Exemplo:

id: GV-22
titulo: Verificação de condições de higiene da cozinha
criticidade: critica
base_legal: [DL04/2009, INSP Protocolos]

---

# 11. Estruturas de Country Overrides

Cada país possui arquivo:

02_country_overrides.yaml

Exemplo de regra:

override:
pais: cabo-verde
item: BF-12
nova_criticidade: critica
nova_base_legal: [DL04/2009]

---

# 12. Como os Copilots Usam os Checklists

| Copilot | Como usa |
|---------|----------|
| Academy | gera exercícios, simula auditoria |
| Implementation Hub | monta planos de ação |
| ColdChain | identifica NCs |
| BestFood | valida PCCs |
| ESG | verifica RSE |
| SafeStay | valida higiene |
| GuestExperience | analisa atendimento |
| Audit | recomenda interdição/advertência |
| GovTech | aplica autos + fiscalização |
| Citizen Safety | cruza denúncia × checklist legal |

---

# 13. Regras RAG para Checklists

Cada checklist segue:

- chunk de 512 a 2048 tokens  
- tags: `categoria`, `criticidade`, `norma`  
- referência jurídica obrigatória  
- identificação única (ID global)  
- versionamento semântico  

---

# 14. Conclusão

Este documento define o núcleo da padronização operacional:

- checklists claros  
- IA utilizável  
- certificação coerente  
- inspeção auditável  
- aderência a normas globais  

É a fundação para todos os módulos BlueShark e DoCognitive Platform.
