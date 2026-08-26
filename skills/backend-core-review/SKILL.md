---
name: backend-core-review
description: Verifica a saúde do backend checando se os testes rodam e se a cobertura de código está acima de 80%.
---

# Backend Core Review

Análise de sanidade de um backend Java/Spring Boot: garante que os testes rodem de `FAIL` para `PASS` e que a cobertura de código esteja acima de 80%.

## Quando usar

Use esta skill ao fazer revisão de um projeto backend, antes de aceitar um PR ou sempre que precisar confirmar que a suíte de testes está saudável.

## Fluxo de execução

### 1. Confirmar o diretório do projeto

Detecte o diretório raiz (onde está o `pom.xml`). Se não encontrar `pom.xml`, informe que este projeto não é um Maven backend.

### 2. Rodar os testes

Execute a suíte completa:

```bash
mvn test
```

- Sucesso: todos os testes passam.
- Falha: algum teste quebrou — reporte os testes que falharam.

### 3. Verificar cobertura

A cobertura é reportada pelo JaCoCo, gerado em `target/site/jacoco/index.html`. Para garantir que o report seja produzido:

```bash
mvn verify
```

Em seguida leia o arquivo `target/site/jacoco/index.html` e extraia os percentuais de cobertura global (linhas e branches).

### 4. Regra de ouro (80%)

Compare os percentuais com o limiar de 80%:

- **Cobertura >= 80%** → PASS na cobertura.
- **Cobertura < 80%** → FALHA na cobertura.

### 5. Verificar o limiar no Maven (opcional, se JaCoCo configurado)

Se o `pom.xml` tiver o plugin JaCoCo com `check`, o próprio build falha quando a cobertura fica abaixo do limiar. Não remova nem enfraqueça esse limite — respeite o valor configurado.

## Relatório final

Estruture a resposta em PT-BR no formato:

```
# Core Review — <artifactId>
✅/❌ Testes: os testes rodam (X executados / Y sucesso / Z falhas)
✅/❌ Cobertura: cobertura de linhas = L% (> ou < 80%)
❌ Se qualquer uma acima falhar → indicar bloquear merge / adoção.
```

## Observações

- Se a cobertura não estiver acima de 80%, sugira pontos específicos de código sem cobertura (o relatório do JaCoCo aponta arquivos e linhas).
- Use exclusivamente Português do Brasil ao comunicar os resultados.
