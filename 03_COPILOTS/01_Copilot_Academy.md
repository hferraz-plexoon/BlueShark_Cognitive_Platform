# 01 — Copilot Academy  
## BlueShark Cognitive Platform  
### Tutor Inteligente, IA Pedagógica e Assistente de Aprendizagem Adaptativa

---

# 1. Visão Geral

O **Copilot Academy** é o agente cognitivo responsável por:

- orientar alunos durante as trilhas do BlueShark Academy  
- responder dúvidas técnicas em tempo real  
- criar exercícios personalizados  
- explicar normas, processos e POPs  
- fornecer feedback imediato  
- acompanhar desempenho e sugerir reforço  
- adaptar trilhas ao ritmo do aluno  

Ele funciona como um **tutor pessoal 24/7**, integrado ao Academy e ao Implementation Hub.

---

# 2. Objetivos do Copilot

| Objetivo | Descrição |
|----------|-----------|
| **Apoiar a aprendizagem** | Explicar conteúdos, gerar exemplos, reforçar boas práticas. |
| **Personalizar o estudo** | Ajustar trilhas ao nível do aluno. |
| **Aumentar retenção** | Microlearning adaptativo baseado em desempenho. |
| **Corrigir exercícios** | IA avaliadora com critérios técnicos. |
| **Garantir conformidade** | Respostas baseadas apenas em materiais oficiais e normas. |
| **Reduzir carga dos instrutores** | A IA assume dúvidas frequentes e triagem inicial. |

---

# 3. Perfis Atendidos

- Jovens em formação  
- Pescadores  
- Manipuladores de alimentos  
- Housekeepers  
- Técnicos de manutenção  
- Supervisores  
- Auditores BeSafe  
- Equipes de hotelaria e turismo  

Cada perfil recebe respostas e linguagem adaptada.

---

# 4. Capacidades Principais

## 4.1 IA Tutor (Explicação + Exemplos)
- Explica conceitos técnicos com simplicidade  
- Oferece versões resumidas, completas e avançadas  
- Explica normas (ISO 22000, HACCP, ESG etc.)  
- Usa exemplos reais do dia a dia:  
  - cozinha  
  - embarcações  
  - housekeeping  
  - receção  
  - manutenção  
  - ESG  

## 4.2 IA Avaliadora (Correção Automática)
Avalia automaticamente:

- questões de múltipla escolha  
- respostas discursivas  
- vídeos práticos enviados pelo aluno  
- checklist de manipulação  
- desempenho por trilha  

Usa rubricas pré-configuradas.

## 4.3 IA Geradora de Exercícios
Gera:

- quizzes  
- estudos de caso  
- práticas simuladas  
- cenários de risco  
- lições personalizadas  

Baseado no progresso individual.

## 4.4 IA Explicadora de Normas e POPs (RAG Normativo)
Responde perguntas como:

- “Qual é a temperatura ideal de conservação de peixe?”  
- “Como higienizar superfícies corretamente?”  
- “O que diz a lei de Cabo Verde sobre água potável?”  
- “Qual ISO fala sobre riscos alimentares?”  

Sempre com **fonte normativa citada**.

---

# 5. Escopo do Copilot

## 5.1 Entradas Aceitas
- Perguntas de texto  
- Perguntas por áudio  
- Vídeos de práticas de trabalho  
- Fotos de procedimentos  
- Dados de desempenho  

## 5.2 Saídas Geradas
- Explicações  
- Recomendações  
- Exercícios  
- Avaliações com nota  
- Listas de reforço  
- Progresso analisado  

---

# 6. Arquitetura do Copilot (Resumo)




Copilot Academy
├─ Input Processor (texto/voz/imagem)
├─ RAG Educacional
│ ├─ Conteúdo oficial BeSafe
│ ├─ Normas de Cabo Verde
│ ├─ POPs
│ └─ Materiais de aula
├─ Reasoning Layer
├─ Safety Layer (Edu + IA Safety)
├─ Personalization Engine
├─ Quiz Generator
├─ Evaluation Engine
└─ Learning Dashboard
---

# 7. Data Sources (Base de Conhecimento)

O Copilot só utiliza fontes oficiais:

- conteúdo de cada trilha  
- PDFs, slides e vídeos da Academy  
- legislação de Cabo Verde  
- normas ISO citadas no contexto  
- POPs e procedimentos BeSafe  
- guias HACCP  
- regras de segurança e biossegurança  
- checklists de auditoria  
- manuais técnicos (ESG, SafeStay, CX)  

---

# 8. Limitações Deliberadas (Safety Rules)

O Copilot **não pode**:

- fornecer diagnóstico médico  
- recomendar medicamentos  
- sugerir irregularidades  
- dar instruções ilegais  
- alterar normas  
- misturar legislações de países diferentes  
- emitir certificações sozinho  
- substituir instrutores em avaliações práticas críticas  

---

# 9. Exemplos de Comportamento

## 9.1 Boa Resposta
Aluno: “Como descongelar peixe corretamente?”

Copilot:

> Para descongelar peixe com segurança, utilize **frigorífico entre 0°C e 4°C**.  
> Evite água quente e nunca deixe o alimento à temperatura ambiente.  
> *Baseado na ISO 22000, Codex Alimentarius e legislação sanitária de Cabo Verde.*

## 9.2 Resposta Explicando e Ensinando
> Quer uma explicação resumida, detalhada ou em vídeo?

## 9.3 Sugestão Automática
> Percebi que teve dificuldade no módulo de Higiene das Mãos.  
> Recomendo refazer o vídeo com essa técnica...

---

# 10. Logging e Auditoria

O Copilot registra:

- perguntas do aluno  
- respostas fornecidas  
- normas consultadas  
- decisões pedagógicas tomadas  
- notas atribuídas  
- desvios detectados  

Tudo armazenado em logs imutáveis.

---

# 11. Integração com Academy

Funcionalidades disponíveis:

- “Explique novamente”  
- “Gerar quiz extra”  
- “Corrigir exercício”  
- “Criar resumo da aula”  
- “Criar simulação prática”  
- “Gerar checklist de estudo”  

---

# 12. Integração com Implementation Hub

Quando o aluno vira consultor:

- o Copilot cria playbooks  
- ajuda a interpretar normas  
- gera ações de implantação  
- ajuda a validar evidências  

---

# 13. Roadmap do Copilot Academy

Fase | Funcionalidade | Status
-----|----------------|--------
Fase 1 | IA Tutor + FAQ | MVP
Fase 2 | Geração de quizzes | MVP
Fase 3 | IA Avaliadora (texto + imagem) | Em desenvolvimento
Fase 4 | Análise de vídeo | Futuro
Fase 5 | Perfis de aprendizagem personalizados | Futuro
Fase 6 | Trilha automática por risco | Futuro

---

# 14. Conclusão

O **Copilot Academy** é o agente cognitivo que garante:

- aprendizado rápido  
- consistência pedagógica  
- padronização nacional  
- inclusão social  
- desenvolvimento profissional  
- aumento de empregabilidade  
- qualidade operacional do BlueShark Program  

É um dos pilares centrais da BeSafe Digital e da transformação educativa do país.

