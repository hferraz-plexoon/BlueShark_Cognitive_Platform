# 02 — RAG Architecture  
## BlueShark Cognitive Platform

O objetivo deste documento é definir como a arquitetura **RAG (Retrieval-Augmented Generation)** será implementada para todos os Copilots e módulos da BlueShark Platform.

Ele é a referência central para:

- Academy Copilot  
- Implementation Copilot  
- ColdChain, BestFood, ESG, SafeStay, GuestExperience Copilots  
- GovTech Copilot  
- Citizen Safety Copilot  
- Auditors & Inspectors Copilot  
- Global Standards Copilot  

---

# 1. Objetivos do RAG

O RAG existe para garantir que:

1. As respostas sejam **baseadas em leis, normas e padrões oficiais**.  
2. A IA não invente regras nem “alucine”.  
3. A BeSafe Digital consiga atualizar a base normativa continuamente.  
4. Cada país e setor tenha seu **pacote de conhecimento próprio**.  
5. Cada Copilot opere com **explicabilidade e auditoria completa**.  
6. A plataforma seja **multi-país, multi-módulo e multi-usuário**.  

---

# 2. Visão Geral da Arquitetura

O RAG da BlueShark é composto por 5 camadas:

1. **Source Layer** – Fontes de conhecimento.  
2. **Ingestion Layer** – Processamento e normalização.  
3. **Index Layer** – Vetorização e armazenamento.  
4. **Retrieval Layer** – Recuperação contextual.  
5. **Orchestration Layer** – Execução final pelo LLM.  

---

# 3. Diagrama Geral (Mermaid)

\```mermaid
flowchart LR
    A[Fontes de Conhecimento<br>(Leis, Normas, Checklists, Academy, Manuais)] --> B[Ingestão & Normalização]
    B --> C[Chunking + Embeddings + Metadados]
    C --> D[(Vector Database<br/>Document Store)]
    D --> E[Retrieval Layer<br/>(Filtros + Context Packs)]
    E --> F[Orquestrador de Copilots]
    F --> G[LLM / IA Generativa]
    G --> H[Respostas com Citações]
    H --> I[Logs de Auditoria]
    I --> D
\```

*(No GitHub o diagrama aparecerá normalmente — aqui o escape \ evita quebrar o bloco)*

---

# 4. Camada 1 — Fontes de Conhecimento (Source Layer)

## 4.1 Fontes Normativas (Alta Prioridade)
- Leis de Cabo Verde  
- Regulamentos sanitários  
- Normas de fiscalização (IGAE, INSP, ERIS, IGQPI, ITCV)  
- Normas ISO:
  - ISO 22000  
  - ISO 21401  
  - ISO 14001  
  - ISO 45001  
  - ISO 9001  
- Guias OMS, FAO, Codex Alimentarius  

## 4.2 Fontes Operacionais BlueShark
- Checklists BestFood  
- Checklists ColdChain  
- Playbooks SafeStay  
- Roteiros de ESG  
- POPs, PCCs e formulários  
- Fluxos de auditoria BeSafe  

## 4.3 Conteúdo Educacional (Academy)
- Trilhas básicas  
- Trilhas avançadas  
- Trilhas expert  
- Materiais multimídia  
- Quizzes e simuladores  

## 4.4 Fontes Dinâmicas (Mobile & IA)
- Não conformidades  
- Evidências  
- Registros de inspeções  
- Denúncias do Citizen Reporter  
- Dashboards GovTech  

---

# 5. Camada 2 — Ingestão & Normalização

## 5.1 Pipeline
1. Upload do documento  
2. Conversão (PDF/DOCX → MD)  
3. Limpeza e estruturação  
4. Extração de seções  
5. Classificação por tipo  
6. Metadados automáticos  
7. Chunking  

## 5.2 Metadados
Exemplo:

```json
{
  "country": "CV",
  "module": "BestFood",
  "doc_type": "law",
  "source": "government",
  "language": "pt-CV",
  "version": "2025-01"
}

---

## 5.3 Chunking
Tamanho ideal: 500–1500 tokens
Regras:
- Leis → por artigo
- ISO → por cláusula
- Checklists → por seção
- Academy → por aula

---

# 6. Camada 3 — Indexação (Vector + Document Store)
## 6.1 Vector DB

Opções:
- Qdrant
- Weaviate
- Pinecone
- PostgreSQL + PGVector

---

## 6.2 Document Store
Armazena:
- Texto completo
- Versões
- Histórico de atualização

---

## 6.3 Multi-país
Índices separados por país e módulo.

---

# 7. Camada 4 — Recuperação Contextual (Retrieval Layer)
## 7.1 Context Packs (por Copilot)
Exemplos:
- BestFood Pack
- ISO 22000
- Codex
- POPs
- Checklists
- Treinos HACCP
- GovTech Pack
- Leis de fiscalização
- Penalidades
- Modelos de autos
- Checklists do IGAE/INSP/ERIS

---

## 7.2 Retrieve Híbrido
- Filtro por metadados
- Similaridade semântica
- BM25 para precisão legal
- Mistura ponderada

---

## 7.3 Prioridade
- Leis
- Normas ISO
- Normas nacionais
- Checklists
- Academy
- Dados operacionais

---

# 8. Camada 5 — Orquestração com LLM
## 8.1 Funções
- Selecionar Copilot
- Carregar Context Pack
- Rodar Retrieval
- Gerar prompt final
- Executar no LLM
- Criar resposta com citações

## 8.2 Exemplo de Prompt Final

Você é o BestFood Copilot de Cabo Verde.
Objetivo: orientar sobre segurança alimentar com base legal.

Contexto recuperado:
<<<CONTEXT>>>

Pergunta:
<<<USER>>>

Regras:
- Somente usar conteúdo das fontes.
- Sempre citar leis e normas.
- Oferecer ações corretivas.

---

# 9. Segurança, Guardrails, Auditoria
## 9.1 Segurança
- Sanitização
- Prevenção de recomendações ilegais
- Limites de escopo

---

## 9.2 Auditoria
Registra:
- ID usuário
- Fontes usadas
- Score de similaridade
- Carimbo de data/hora

---

# 10. Governança do Conhecimento
Papéis
- BeSafe Content Team
- BeSafe Digital Engineering
- Institutos oficiais

Ciclo
- Submissão
- Validação
- Ingestão
- Publicação

---

#11. Relação com Outras Pastas
/04_KNOWLEDGE_BASE/
/05_RAG_PIPELINE/
/09_SECURITY_GOVERNANCE/

---

# 12. Conclusão
A arquitetura RAG da BlueShark garante:
- Confiabilidade
- Base legal
- Escalabilidade
- Multi-país
- Governança total
- Zero alucinação
- Explicabilidade
- Auditoria completa

É o núcleo da inteligência normativa dos Copilots.
