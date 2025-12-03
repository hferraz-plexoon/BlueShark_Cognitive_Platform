# 03 — Human-In-The-Loop (HITL) Framework  
BlueShark Cognitive Platform – 2025  
Versão 1.0

---

# 1. Objetivo do HITL

O Framework HITL define **quando, como e por quem** um humano deve intervir nas operações de IA da plataforma BlueShark, garantindo:

✔ segurança  
✔ precisão  
✔ responsabilidade legal  
✔ transparência  
✔ confiança governamental  
✔ proteção ao cidadão  
✔ alinhamento com normas (ISO 42001, ISO 31000, GDPR-like CV, FAO/OMS)

---

# 2. Princípios do HITL

1. **IA auxilia, mas não decide sozinha** em qualquer evento crítico.  
2. **Toda decisão com impacto legal, sanitário ou de fiscalização exige validação humana.**  
3. A IA deve sempre **explicar o raciocínio e apontar a evidência utilizada**.  
4. **Nenhuma penalidade** pode ser emitida sem humano.  
5. Cidadãos e empresas têm direito de contestar recomendações.  
6. Logs, trilha de auditoria e justificativas são **obrigatórios**.  
7. HITL é multilayer: consultores, auditores, supervisores do governo e BeSafe.  

---

# 3. Onde o HITL é Obrigatório

A seguir a lista oficial de fluxos que **exigem intervenção humana**.

---

## 3.1. Academy (Treinamentos)

| Evento | HITL Obrigatório? | Responsável |
|-------|--------------------|-------------|
| Correção de prova objetiva | ❌ Opcional | IA com auditoria posterior |
| Correção de prova discursiva | ✔ Sim | Instrutor |
| Certificação final do aluno | ✔ Sim | Instrutor + BeSafe |
| Reprovação em trilha obrigatória | ✔ Sim | Instrutor |
| Revisão de conteúdo pedagógico sugerido pela IA | ✔ Sim | Comitê pedagógico |

---

## 3.2. Implementation Hub

| Evento | HITL | Responsável |
|--------|------|-------------|
| Aprovação de evidência fotográfica | ✔ | Consultor |
| Aprovação de evidência de vídeo | ✔ | Consultor/Auditor |
| Reprovação de item crítico do checklist | ✔ | Consultor |
| Aprovação de Plano de Ação | ✔ | Auditor |
| Alteração de prazo | ❌ | IA + aprovação automática |
| Fechamento de auditoria | ✔ | Auditor + Supervisor |

---

## 3.3. Mobile & IA (Operações)

| Evento | HITL | Responsável |
|--------|------|-------------|
| Detecção de risco sanitário crítico | ✔ | INSP / IGAE |
| Emissão de alerta de intoxicação alimentar | ✔ | INSP |
| Notificação de risco ESG grave | ✔ | IGQPI |
| Desativação de equipamento crítico (IoT) | ✔ | Técnico autorizado |
| Atualização de parâmetros normativos | ✔ | Comitê técnico +

---

## 3.4. GovTech (Supervisão Nacional)

| Evento | HITL | Responsável |
|--------|------|-------------|
| Geração de ranking de risco nacional | ✔ | Supervisor do ITCV |
| Notificação pública de estabelecimentos | ✔ | ITCV + IGAE |
| Publicação de mapa de risco | ✔ | ITCV |
| Reclassificação de empresa | ✔ | Supervisor governamental |

---

## 3.5. Citizen Safety Reporter

| Evento | HITL | Responsável |
|--------|------|-------------|
| Denúncia com potencial crime | ✔ | IGAE |
| Denúncia de intoxicação | ✔ | INSP |
| Conteúdo impróprio / falso positivo | ✔ | Moderador |
| Requisição de prova adicional | ❌ | IA |
| Encerramento de denúncia | ✔ | Agente do governo |

---

# 4. Matriz de Risco para Acionamento Automático do HITL

A plataforma aciona automaticamente HITL conforme o nível de risco:

```
Nível 1 — Informativo → IA pode atuar sozinha, sem HITL.
Nível 2 — Moderado → IA recomenda; humano confirma.
Nível 3 — Alto → IA alerta; humano decide.
Nível 4 — Crítico → IA bloqueia temporariamente e obriga HITL imediato.
```

### Tabela oficial:

| Nível | Descrição | Acionamento |
|------|-----------|-------------|
| 1 | Sem impacto sanitário ou legal | Automatizado |
| 2 | Impacto leve em operação | Homologação leve |
| 3 | Risco sanitário operacional | Auditor/Consultor |
| 4 | Risco grave / saúde pública | Autoridade competente |

---

# 5. Fluxo Geral HITL na Plataforma

```
Evento detectado (IA)  
       ↓  
Classificação de risco (1-4)  
       ↓  
Se Nível 1 → IA executa  
Se Nível 2 → IA executa + humano notificado  
Se Nível 3 → IA bloqueia e aguarda humano  
Se Nível 4 → IA bloqueia + escalanento governamental automático  
       ↓  
Humano valida / corrige / revisa  
       ↓  
Log e auditoria  
       ↓  
Sistema aprende e ajusta futuros prompts  
```

---

# 6. Regras para Revisão Humana

### 6.1. O que um humano pode fazer:
✔ editar  
✔ confirmar  
✔ reprovar  
✔ justificar  
✔ solicitar nova análise IA  
✔ pedir documentação adicional  
✔ reclassificar o risco  

### 6.2. O que um humano **não** pode fazer:
❌ apagar logs  
❌ remover histórico  
❌ alterar classificação normativa  
❌ ignorar recomendações críticas sem justificativa  

---

# 7. Regras de Auditoria e Log

Todos os eventos HITL geram logs:

- timestamp  
- usuário humano  
- tipo de evento  
- modelo de IA usado  
- versão do prompt  
- fonte RAG usada  
- classificação de risco  
- decisão tomada  
- justificativa anotada  
- prazo de resolução  

Logs são imutáveis (WORM / Locked S3).

---

# 8. HITL para Atualização da Base Normativa

Nenhum documento pode ser usado pela IA sem:

1. upload  
2. pré-análise automática  
3. aprovação humana técnica  
4. aprovação governamental  
5. versionamento  
6. indexação RAG  

---

# 9. HITL para Copilots

Cada copilot tem configuração própria:

- Academy: HITL moderado  
- Implementation: HITL alto  
- ColdChain: HITL alto  
- BestFood: HITL alto  
- ESG+Social: HITL alto  
- SafeStay: HITL moderado  
- GuestExperience: HITL baixo  
- GovTech Supervisor: HITL crítico  
- Citizen Safety: HITL crítico  

---

# 10. Conclusão

O modelo HITL garante que a IA:

- não substitui decisões críticas  
- segue padrões de segurança  
- fortalece a confiança das autoridades  
- sustenta o programa nacional de certificação  
- protege turistas, estabelecimentos e cidadãos  
- reduz riscos legais e reputacionais  

Este documento é obrigatório para certificação, auditorias e conformidade internacional.

