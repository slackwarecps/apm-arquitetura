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
- `skills/backend-core-review/SKILL.md` — roda `mvn test`/`mvn verify` num backend Java/Spring Boot e valida cobertura de testes >= 80% via JaCoCo
- `CLAUDE.md` — gerado a partir do `apm.yml`/`.apm/` pela APM CLI, para consumo direto pelo Claude Code

## Distribuicao

Este apm segue o formato da **APM CLI** (mesmo padrao usado em `apm-core-security`), publicado no repositorio https://github.com/slackwarecps/apm-arquitetura, para ser instalado por qualquer squad da empresa independente da CLI de IA que usa.
