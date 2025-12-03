# 10 — Copilot CitizenSafety  
## BlueShark Cognitive Platform  
### IA para Denúncias, Triagem de Incidentes, Proteção ao Turista e Vigilância Comunitária

---

# 1. Visão Geral

O **Copilot CitizenSafety** é o agente cognitivo responsável por:

- receber denúncias de cidadãos e turistas  
- analisar automaticamente a gravidade  
- classificar risco sanitário, turístico e social  
- identificar padrões de surtos  
- orientar o cidadão em tempo real  
- encaminhar cada caso ao instituto correto (ITCV, INSP, IGAE, ERIS)  
- alimentar o painel do GovTech Suite  

É a “ponte inteligente” entre a **população / turistas** e os **órgãos governamentais**.

---

# 2. Problemas que Resolve

| Problema atual | Solução CitizenSafety |
|----------------|-----------------------|
| Denúncias chegam incompletas | IA orienta o cidadão a preencher corretamente |
| Triagem manual lenta | Classificação automática por risco |
| Surtos só são percebidos tarde | IA detecta padrões e alerta antes |
| População não sabe a quem recorrer | Copilot orienta e encaminha |
| Turista não sabe como reportar | Interface simplificada + QR Codes nos estabelecimentos |
| Denúncias falsas ou vazias | IA valida e filtra ruído |

---

# 3. Casos de Uso Principais

### 3.1 Denúncia Sanitária
Exemplos:
- intoxicação alimentar  
- comida estragada  
- falta de higiene  
- insetos/pragas  
- funcionário sem EPI  

A IA:
- avalia sintomas  
- analisa fotos  
- cruza com padrões sanitários  
- determina gravidade  

---

### 3.2 Denúncia de Experiência do Turista
Exemplos:
- má conduta de funcionários  
- problemas de segurança  
- instalações inapropriadas  
- agressões, abusos ou discriminação  

A IA:
- classifica criticidade  
- aciona setor correto  
- protege identidade do turista  

---

### 3.3 Denúncia Econômica
Exemplo:
- cobrança abusiva  
- falsificação de produtos  
- irregularidade comercial  

Encaminhamento automático para:
- **IGAE**  

---

### 3.4 Denúncia de Cadeia de Frio
Exemplo:
- peixe estragado  
- produto fora da temperatura  

Encaminhamento automático para:
- **ERIS**  
- **INSP**  

---

# 4. Funcionalidades do Copilot CitizenSafety

---

## 4.1 Triagem Automática (Classificador Multimodal)

O copiloto classifica denúncias considerando:

- texto  
- fotos  
- vídeos  
- localização  
- sintomas  
- horário  
- histórico de casos na região  

Ele entrega:
Classificação: Risco Sanitário Crítico
Encaminhar para: INSP + ERIS
Motivo: padrões compatíveis com intoxicação alimentar aguda.

---

## 4.2 Orientação ao Cidadão/Turista

O Copilot orienta:

- como proceder em caso de intoxicação  
- onde buscar atendimento  
- como registrar evidências  
- como acompanhar a denúncia  
- seus direitos como consumidor/turista  

---

## 4.3 Priorização de Casos

Critérios usados pelo modelo:

- risco à saúde  
- número de pessoas afetadas  
- reincidência no local  
- impacto ao turismo  
- gravidade legal  
- urgência sanitária  

---

## 4.4 Encaminhamento Automático

| Tipo de denúncia | Instituto acionado |
|------------------|-------------------|
| intoxicação alimentar | INSP + ERIS |
| má higiene | ERIS + IGAE |
| abuso/violência | Polícia + ITCV |
| perigo ao turista | ITCV |
| irregularidade econômica | IGAE |
| risco alimentar crítico | ERIS |
| reincidência | GovTech Suite (investigação automática) |

---

# 5. Entradas do Copilot

- Texto natural  
- Fotos e vídeos  
- Geolocalização  
- Sintomas e horários  
- Dados do histórico do estabelecimento  
- Nível de risco municipal/insular  
- Base legal  
- Normas ISO  
- Histórico de denúncias do mesmo local  

---

# 6. Saídas do Copilot

- classificação de risco  
- recomendação ao cidadão  
- encaminhamento automático  
- relatório inicial para o instituto  
- contribuição para o mapa de calor  
- atualização do score municipal  
- alertas de possível surto local  

---

# 7. Arquitetura Interna

Copilot CitizenSafety
├── Input Processor (texto/imagem/vídeo)
├── Multimodal Classifier (LLM + Vision)
├── RAG Normativo Sanitário/Turístico
├── Risk Scoring Engine
├── Institute Routing Engine
├── Citizen Guidance Module
├── GovTech Sync Publisher
└── Audit/Trace Layer


---

# 8. RAG Normativo (Base Legal)

### Cabo Verde
- Decreto-Lei 04/2009 – Segurança Alimentar  
- Normas ERIS  
- Procedimentos INSP para intoxicações  
- Regulamentações IGAE  
- Regras ITCV para turismo seguro  

### Normas Internacionais
- HACCP  
- ISO 22000  
- Codex Alimentarius  
- Diretrizes UNWTO  
- WHO – Food Safety & Public Health  

---

# 9. Integrações com Outros Módulos

| Copilot | Integração |
|---------|------------|
| GovTech | encaminhamento + investigação automática |
| BestFood | NCs que viram casos críticos |
| ColdChain | denúncias relacionadas a pescado e temperatura |
| GuestExperience | reclamações que viram incidentes |
| Training/Academy | casos críticos geram trilhas obrigatórias |
| Audit | material para auditorias corretivas |

---

# 10. Painéis que Ele Alimenta

- Mapa de calor por concelho  
- Incidentes por tipo  
- Casos sanitários por ilha  
- Ranking de estabelecimentos com mais denúncias  
- Análise preditiva de surtos  
- Reincidência por segmento  
- Score de segurança turística  

---

# 11. Exemplo de Resposta do Copilot

Sua denúncia foi registrada.

Classificação: Risco Sanitário Alto
De acordo com: Decreto 04/2009 + ISO 22000 (APPCC)
Institutos acionados: INSP e ERIS
Tempo estimado de resposta: 24 a 48 horas

Recomendação:
Caso os sintomas persistam, procure atendimento médico no centro de saúde mais próximo.


---

# 12. Roadmap do Copilot CitizenSafety

Fase | Entrega | Status
-----|---------|--------
Fase 1 | Classificação multimodal de denúncias | MVP
Fase 2 | Encaminhamento automático a institutos | MVP
Fase 3 | Orientação ao turista/cidadão | Em desenvolvimento
Fase 4 | IA para previsão de surtos | Futuro
Fase 5 | Inteligência municipal e pontuação | Futuro
Fase 6 | Integração CPLP | Futuro

---

# 13. Conclusão

O **Copilot CitizenSafety** transforma denúncias simples em dados estruturados, seguros e úteis para:

- proteger o turista  
- melhorar a segurança alimentar  
- antecipar riscos  
- reduzir surtos  
- orientar decisões governamentais  

Ele é um pilar essencial na **transformação digital da saúde, turismo e economia azul** de Cabo Verde e da CPLP.
