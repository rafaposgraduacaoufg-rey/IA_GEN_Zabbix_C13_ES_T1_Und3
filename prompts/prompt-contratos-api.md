# Prompt 3: geração de casos de erro e contratos de API

## Objetivo
Produzir critérios de contrato e casos de erro para validar a consistência das integrações entre serviços.

## Prompt base

"Atue como especialista em testes de API e integração de sistemas. Considere um ambiente de monitoramento com endpoints para autenticação, criação de alertas, consulta de alertas e sincronização com Zabbix.

Crie um contrato de API em formato de documentação estruturada, incluindo:
- endpoint;
- método HTTP;
- autenticação necessária;
- payload de entrada;
- payload de saída;
- status codes esperados;
- regras de validação;
- casos de erro;
- cenários de integração com Zabbix.

Também inclua uma matriz de testes que relacione cada cenários a um resultado esperado e a um sinal observável no Zabbix. Produza a resposta em português e em formato legível para uso em testes automatizados."

## Ajustes úteis para melhorar qualidade

- pedir definição de status codes e payloads;
- incluir contrato de erro padronizado;
- exigir exemplos de resposta para casos de sucesso e falha;
- deixar explícito o papel do Zabbix como canal de observabilidade;
- acrescentar regras de retry e idempotência.

## Saída esperada

A LLM deve gerar um conjunto de especificações com:
- endpoint de autenticação;
- criação de alertas com código 201;
- erro 400 para dados inválidos;
- erro 401 para token expirado;
- erro 500 para falha do serviço de integração;
- resposta consistente para timeouts e mensagens em fila.
