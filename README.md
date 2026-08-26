# apm-arquitetura

Apm de Arquitetura — contexto e regras compartilhadas da vertical **Arquitetura** da FabaoCorp, distribuidos via **APM CLI** (`apm.yml` + `.apm/instructions/`) para qualquer CLI de IA usada pelas squads (Claude Code, GitHub Copilot CLI, Gemini CLI).

## Sobre a FabaoCorp

Empresa com mais de 200 projetos organizados em 4 verticais: Banking, Seguros, Financeiro e Arquitetura. Cada vertical tem varias squads, e cada squad cuida de um ou mais projetos (ex.: a squad `pix-pf`, na vertical Banking, cuida de 9 microsservicos).

## Stack padrao

- Backends e BFFs: Java Spring Boot
- Frontend web: Angular
- Mobile: Android e iOS nativos

## O que este apm distribui

- `apm.yml` — manifesto: `custom_instructions` (regras globais de arquitetura) e `scripts` (comandos utilitarios)
- `.apm/instructions/revisao-arquitetural.instructions.md` — checklist de revisao arquitetural (acoplamento, contratos de API, resiliencia, observabilidade, seguranca), aplicado a `**/*.java,**/*.ts,**/*.kt,**/*.swift`
- `.apm/instructions/adr.instructions.md` — template de Architecture Decision Record, aplicado a `docs/adr/**`
- `CLAUDE.md` — gerado a partir do `apm.yml`/`.apm/` pela APM CLI, para consumo direto pelo Claude Code

## Distribuicao

Este apm segue o formato da **APM CLI** (mesmo padrao usado em `apm-core-security`), publicado no repositorio https://github.com/slackwarecps/apm-arquitetura, para ser instalado por qualquer squad da empresa independente da CLI de IA que usa.

## Migracao (nota da POC)

Esta vertical usava anteriormente o formato de **plugin do Claude Code** (`.claude-plugin/plugin.json` + `marketplace.json`, `skills/*/SKILL.md`, `agents/*.md`, `.mcp.json`). A migracao para APM CLI resolveu a lacuna de compatibilidade multi-CLI, mas tem um custo: dois recursos exclusivos do formato de plugin foram removidos e ainda **nao tem equivalente** na APM CLI:

- `agents/arquiteto-revisor.md` — subagente dedicado (com tools proprias) para revisoes multi-arquivo mais profundas
- `.mcp.json` — servidor MCP `fabaocorp-arquitetura-docs` compartilhado

As skills `revisao-arquitetural` e `adr` foram convertidas de skill (ativada por descricao) para instructions passivas (`applyTo`), o que muda a semantica: antes eram acionadas sob demanda pelo agente ao reconhecer a intencao do usuario; agora sao sempre carregadas como contexto quando o arquivo/pasta bate no `applyTo`.
