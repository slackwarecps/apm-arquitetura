# apm-arquitetura

Apm de Arquitetura — contexto, skills, agents e MCP compartilhados da vertical **Arquitetura** da FabaoCorp, distribuidos como plugin do Claude Code para todas as squads que instalarem este apm.

## Sobre a FabaoCorp

Empresa com mais de 200 projetos organizados em 4 verticais: Banking, Seguros, Financeiro e Arquitetura. Cada vertical tem varias squads, e cada squad cuida de um ou mais projetos (ex.: a squad `pix-pf`, na vertical Banking, cuida de 9 microsservicos).

## Stack padrao

- Backends e BFFs: Java Spring Boot
- Frontend web: Angular
- Mobile: Android e iOS nativos

## O que este apm distribui

- `skills/revisao-arquitetural` — checklist de revisao arquitetural (acoplamento, contratos de API, resiliencia, observabilidade, seguranca)
- `skills/adr` — geracao de Architecture Decision Records no formato padrao da empresa
- `agents/arquiteto-revisor` — agente para revisoes de arquitetura mais profundas, multi-arquivo
- `.mcp.json` — servidor MCP `fabaocorp-arquitetura-docs` (placeholder nesta POC — aponta para um pacote fictício `@fabaocorp/mcp-arquitetura-docs` que ainda nao existe; substituir pelo servidor real antes de qualquer uso fora da POC)

## Distribuicao

Este plugin e publicado no marketplace local `repo-apm` (`.claude-plugin/marketplace.json`) e, no modelo real, seria versionado no repositorio https://github.com/slackwarecps/apm-arquitetura para ser instalado por qualquer squad da empresa.
