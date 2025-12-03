# 04 — API Versioning Guidelines  
BlueShark Cognitive Platform – Versão 2025

---

## 1. Objetivo do Documento

O objetivo deste documento é definir o padrão oficial de versionamento das APIs e Copilots da **BlueShark Cognitive Platform**, garantindo:

- Estabilidade para clientes, governo e parceiros
- Evolução segura sem breaking changes inesperadas
- Suporte multiplataforma (Academy, Implementation, Mobile & IA, GovTech)
- Compatibilidade com multi-país, multi-tenant e multi-modules
- Rastreamento claro das versões ativas e deprecated

---

# 2. Princípios de Versionamento

1. **Backward compatibility sempre preservada**  
   Nenhuma mudança pode quebrar clientes existentes sem anúncio prévio.

2. **Versionamento explícito**  
   Toda API deve conter versão no path, header ou ambos.

3. **“Sunset Policy” clara**  
   Toda versão antiga deve ter o status:  
   `active`, `maintenance`, `deprecated`, `sunset`.

4. **Separação entre versão da API e versão dos Copilots**  
   Copilots evoluem mais rápido que o Core API.

5. **Documentação obrigatória para mudanças**  
   Qualquer mudança deve ser acompanhada por release note.

6. **Sem versionamento por querystring**  
   Padrão proibido (confuso e inseguro).

---

# 3. Padrão Oficial de Versionamento

A plataforma adota o padrão **MAJOR.MINOR.PATCH**, idêntico ao Semantic Versioning, mas aplicado a APIs.

### Exemplo:
```
v1.3.2
```

### Significado:
- **MAJOR** → mudanças que quebram compatibilidade  
- **MINOR** → novas funcionalidades compatíveis  
- **PATCH** → correções sem impacto no contrato  

---

# 4. Formato de URL da API

### 4.1. Path Versioning (obrigatório)

```
/api/v1/coldchain/lots
/api/v1/bestfood/audits
/api/v1/govtech/incidents
/api/v1/copilot/governance/query
```

### 4.2. Header Versioning (opcional complementar)

```
X-API-Version: 1.3.2
```

### 4.3. WebSocket Versioning (para Copilots)

```
wss://api.blueshark.cv/ws/v1/copilot
Sec-WebSocket-Protocol: bs-copilot-v1
```

---

# 5. Versionamento dos Copilots (RAG + Reasoning)

Os Copilots têm evolução mais rápida e por isso usam **versionamento independente**.

### Padrão:
```
copilot.academy.v1
copilot.bestfood.v2
copilot.govtech.v3
```

### Motivo:
- O dataset pode mudar  
- A estratégia de RAG pode melhorar  
- Os prompts podem evoluir  
- Os guardrails podem ser revisados  

Nenhuma dessas mudanças precisa impactar a versão da API.

---

# 6. Estratégia de Depreciação

Cada versão da API pode estar em um dos estados:

| Estado | Significado |
|--------|-------------|
| **active** | Versão atual e recomendada |
| **maintenance** | Recebe apenas patches críticos |
| **deprecated** | Anunciada para desativação |
| **sunset** | Data de desligamento confirmada |

### Exemplo de ciclo:

| Versão | Estado |
|--------|--------|
| v1 | active |
| v2 | active |
| v1 | maintenance (lançamento do v3) |
| v1 | deprecated (6 meses depois) |
| v1 | sunset (12 meses depois) |

---

# 7. Regras para Introduzir Nova Versão

Uma nova versão **MAJOR** é criada apenas quando:

- Há mudança no formato do JSON
- Mudança em rotas existentes
- Mudança no fluxo de autenticação
- Mudança estrutural no modelo de dados de resposta
- Alterações regulatórias obrigatórias (GovTech)

---

# 8. Compatibilidade com Multi-Tenant e Multi-País

Versões são **globais**, mas os conteúdos (RAG, normas, checklists, leis) são:

- por país  
- por ilha  
- por módulo  
- por tenant  

Exemplo:

```
v1 (Brasil) ≠ v1 (Cabo Verde) nos dados normativos
```

Mas **a API é a mesma**.

---

# 9. Padrão de Release Notes

Para cada nova versão deve existir:

```
/docs/releases/api/v1.4.0.md
```

Com seções:

1. O que mudou  
2. O que foi corrigido  
3. Impacto no cliente  
4. Ações necessárias  
5. Estado da versão anterior  

---

# 10. Exemplo Completo de Versionamento

### Exemplo de endpoint:

```
GET /api/v1/bestfood/checklists?module=kitchen
```

### Headers:

```
Authorization: Bearer <token>
X-API-Version: 1.3.0
X-Tenant-ID: oasis_sal
X-Country: CV
```

### Versão do Copilot envolvido:

```
copilot.bestfood.v2
```

---

# 11. Boas Práticas

- Nunca renomear campos sem criar uma nova versão.
- Nunca deletar endpoints: apenas marcar como deprecated.
- Evitar BREAKING CHANGES dentro de versões MINOR/PATCH.
- Sempre validar comportamento no staging antes de publicar.
- Criar automações CI/CD para validar compatibilidade.

---

# 12. Conclusão

O sistema de versionamento aqui documentado garante:

- Evolução contínua sem risco  
- Padronização em toda BlueShark Platform  
- Segurança para governo e empresas  
- Longevidade dos contratos  
- Modularidade dos Copilots  

Este documento deve ser incluído em:

```
/08_API/04_Versioning_Guidelines.md
```

e usado como referência para equipes de:

- Backend  
- Mobile  
- Web  
- DevOps  
- IA / Copilots  
- Governança e Compliance  

