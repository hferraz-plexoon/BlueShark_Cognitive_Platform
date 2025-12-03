# 05 — Memory Policies  
## BlueShark Cognitive Platform — BeSafe Digital (2025)

Este documento define as políticas oficiais de **Memória**, **Context Persistence** e **Context Lifecycle** para todos os Agentes Cognitivos BlueShark.

A memória é um dos pilares mais críticos da plataforma porque influencia:

- precisão das respostas  
- consistência pedagógica (Academy)  
- rastreabilidade regulatória (GovTech)  
- auditoria e conformidade  
- experiência personalizada para usuários  
- evolução dos Copilots por função  

---

# 🎯 1. Objetivos da Política de Memória

As Memory Policies devem garantir:

1. **Segurança normativa** — legislação nunca pode ser sobrescrita ou reinterpretada pelo agente.
2. **Isolamento multi-tenant** — empresas, consultores, governos e países NÃO compartilham memória.
3. **Explicabilidade** — toda memória deve ser auditável por BeSafe Digital.
4. **Privacidade total** — nenhuma memória pessoal persistente para usuários finais.
5. **Eficiência** — reduzir tokenização e melhorar velocidade de resposta.
6. **Controle Governamental** — o GovTech sempre tem logs imutáveis para auditoria.

---

# 🧩 2. Tipos de Memória

A plataforma utiliza **4 camadas**:

| Camada | Descrição | Persiste? | Onde é usada |
|--------|-----------|-----------|--------------|
| **Ephemeral Memory** | Memória da conversa atual | NÃO | Chat, Copilot, Academy Tutor |
| **Session Memory** | Persistência curta (até 24h) | SIM | Projetos, auditorias, treinamentos |
| **Organizational Memory** | Dados do cliente/empresa | SIM | Mobile & IA, dashboards |
| **Normative Memory (Read-Only)** | Base de normas e leis | SIM (imutável) | GovTech, Auditoria, Copilots |

---

# 🔐 3. Regras de Privacidade e Isolamento (Obrigatório)

## 3.1. Proibido memorizar:
- preferências pessoais de usuários finais  
- informações sensíveis do turismo  
- dados pessoais sem consentimento  
- informações médicas  
- conclusões jurídicas não oficiais  

## 3.2. Permitido memorizar:
- progresso de treinamento do Academy  
- auditorias em andamento  
- status de implantação  
- equipe por organização  
- histórico de não conformidades  

## 3.3. Somente o usuário pode ativar:
- memórias de performance  
- personalização pedagógica  

---

# 🧠 4. Estrutura da Função de Memória (Memory Engine)
[1] Input Interceptor
[2] Intent Classifier
[3] Memory Writer
[4] Memory Retriever
[5] Safety Filter (HITL opcional)


### Explicação:

- **Interceptor** captura o input e verifica se é memorizável.  
- **Intent Classifier** define se é “memória válida”.  
- **Writer** salva conforme política (tenant, sessão, módulo).  
- **Retriever** retorna ao Copilot de forma contextualizada.  
- **Safety Filter** garante que nada sensível seja preservado.

---

# 🗄️ 5. Estrutura do Armazenamento

| Tipo de memória | Armazenamento |
|-----------------|---------------|
| Ephemeral | RAM + contexto imediato |
| Session | Redis TTL 24–72h |
| Organizational | Postgres (tenant isolado) |
| Normative | ElasticSearch + ChromaDB (somente leitura) |

---

# 📌 6. Regras Específicas por Módulo

---

## 6.1 Academy (Treinamentos)

Armazenar:

- progresso
- quizzes
- notas
- recomendações do Tutor
- gaps de aprendizado

NÃO armazenar:

- preferências pessoais
- conclusões de IA sobre comportamento

---

## 6.2 Implementation Hub

Armazenar:

- etapas concluídas
- evidências
- planos de ação
- histórico de auditoria

NÃO armazenar:

- conclusões subjetivas sobre consultores

---

## 6.3 Mobile & IA

Armazenar:

- checklists
- auditorias internas
- cadeia de frio
- registros ESG
- higienização

NÃO armazenar:

- inferências subjetivas ou predições não validadas

---

## 6.4 GovTech Suite

Armazenar:

- inspeções
- autos de infração
- histórico nacional
- incidentes
- notas técnicas do Copilot

NÃO armazenar:

- julgamentos pessoais sobre empresas
- inferências não previstas na legislação

---

# 🧱 7. Política de Retenção

| Memória | Retenção |
|---------|----------|
| Ephemeral | 1 sessão |
| Session | 24–72h |
| Organizational | 5 anos |
| Normative | permanente |

---

# 📦 8. Política de Exclusão (Forget Mechanism)

O usuário pode solicitar exclusão de:

- progresso do Academy (reset)  
- sessões anteriores  
- históricos de conversas  

Não pode excluir:

- auditorias
- incidentes
- autos de infração
- registros GovTech

---

# 🧪 9. Testes e Garantias

Cada Copilot deve ser testado com critérios:

- **Leakage Test:** memória indevida entre empresas  
- **Privacy Test:** dados sensíveis não armazenados  
- **Normative Integrity Test:** normas nunca alteradas  
- **Governance Test:** trilha auditável 100% ativa  

---

# 👑 10. Conclusão

Esta política:

- reduz riscos legais,
- garante conformidade com GovTech,
- mantém o Academy confiável,
- protege empresas e turistas,
- e assegura precisão técnica e jurídica.

É um documento obrigatório para todos os desenvolvedores BeSafe Digital.


O Memory Engine opera com 5 etapas:

