# 04 — Use Cases Overview  
BlueShark Cognitive Platform — BeSafe Digital  
Versão 1.0 — Janeiro/2025

Este documento apresenta uma visão consolidada dos **principais casos de uso** dos agentes cognitivos (Copilots) do BlueShark Program, conectando:

- BlueShark Academy & Implementation Hub  
- BlueShark Mobile & IA (ColdChain, BestFood, ESG+Social, SafeStay, GuestExperience)  
- GovTech Suite (ITCV, IGAE, INSP, IGQPI, ERIS, Ministério)  
- Citizen Safety Reporter  
- Selos digitais BlueShark (QR Code)  

Ele serve como **ponte** entre:

- a visão estratégica (01_Vision, 02_Scope, 03_Principles)  
- e a arquitetura, RAG, Copilots e APIs que serão detalhados nos próximos diretórios.

---

## 1. Macro-Cenários de Uso

Os casos de uso do BlueShark Cognitive Platform podem ser organizados em **5 macro-cenários**:

1. **Educação & Capacitação (Academy)**  
2. **Implantação & Auditoria Operacional (Implementation Hub + Mobile & IA)**  
3. **Supervisão Governamental & Políticas Públicas (GovTech)**  
4. **Participação Social & Transparência (Citizen Reporter + Selos Digitais)**  
5. **Análise Avançada & Decisão Estratégica (Copilots analíticos)**  

Cada macro-cenário é suportado por um conjunto de **Copilots específicos** e pela **Base Normativa (RAG)**.

---

## 2. Casos de Uso por Macro-Cenário

### 2.1. Educação & Capacitação (Academy)

**Objetivo:**  
Formar e certificar milhares de profissionais em Cabo Verde (e CPLP), em temas como:

- Boas Práticas de Higiene (BPH)  
- Segurança Alimentar (HACCP + ISO 22000)  
- ESG & Sustentabilidade  
- Turismo, Experiência & Hospitalidade  
- Cadeia de Frio & Pescas  
- Normas ISO e legislação nacional  

**Principais casos de uso:**

1. Trabalhador acessa o app da Academy, faz trilhas obrigatórias e obtém certificado.  
2. Jovem de programa social conclui trilha “Jovem BlueShark” e se torna elegível para atuar como multiplicador.  
3. Governo acompanha, por ilha, quantos profissionais estão certificados em cada trilha mínima.  
4. Consultor BeSafe usa a Academy para treinar equipes antes da implantação do Mobile & IA.  

**Copilots envolvidos:**

- **Training Copilot**  
- **Consultant Copilot (modo formação)**  

---

### 2.2. Implantação & Auditoria Operacional

**Objetivo:**  
Transformar requisitos normativos em **rotina diária** de operação em:

- Embarcações, processadores, armazéns, importadores (ColdChain)  
- Hotéis, restaurantes, cantinas, operadores turísticos (BestFood, SafeStay, GuestExperience)  

**Principais casos de uso:**

1. Consultor BeSafe abre um projeto de implantação para um hotel.  
2. O Implementation Hub gera automaticamente um **playbook de implantação** com base em:  
   - normas aplicáveis  
   - porte da empresa  
   - trilhas da Academy concluídas  
3. Durante a implantação, a equipe executa checklists, envia evidências (foto, vídeo, documentos).  
4. O **Consultant Copilot** analisa evidências e sugere planos de ação.  
5. Ao final, o cliente está pronto para operar no **BlueShark Mobile & IA** e buscar o **selo digital**.  

No ciclo contínuo:

6. O **BestFood Copilot** e o **ColdChain Copilot** analisam dados em tempo real (temperatura, checklists, NCs).  
7. O **Audit Copilot** gera relatórios de auditoria interna prontos para serem compartilhados com governo.  

**Copilots envolvidos:**

- **Consultant Copilot**  
- **ColdChain Copilot**  
- **BestFood Copilot**  
- **ESG+Social Copilot**  
- **SafeStay Copilot**  
- **GuestExperience Copilot**  
- **Audit Copilot**  

---

### 2.3. Supervisão Governamental & Políticas Públicas (GovTech)

**Objetivo:**  
Permitir que o governo faça **regulação inteligente**, baseada em:

- dados reais de operação das empresas  
- trilhas de formação  
- dados de inspeção  
- denúncias da população  

**Principais casos de uso:**

