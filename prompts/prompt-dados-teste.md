# Prompt 2: geração de dados de teste

## Objetivo
Gerar massa de dados realista para validar regras de negócio e integração entre serviços.

## Prompt base

"Atue como especialista em QA e testes de API. Gere dados de teste para uma plataforma de monitoramento que integra front-end, serviço de alertas e Zabbix. Os dados devem ser realistas e cobrir casos válidos, inválidos, de borda e de falha de integração.

Crie uma tabela com:
- identificador do caso;
- tipo de dado;
- payload de entrada;
- cenário de uso;
- expectativa de sucesso ou falha;
- impacto no sistema;
- observação de monitoramento.

Inclua exemplos para: autenticação, alertas de alta severidade, campos vazios, IDs duplicados, limite de caracteres, timeouts, payloads grandes e dados em formatos inconsistentes. A resposta deve ser em português e seguir estrutura clara para testes automatizados."

## Ajustes úteis para melhorar qualidade

- especificar o formato do payload (JSON, XML ou form-data);
- pedir dados representando os diferentes perfis de usuário;
- incluir valores limite e valores inválidos;
- perguntar por cenários de concorrência e idempotência;
- pedir priorização por categoria de risco.

## Saída esperada

A LLM deve gerar conjuntos de entrada com:
- alertas válidos;
- autenticação expirada;
- campos nulos e ausentes;
- payload com tamanho excessivo;
- status de severidade inválido;
- duplicidade de identificadores;
- eventos incompletos enviados para o Zabbix.
