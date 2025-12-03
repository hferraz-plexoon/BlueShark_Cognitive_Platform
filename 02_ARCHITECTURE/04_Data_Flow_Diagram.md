# 04_Architecture_C4  
BlueShark Cognitive Platform — C4 (System & Container View)

---

## 1. System Context (Nível 1)

**Sistema Principal: BlueShark Cognitive Platform**

Atores Externos:

- **Trabalhadores / Alunos**
  - Pescadores, cozinheiros, garçons, técnicos de qualidade, jovens em formação.
  - Usam o Academy para trilhas, aulas, certificações.

- **Consultores BeSafe Digital**
  - Usam o Academy & Implementation Hub para implantar e auditar.

- **Inspetores Governamentais**
  - IGAE, INSP, ERIS, IGQPI, ITCV.
  - Usam o GovTech Suite para inspeções, autos e relatórios.

- **Diretoria de Governo**
  - Ministério da Economia, Turismo, Saúde.
  - Usam dashboards nacionais e relatórios de risco.

- **Cidadãos e Turistas**
  - Reportam incidentes (intoxicação, má higiene, reclamações).

- **Sistemas Externos (futuro)**
  - ERPs, HR, sensores IoT, Booking/TripAdvisor, sistemas fiscais.

Relação geral:

- Todos os atores interagem com a **BlueShark Cognitive Platform** via:
  - Portais Web  
  - Apps Mobile (futuro)  
  - APIs (integrações externas)  

---

## 2. Container Diagram (Nível 2)

### 2.1. Contêineres Principais

1. **Web Frontend – GovTech Portal**
   - Tecnologia: Next.js / React
   - Função: dashboards de risco, heatmap, inspeções, GovTech Copilot.

2. **Web Frontend – Academy Portal**
   - Tecnologia: Next.js / React
   - Função: trilhas, aulas, quizzes, certificados, IA Tutor.

3. **Web Frontend – Admin / BeSafe Portal**
   - Tecnologia: Next.js / React
   - Função: gestão de tenants, normas, conteúdos, IA, parâmetros globais.

4. **API Gateway / Edge**
   - Tecnologia: API Gateway (AWS) / Nginx / Kong (a definir)
   - Função: entrada única de todas as requisições, autenticação, roteamento.

5. **BFF – GovTech**
   - Tecnologia: Node.js / NestJS
   - Função: adaptar APIs para experiência GovTech Web & Mobile.

6. **BFF – Academy**
   - Tecnologia: Node.js / NestJS
   - Função: adaptar APIs para experiência Academy Web & Mobile.

7. **Core Backend (Monolito Modular ou Microserviços no mesmo cluster)**
   - Módulos internos:
     - Auth & Identity  
     - Tenant & Org Registry  
     - Academy Service  
     - Implementation Hub Service (futuro)  
     - GovTech Service  
     - Incident & Citizen Reporter Service  
     - Notification Service  

8. **AI Layer**
   - Subcontêineres lógicos:
     - RAG Engine (Normatives Index)  
     - Copilot Orchestrator  
     - Vision & Document AI  

9. **Database Cluster**
   - PostgreSQL (schemas separados por domínio)
   - Redis (cache, sessões)
   - TimescaleDB / extensão para séries temporais (sensores, IoT — futuro).

10. **Object Storage**
    - S3 / compatível
    - Evidências de inspeção, documentos, laudos, anexos.

11. **Event / Message Bus (futuro – para Arquitetura C)**
    - Kafka / RabbitMQ / SNS+SQS
    - Eventos de domínio.

---

## 3. Relações entre Contêineres

- **Usuários Web (Gov, Academy, Admin)**  
  → acessam **Frontends Web**  
  → que chamam o **API Gateway**

- **API Gateway**  
  → aplica autenticação / autorização  
  → encaminha para os **BFFs** corretos (GovTech, Academy, Admin)

- **BFFs**  
  → consomem serviços do **Core Backend**  
  → orquestram chamadas ao **AI Layer** quando necessário

- **Core Backend**  
  → lê/grava dados no **Database Cluster**  
  → envia/recebe arquivos do **Object Storage**  
  → (futuro) publica/consome eventos do **Event / Message Bus**

- **AI Layer**  
  → consulta o **Object Storage** (documentos normativos)  
  → consulta índices vetoriais (RAG)  
  → registra logs/análises em banco / observabilidade

---

## 4. Zoom nos Módulos MVP (GovTech + Academy)

### 4.1. MVP GovTech (em 60 dias)

Fluxo típico:

1. Diretor acessa GovTech Web → vê **heatmap** e dashboards.  
2. Inspetor acessa GovTech Web / Mobile → recebe lista de inspeções.  
3. Inspetor realiza inspeção → registra checklist, fotos, observações.  
4. GovTech Service grava inspeção + evidências no DB + S3.  
5. AI Layer (GovTech Copilot) sugere enquadramento legal e ação.  
6. Sistema gera auto/relatório → disponível no portal + exportável (PDF).

Contêineres envolvidos:

- GovTech Web Frontend  
- API Gateway  
- BFF – GovTech  
- Core Backend (GovTech Service, Incident Service, Auth, Tenant)  
- AI Layer (RAG + Copilot de inspeção)  
- Database Cluster  
- Object Storage  

### 4.2. MVP Academy (em 60 dias)

Fluxo típico:

1. Aluno entra no Academy Web → vê trilhas disponíveis.  
2. Matricula-se em trilha obrigatória.  
3. Consome aulas, faz quizzes, pede ajuda ao IA Tutor.  
4. Academy Service registra progresso e notas.  
5. Ao concluir trilha + critérios → certificação automática.  
6. Dados de % de equipe treinada ficam disponíveis para GovTech.

Contêineres envolvidos:

- Academy Web Frontend  
- API Gateway  
- BFF – Academy  
- Core Backend (Academy Service, Auth, Tenant)  
- AI Layer (Academy Tutor)  
- Database Cluster  
- Object Storage (materiais, PDFs, vídeos)  

---

## 5. Preparação para Arquitetura C (Multi-Agent)

Mesmo com contêiner unificado de backend, o desenho já:

- isola os domínios (Academy, GovTech, Incidents, Notifications)  
- isola o **AI Layer** como contêiner independente  
- prevê um **Event / Message Bus** para transformação futura em agentes:

  - `Academy Agent` consumindo eventos de curso/conclusão  
  - `GovTech Agent` consumindo inspeções e incidentes  
  - `Citizen Agent` consumindo denúncias  
  - `Policy Agent` monitorando mudanças normativas  

Isso permite:

- começar “monolito modular + AI desacoplado” (rápido pro MVP)  
- migrar gradualmente para **multi-agent distribuído**,  
  sem reescrever tudo do zero.

---
