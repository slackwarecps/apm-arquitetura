# apm-arquitetura

Pacote de governança e padronização arquitetural da vertical **Arquitetura** da FabaoCorp. Seu objetivo é fornecer contexto, regras e ferramentas compartilhadas para orientar os agentes de IA utilizados pelas squads, independentemente da CLI adotada.

O conteúdo é distribuído via **APM CLI** (`apm.yml` + `.apm/instructions/`) e pode ser consumido por Claude Code, GitHub Copilot CLI, Gemini CLI e outras ferramentas compatíveis.

## Sobre a FabaoCorp

Empresa com mais de 200 projetos organizados em 4 verticais: Banking, Seguros, Financeiro e Arquitetura. Cada vertical tem varias squads, e cada squad cuida de um ou mais projetos (ex.: a squad `pix-pf`, na vertical Banking, cuida de 9 microsservicos).

## Stack padrao

- Backends e BFFs: Java Spring Boot
- Frontend web: Angular
- Mobile: Android e iOS nativos

## O que este apm distribui

Este projeto não é uma aplicação de negócio: é um pacote de referência e governança técnica para padronizar decisões e revisões arquiteturais nos projetos da empresa.

- `apm.yml` — manifesto: metadados do pacote e `scripts` (comandos utilitarios)
- `.apm/instructions/diretrizes-gerais.instructions.md` — diretrizes gerais de arquitetura (stack, comunicacao entre servicos, contratos, resiliencia, observabilidade), aplicado a `**/*`
- `.apm/instructions/lgpd-dados-pessoais.instructions.md` — regra de LGPD: nunca logar CPF/RG/CNPJ/e-mail/telefone em texto claro, sempre mascarar/criptografar antes de logar, aplicado a `**/*.java,**/*.ts,**/*.kt,**/*.swift`
- `.apm/instructions/revisao-arquitetural.instructions.md` — checklist de revisao arquitetural (acoplamento, contratos de API, resiliencia, observabilidade, seguranca), aplicado a `**/*.java,**/*.ts,**/*.kt,**/*.swift`
- `.apm/instructions/adr.instructions.md` — template de Architecture Decision Record, aplicado a `docs/adr/**`
- `skills/backend-sboot-review/SKILL.md` — roda `mvn test`/`mvn verify` num backend Java/Spring Boot e valida cobertura de testes >= 80% via JaCoCo

## Distribuição do MCP remoto

O `apm.yml` distribui a configuração do MCP `meu-mcp-remoto` para Claude, Codex, Gemini e Copilot. A configuração atual usa transporte SSE e o endpoint `http://192.168.1.100:3030/sse`.

Esse endereço é privado e usa HTTP: os clientes precisam estar na mesma rede ou conectados à VPN que alcança a VPS. Para acesso pela internet, publique o serviço atrás de um domínio com HTTPS, mantenha o transporte compatível com o servidor e atualize o `url` no `apm.yml`.

### Pré-requisito: obter e configurar o token

Antes de instalar, obtenha o `MCP_SERVER_TOKEN` com o responsável pela configuração do MCP na VPS. Esse token é obrigatório para o servidor aceitar as requisições autenticadas. Sem ele, os clientes não conseguirão se conectar ao MCP.

O token não deve ser colocado diretamente no `apm.yml`, commitado ou compartilhado em logs. Disponibilize-o apenas no ambiente onde o APM será executado:

```bash
export MCP_SERVER_TOKEN='<token-fornecido-pelo-responsavel-do-mcp>'
apm install
```

Em uma VPS, configure essa variável no mecanismo de secrets do serviço que executa o agente (por exemplo, systemd, Docker Compose ou outro gerenciador de secrets) e reinicie o serviço após alterar o token. A variável precisa estar disponível tanto durante a instalação quanto no momento em que o cliente iniciar a conexão, conforme o cliente de IA utilizado.

Para validar sem escrever arquivos, use:

```bash
MCP_SERVER_TOKEN='seu-token' apm install --dry-run
```

Após uma instalação bem-sucedida, versione o `apm.lock.yaml`. O APM distribuirá a configuração nos arquivos nativos de cada cliente; ele não gerencia o processo do MCP, o proxy reverso, o TLS ou o firewall da VPS. Consulte o [guia oficial de instalação de servidores MCP](https://microsoft.github.io/apm/guides/mcp-servers/) para detalhes sobre transportes, targets e credenciais.

## Distribuicao multi-CLI: AGENTS.md como fonte canonica

`AGENTS.md` e a fonte canonica gerada pela APM CLI a partir de `.apm/instructions/` — e o formato lido nativamente por GitHub Copilot e por qualquer ferramenta compativel com o padrao `AGENTS.md`. `GEMINI.md` e um arquivo fino gerado pela APM CLI que so faz `@./AGENTS.md` (import).

`CLAUDE.md` **e mantido manualmente** com o mesmo import (`@./AGENTS.md`): a APM CLI 0.28.0 nao gera CLAUDE.md como import para o target `claude` (sempre inlina o conteudo inteiro), entao **nunca rode `apm compile --target claude` (nem `--all`) neste repo** — isso sobrescreveria o `CLAUDE.md` com conteudo duplicado. Para recompilar depois de mudar `.apm/instructions/`, use:

```
apm compile --target agents,gemini --clean
```

Este apm segue o formato da **APM CLI**, para ser instalado por qualquer squad da empresa independentemente da CLI de IA utilizada.

Consulte a [documentação oficial do APM CLI](https://microsoft.github.io/apm/) para conhecer a instalação, os comandos e o funcionamento da ferramenta. O código-fonte e as referências da CLI estão disponíveis no [repositório oficial do APM](https://github.com/microsoft/apm).

Este pacote está publicado no [repositório `slackwarecps/apm-arquitetura`](https://github.com/slackwarecps/apm-arquitetura).
