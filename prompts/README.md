# Prompts para testes de integração

Este diretório reúne exemplos de prompts usados para apoiar a geração de testes de integração com apoio de IA. A ideia é criar cenários que sejam mais específicos, estruturados e diretamente úteis para QA, testes de API e validação de contrato.

## Prompts disponíveis

- `prompt-cenarios-integracao.md` – gera cenários de integração com diferentes tipos de falha e fluxo principal
- `prompt-dados-teste.md` – gera massa de dados para validar contratos, limites e regras de negócio
- `prompt-contratos-api.md` – auxilia na validação de contratos, erros e respostas esperadas

## Estratégia de uso

Cada prompt foi desenhado para provocar respostas da LLM em diferentes níveis:

- cenário: foco em comportamento do sistema e na interação entre componentes;
- dados: foco em cobertura de borda e variação de entradas;
- contrato: foco em regras formais da API e nas respostas esperadas.

## Benefício da combinação

A combinação desses três tipos de prompt gera uma suíte de testes mais rica, mais realista e mais útil para identificar problemas de integração antes do deploy.
