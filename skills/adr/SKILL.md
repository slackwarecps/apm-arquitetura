---
name: adr
description: Cria ou atualiza um Architecture Decision Record (ADR) no formato padrao da FabaoCorp para registrar decisoes tecnicas relevantes de um projeto/squad. Use quando o usuario pedir para "documentar uma decisao de arquitetura", "criar um ADR" ou similar.
---

# ADR - FabaoCorp

Gere o ADR em Markdown com estas secoes, nesta ordem:

```
# ADR NNNN: <titulo curto da decisao>

- Status: proposta | aceita | substituida
- Vertical: <Banking | Seguros | Financeiro | Arquitetura>
- Squad: <nome da squad>
- Data: <data absoluta>

## Contexto
<qual problema motivou a decisao>

## Decisao
<o que foi decidido>

## Consequencias
<impactos positivos e negativos, incluindo em outras squads/servicos se houver>
```

Numere sequencialmente a partir do ultimo ADR existente na pasta `docs/adr/` do projeto, se houver. Nao presuma decisoes que o usuario nao descreveu.
