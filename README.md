# 🔐 Endpoints Protegidos por Perfil - Documentação Completa

## 📊 Resumo Executivo

- **Endpoints admin-only:** 92
- **Endpoints acessíveis por traders (+ admins):** 15
- **Endpoints públicos (sem auth):** 12
- **Arquivos de rota:** 21
- **Padrão admin:** Middleware `requireAdmin` que valida `perfil === 'admin'`
- **Padrão trader:** Apenas JWT válido (qualquer perfil autenticado acessa)
- **Resposta em acesso negado (admin-only):** 403 Forbidden
- **Status:** ✅ 100% coberto por testes Jest (314 testes)

---

## 📋 Tabela Consolidada - Endpoints Admin-Only (93 endpoints)

| #   | Método | Rota                                                                          | Descrição                                        | Arquivo                         |
| --- | ------ | ----------------------------------------------------------------------------- | ------------------------------------------------ | ------------------------------- |
| 1   | GET    | `/api/v1/audit-history`                                                       | Listar logs de auditoria                         | audit_history.js                |
| 2   | GET    | `/api/v1/audit-history/actions`                                               | Listar ações auditadas                           | audit_history.js                |
| 3   | GET    | `/api/v1/cors`                                                                | Obter configurações de CORS                      | corsConfig.js                   |
| 4   | POST   | `/api/v1/nelogica/ativar`                                                     | Ativa subconta de teste na Nelogica              | nelogica.js                     |
| 5   | DELETE | `/api/v1/nelogica/cancelar`                                                   | Cancela conta/subconta na Nelogica               | nelogica.js                     |
| 6   | GET    | `/api/v1/nelogica/listar`                                                     | Retorna mesas proprietárias e subcontas          | nelogica.js                     |
| 7   | GET    | `/api/v1/nelogica/planos`                                                     | Retorna planos de assinatura Nelogica            | nelogica.js                     |
| 8   | GET    | `/api/v1/nelogica/status/:document`                                           | Consulta se trader está ativo na Nelogica        | nelogica.js                     |
| 9   | POST   | `/api/v1/nelogica/toggle/:document`                                           | Ativa/desativa trader na Nelogica                | nelogica.js                     |
| 10  | POST   | `/api/v1/nelogica/request`                                                    | Proxy para API da Nelogica                       | nelogica.js                     |
| 11  | POST   | `/api/v1/rpa/upload`                                                          | Upload de RPA                                    | rpa.js                          |
| 12  | GET    | `/api/v1/rpa/exists?conta=X&ciclo_pagamento_id=Y`                             | Verifica se existe RPA para trader/ciclo         | rpa.js                          |
| 13  | GET    | `/api/v1/rpa/:id/download`                                                    | Download de RPA                                  | rpa.js                          |
| 14  | DELETE | `/api/v1/rpa/:id`                                                             | Remove RPA (arquivo + registro)                  | rpa.js                          |
| 15  | GET    | `/api/v1/solicitacao-saque`                                                   | Lista todas as solicitações (admin, com filtros) | solicitacao_saque.js            |
| 16  | GET    | `/api/v1/solicitacao-saque/:id/verificar-fechamento`                          | Verifica elegibilidade no fechamento             | solicitacao_saque.js            |
| 17  | DELETE | `/api/v1/solicitacao-saque/:id/nota-fiscal`                                   | Deleta nota fiscal (volta status para 'pago')    | solicitacao_saque.js            |
| 18  | PATCH  | `/api/v1/solicitacao-saque/:id/aprovar`                                       | Aprova solicitação de saque                      | solicitacao_saque.js            |
| 19  | PATCH  | `/api/v1/solicitacao-saque/:id/reprovar-nota-fiscal`                          | Reprova nota fiscal (volta a 'aprovado')         | solicitacao_saque.js            |
| 19  | PATCH  | `/api/v1/solicitacao-saque/:id/rejeitar`                                      | Rejeita solicitação (motivo obrigatório)         | solicitacao_saque.js            |
| 20  | PATCH  | `/api/v1/solicitacao-saque/:id/pagamento`                                     | Registra pagamento (PIX/TED/DOC)                 | solicitacao_saque.js            |
| 21  | DELETE | `/api/v1/solicitacao-saque/:id`                                               | Deleta permanentemente solicitação               | solicitacao_saque.js            |
| 30  | POST   | `/api/v1/testes`                                                              | Cria registro de teste para Canário              | testes.js                       |
| 31  | GET    | `/api/v1/testes`                                                              | Lista testes com paginação                       | testes.js                       |
| 32  | GET    | `/api/v1/traders-mesa`                                                        | Lista registros de traders da mesa               | traders_mesa.js                 |
| 33  | POST   | `/api/v1/traders-mesa`                                                        | Cria novo registro de trader                     | traders_mesa.js                 |
| 34  | PUT    | `/api/v1/traders-mesa/:id`                                                    | Atualiza registro de trader                      | traders_mesa.js                 |
| 35  | POST   | `/api/v1/traders-mesa-avaliacao/processar-todos`                              | Processa avaliação para todos                    | traders_mesa_avaliacao.js       |
| 36  | POST   | `/api/v1/traders-mesa-avaliacao/:traderId/processar`                          | Processa avaliação de trader específico          | traders_mesa_avaliacao.js       |
| 37  | GET    | `/api/v1/traders-mesa-avaliacao/snapshots/ativos`                             | Retorna snapshots ativos com paginação           | traders_mesa_avaliacao.js       |
| 40  | GET    | `/api/v1/traders-mesa-ciclo-pagamento/pendentes`                              | Lista pagamentos pendentes                       | traders_mesa_ciclo_pagamento.js |
| 41  | GET    | `/api/v1/traders-mesa-ciclo-pagamento/trader/:traderId`                       | Pagamentos por trader                            | traders_mesa_ciclo_pagamento.js |
| 42  | GET    | `/api/v1/traders-mesa-ciclo-pagamento/conta/:conta`                           | Pagamentos por conta                             | traders_mesa_ciclo_pagamento.js |
| 43  | GET    | `/api/v1/traders-mesa-ciclo-pagamento/dashboard-pagamentos`                   | Dashboard consolidado de pagamentos              | traders_mesa_ciclo_pagamento.js |
| 44  | GET    | `/api/v1/traders-mesa-ciclo-pagamento/dashboard-pagamentos/:cicloFim/traders` | Dashboard por ciclo específico                   | traders_mesa_ciclo_pagamento.js |
| 45  | GET    | `/api/v1/traders-mesa-ciclo-pagamento/estatisticas`                           | Estatísticas de ciclos de pagamento              | traders_mesa_ciclo_pagamento.js |
| 46  | POST   | `/api/v1/traders-mesa-ciclo-pagamento/:pagamentoId/aprovar`                   | Aprova pagamento                                 | traders_mesa_ciclo_pagamento.js |
| 47  | POST   | `/api/v1/traders-mesa-ciclo-pagamento/:pagamentoId/pagar`                     | Registra pagamento realizado                     | traders_mesa_ciclo_pagamento.js |
| 48  | POST   | `/api/v1/traders-mesa-ciclo-pagamento/:pagamentoId/nota-fiscal`               | Processa nota fiscal de pagamento                | traders_mesa_ciclo_pagamento.js |
| 49  | POST   | `/api/v1/traders-mesa-ciclo-pagamento/:pagamentoId/cancelar`                  | Cancela pagamento                                | traders_mesa_ciclo_pagamento.js |
| 50  | GET    | `/api/v1/vendas`                                                              | Lista todas as vendas                            | vendas.js                       |
| 51  | GET    | `/api/v1/vendas/status`                                                       | Status das vendas                                | vendas.js                       |
| 52  | GET    | `/api/v1/vendas/produtos`                                                     | Produtos disponíveis                             | vendas.js                       |
| 53  | GET    | `/api/v1/vendas/:id`                                                          | Busca venda por ID                               | vendas.js                       |
| 54  | POST   | `/api/v1/vendas`                                                              | Cria nova venda                                  | vendas.js                       |
| 55  | PUT    | `/api/v1/vendas/:id`                                                          | Atualiza venda                                   | vendas.js                       |
| 56  | DELETE | `/api/v1/vendas/:id`                                                          | Deleta venda                                     | vendas.js                       |
| 57  | PATCH  | `/api/v1/vendas/:id/status`                                                   | Atualiza status da venda                         | vendas.js                       |
| 58  | POST   | `/api/v1/vendas/:conta/reset-teste`                                           | Reset de teste de venda                          | vendas.js                       |
| 59  | GET    | `/api/v1/vendas/mesa/aprovadas/inativas`                                      | Vendas aprovadas mas inativas                    | mesa.js                         |
| 60  | GET    | `/api/v1/vendas/mesa/aprovadas/inativas/planos`                               | Planos das vendas inativas                       | mesa.js                         |
| 61  | GET    | `/api/v1/vendas/mesa/aprovadas/ativas`                                        | Vendas aprovadas e ativas                        | mesa.js                         |
| 62  | GET    | `/api/v1/vendas/mesa/por-conta`                                               | Vendas agrupadas por conta                       | mesa.js                         |
| 63  | PATCH  | `/api/v1/vendas/mesa/ativar`                                                  | Ativa uma venda                                  | mesa.js                         |
| 64  | GET    | `/api/v1/vendas/mesa/status-teste-ativo`                                      | Status de teste ativo                            | mesa.js                         |
| 65  | GET    | `/api/v1/vendas/logs/basic`                                                   | Logs básicos de vendas                           | logs.js                         |
| 66  | GET    | `/api/v1/vendas/logs/basic/stats`                                             | Estatísticas de logs                             | logs.js                         |
| 67  | GET    | `/api/v1/vendas/logs/basic/:id`                                               | Log específico por ID                            | logs.js                         |
| 68  | GET    | `/api/v1/vendas/logs/basic/:id/payload`                                       | Payload completo do log                          | logs.js                         |
| 69  | GET    | `/api/v1/vendas/estatisticas/dashboard/vendas-aprovadas-mes`                  | Dashboard: vendas aprovadas no mês               | estatisticas.js                 |
| 70  | GET    | `/api/v1/vendas/estatisticas/dashboard/resumo`                                | Dashboard: resumo geral                          | estatisticas.js                 |
| 71  | GET    | `/api/v1/vendas/estatisticas/dashboard/timeline`                              | Dashboard: timeline de vendas                    | estatisticas.js                 |
| 72  | GET    | `/api/v1/vendas/estatisticas/dashboard/status-distribuicao`                   | Dashboard: distribuição de status                | estatisticas.js                 |
| 73  | GET    | `/api/v1/vendas/estatisticas/dashboard/top-produtos`                          | Dashboard: top 10 produtos                       | estatisticas.js                 |
| 74  | GET    | `/api/v1/vendas/estatisticas/relatorios/financeiro`                           | Relatório: análise financeira                    | estatisticas.js                 |
| 75  | GET    | `/api/v1/vendas/estatisticas/relatorios/produtos`                             | Relatório: performance de produtos               | estatisticas.js                 |
| 76  | GET    | `/api/v1/vendas/estatisticas/relatorios/geografico`                           | Relatório: análise geográfica                    | estatisticas.js                 |
| 77  | GET    | `/api/v1/vendas/estatisticas/relatorios/afiliados`                            | Relatório: performance de afiliados              | estatisticas.js                 |
| 78  | GET    | `/api/v1/vendas/estatisticas/relatorios/temporal`                             | Relatório: análise temporal                      | estatisticas.js                 |
| 79  | GET    | `/api/v1/planos`                                                              | Lista todos os planos                            | planos/index.js                 |
| 80  | GET    | `/api/v1/planos/:id`                                                          | Busca plano por ID                               | planos/index.js                 |
| 81  | POST   | `/api/v1/planos`                                                              | Cria novo plano                                  | planos/index.js                 |
| 82  | PUT    | `/api/v1/planos/:id`                                                          | Atualiza plano                                   | planos/index.js                 |
| 83  | DELETE | `/api/v1/planos/:id`                                                          | Deleta plano                                     | planos/index.js                 |
| 84  | GET    | `/api/v1/planos/buscar/:nome`                                                 | Busca planos por nome (busca parcial)            | planos/index.js                 |
| 85  | GET    | `/api/v1/planos/stats/resumo`                                                 | Estatísticas dos planos                          | planos/index.js                 |
| 86  | GET    | `/api/v1/plano-profit`                                                        | Lista todos os planos profit                     | plano_profit/index.js           |
| 87  | GET    | `/api/v1/plano-profit/:id`                                                    | Busca plano profit por ID                        | plano_profit/index.js           |
| 88  | POST   | `/api/v1/plano-profit`                                                        | Cria novo plano profit                           | plano_profit/index.js           |
| 89  | PUT    | `/api/v1/plano-profit/:id`                                                    | Atualiza plano profit                            | plano_profit/index.js           |
| 90  | DELETE | `/api/v1/plano-profit/:id`                                                    | Deleta plano profit                              | plano_profit/index.js           |
| 91  | GET    | `/api/v1/plano-profit/buscar/nome/:nome`                                      | Busca planos profit por nome                     | plano_profit/index.js           |
| 92  | GET    | `/api/v1/plano-profit/buscar/produto/:produto_id`                             | Busca planos profit por produto                  | plano_profit/index.js           |
| 93  | GET    | `/api/v1/plano-profit/stats/resumo`                                           | Estatísticas dos planos profit                   | plano_profit/index.js           |