1. O **IGAE** recebe um painel com empresas em maior risco econômico/regulatório.  
2. O **INSP** vê clusters de intoxicação e surto alimentar em certos concelhos.  
3. A **ERIS** cruza denúncias, dados de lotes, importações e incidentes.  
4. O **IGQPI** acompanha a qualidade de empresas certificadas com selos BlueShark.  
5. O **ITCV** vê como selos, NPS e certificações impactam o turismo por ilha.  
6. O **Ministério** recebe recomendações de políticas públicas diretamente do **Ministry Copilot**.  

**Copilots envolvidos:**

- **IGAE Copilot**  
- **INSP Copilot**  
- **ERIS Copilot**  
- **IGQPI Copilot**  
- **ITCV Copilot**  
- **Ministry Copilot**  

---

### 2.4. Participação Social & Transparência (Citizen Reporter & Selos)

**Objetivo:**  
Transformar população e turistas em **sensores sociais**, gerando:

- denúncias de intoxicação  
- reclamações de higiene e atendimento  
- avaliações de experiência do turista  
- validação social dos selos  

**Principais casos de uso:**

1. Turista escaneia um QR Code do selo BlueShark de um hotel:  
   - vê a nota geral  
   - vê resumo de evidências públicas  
   - vê se há incidentes recentes relevantes  

2. Cidadão usa o app Citizen Safety Reporter para relatar um caso de:  
   - intoxicação alimentar  
   - ambiente insalubre  
   - contaminação de pescado  
   - falha grave de higiene  

3. O **Citizen Copilot** classifica gravidade, cruza com dados do Mobile & IA e dispara:  
   - alerta para ERIS/INSP/IGAE/ITCV  
   - recomendação de inspeção imediata se necessário  

**Copilots envolvidos:**

- **Citizen Reporter Copilot**  
- **Seal Verification Copilot**  
- Copilots governamentais que recebem os alertas (INSP, ERIS, IGAE, ITCV)  

---

### 2.5. Análise Avançada & Decisão Estratégica

**Objetivo:**  
Permitir que governo, grandes redes e parceiros internacionais (FAO, OMS, UNWTO, bancos de fomento) tenham **visão macro**:

- riscos por ilha/segmento  
- impacto de políticas públicas  
- evolução da qualificação  
- efeito dos selos no turismo  

**Principais casos de uso:**

1. Ministério da Economia consulta o **Ministry Copilot** para entender:  
   - quais concelhos merecem prioridade em investimentos  
   - quais setores estão mais vulneráveis  
   - quais trilhas da Academy mais reduzem risco em menor tempo  

2. Banco de desenvolvimento analisa, com apoio do Copilot, onde investir em:  
   - cadeia de frio  
   - qualificação  
   - incentivos fiscais  

3. BeSafe Digital e parceiros usam os dados para expandir a solução a outros países da CPLP, com base em resultados concretos.  

**Copilots envolvidos:**

- **Ministry Copilot**  
- **Global Standards / Analytics Copilot**  
- **ESG+Social Copilot**  

---

## 3. Matriz de Casos de Uso x Copilots

(Visão resumida para orientar a fase 03_COPILOTS)

| Macro-Cenário                      | Copilots Principais                                           |
|-----------------------------------|---------------------------------------------------------------|
| Educação & Capacitação            | Training, Consultant (modo formação)                         |
| Implantação & Auditoria           | Consultant, ColdChain, BestFood, ESG, SafeStay, GuestExp, Audit |
| Supervisão Governamental          | IGAE, INSP, ERIS, IGQPI, ITCV, Ministry                      |
| Participação Social & Transparência | Citizen Reporter, Seal Verification                          |
| Análise Avançada & Estratégica    | Ministry, Global/ESG Analytics                               |

---

## 4. Uso em Roadmap e Arquitetura

Este documento deve ser usado para:

- priorizar quais Copilots entram no **MVP**  
- definir quais fontes da **Knowledge Base (04_KNOWLEDGE_BASE)** cada Copilot precisa  
- orientar o design dos **prompts padrão (06_PROMPT_ENGINEERING)**  
- guiar a definição de **endpoints (08_API)**  
- suportar os critérios de **avaliação (07_EVALUATION)**  

---

## 5. Próximos Passos

1. Detalhar cada Copilot em `03_COPILOTS/NN_Copilot_*.md` usando o template de especificação.  
2. Conectar cada caso de uso às fontes de dados da **Knowledge Base**.  
3. Definir prioridades de implementação para o MVP de 60 dias (GovTech + Academy).  

