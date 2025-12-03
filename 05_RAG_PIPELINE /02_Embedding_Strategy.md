# 02 — Embedding Strategy  
## BlueShark Cognitive Platform — BeSafe Digital (2025)

Este documento define a estratégia oficial de embeddings utilizada por todos os Copilots da BlueShark Cognitive Platform.

A estratégia é otimizada para:

- Normas (ISO, HACCP, legislações de Cabo Verde)
- Checklists operacionais
- Conteúdos educacionais da Academy
- Procedimentos de auditoria
- Dados de risco e padrões de conformidade
- Escalabilidade multinacional (CPLP)
- Baixa latência para uso no Mobile & IA

---

# 🎯 1. Objetivos da Estratégia de Embeddings

A estratégia de embeddings deve assegurar:

1. **Alto recall normativo**  
   Normas, leis e checklists precisam ser encontrados mesmo com variações linguísticas.

2. **Contexto interpretável**  
   Cada chunk traz metadados estruturados para priorização inteligente.

3. **Base multi-país**  
   Embeddings separados por país, norma e módulo operacional.

4. **Alta precisão sem sobrecarga**  
   Modelos eficientes para baixa latência no app mobile.

5. **Compatibilidade com RAG híbrido**  
   Suporte a:  
   - busca semântica vetorial  
   - BM25/keyword search  
   - filtros normativos por metadados

6. **Baixa alucinação**  
   Embeddings + metadados devem reduzir alucinação para <2%.

---

# 🧩 2. Modelos de Embedding Recomendados

A estratégia considera três níveis:

## Nível A — Alto desempenho (produção oficial)

| Modelo | Dimensões | Ponto Forte | Uso |
|-------|-----------|-------------|-----|
| **OpenAI text-embedding-3-large** | 3072 | Precisão máxima | Produção GovTech, Auditoria |
| **VoyageAI voyage-large-2** | 2048 | Recuperação normativa | ISO + HACCP + legislação |
| **Jina Embeddings v3** | 1024 | Rápido + OSS | Produção local futura |

Motivo: documentação normativa é densa e exige embeddings grandes.

---

## Nível B — Equilíbrio custo/velocidade (mobile & IA)

| Modelo | Dimensões | Uso |
|--------|-----------|------|
| **text-embedding-3-small** | 1536 | Tutoria, Academy, mobile offline |
| **bge-large-en-v1.5** | 1024 | RAG educacional |
| **Instructor-xl** | 768 | Expansão CPLP |

---

## Nível C — Recursos limitados (edge, mobile futuro)

| Modelo | Dimensões | Uso |
|--------|-----------|------|
| **nomic-embed-text** | 768 | Operações offline |
| **MiniLM-L6** | 384 | Baixa latência extrema |

---

# 🧱 3. Estratégia de Chunking (Regra Oficial BlueShark)

Documentos normativos e checklists precisam seguir regras específicas.

## 3.1 Chunk Size

| Tipo de Documento | Tamanho Ideal |
|------------------|---------------|
| Leis e decretos | 500–800 tokens |
| ISO 22000 / HACCP | 450–650 tokens |
| Checklists técnicos | 200–350 tokens |
| Academy (aulas) | 300–450 tokens |
| Relatórios | 300–600 tokens |
| Casos Cidadão | 100–200 tokens |

---

## 3.2 Regras de Corte

1. Nunca cortar artigos legais no meio.  
2. Nunca misturar países diferentes no mesmo chunk.  
3. Manter componentes HACCP agrupados.  
4. Manter listas de NCs agrupadas.  
5. Priorizar cortes por headers (##, ###).

---

# 🏷 4. Metadados Obrigatórios por Chunk

Todos os chunks da BlueShark Cognitive Platform devem conter:

```json
{
  "source": "Decreto-Lei 04/2009",
  "country": "Cabo Verde",
  "module": "BestFood",
  "norm": "HACCP",
  "iso": "ISO 22000:2018",
  "type": "legislation | checklist | guideline | academy_content",
  "version": "2025.01",
  "validity": "2024-2030",
  "risk_level": "low | medium | high | critical"
}
````
### Motivo:
Permite que o RAG:
- filtre apenas normas válidas;
- aplique precisão normativa por módulo;
- personalize respostas por país;
- construa auditoria automática.

---

# 🔍 5. Estratégia de Indexação

## 5.1 Indexes Separados (Regra Oficial)

Cada país tem seu próprio repositório:
/kb/CV/   (Cabo Verde)
/kb/BR/   (Brasil)
/kb/PT/   (Portugal)
/kb/AO/   (Angola)
/kb/MZ/   (Moçambique)

Cada módulo também:
/kb/CV/bestfood/
/kb/CV/coldchain/
/kb/CV/safestay/
/kb/CV/esg/
/kb/CV/guestexp/
/kb/CV/govtech/

---

## 5.2 Híbrido Vetorial + BM25

O pipeline utiliza Hybrid Retrieval, combinando:
- Similaridade vetorial (cosine)
- Lexicalização (BM25)
- Filtros normativos (metadados)
- Repriorização por risco

Fórmula de fusão recomendada:
score = 0.55 * vector_score +
        0.30 * bm25_score +
        0.15 * normative_score

---

# 📦 6. Atualização de Embeddings (Governança)

---

## 6.1 Frequência Oficial
- Normas ISO → semestral
- Leis do governo → trimestral
- Checklists BeSafe → mensal
- Conteúdo Academy → semanal

---

## 6.2 Versionamento
embedding_version: BS-EMB-2025.01

Atualizações seguem padrão:
BS-EMB-YYYY.MM

---

# 🧪 7. Validação e Evals

Para cada nova atualização:
🔹 Testes de precisão
🔹 Testes de recall normativo
🔹 Testes de bias regulatório
🔹 Testes com auditores humanos
🔹 Auditabilidade GovTech

Meta mínima:
Recall normativo > 92%
Precisão > 85%
Alucinação < 2%

---

🧩 8. Conclusão

A estratégia de embeddings é uma peça crítica do ecossistema BlueShark, garantindo:
- segurança normativa
- precisão regulatória
- respostas explicáveis
- governança multinacional
- escalabilidade para todos os Copilots

Este documento serve como base para:
- 03_Contextual_Retrieval.md
- 04_Prompt_Chains.md
- 05_Memory_Policies.md