---

## 🟡 Endpoints Acessíveis por Traders (+ Admins)

Estes endpoints requerem JWT válido mas **não** exigem `perfil === 'admin'`. Qualquer usuário autenticado acessa.

| #   | Método | Rota                                                            | Descrição                                      | Arquivo                   |
| --- | ------ | --------------------------------------------------------------- | ---------------------------------------------- | ------------------------- |
| T1  | GET    | `/api/v1/solicitacao-saque/elegibilidade`                       | Trader verifica sua elegibilidade para saque   | solicitacao_saque.js      |
| T2  | GET    | `/api/v1/solicitacao-saque/ciclos`                              | Trader lista seus próprios ciclos de pagamento | solicitacao_saque.js      |
| T3  | GET    | `/api/v1/solicitacao-saque/minhas`                              | Trader lista suas próprias solicitações        | solicitacao_saque.js      |
| T4  | POST   | `/api/v1/solicitacao-saque`                                     | Trader registra intenção de saque              | solicitacao_saque.js      |
| T5  | GET    | `/api/v1/solicitacao-saque/:id`                                 | Trader busca uma solicitação específica        | solicitacao_saque.js      |
| T6  | GET    | `/api/v1/solicitacao-saque/:id/nota-fiscal`                     | Trader faz download da própria nota fiscal     | solicitacao_saque.js      |
| T7  | POST   | `/api/v1/solicitacao-saque/:id/nota-fiscal`                     | Trader faz upload da nota fiscal               | solicitacao_saque.js      |
| T8  | POST   | `/api/v1/solicitacao-saque/:id/marcar-notificado`               | Trader marca que foi notificado da aprovação   | solicitacao_saque.js      |
| T9  | POST   | `/api/v1/solicitacao-saque/:id/marcar-notificado-reprovacao-nf` | Trader marca que foi notificado da reprovação  | solicitacao_saque.js      |
| T10 | GET    | `/api/v1/trader-profile/me`                                     | Trader consulta próprio perfil                 | trader_profile.js         |
| T10 | PUT    | `/api/v1/trader-profile/me`                                     | Trader atualiza próprio perfil                 | trader_profile.js         |
| T11 | GET    | `/api/v1/trader-profile/regulamento`                            | Trader verifica se aceitou o regulamento       | trader_profile.js         |
| T12 | PATCH  | `/api/v1/trader-profile/regulamento`                            | Trader registra aceite do regulamento          | trader_profile.js         |
| T13 | GET    | `/api/v1/traders-mesa/:conta/ciclos`                            | Trader consulta ciclos da própria conta        | traders_mesa.js           |
| T14 | GET    | `/api/v1/traders-mesa/:conta/pnl-diario`                        | Trader consulta PnL diário da própria conta    | traders_mesa.js           |
| T15 | GET    | `/api/v1/traders-mesa-avaliacao/:conta/avaliacao`               | Trader consulta própria avaliação              | traders_mesa_avaliacao.js |
| T16 | GET    | `/api/v1/traders-mesa-avaliacao/:conta/ciclos`                  | Trader consulta próprios ciclos de avaliação   | traders_mesa_avaliacao.js |

