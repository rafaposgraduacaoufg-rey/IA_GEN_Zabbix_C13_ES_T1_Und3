# IA_GEN_Zabbix_C13_ES_T1_Und3

Repositório de apoio para a atividade de testes de integração com uso de IA generativa, utilizando o contexto de observabilidade e monitoramento do Zabbix.

## Objetivo

Este projeto demonstra como prompts de IA podem apoiar a geração de cenários, dados e contratos para testes de integração, com foco em fluxos entre serviços e em observabilidade de sistemas distribuídos.

## Cenário de integração adotado

Considera-se um ambiente de monitoramento e integração composto por:

- Front-end de operação de monitoramento
- API de gestão de alertas
- Serviço de integração com Zabbix
- Serviço de inventário de hosts e métricas
- Banco de dados de eventos e alertas
- Mensageria/eventos para sincronização assíncrona

A ideia é validar que o fluxo entre o front-end e os serviços de integração funcione corretamente, que os contratos de API sejam respeitados e que falhas de rede, timeout, autenticação e inconsistência de dados sejam detectadas com evidência observável no Zabbix.

## Contexto de observabilidade com Zabbix

O Zabbix é usado como referência para:

- monitorar latência de chamadas entre serviços;
- detectar falhas em integrações por timeout ou erro HTTP;
- acompanhar taxa de erro de APIs e filas de eventos;
- verificar disponibilidade e integridade de hosts e métricas;
- registrar indicadores de desempenho para incidentes de integração.

## Tipos de prompt utilizados

### 1) Prompt para geração de cenários de integração
Gera cenários de comunicação entre módulos, serviços ou interfaces, incluindo fluxos felizes, falhas e transições entre estados.

### 2) Prompt para geração de dados de teste
Cria massa de dados realista para validar autenticação, payloads, limites, valores inválidos, casos de concorrência e idempotência.

### 3) Prompt para geração de casos de erro e contratos de API
Ajuda a descrever contratos, validar campos obrigatórios, status HTTP esperados, regras de negócio e cenários de falha operacional.

## Estrutura do repositório

- `docs/` – documentação do cenário e da observabilidade
- `prompts/` – exemplos dos prompts empregados
- `resultados/` – casos de teste gerados e validados

## Conteúdo principal

- [docs/observabilidade-zabbix.md](docs/observabilidade-zabbix.md) – descrição do cenário e do contexto de observabilidade
- [prompts/README.md](prompts/README.md) – catálogo dos prompts usados
- [resultados/casos-teste-integracao.md](resultados/casos-teste-integracao.md) – casos de teste gerados pela LLM

## Repositório público

- GitHub: https://github.com/rafaposgraduacaoufg-rey/IA_GEN_Zabbix_C13_ES_T1_Und3

## Como foi experimentado

Os prompts foram elaborados para orientar a LLM a gerar cenários de integração com foco em:

- fluxo principal de operação;
- validação de contrato de API;
- dados de teste com casos de borda;
- cenários de erro e recuperação;
- indicadores observáveis relevantes para Zabbix.

O resultado foi uma série de casos de teste mais úteis, diversificados e mais próximos do comportamento real de sistemas integrados.

## Observações finais

A principal diferença entre os tipos de prompt está no nível de detalhamento entregue à LLM:

- prompts de cenário geram maior diversidade de fluxos;
- prompts de dados geram maior cobertura de borda e realisticidade;
- prompts de contrato geram maior precisão para validação e automação.

Os ajustes de prompt mais importantes foram: especificar contexto de negócio, limitar o escopo da integração, pedir saídas estruturadas e incluir critérios de aceite observáveis.
