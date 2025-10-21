---
document: publicacao-e-deploy.md
version: 0.1.0
last_update: 2025-10-21
maintainer: thadio
status: active
---
# Publicação e Deploy

## Pipeline de Build (Local)

1. Executar `composer install --no-dev` em ambiente local para garantir dependências PHP e gerar o diretório `vendor/`.
2. Rodar `phpunit` para validar testes automatizados disponíveis.
3. Revisar assets estáticos (`/assets/css`, `/assets/js`) e minificar arquivos críticos manualmente, quando necessário.
4. Atualizar arquivo `app/config/app_config.php` com chaves e endpoints corretos para o ambiente de destino.

> Observação: não há pipeline CI/CD automatizado devido às restrições do HostGator em servidores compartilhados.

## Ambientes

| Ambiente | URL                                    | Branch             | Observações |
|----------|----------------------------------------|--------------------|-------------|
| Desenvolvimento | Localhost com Apache + PHP 8.x | `develop` (local)  | Utiliza `.env.local` com banco MySQL local. |
| Homologação     | Subdomínio `staging.dominio.com` (opcional) | `staging` (mirror) | Deploy manual para validação com dados mascarados. |
| Produção        | `https://dominio.com`           | `main`             | Requer aprovação do responsável e janela de manutenção curta. |

## Fluxo de Deploy no HostGator

1. **Empacotamento** — Gerar arquivo `.zip` contendo `public_html` (frontend) e `app`, mantendo `config/` fora da raiz pública. Excluir diretórios de desenvolvimento.
2. **Upload** — Utilizar File Manager do cPanel, FTP/SFTP ou `git push` para o repositório configurado no servidor.
3. **Extração** — Descompactar o pacote dentro do `public_html`, confirmando permissões `644` para arquivos e `755` para diretórios.
4. **Configuração** — Ajustar credenciais em `app/config/db.php` com dados do banco criado no cPanel e garantir que `.htaccess` esteja ativo para reescrita de URL.
5. **Banco de Dados** — Importar migrações ou dumps via phpMyAdmin. Para atualizações incrementais, executar scripts SQL versionados em `/docs/migrations`.
6. **Verificação** — Validar rotas críticas, envio de e-mails (PHPMailer configurado via SMTP) e geração de relatórios (FPDF/TCPDF).

## Controles Operacionais

- **Backups** — Habilitar backup diário no HostGator. Antes de cada deploy, exportar banco (`mysqldump` via cPanel) e baixar snapshot dos arquivos críticos.
- **Logs** — Monitorar `error_log` pelo cPanel e registrar atividades de auditoria na tabela `app_audits`.
- **Limitações** — Sem suporte a Docker, Node.js, filas ou serviços em background. Qualquer tarefa agendada deve ser configurada como Cron Job PHP.

## Procedimentos de Rollback

1. Restaurar snapshot de arquivos através da ferramenta de backup do HostGator ou upload do pacote anterior.
2. Reimportar o dump SQL mais recente para o banco de produção.
3. Limpar cache de navegador e validar endpoints principais.
4. Registrar o incidente no `CHANGELOG.md` e comunicar stakeholders.