---

## 🌐 Endpoints Públicos (sem autenticação)

Estes endpoints **não exigem JWT**. São acessíveis por qualquer cliente.

| #   | Método | Rota                                        | Descrição                                           | Arquivo / Localização |
| --- | ------ | ------------------------------------------- | --------------------------------------------------- | --------------------- |
| P1  | POST   | `/api/v1/auth/login`                        | Autenticação — retorna access_token e refresh_token | auth.js               |
| P2  | POST   | `/api/v1/auth/refresh`                      | Renova par de tokens via refresh_token (rotation)   | auth.js               |
| P3  | POST   | `/api/v1/auth/logout`                       | Invalida o refresh_token do usuário                 | auth.js               |
| P4  | GET    | `/`                                         | Informações gerais da API                           | app.js                |
| P5  | GET    | `/health`                                   | Health check do serviço                             | app.js                |
| P6  | GET    | `/docs/*`                                   | Documentação Swagger (UI + JSON spec)               | @fastify/swagger-ui   |
| P7  | POST   | `/api/v1/vendas/webhook/guru`               | Webhook de vendas — plataforma Guru                 | vendas/webhooks.js    |
| P8  | POST   | `/api/v1/vendas/webhook/guru-treinamentos`  | Webhook de vendas — Guru Treinamentos               | vendas/webhooks.js    |
| P9  | POST   | `/api/v1/vendas/webhook/guru-tech`          | Webhook de vendas — Guru Tech                       | vendas/webhooks.js    |
| P10 | POST   | `/api/v1/vendas/webhook/eduzz-treinamentos` | Webhook de vendas — Eduzz Treinamentos              | vendas/webhooks.js    |
| P11 | POST   | `/api/v1/vendas/webhook/eduzz-tech`         | Webhook de vendas — Eduzz Tech                      | vendas/webhooks.js    |
| P12 | POST   | `/api/v1/vendas/webhook/woocommerce`        | Webhook de vendas — WooCommerce                     | vendas/webhooks.js    |

