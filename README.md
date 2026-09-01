# ⚙️ Nginx Status Monitor

> Script Bash para verificação automatizada do serviço Nginx, geração de logs e publicação de um relatório HTML de status.

[![Status](https://img.shields.io/badge/status-projeto%20técnico-blue)](#status)
[![Stack](https://img.shields.io/badge/stack-Bash%20%7C%20Linux%20%7C%20Nginx-black)](#tecnologias)
[![Automação](https://img.shields.io/badge/automação-Cron-orange)](#automação)

## Sobre o projeto

O **Nginx Status Monitor** é um projeto de infraestrutura voltado ao monitoramento simples de disponibilidade do serviço Nginx em ambientes Linux.

O script verifica o estado do serviço, registra o resultado em arquivos de log e gera uma página HTML com o histórico das verificações. A execução pode ser automatizada por meio do Cron.

O projeto representa uma base didática para práticas de **Linux, Bash scripting, observabilidade e administração de servidores web**.

## Funcionalidades

- 🔎 Verificação do status do Nginx via `systemctl`
- 📝 Registro de status ativo e inativo
- 🕐 Registro com data e hora
- 🌐 Geração de relatório HTML
- 🔄 Atualização periódica do relatório
- ⏱️ Automação com Cron
- 📁 Organização dos logs em diretório próprio
- 🐧 Execução em ambiente Linux

## Tecnologias

- Linux
- Bash
- Nginx
- systemd / `systemctl`
- Cron
- HTML

## Fluxo

```text
Cron
 │
 ▼
Script Bash
 │
 ├── systemctl → verifica Nginx
 │
 ├── logs → registra resultado
 │
 └── HTML → gera relatório
              │
              ▼
        Nginx /var/www/html
```

## Requisitos

- Servidor Linux
- Bash
- Nginx instalado e configurado
- `systemctl` disponível
- Permissão para escrever nos diretórios utilizados pelo script
- Cron, caso a execução automática seja desejada

## Configuração

A implementação original utiliza caminhos de trabalho específicos para logs e publicação do HTML. Em uma implantação real, recomenda-se parametrizar esses caminhos de acordo com o ambiente.

Exemplos de parâmetros utilizados pelo projeto:

```text
log_dir
log_ativo
log_inativo
html_output
```

## Execução

Torne o script executável:

```bash
chmod +x verificar_nginx.sh
```

Execute manualmente:

```bash
./verificar_nginx.sh
```

O relatório poderá ser disponibilizado pelo servidor web conforme o diretório configurado para publicação.

## Automação com Cron

Para executar a verificação a cada cinco minutos:

```bash
crontab -e
```

Adicione uma entrada equivalente a:

```cron
*/5 * * * * /caminho/para/seu/script/verificar_nginx.sh
```

## Logs

O projeto trabalha com registros separados para diferentes estados do serviço, permitindo acompanhar o histórico das verificações.

Também é possível direcionar erros de execução para um arquivo específico:

```bash
./verificar_nginx.sh 2>> /caminho/para/logs/error.log
```

## Segurança e permissões

O script pode exigir permissões administrativas dependendo da configuração do servidor. Evite conceder privilégios excessivos ao usuário de execução.

A concessão de `sudo` sem senha para comandos administrativos deve ser avaliada cuidadosamente e, quando necessária, limitada ao menor conjunto de comandos possível.

Não coloque senhas, tokens, chaves privadas ou outras credenciais no script ou no repositório.

## Possíveis problemas

### HTML não é atualizado

Verifique:

- permissões do diretório de saída;
- existência do diretório de logs;
- execução manual do script;
- caminho configurado para publicação;
- erros registrados no log.

### Logs vazios

Confirme se o script possui permissão de escrita e se o `systemctl` consegue consultar o serviço Nginx.

### `systemctl` exige privilégios

Verifique as permissões do usuário e as políticas de `sudo` do ambiente. Evite liberar privilégios administrativos de forma ampla.

## Estrutura esperada

A estrutura exata pode variar conforme os arquivos presentes no ambiente de execução. Conceitualmente:

```text
Project_nginx/
├── verificar_nginx.sh
├── logs/
│   ├── nginx_status_ativo.log
│   ├── nginx_status_inativo.log
│   └── error.log
├── status_nginx.html
└── README.md
```

## Roadmap

### V1 — Monitoramento básico

- [x] Verificação do Nginx
- [x] Logs de status
- [x] Relatório HTML
- [x] Automação por Cron

### V2 — Observabilidade

- [ ] Histórico visual de disponibilidade
- [ ] Indicadores de uptime
- [ ] Dashboard mais completo
- [ ] Rotação automática de logs
- [ ] Alertas de indisponibilidade

### V3 — Infraestrutura

- [ ] Configuração por arquivo `.env` ou equivalente seguro
- [ ] Execução como serviço dedicado
- [ ] Integração com ferramentas de monitoramento
- [ ] Health checks
- [ ] Métricas estruturadas

## Status

🔧 **Projeto técnico / laboratório de infraestrutura**

O projeto funciona como base para estudos de automação, administração Linux e monitoramento de serviços web.

## Licenciamento

As condições de uso devem ser observadas conforme a licença eventualmente definida no repositório.

## Autor

Desenvolvido por **Bruno Silva**.

GitHub: `eubruno-coder`

---

**Projeto:** Nginx Status Monitor  
**Categoria:** Infraestrutura / Linux / Automação  
**Status:** Projeto técnico em evolução
