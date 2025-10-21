---
document: funcionalidades-e-regras.md
version: 0.1.0
last_update: 2025-10-21
maintainer: thadio
status: active
---
# Funcionalidades e Regras de Negócio

## Módulos e Componentes
- **Nome do módulo** — resumo funcional, integrações e dependências principais.
- **Tela ou fluxo** — públicos, jornadas e validações obrigatórias.
- **Dashboards Operacionais** — consolida gráficos (Chart.js) e tabelas (DataTables.js) com filtros por período, área e status. Dados alimentados por consultas otimizadas em MySQL com views específicas.
- **Relatórios e Exportações** — geração de PDF (TCPDF/FPDF) e CSV diretamente no PHP, sem dependências de serviços externos.
- **Administração** — controle de usuários, perfis e trilhas de auditoria registradas em tabela dedicada.

## Regras de Negócio Atuais

| Regra | Descrição | Fonte | Impacto |
|-------|-----------|-------|---------|
| RB-001 | Resumir a regra e o comportamento esperado. | Documento ou equipe | Áreas afetadas |
| RB-002 | Apenas usuários autenticados; sessões expiram após 30 minutos de inatividade. | Segurança | Todas as áreas |

## Regras Pendentes de Validação

- Listar requisitos em análise ou aguardando homologação.

## Anexos e Referências

- Link para protótipos, diagramas BPMN ou especificações de API relacionadas.