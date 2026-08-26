# apm-arquitetura

Apm de Arquitetura — contexto e regras compartilhadas da vertical **Arquitetura** da FabaoCorp, distribuidos via **APM CLI** (`apm.yml` + `.apm/instructions/`) para qualquer CLI de IA usada pelas squads (Claude Code, GitHub Copilot CLI, Gemini CLI).

## Sobre a FabaoCorp

Empresa com mais de 200 projetos organizados em 4 verticais: Banking, Seguros, Financeiro e Arquitetura. Cada vertical tem varias squads, e cada squad cuida de um ou mais projetos (ex.: a squad `pix-pf`, na vertical Banking, cuida de 9 microsservicos).

## Stack padrao

- Backends e BFFs: Java Spring Boot
- Frontend web: Angular
- Mobile: Android e iOS nativos

## O que este apm distribui

- `apm.yml` — manifesto: metadados do pacote e `scripts` (comandos utilitarios)
- `.apm/instructions/diretrizes-gerais.instructions.md` — diretrizes gerais de arquitetura (stack, comunicacao entre servicos, contratos, resiliencia, observabilidade), aplicado a `**/*`
- `.apm/instructions/lgpd-dados-pessoais.instructions.md` — regra de LGPD: nunca logar CPF/RG/CNPJ/e-mail/telefone em texto claro, sempre mascarar/criptografar antes de logar, aplicado a `**/*.java,**/*.ts,**/*.kt,**/*.swift`
- `.apm/instructions/revisao-arquitetural.instructions.md` — checklist de revisao arquitetural (acoplamento, contratos de API, resiliencia, observabilidade, seguranca), aplicado a `**/*.java,**/*.ts,**/*.kt,**/*.swift`
- `.apm/instructions/adr.instructions.md` — template de Architecture Decision Record, aplicado a `docs/adr/**`
- `skills/backend-core-review/SKILL.md` — roda `mvn test`/`mvn verify` num backend Java/Spring Boot e valida cobertura de testes >= 80% via JaCoCo

## Distribuicao multi-CLI: AGENTS.md como fonte canonica

`AGENTS.md` e a fonte canonica gerada pela APM CLI a partir de `.apm/instructions/` — e o formato lido nativamente por GitHub Copilot e por qualquer ferramenta compativel com o padrao `AGENTS.md`. `GEMINI.md` e um arquivo fino gerado pela APM CLI que so faz `@./AGENTS.md` (import).

`CLAUDE.md` **e mantido manualmente** com o mesmo import (`@./AGENTS.md`): a APM CLI 0.28.0 nao gera CLAUDE.md como import para o target `claude` (sempre inlina o conteudo inteiro), entao **nunca rode `apm compile --target claude` (nem `--all`) neste repo** — isso sobrescreveria o `CLAUDE.md` com conteudo duplicado. Para recompilar depois de mudar `.apm/instructions/`, use:

```
apm compile --target agents,gemini --clean
```

Este apm segue o formato da **APM CLI**, publicado no repositorio https://github.com/slackwarecps/apm-arquitetura, para ser instalado por qualquer squad da empresa independente da CLI de IA que usa.
