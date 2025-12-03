# 04 — Auditability & Logging Framework  
BlueShark Cognitive Platform – 2025  
Versão 1.0

---

# 1. Objetivo do Sistema de Auditoria

Este documento define o modelo unificado de:

- **Logs**
- **Auditoria**
- **Rastreabilidade**
- **Versionamento**
- **Registro de IA**
- **Observabilidade ética**
- **Conformidade legal**

Aplicado em **toda** a BlueShark Cognitive Platform:

- Academy  
- Implementation Hub  
- Mobile & IA  
- GovTech  
- Citizen Safety Reporter  
- Copilots de IA  

---

# 2. Princípios Fundamentais

1. **Tudo é auditável.**  
   Cada ação humana ou da IA gera um registro verificável.

2. **Logs são imutáveis.**  
   Seguem padrões WORM (Write Once Read Many) com retenção mínima de 5 anos.

3. **Decisões da IA sempre incluem explicação.**

4. **Toda ação crítica requer histórico completo e justificativa.**

5. **Transparência governamental:**  
   Os institutos ITCV, IGAE, INSP e IGQPI têm leitura garantida.

6. **Privacidade preservada:**  
   Dados pessoais seguem padrões GDPR-like + DPA de Cabo Verde.

---

# 3. Tipos de Logs na Plataforma

A plataforma usa um modelo de logs unificado, com padronização em JSON.

## 3.1. Audit Logs (alto impacto)
Registros imutáveis relacionados a:

- inspeções  
- certificações  
- denúncias  
- incidentes  
- decisões governamentais  
- reclassificações  
- aprovação/reprovação de planos de ação  
- alterações de status de empresa  

Exemplo:
```json
{
  "type": "audit",
  "entity": "inspection",
  "entityId": "INS-2025-001233",
  "user": "auditor_igae",
  "decision": "reproved_critical_failure",
  "justification": "Temperature logs missing for 48h",
  "timestamp": "2025-02-10T14:22:01Z",
  "ip": "102.12.33.10"
}
```

---

## 3.2. Activity Logs (uso geral)
Gerados em todas as ações operacionais:

- login/logout  
- upload de evidências  
- atualização de cadastros  
- avanço de trilhas  
- submissão de exercícios  
- ações do consultor  

---

## 3.3. AI Logs (toda interação com IA)
Obrigatórios por norma interna (AI Governance).

Cada requisição gera:

- modelo usado  
- versão do modelo  
- versão do prompt  
- fontes RAG retornadas  
- score de similaridade  
- explicação do reasoning  
- segurança aplicada  
- decisão final  
- nível de risco  

Exemplo:
```json
{
  "type": "ai",
  "model": "gpt-5.1",
  "promptVersion": "academy_exam_v3",
  "ragFilesUsed": ["DL-04-2009-HACCP.pdf", "ISO22000:2018-Section7"],
  "reasoning": "Step-by-step chain omitted for compliance",
  "decision": "suggest_retake",
  "confidence": 0.83,
  "riskLevel": "moderate",
  "timestamp": "2025-02-10T14:22:01Z"
}
```

---

## 3.4. Data Access Logs (LGPD/GDPR)
Sempre que dados sensíveis forem acessados:

- alunos  
- trabalhadores  
- dados de saúde  
- denúncias  
- dados pessoais de turistas  

---

## 3.5. System Logs (infraestrutura)

- utilização de CPU, memória, rede  
- erros 500  
- falhas em containers  
- problemas de latência  
- falhas de ingestão IoT  

---

# 4. Eventos Críticos que Requerem Logs Obrigatórios

| Evento | Tipo de Log | Obrigatório? |
|--------|--------------|--------------|
| Reprovação de auditoria | Audit Log | ✔ |
| Risco sanitário grave | AI Log + Audit Log | ✔ |
| Publicação no GovTech | Audit Log | ✔ |
| Denúncia séria | Audit Log | ✔ |
| Alteração de norma | Audit Log | ✔ |
| Correção IA de prova discursiva | AI Log | ✔ |
| Edição manual de evidência | Audit Log | ✔ |
| Exclusão de usuário | Activity + Audit | ✔ |
| Ação policial/INSP | Audit Log | ✔ |

---

# 5. Estrutura Unificada de Logs

Todos os logs seguem o formato:

```json
{
  "id": "uuid",
  "type": "audit|activity|ai|data|system",
  "category": "academy|implementation|govtech|citizen|mobile|auth|infra",
  "actorType": "human|ai|system",
  "actorId": "user_or_model",
  "action": "string",
  "details": {},
  "timestamp": "ISO8601",
  "origin": {
    "ip": "string",
    "device": "web|mobile|iot",
    "tenant": "besafe-cv"
  }
}
```

---

# 6. Trilhas de Auditoria Imutáveis (WORM)

- S3 Glacier Locked Mode  
- Retenção mínima: **5 anos**  
- Modo litigioso: **10 anos**  
- Regras ZTNA (Zero Trust Network Access)  
- IAM Roles segregados:

  - **Escrita:** apenas serviços  
  - **Leitura:** governo + auditores  
  - **Nenhuma entidade tem permissão de apagar logs**  

---

# 7. Versionamento e Conformidade

## 7.1. Versionamento de Normas
Toda atualização gera:

| Campo | Descrição |
|-------|-----------|
| Version | v1, v2, v3 |
| Editor | humano responsável |
| IA Reviewer | sim/não |
| Diff automático | páginas alteradas |
| RAG Index | reindexado? |
| Aprovador governamental | obrigatório |

---

## 7.2. Versionamento de Evidências
Evidências nunca são substituídas.

- nova versão = novo ID  
- links relacionam versões  
- auditor vê histórico completo  

---

# 8. Painel de Auditoria no GovTech

O GovTech terá um painel exclusivo:

- lista de todos logs por setor  
- filtro por ilha/concelho  
- filtro por risco  
- replay de decisões da IA  
- comparativos entre auditores  
- detecção de anomalias  
- detecção de inconsistências  

---

# 9. Segurança Aplicada aos Logs

- Criptografia KMS AES-256  
- Network segmentation  
- API Logging (mTLS)  
- Rate limit  
- ZTNA  
- MFA para autoridades  
- Detect anomaly patterns (Falcon)  
- Guardrails automáticos para IA  

---

# 10. Conclusão

O sistema de logs torna tudo:

✔ rastreável  
✔ confiável  
✔ auditável  
✔ legalmente defensável  
✔ transparente para governo e sociedade  
✔ compatível com normas internacionais  

Serve como **base de confiança** do BlueShark Program e ponto crítico para:

- expansão CPLP  
- uso internacional  
- compliance  
- certificação  

