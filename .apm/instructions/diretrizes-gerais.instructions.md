---
description: "Diretrizes gerais de arquitetura da FabaoCorp (stack, comunicacao entre servicos, contratos, resiliencia, observabilidade)"
applyTo: "**/*"
---

# Diretrizes de Arquitetura - Fabao-Corp

1. Backends e BFFs sao Java Spring Boot; frontend web e Angular; mobile e Android/iOS nativos.
2. Comunicacao sincrona (REST).
3. Contratos de API: versionamento explicito, compatibilidade retroativa, OpenAPI/AsyncAPI publicado.
4. Resiliencia: timeout, retry com backoff, circuit breaker em chamadas entre servicos (Spring Boot: Resilience4j).
5. Observabilidade: logs estruturados, tracing distribuido, metricas minimas (latencia, erro, saturacao) em todo novo endpoint.
6. Front/Mobile consomem sempre o BFF, nunca o backend diretamente; tratamento de erro e estados de loading padronizados.
