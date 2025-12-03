# 04 — Data Flow Diagrams (DFD)
## BlueShark Cognitive Platform  
### Versão 2025 — BeSafe Digital

Este documento descreve os **Data Flow Diagrams (DFDs)** da BlueShark Cognitive Platform, cobrindo:

- Fluxos de dados entre módulos de IA  
- Interação entre Copilots, RAG e Knowledge Base  
- Comunicação entre usuários, APIs e orquestradores  
- Integração GovTech, Academy, Mobile & IA  
- Processamento de documentos normativos  
- Auditoria e registro de logs  

Os DFDs aqui apresentados abrangem níveis **DFD-0 (contexto)**, **DFD-1 (nível macro)** e **DFD-2 (fluxos detalhados)**.

---

# 🟦 DFD-0 — Context Diagram (Visão Geral)

Representa a plataforma como um único sistema cognitivo.

[Usuários] →
(API Gateway → Cognitive Platform) →
[Respostas / Ações / Relatórios]

[Governos] →
(GovTech Copilot) ↔ (Knowledge Base)

[Empresas / Hotéis / Restaurantes] →
(Operational Copilots) ↔ (RAG Retrieval)

[Academy Usuários] →
(Academy Copilot) → (Learning Engine)

### Entradas gerais
- Perguntas dos usuários  
- Checklists e evidências  
- Normas, leis e documentos  
- Dados operacionais  
- Ocorrências cidadãs  

### Saídas gerais
- Respostas do Copilot  
- Planos de ação  
- Relatórios  
- Insights preditivos  
- Alertas e notificações  

---

# 🟧 DFD-1 — Estrutura Macro do Fluxo de Dados

Mostra como cada componente se relaciona internamente.
           ┌────────────────────┐
           │   API GATEWAY      │
           └─────────┬──────────┘
                     │
                     ▼
           ┌────────────────────┐
           │ COGNITIVE ENGINE   │
           │ - Orchestration    │
           │ - Multi-Copilot    │
           └─────────┬──────────┘
                     │
   ┌─────────────────┼─────────────────┐
   │                 │                 │
   ▼                 ▼                 ▼
┌────────────┐ ┌────────────┐ ┌────────────┐
│ RAG Engine │ │ Reasoning  │ │ Vision/VC  │
└────┬───────┘ └────┬───────┘ └────┬───────┘
     │              │              │
     ▼              ▼              ▼
┌────────────┐ ┌────────────┐ ┌────────────┐
│ Embeddings │ │ Policies   │ | Evidence DB│
└────┬───────┘ └────────────┘ └────────────┘
     │
     ▼
┌──────────────────────────────┐
│ Knowledge Base (Normativas)  │
│ - Leis CV                    │
│ - ISO 22000, 14001, 9001     │
│ - HACCP                      │
│ - Checklists BlueShark       │
└──────────────────────────────┘


---

# 🟩 DFD-2 — Detalhamento dos Fluxos

---

## 1. Fluxo — Consulta do Copilot (Pergunta → Resposta)

1. Usuário envia pergunta
2. API Gateway recebe e autentica
3. Orchestrator identifica o copilot
4. RAG Engine pesquisa no Knowledge Base
5. Reasoning Engine monta resposta contextual
6. Security Layer aplica filtragens
7. Logs gravados no Audit Layer

Resposta enviada ao usuário

### Dados envolvidos
- Query do usuário  
- Documentos recuperados  
- Chain-of-thought controlado  
- Referências normativas  

---

## 2. Fluxo — Classificação de Não Conformidade (NC)

1. App/Portal envia evidência (foto, texto, checklist)
2. Vision Engine extrai informações
3. RAG verifica norma aplicável
4. Reasoning compara situação vs. norma
5. Gerado: Classificação NC + Plano de Ação

### Dados envolvidos
- Imagens (JPEG, PNG)  
- Leis aplicáveis  
- Normas técnicas  
- Pesos de risco  

---

## 3. Fluxo — GovTech (Surtos, Mapas de Risco e Inspeções)

1. Sistema recebe: incidente, denúncia ou inspeção
2. Dados são enviados ao GovTech Copilot
3. RAG cruza: legislação + histórico + empresa
4. Reasoning classifica a gravidade do incidente
5. Gera: alerta, recomendação e ordem de inspeção
6. Dashboard atualiza o mapa de risco

### Dados envolvidos
- Relatórios públicos  
- Coordenadas geográficas  
- Histórico sanitário  
- Base normativa do governo  

---

## 4. Fluxo — Academy (Tutor de IA + Avaliação Automática)

1. Aluno faz pergunta sobre o curso
2. Academy Copilot processa
3. RAG busca conteúdo pedagógico
4. Reasoning cria explicação personalizada
5. IA Tutor envia resposta + exercício adaptado

Se for prova → IA Avaliador analisa e classifica


### Dados envolvidos
- Material pedagógico  
- Conteúdos da trilha  
- Regras de certificação  
- Respostas e acertos do aluno  

---

# 🟪 DFD — Data Lineage e Auditoria

[Input User]
↓
[API Layer]
↓
[Cognitive Engine]
↓
[RAG + Reasoning]
↓
[Outputs]
↓
[Audit Log Store] → [Immutability Layer]

### A rastreabilidade inclui:
- Prompt recebido  
- Documentos consultados  
- Tempo de processamento  
- IA usada  
- Resposta enviada  
- Versão do modelo  
- Hash do conjunto de evidências  

---

# 🟫 DFD — Atualização de Conhecimento (Normativas e Leis)

1. Admin envia PDF / URL / texto de norma
2. Pipeline de ingestão limpa e transforma conteúdo
3. Documento é enviado ao Embedding Generator
4. Vetores são criados e armazenados
5. Tabela de metadados registra:
  - País
  - Instituto
  - Norma
  - Versão
  - Validade
6. KB é atualizada
7. Copilots passam a consultar a nova norma

---

# 🟨 DFD — Orquestração Multi-Copilot

1. Pergunta recebida
2. Intent Classification seleciona:
  — Academy?
  — ColdChain?
  — BestFood?
  — ESG?
  — SafeStay?
  — GovTech?
3. Orchestrator aciona copilots necessários
4. Outputs são mesclados
5. Resultado final enviado ao usuário


---

# ✔️ Conclusão

Este documento formaliza:

- como os dados fluem pela plataforma,  
- como os copilots conversam entre si,  
- como RAG → Reasoning → Security → Logging funcionam,  
- como a base normativa alimenta TODOS os módulos.

Ele servirá de base para:

- desenvolvimento  
- API design  
- segurança  
- auditoria  
- compliance  
- treinamento de novos engenheiros  
- apresentações para governo e parceiros  

---

