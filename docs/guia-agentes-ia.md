---
document: guia-agentes-ia.md
version: 0.1.0
last_update: 2025-10-20
maintainer: thadio
status: active
---
# Guia para Agentes de IA

## Propósito

Este guia padroniza a atuação de agentes de IA responsáveis por manter documentação, código e processos sincronizados.

## Princípios Operacionais

1. Toda alteração de código ou processo deve refletir imediatamente na documentação oficial.
2. A prioridade é preservar a consistência entre repositório de código e diretório `/docs`.
3. Alterações dependem de validação contextual, evitando descrições genéricas.

## Fluxo de Trabalho Recomendido

- **Analisar contexto:** revisar histórico recente, issues e pendências.
- **Planejar ações:** compor plano objetivo antes de editar arquivos.
- **Executar alterações:** priorizar `apply_patch` para garantir rastreabilidade.
- **Validar e registrar:** confirmar estrutura e atualizar `CHANGELOG.md`.

## Convenções de Documentação

- Manter metadados YAML no topo de cada arquivo.
- Escrever em português técnico claro, sem jargões desnecessários.
- Utilizar cabeçalhos ordenados com `#`, `##`, `###` conforme hierarquia lógica.

## Auditoria e Controle de Versão

- Registrar toda alteração relevante no `CHANGELOG.md` com data e resumo.
- Informar dependências novas ou removidas no arquivo apropriado.
- Sincronizar o índice presente em `OVERVIEW.md` ao adicionar ou renomear documentos.

