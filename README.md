# Nginx Status Monitor

> Laboratório Bash para consultar o estado do serviço Nginx em Linux, registrar verificações e gerar um relatório HTML.

[![Categoria](https://img.shields.io/badge/categoria-infraestrutura-blue)](#objetivo)
[![Stack](https://img.shields.io/badge/stack-Bash%20%7C%20Linux%20%7C%20Nginx-black)](#tecnologias)
[![Status](https://img.shields.io/badge/status-protótipo%20didático-orange)](#status-atual)

---

## Objetivo

O **Nginx Status Monitor** explora automação de tarefas administrativas em Linux por meio de um script Bash. A proposta é consultar o serviço Nginx, registrar o resultado em arquivos de log e montar uma página HTML simples para consulta.

O projeto serve como exercício de shell scripting, administração de serviços com systemd, permissões de arquivos e geração de relatórios.

## Fluxo pretendido

```text
Execução manual ou agendada
          │
          ▼
     Script Bash
          │
          ├── systemctl is-active nginx
          │
          ├── Registro do resultado
          │      ├── log ativo
          │      └── log inativo
          │
          ▼
    Geração de HTML
          │
          ▼
 Diretório servido pelo Nginx
```

## Tecnologias e conceitos

- Linux
- Bash
- Nginx
- systemd / `systemctl`
- Cron (para agendamento externo)
- Logs em arquivos
- HTML gerado por script

## Estrutura observada

O repositório contém um script principal chamado `Project_nginx` e material de apoio em PDF. O README documenta o propósito e o fluxo pretendido; os caminhos de execução ainda estão associados ao ambiente original de desenvolvimento.

## Execução e ambiente

O script deve ser revisado e adaptado antes de ser executado em outro servidor. Na versão atual, há caminhos absolutos definidos no próprio código:

- diretório de logs: `/home/bruno/projeto_nginx/logs`;
- destino do relatório: `/var/www/html/status_nginx.html`.

Esses caminhos não são portáveis. A escrita no diretório servido pelo Nginx pode exigir permissões específicas.

Para inspecionar o serviço manualmente:

```bash
systemctl is-active nginx
```

Para executar um script Bash após revisar caminhos e permissões:

```bash
chmod +x Project_nginx
./Project_nginx
```

O agendamento por Cron é uma possibilidade de evolução e deve ser configurado somente depois que a execução manual estiver validada no ambiente de destino.

## Estado atual e limitações conhecidas

<badge color="warning">Revisão técnica necessária antes de uso operacional</badge>

A implementação deve ser tratada como protótipo didático, não como monitor de produção. A inspeção do script identificou pontos que precisam ser corrigidos e testados:

- a variável de data/hora é definida dentro da função de verificação, mas também é referenciada fora dela;
- os caminhos de log e publicação estão fixos no código;
- a geração e a movimentação do HTML dependem de permissões do ambiente;
- a criação e a verificação dos arquivos de log precisam ser ordenadas para evitar estados inconsistentes;
- mensagens, tratamento de erros e validação de comandos podem ser fortalecidos;
- não há testes automatizados documentados.

Por isso, o README não declara que a execução agendada ou a publicação do relatório estejam homologadas em um ambiente independente.

## Segurança e operação

- Execute com o menor privilégio possível.
- Não conceda permissões administrativas amplas apenas para facilitar a escrita de arquivos.
- Valide cuidadosamente qualquer regra de `sudoers`.
- Evite inserir credenciais ou dados sensíveis em scripts e logs.
- Restrinja o acesso ao relatório se ele revelar informações sobre a infraestrutura.
- Considere rotação e retenção de logs antes de executar continuamente.

## Roadmap

### V1 — Protótipo de monitoramento
- [x] Consulta do estado do Nginx por `systemctl`
- [x] Separação conceitual de logs por estado
- [x] Geração de relatório HTML

### V1.1 — Correção e portabilidade
- [ ] Corrigir escopo e inicialização das variáveis
- [ ] Parametrizar diretórios e caminhos de saída
- [ ] Adicionar validação de dependências e permissões
- [ ] Tratar falhas de `systemctl` e escrita de arquivos
- [ ] Validar execução manual em uma VM Linux limpa

### V2 — Automação e observabilidade
- [ ] Configurar Cron após validação manual
- [ ] Implementar rotação de logs
- [ ] Adicionar histórico e indicadores de disponibilidade
- [ ] Criar alertas para indisponibilidade
- [ ] Adicionar testes automatizados

## Status atual

**Protótipo didático em evolução.** O repositório demonstra a ideia e os conceitos utilizados, mas requer correções e validação em ambiente limpo antes de ser considerado uma ferramenta operacional.

## Autor

Desenvolvido por **Bruno Silva**.

GitHub: [eubruno-coder](https://github.com/eubruno-coder)

---

**Projeto:** Nginx Status Monitor  
**Categoria:** Infraestrutura / Linux / Automação  
**Linguagem:** Bash  
**Status:** Protótipo didático — revisão técnica pendente
