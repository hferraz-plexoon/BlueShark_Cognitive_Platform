# 05_AGENT_SPEC_TEMPLATE.md  
## BlueShark Copilots – Template de Especificação de Agente

> **Objetivo deste documento**  
> Este template padroniza como descrevemos cada agente cognitivo (Copilot) do ecossistema BlueShark / BeSafe Digital, garantindo:
> - alinhamento entre negócio, tecnologia e governo  
> - reuso de padrões (RAG + Reasoning)  
> - estimativa consistente de esforço (ABCDEF)  
> - facilidade de onboarding para novos devs e consultores  

> **Como usar**  
> 1. Copie este arquivo.  
> 2. Renomeie para:  
>    `AGENT_<NOME>_<DOMÍNIO>.md` (ex: `AGENT_GOVTECH_ITCV.md`, `AGENT_ACADEMY_TUTOR.md`)  
> 3. Preencha sempre em português claro, pensando em:  
>    - Helder / Zuleika / Ricardo (negócio)  
>    - Desenvolvedores (implementação)  
>    - Governo / Clientes (pitch executivo)  

---

## 1. Identificação do Agente

- **Nome do Agente (curto):**  
  Ex.: `GovTech ITCV Copilot`

- **Nome descritivo (marketing / pitch):**  
  Ex.: `Copilot de Qualidade Turística & Certificação Contínua`

- **Domínio principal:**  
  - [ ] GovTech  
  - [ ] Academy  
  - [ ] Auditoria / Certificação  
  - [ ] Cadeia de Frio / Pesca  
  - [ ] Segurança Alimentar (BestFood)  
  - [ ] ESG + Sustentabilidade  
  - [ ] SafeStay  
  - [ ] Customer Experience  
  - [ ] Outros: __________________

- **Tipo de agente (função principal):**  
  - [ ] Assistente de Decisão (governo / diretoria)  
  - [ ] Tutor (formação / Academy)  
  - [ ] Auditor Assistido (checklist / NC / plano de ação)  
  - [ ] Orquestrador de Fluxo (workflow / automação)  
  - [ ] Analisador de Evidências (VC / documentos / fotos)  
  - [ ] Gerador de Relatórios / Sumários Executivos  
  - [ ] Outro: __________________

- **Usuário primário:**  
  Ex.: Diretor do ITCV, inspetor, consultor BeSafe, gestor de hotel, etc.

- **Usuários secundários:**  
  Ex.: equipe técnica, analistas, coordenadores regionais.

---

## 2. Problema que o Agente Resolve

### 2.1. Contexto de Dor

Explique em poucas linhas:

- Qual é o problema real hoje?  
- Quem sofre com isso (pessoas / instituições)?  
- Quais são as consequências (operacionais, financeiras, políticas, reputacionais)?

> Exemplo:  
> “Hoje o ITCV não consegue ver, em tempo real, o nível de risco turístico por ilha, nem cruzar dados de intoxicação, certificação e reclamações. As decisões são reativas, manuais e fragmentadas.”

### 2.2. Tabela de Dores x Impacto x Solução (RAG + Reasoning)

| # | Dor (situação atual) | Impacto (risco / custo) | Como o agente resolve (visão executiva) |
|---|----------------------|--------------------------|-----------------------------------------|
| 1 |                      |                          |                                         |
| 2 |                      |                          |                                         |
| 3 |                      |                          |                                         |

---

## 3. O que o Agente Faz (Visão Funcional)

### 3.1. Principais Capacidades

Liste em bullets:

- Responde perguntas como: “__________”
- Gera relatórios como: “__________”
- Ajuda o usuário a: “__________”
- Faz análise automática de: “__________”
- Sugere planos de ação para: “__________”

### 3.2. Exemplos de Perguntas que o Agente Responde

- “Mostra os concelhos com maior risco de intoxicação nos últimos 30 dias.”
- “Gera um relatório executivo para o Ministro da Economia sobre o estado da certificação hoteleira em Santiago.”
- “Quais restaurantes certificados BestFood tiveram incidentes recorrentes nos últimos 6 meses?”

---

## 4. Onde entra RAG e onde entra Reasoning

### 4.1. RAG – Fontes de Conhecimento que o Agente Consulta

Marque e detalhe:

- [ ] Leis e decretos de Cabo Verde  
- [ ] Normas ISO (22000, 21401, 14001, 45001, 42001)  
- [ ] Manuais e POPs BeSafe  
- [ ] Checklists e registros do BlueShark Mobile & IA  
- [ ] Dados do Academy (formação / certificação)  
- [ ] Incident reports (Citizen Reporter / GovTech)  
- [ ] Outros: __________________________________

Descreva em 3–5 linhas como o agente usa RAG:

> Ex.: “O agente busca leis, normas, registros de inspeção e estatísticas de certificação para contextualizar cada resposta, sempre citando a base normativa e o risco regulatório associado.”

### 4.2. Reasoning – O que o Agente “Raciocina”

Quais tarefas exigem raciocínio em múltiplas etapas?

- Explicar **por que** uma situação é crítica  
- Priorizar **quais casos investigar primeiro**  
- Gerar **plano de ação** baseado em risco, custo e impacto  
- Construir **cenários** (se melhorar X, o que acontece com Y?)  
- Traduzir linguagem técnica para linguagem executiva (Ministro / Diretor)

