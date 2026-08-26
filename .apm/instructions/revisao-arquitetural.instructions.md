---
description: "Checklist de revisao arquitetural da FabaoCorp (acoplamento, contratos de API, resiliencia, observabilidade, seguranca)"
applyTo: "**/*.java,**/*.ts,**/*.kt,**/*.swift"
---

# Revisao Arquitetural FabaoCorp

Avalie decisoes de design tecnico nas verticais da FabaoCorp (Banking, Seguros, Financeiro, Arquitetura) contra este checklist:

1. **Acoplamento entre servicos**: comunicacao sincrona (REST/gRPC) so quando necessario; preferir eventos para fluxos assincronos entre squads/microsservicos.
2. **Contratos de API**: versionamento explicito, compatibilidade retroativa, OpenAPI/AsyncAPI publicado.
3. **Resiliencia**: timeout, retry com backoff, circuit breaker em chamadas entre servicos (Spring Boot: Resilience4j).
4. **Observabilidade**: logs estruturados, tracing distribuido, metricas minimas (latencia, erro, saturacao) em todo novo endpoint.
5. **Seguranca**: segredos fora do codigo, autenticacao/autorizacao consistente entre BFF e backend.
6. **Front/Mobile**: Angular e apps Android/iOS consumindo BFF (nunca backend diretamente), tratamento de erro e estados de loading padronizados.

## Saida esperada

Liste achados como bullets curtos: `[severidade] area — problema — sugestao`. Nao invente contexto do projeto que voce nao verificou no codigo.