> **Segurança dos webhooks:** Apesar de públicos (sem JWT), os webhooks validam autenticidade via token/HMAC proprietário de cada plataforma.

### 1. **Auditoria & Logs** (3 endpoints)

Monitoramento de ações administrativas e histórico de auditoria.

### 2. **Integração Nelogica** (7 endpoints)

Gerenciamento de contas e mesas proprietárias na plataforma Nelogica (broker).

### 3. **RPA (Robôs de Automação)** (4 endpoints)

Upload, download e gerenciamento de scripts RPA para trading automático.

### 4. **Solicitação de Saque - Gestão** (11 endpoints)

Aprovação, rejeição, pagamento e controle admin das solicitações.

### 5. **Testes de Integração** (2 endpoints)

Criação e listagem de testes de mesa para integração com Canário Dashboard.

### 6. **Traders da Mesa Proprietária - Gestão** (3 endpoints)

CRUD administrativo dos traders cadastrados na mesa.

### 7. **Avaliação de Traders - Processamento** (3 endpoints)

Disparar processamentos e ver todos os snapshots ativos.

### 8. **Ciclos de Pagamento** (10 endpoints)

Gerenciamento de pagamentos: aprovar, pagar, cancelar, dashboards.

### 9. **Permissões de Usuários** (4 endpoints)

