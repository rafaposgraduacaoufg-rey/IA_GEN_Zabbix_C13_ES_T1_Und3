# Contexto de observabilidade e teste de integração

## Cenário principal

Uma plataforma de monitoramento integra um front-end com uma API de gestão de alertas e com uma conexão com Zabbix. O objetivo é garantir que:

1. o usuário consiga criar e consultar alertas;
2. o serviço de alertas apresente dados consistentes;
3. os eventos enviados ao Zabbix sejam rastreáveis;
4. falhas de autenticação, timeout e inconsistência de dados sejam detectadas;
5. a operação seja observável por métricas e alertas.

## Componentes do cenário

- Front-end: interface de operação e consulta
- API Gateway: controle de acesso e roteamento
- Serviço de Alertas: lógica de criação e atualização de alertas
- Serviço de Integração Zabbix: envio de eventos e métricas
- Banco de Dados: persistência dos alertas e eventos
- Mensageria: processamento assíncrono de alertas e métricas

## Indicadores relevantes para o Zabbix

- tempo médio de resposta da API
- taxa de erro HTTP por endpoint
- disponibilidade do serviço de integração
- fila de eventos pendentes
- taxa de rejeição por validação
- número de alertas duplicados
- tempo de processamento de sincronização

## Objetivo dos testes de integração

Os testes devem verificar que a troca de mensagens e a composição de serviços funcionam corretamente em conjunto, mesmo quando há:

- falha de autenticação;
- erro de contrato entre serviços;
- timeout no serviço de destino;
- payload incompleto ou malformado;
- falha parcial em etapas assíncronas;
- retry e deduplicação de eventos.

## Relação com observabilidade

A observabilidade não é apenas um suporte diagnóstico; ela é parte essencial do critério de aceitação do teste. Sempre que um cenário falha, o teste deve permitir verificar:

- no Zabbix, se houve disparo de alerta ou evento de indisponibilidade;
- se a latência excedeu o limite aceitável;
- se o serviço retornou erro estrutural ou de negócio;
- se houve recuperação automática ou necessidade de intervenção manual.

## Critérios de sucesso do cenário

- API responde corretamente para solicitações válidas
- falhas são refletidas em status HTTP e mensagens consistentes
- integrações mais lentas são identificadas por monitoramento
- integrações com erro não causam duplicidade ou inconsistência
- eventos enviados ao Zabbix são auditáveis e rastreáveis

## Visão do sistema a ser testado

A arquitetura pode ser representada como:

Front-end -> API Gateway -> Serviço de Alertas -> Serviço de Integração Zabbix
\n       \-> Banco de Dados
       \-> Mensageria

Em cenários com falha, o Zabbix passa a funcionar como camada de observabilidade que sinaliza indisponibilidade, latência e perda de mensagens.
