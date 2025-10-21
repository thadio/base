---
document: pilha-tecnologica.md
version: 0.1.0
last_update: 2025-10-21
maintainer: thadio
status: active
---
# Pilha Tecnológica

## Linguagens e Frameworks

- **Frontend (Apresentação)** — HTML5, CSS3 e Bootstrap 5 como base responsiva. JavaScript puro ou jQuery para interações pontuais. Chart.js e DataTables.js suportam dashboards, filtros e relatórios. Compiladores ou bundlers não são utilizados para manter compatibilidade com o ambiente compartilhado do HostGator.
- **Backend (Lógica de Negócio)** — PHP 8.x executando sob Apache 2.4 em padrão MVC. Utilizar PDO com prepared statements para acesso seguro ao MySQL. Frameworks leves (Slim, Lumen) são opcionais e devem ser incluídos via Composer sem demandar processos residentes.
- **Scripts e Agendamentos** — Automatizações rodam como scripts PHP disparados manualmente ou por Cron Jobs do cPanel, respeitando limites do servidor compartilhado (sem processos em background permanentes).
- **Mobile** — Sem aplicação dedicada. O layout responsivo cobre acesso mobile via navegadores modernos.

## Infraestrutura e Serviços

- **Hospedagem** — HostGator (servidor compartilhado) com Apache 2.4, PHP 8.x e MySQL 8.x. Não há suporte a containers Docker, Node.js, WebSockets persistentes ou serviços residentes.
- **Gestão** — Administração via cPanel: gerenciamento de arquivos, cron jobs, backups e SSL Let's Encrypt. Deploy por upload (FTP/SFTP) ou Git Deploy nativo do painel.
- **Banco de Dados** — MySQL provisionado pelo cPanel. O acesso administrativo ocorre via phpMyAdmin ou túneis seguros. Configurações ficam centralizadas em `app/config/db.php`, fora do `public_html`.
- **Segurança Aplicacional** — Sanitização de entradas com PDO, CSRF tokens nas rotas sensíveis, armazenamento de senhas com `password_hash` (bcrypt/sodium) e logs de auditoria em tabela dedicada.

## Qualidade e Observabilidade

- **Testes** — PHPUnit para testes unitários. Testes de interface executados manualmente antes do deploy, dado que o ambiente não permite pipelines automatizados.
- **Monitoramento** — Logs de aplicação armazenados no MySQL. Acesso ao log de erros do Apache pelo cPanel para identificação de falhas de execução.
- **Resiliência** — Backups automáticos diários habilitados no HostGator e exportação semanal do banco (`mysqldump` via painel ou script PHP agendado).

## Dependências Externas

- **Bibliotecas PHP** — Composer gerencia pacotes como PHPMailer (SMTP), Slim Framework (opcional) e TCPDF/FPDF para relatórios.
- **Bibliotecas Frontend** — Bootstrap 5, Chart.js, DataTables.js, Font Awesome (CDN). Dependências devem estar em `/assets` ou servidas via CDN para simplificar o deploy.
- **Serviços de Terceiros** — SMTP autenticado para e-mails transacionais (HostGator ou provedor externo). Qualquer integração adicional precisa operar via chamadas HTTP/HTTPS síncronas devido à ausência de workers persistentes.