Descreva 1–2 fluxos de reasoning:

> Exemplo de fluxo:  
> 1. Recebe lista de estabelecimentos com muitas NCs.  
> 2. Cruza com incidentes de intoxicação.  
> 3. Avalia criticidade (turistas / população / mídia).  
> 4. Sugere rota de inspeção prioritária para inspetores.  
> 5. Gera nota executiva para diretoria.

---

## 5. Exemplo Prático – Antes x Depois

### 5.1. Antes do Agente

Descreva um cenário realista (curto):

- Como o processo é feito hoje  
- Quanto tempo leva  
- Quantas pessoas envolvidas  
- Principais riscos

### 5.2. Depois do Agente

Descreva o mesmo cenário usando o agente:

- Quem aciona o agente?  
- O que ele pede?  
- O que o agente devolve (passo a passo)?  
- Qual o ganho (tempo, clareza, segurança, narrativa política)?

---

## 6. Métricas de Sucesso (KPIs)

Liste métricas que permitam provar que o agente funciona.

### 6.1. Métricas Operacionais

Exemplos:

- Tempo para gerar um relatório cai de X dias para Y minutos  
- Nº de decisões baseadas em dados por mês  
- Nº de planos de ação gerados automaticamente e implementados  

### 6.2. Métricas de Resultado

Exemplos:

- Redução de intoxicações notificadas (% ao ano)  
- Aumento de estabelecimentos certificados  
- Melhora no NPS turístico  
- Redução de tempo entre denúncia e inspeção

---

## 7. Riscos que o Agente Mitiga

Liste os principais riscos que este agente ajuda a reduzir:

- [ ] Risco sanitário  
- [ ] Risco regulatório (multas, fechamentos)  
- [ ] Risco de imagem (mídia, redes sociais)  
- [ ] Risco político (crise de governo)  
- [ ] Risco econômico (perda de turistas / receitas)  
- [ ] Outros: _________________________

Descreva em 3–5 linhas:

> “Este agente reduz o risco de ________ porque ______________________.”

---

## 8. Limites do Agente (O que ele NÃO faz)

Muito importante para gestão de expectativa e segurança:

- Não substitui decisões humanas de fechamento/interdição.  
- Não emite parecer legal definitivo.  
- Não toma decisões financeiras automáticas.  
- Não altera dados de sistemas transacionais.  
- Não atua sem supervisão em casos de risco extremo.

Adapte para cada agente.

---

## 9. Requisitos Técnicos Específicos

### 9.1. Integrações Necessárias

- APIs que precisa consumir (ex.: Mobile & IA, Academy, GovTech Dashboards etc.)  
- Conectores de dados (Postgres, Elasticsearch, S3, etc.)  

### 9.2. Latência / Disponibilidade

- Tempo máximo aceitável de resposta (ex.: 5s)  
- Disponibilidade alvo (ex.: 99,5% em horário comercial)  

### 9.3. Segurança & Privacidade

- Dados sensíveis que o agente acessa  
- Nível de anonimização necessário  
- Logs e trilhas de auditoria obrigatórias  

---

## 10. Esforço Estimado (Mini ABCDE do Agente)

> **Obs.: aqui é um mini-ABCDE só para este agente, não para o programa inteiro.**

- **A – Custo estimado sem IA acelerando o dev deste agente:**  
  Ex.: R$ 180.000

- **B – Custo estimado com IA (GitHub Copilot + templates + RAG pronto):**  
  Ex.: R$ 60.000

- **C – O que já está pronto (documentação, protótipos, prompts, POCs):**  
  Ex.: R$ 15.000 equivalentes

- **D – O que falta (B – C):**  
  Ex.: R$ 45.000 (base para negociar com dev responsável)

- **E – Conteúdos / Knowledge Packs dedicados a este agente:**  
  Ex.: R$ 20.000 (organizar leis, normas, guias, exemplos, FAQs)

Preencher com números indicativos (podem ser revisados depois).

---

## 11. Roadmap Específico do Agente

Divida em 3 fases rápidas:

### Fase 1 — MVP (4–8 semanas)
- Escopo mínimo  
- Usuários-chave  
- 3–5 perguntas que precisa responder bem  

### Fase 2 — Versão 1.0 (3–6 meses)
- Conexão com mais sistemas  
- Dashboards específicos  
- Refinos de prompting + guardrails  

### Fase 3 — Versão 2.0 (6–12 meses)
- Preditivo  
- Integração profunda com Mobile & IA  
- Expansão CPLP  

---

## 12. Checklist de Pronto para Produção

Marque “OK” quando estiver validado:

- [ ] Persona do usuário clara  
- [ ] Dores bem descritas  
- [ ] Fontes de RAG mapeadas  
- [ ] Limites do agente definidos  
- [ ] KPIs claros  
- [ ] Avaliação de risco feita  
- [ ] Aprovação de Helder / BeSafe Digital  
- [ ] Aderência ética (sem risco de uso político indevido)  

---

_Fim do template. A partir deste modelo você poderá documentar: Academy Tutor, Implementation Copilot, Government Copilots (ITCV, IGAE, INSP, IGQPI, ERIS), Citizen Reporter Copilot, Auditoria Copilot etc. de forma totalmente padronizada._
