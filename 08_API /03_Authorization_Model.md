# 03 — Authorization & Access Control Model  
BlueShark Cognitive Platform – API Layer  
Versão 2025

---

## 1. Objetivo do Documento
Este documento define o **modelo oficial de autorização e controle de acesso (RBAC + ABAC)** da BlueShark Cognitive Platform, cobrindo:

- Perfis e papéis dos usuários  
- Regras de acesso por Copilot  
- Escopo de tenant (multi-país e multi-organização)  
- Tokens, permissões, políticas e restrições  
- Limites de acesso para governo, empresas e cidadãos  
- Camada de segurança para integração com GovTech  

Este modelo será implementado tanto na API quanto nos Copilots.

---

# 2. Princípios de Autorização

1. **Least privilege**  
   Cada usuário só acessa exatamente o que precisa.

2. **Multi-tenant isolado**  
   Cada país, ilha e organização tem dados completamente isolados.

3. **RBAC + ABAC híbrido**  
   Papéis tradicionais (RBAC) + atributos contextuais (ABAC).

4. **Log de auditoria obrigatório**  
   Toda ação é registrada, especialmente acessos governamentais.

5. **Contexto obrigatório para IA**  
   A IA só responde dentro do escopo permitido pelo usuário.

---

# 3. Perfis Principais (RBAC)

| Perfil | Descrição |
|-------|-----------|
| **Citizen** | Usuários do Citizen Safety Reporter |
| **Worker** | Funcionário de restaurantes, hotéis, pesca |
| **Consultant** | Consultores BeSafe Digital |
| **Auditor** | Auditores internos/externos |
| **Manager** | Gestores de empresas |
| **Inspector** | IGAE, INSP, ERIS, IGQPI, ITCV |
| **Director** | Direção governamental |
| **Admin (BeSafe Digital)** | Operação nacional |
| **SuperAdmin** | Operação global / suporte técnico |

---

# 4. Atributos de Contexto (ABAC)

Além do papel, cada request é avaliado por atributos como:

| Atributo | Exemplo | Uso |
|----------|---------|-----|
| `tenant_id` | `cv_oasis_hotel01` | Isola os dados da empresa |
| `country` | `CV`, `AO`, `BR` | Restringe normas e RAG |
| `region` | `Sal`, `Praia` | GovTech e Citizen Safety |
| `module` | `bestfood`, `coldchain` | Restringe Copilots |
| `sensitivity` | `low`, `high`, `critical` | Controle de dados sensíveis |
| `entity_type` | `restaurant`, `ship`, `inspector` | Regras por setor |

---

# 5. Matriz de Acesso por Copilot

### 5.1. Tabela Consolidada

| Copilot | Citizen | Worker | Consultant | Manager | Auditor | Inspector | Director | Admin |
|---------|---------|--------|-----------|---------|---------|-----------|----------|--------|
| Academy | ❌ | ✔ | ✔ | ✔ | ✔ | ❌ | ❌ | ✔ |
| Implementation | ❌ | ❌ | ✔ | ✔ | ✔ | ❌ | ❌ | ✔ |
| ColdChain | ❌ | ✔ (pescador) | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| BestFood | ❌ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| ESG | ❌ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| SafeStay | ❌ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| GuestExperience | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Audit | ❌ | ❌ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| GovTech | ❌ | ❌ | ❌ | ❌ | ✔ | ✔ | ✔ | ✔ |
| CitizenSafety | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
| Global Standards | ❌ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ | ✔ |

Legenda:  
✔ acesso permitido  
❌ acesso bloqueado  

---

# 6. Regras de Autorização por Camada

## 6.1. API REST
Toda requisição deve conter:

```
Authorization: Bearer <jwt>
X-Tenant-ID: <org_id>
X-Country-Code: CV
```

Sessões expiram em 30 minutos de inatividade.

---

## 6.2. WebSocket (Stream de IA)

Para usar:

```
Authorization: Bearer token
Sec-WebSocket-Protocol: bs-copilot
```

Permissões:

- **Citizen** → apenas CitizenSafety Copilot  
- **Inspector** → GovTech Copilot + Audit Copilot  
- **Worker** → Academy + módulo do setor  
- **Consultant** → acesso completo por cliente  

---

# 7. Políticas de Filtragem do RAG

A IA só pode acessar documentos que pertencem ao usuário:

## Exemplo
Um auditor de HACCP:

- pode acessar normas HACCP, ISO, DL 04/2009  
- **não pode** acessar dados de outras empresas  
- **pode** acessar somente o tenant atual  
- tudo passado como contexto ao RAG

---

# 8. Escopo de Tokens

## 8.1. Tipos de Tokens

| Tipo | Uso |
|------|-----|
| `user_token` | Mobile/Web |
| `system_token` | Serviços internos |
| `gov_token` | Uso exclusivo do GovTech Suite |
| `admin_token` | Suporte mestre |

---

# 9. Acesso Governamental (Regras Criticamente Sensíveis)

## 9.1. Inspectors (IGAE/INSP/ERIS/IGQPI/ITCV)
Podem:

✔ acessar o Copilot GovTech  
✔ acessar Audit Copilot  
✔ consultar normas e leis  
✔ criar autos, advertências e inspeções  

Não podem:

❌ acessar dados pessoais de trabalhadores  
❌ ver detalhes financeiros de empresas  
❌ consultar empresas fora de sua jurisdição

---

## 9.2. Directors (nível nacional)
Podem:

✔ visualizar dashboards nacionais  
✔ consultar dados agregados  
✔ usar IA para análises de risco macro  

Não podem:

❌ acessar dados individuais de trabalhadores  
❌ editar registros operacionais

---

# 10. Multi-Tenant Isolation

Cada tenant possui:

- Base lógica separada  
- Chaves criptográficas exclusivas  
- Políticas de RAG isoladas  
- Sessões isoladas  

Garante segurança nacional e neutralidade política.

---

# 11. Auditoria e Logging

Toda ação de alto impacto gera log obrigatório:

| Evento | Log |
|--------|-----|
| Ações de GovTech | mandatory |
| Decisões de IA | mandatory |
| Consultas sensíveis | mandatory |
| Classificação de incidentes | mandatory |
| Acesso inter-ilhas | mandatory |

Formato:

```json
{
  "timestamp": "2025-01-20T12:30:11Z",
  "user": "inspector_igae_001",
  "tenant": "cv_sal",
  "module": "govtech",
  "action": "inspection.create",
  "details": { "entity": "restaurante123" }
}
```

---

# 12. Conclusão

Este modelo de autorização garante:

- Segurança forte (RBAC + ABAC híbrido)  
- Governança adequada para governo  
- Compatibilidade com auditorias ISO  
- Escalabilidade para CPLP  
- Proteção rigorosa de dados sensíveis  

Pronto para incluir no repositório `/08_API/03_Authorization_Model.md`.

