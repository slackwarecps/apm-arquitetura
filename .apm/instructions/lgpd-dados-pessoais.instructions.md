---
description: "LGPD: mascaramento de dados pessoais (CPF, RG, CNPJ, etc.) em logs"
applyTo: "**/*.java,**/*.ts,**/*.kt,**/*.swift"
---

# LGPD - Dados Pessoais em Log (FabaoCorp)

Nunca escreva CPF, RG, CNPJ, e-mail, telefone ou qualquer outro dado pessoal
identificável em texto claro em log (println, logger, tracing, eventos).

1. **Mascare ou criptografe antes de logar**: aplique o utilitário de
   mascaramento/criptografia padrão da stack (ex.: `***.***.***-XX` para CPF)
   em vez de logar o valor bruto.
2. Vale para todos os níveis de log (DEBUG incluso) e para tracing distribuído
   (spans, atributos, eventos).
3. Ao revisar código (`revisao-arquitetural`) ou gerar novo endpoint, sinalize
   qualquer log que exponha dado pessoal em claro como achado de severidade alta.
4. Não presuma qual utilitário de mascaramento o projeto já tem — se não existir
   um padrão, sinalize a lacuna em vez de inventar uma implementação.
