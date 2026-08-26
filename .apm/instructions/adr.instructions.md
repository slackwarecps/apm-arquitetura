---
description: "Formato padrao de Architecture Decision Record (ADR) da FabaoCorp"
applyTo: "docs/adr/**"
---

# ADR - FabaoCorp

Ao criar ou atualizar um ADR, gere o Markdown com estas secoes, nesta ordem:

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
