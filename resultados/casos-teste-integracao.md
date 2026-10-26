# Casos de teste de integração gerados com apoio de IA

## Resumo executivo

Os casos abaixo foram produzidos a partir dos prompts descritos na pasta `prompts/`, com contexto de observabilidade de uma arquitetura de monitoramento usando Zabbix como referência de telemetria e alerta.

## 1) Cenários de integração gerados

### CT-01: criação de alerta com sucesso
- Objetivo: validar o fluxo completo entre front-end, API e serviço de alertas
- Componentes: front-end, API gateway, serviço de alertas, banco de dados
- Sequência: front-end envia alerta -> API valida autenticação -> serviço persiste alerta -> resposta 201
- Resultado esperado: alerta persistido e visível para consulta
- Falha possível: validação insuficiente ou duração de transação elevada
- Observabilidade: tempo de resposta normal; logs sem erro; Zabbix sem disparo de alerta
- Criticidade: alta

### CT-02: autenticação inválida na API gateway
- Objetivo: validar rejeição de requisições sem token válido
- Sequência: cliente sem token -> API gateway -> bloqueio
- Resultado esperado: resposta 401 ou 403 com erro padronizado
- Falha possível: autenticação bypassada ou token aceito indevidamente
- Observabilidade: aumento de tentativas falhas; Zabbix sinaliza spikes de erro
- Criticidade: crítica

### CT-03: timeout no serviço de integração com Zabbix
- Objetivo: verificar comportamento quando o serviço de integração demora demais
- Sequência: alerta gerado -> integração Zabbix não responde -> timeout
- Resultado esperado: retriável e registro do erro em fila/monitoramento
- Falha possível: falha em retry ou perda de evento
- Observabilidade: latência elevada; Zabbix dispara alerta por tempo de resposta e falhas de integridade
- Criticidade: crítica

### CT-04: payload malformado
- Objetivo: validar rejeição de payload sem campos obrigatórios
- Entrada: JSON sem campos essenciais, com tipos inconsistentes
- Resultado esperado: 400 e mensagem de erro detalhada
- Falha possível: processamento parcial ou acúmulo de dados inválidos
- Observabilidade: aumento de erros de validação; Zabbix mostra taxa de rejeição
- Criticidade: alta

### CT-05: duplicidade de eventos em mensageria
- Objetivo: garantir idempotência na criação de alertas
- Sequência: mesma mensagem enviada duas vezes
- Resultado esperado: operação sem duplicidade no banco e sem alertas repetidos
- Falha possível: insert duplicado ou múltiplos alertas
- Observabilidade: Zabbix mostra aumento de eventos duplicados e picos de carga
- Criticidade: alta

### CT-06: inconsistência entre banco e fila
- Objetivo: verificar consistência entre persistência e processamento assíncrono
- Resultado esperado: reconciliador ou compensação para tentar sincronizar estado
- Falha possível: dados processados sem registro primário
- Observabilidade: Zabbix dispara por erros de sincronização e atrasos de fila
- Criticidade: crítica

### CT-07: falha transitória com recuperação automática
- Objetivo: confirmar retry e recuperação do serviço
- Sequência: falha temporária -> retry -> sucesso
- Resultado esperado: operação concluída após compensação
- Falha possível: retry infinito ou perda de eventos
- Observabilidade: picos de latência e recuperação no dashboard
- Criticidade: média/alta

### CT-08: alta severidade sem status correto
- Objetivo: verificar que severidade fora do padrão seja rejeitada
- Resultado esperado: erro de regra de negócio ou conversão padronizada
- Falha possível: alerta de severidade inválida e interpretação incorreta no front-end
- Observabilidade: erros de ingestão e alertas de inconsistência no Zabbix
- Criticidade: alta

## 2) Dados de teste gerados

### DT-01: payload válido
```json
{
  "alertaId": "ALT-1001",
  "titulo": "CPU saturada",
  "severidade": "high",
  "host": "zabbix-server-01",
  "descricao": "Uso de CPU acima de 90% por 10 minutos",
  "timestamp": "2026-10-25T10:00:00Z",
  "usuario": "operador@empresa.com"
}
```

### DT-02: payload sem campo obrigatório
```json
{
  "titulo": "CPU saturada",
  "severidade": "high",
  "host": "zabbix-server-01"
}
```

### DT-03: payload com token expirado
```json
{
  "Authorization": "Bearer expired-token",
  "alertaId": "ALT-1002"
}
```

### DT-04: payload duplicado
```json
{
  "alertaId": "ALT-1001",
  "titulo": "CPU saturada",
  "severidade": "high",
  "host": "zabbix-server-01"
}
```

### DT-05: payload com severidade inválida
```json
{
  "alertaId": "ALT-1005",
  "titulo": "Temperatura alta",
  "severidade": "criticalx",
  "host": "monitor-03"
}
```

## 3) Casos de erro e contrato de API

### EC-01: criação de alerta aceita somente payload completo
- Método: POST /api/alertas
- Status esperado: 201 em sucesso; 400 em ausência de campos;
- Critério: payload com campos obrigatórios

### EC-02: autenticação obrigatória
- Método: GET /api/alertas/{id}
- Status esperado: 401 quando token ausente ou inválido

### EC-03: timeout na integração Zabbix
- Método: POST /api/sincronizacao/zabbix
- Status esperado: 504 ou 503 com registro de retry

### EC-04: erro de consistência de fila
- Método: POST /api/eventos
- Status esperado: 202 em aceitação assíncrona; 409 em evento duplicado

### EC-05: contrato de resposta padronizado
- Campos esperados: id, status, mensagem, timestamp, codigoErro
- Critério: respostas devem ser consistentes em formato JSON

## 4) Observações sobre o uso da LLM

A LLM foi útil para enriquecer os cenários com:
- variedade de falhas reais;
- descrição de indicadores observáveis;
- previsão de impacto operacional;
- tradução dos cenários para linguagem de teste.

Para obter bons resultados, foi necessário pedir explicitamente:
- cenário de integração com componentes reais;
- sinal de observabilidade no Zabbix;
- critérios de sucesso e falha;
- saída em estrutura organizada e em português.
