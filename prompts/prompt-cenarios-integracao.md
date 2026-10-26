# Prompt 1: geração de cenários de integração

## Objetivo
Gerar cenários de integração para um sistema monitorado com Zabbix, com foco em API, comunicação entre serviços e observabilidade.

## Prompt base

"Atue como especialista em testes de integração e QA de sistemas distribuídos. Considere o seguinte cenário: uma plataforma de monitoramento possui front-end, API gateway, serviço de alertas, serviço de integração com Zabbix, banco de dados e mensageria. O objetivo é validar a comunicação entre esses componentes e a observabilidade do comportamento do sistema.

Crie uma lista de cenários de integração com:
- identificação do cenário;
- objetivo do teste;
- componentes envolvidos;
- sequência de eventos;
- entrada esperada;
- resultado esperado;
- falha possível;
- sinal de observabilidade no Zabbix;
- nível de criticidade.

Inclua fluxos principais, falhas de autenticação, falha de integração com Zabbix, timeout, payload inválido, duplicidade e inconsistência de dados. Produza a resposta em linguagem portuguesa, em formato estruturado e com foco em testes reais de integração."

## Ajustes úteis para melhorar qualidade

- especificar a arquitetura do sistema;
- pedir retorno em JSON ou checklist;
- exigir mapeamento com sinais observáveis;
- incluir casos de borda e falhas assíncronas;
- pedir priorização por criticidade.

## Saída esperada

A LLM deve produzir cenários como:
- criação de alerta com sucesso;
- falha de autenticação no gateway;
- timeout no serviço de integração Zabbix;
- mensagem duplicada na fila;
- dados inconsistentes entre banco e serviço;
- recuperação automática após falha transitória.