Controle granular de acesso a telas/funcionalidades.

### 10. **Vendas & Produtos** (9 endpoints)

CRUD completo de vendas, controle de status, reset de testes.

### 11. **Mesa de Vendas** (6 endpoints)

Visão administrativa: vendas aprovadas/inativas, ativação.

### 12. **Logs de Vendas** (4 endpoints)

Rastreamento detalhado de eventos e transações de vendas.

### 13. **Estatísticas & Relatórios** (10 endpoints)

Dashboards executivos, relatórios financeiros, geográficos, temporais.

### 14. **Planos & Produtos** (15 endpoints)

CRUD de planos padrão e Profit, busca e estatísticas.

### 1. **Auditoria & Logs** (3 endpoints)

Monitoramento de ações administrativas e histórico de auditoria.

### 2. **Integração Nelogica** (7 endpoints)

Gerenciamento de contas e mesas proprietárias na plataforma Nelogica (broker).

### 3. **RPA (Robôs de Automação)** (4 endpoints)

Upload, download e gerenciamento de scripts RPA para trading automático.

### 4. **Solicitação de Saque** (16 endpoints)

**Fluxo crítico de retirada de lucros pelos traders:**

- Verificação de elegibilidade
- Registro de intenção
- Aprovação/rejeição
- Upload de documentação (nota fiscal)
- Processamento de pagamento
- Notificações

### 5. **Testes de Integração** (2 endpoints)

Criação e listagem de testes de mesa para integração com Canário Dashboard.

### 6. **Traders da Mesa Proprietária** (19 endpoints)

**Gerenciamento de operadores internos:**

- Ciclagem de pagamentos (períodos de avaliação)
- Processamento de P&L (ganho/perda)
- Avaliação de performance
- Dashboard de pagamentos pendentes

---

## 🎯 Categorias de Endpoints Admin (por domínio de negócio)

## 🔒 Como Funciona a Proteção

### Middleware `requireAdmin`

```javascript
// Localização: src/middleware/requireAdmin.js
async function requireAdmin(request, reply) {
  if (!request.user) {
    return reply.status(401).send({ error: "Autenticação requerida" });
  }

  const normalizedPerfil = request.user.perfil?.toLowerCase?.() ?? "";

  if (normalizedPerfil !== "admin") {
    return reply.status(403).send({
      error:
        "Acesso negado. Apenas administradores podem acessar este endpoint.",
      code: "ADMIN_REQUIRED",
      userPerfil: request.user.perfil,
    });
  }
}
```

### Aplicação em Rotas

```javascript
// Padrão em todos os 107 endpoints
fastify.get("/endpoint", {
  onRequest: [requireAdmin],  // ← Middleware aplicado
  schema: {
    description: "[ADMIN] Descrição da rota",
    // ... resto do schema
  },
  async (request, reply) => {
    // handler
  }
});
```

---

## ✅ Cobertura de Testes

**314 testes Jest automatizados cobrindo:**

**Para endpoints admin-only (93):** 401 sem token | 403 com token trader | admin passa

**Para endpoints de trader (14):** 401 sem token | trader passa | admin passa

**Execução:** `npm test` (~2 segundos)

---

## 🚀 Uso em Produção

### Fluxo de Requisição

```
1. Cliente faz POST /api/v1/vendas/mesa/ativar
2. Global Hook verifyJWT valida Authorization header
3. verifyJWT injeta request.user (id, email, nome, perfil, ativo)
4. Middleware requireAdmin verifica request.user.perfil === 'admin'
5. Se admin: executa handler | Se não-admin: 403 Forbidden
```

### Tokens Esperados

```json
{
  "sub": "admin@empresa.com",
  "id": 1,
  "nome": "Administrador",
  "perfil": "admin",
  "ativo": true,
  "type": "access"
}
```

---

## 📌 Notas Importantes

1. **Rotas públicas** (sem autenticação): ver tabela P1–P12 acima.

2. **Rotas de trader** não têm `requireAdmin` mas ainda exigem JWT válido (o hook global `verifyJWT` cobre todas as rotas não-públicas).

3. **Case-insensitive:** Perfil é normalizado com `toLowerCase()`

4. **Tokens expirados:** Retornam 401 via hook global

5. **Rotas órfãs:** Alguns arquivos existem com `requireAdmin` mas não estão registrados em `app.js`:
   - `vendas/admin-logs.js`
   - `vendas/webhooks-logs.js`
   - `vendas/canario-integration.js`
   - `vendas/debug/index.js`

---

**Última atualização:** 16 de abril de 2026  
**Status:** ✅ 100% implementado e testado
