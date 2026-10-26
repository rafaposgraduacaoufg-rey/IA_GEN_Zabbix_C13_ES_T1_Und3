# Experimento com LLM e análise de qualidade dos prompts

## Como os prompts foram usados

Os prompts foram aplicados em uma sequência de refinamento:

1. Prompt de cenário de integração
2. Prompt de dados de teste
3. Prompt de contrato e casos de erro

Essa sequência melhorou a qualidade dos resultados porque cada etapa adicionou nível de detalhe para o próximo.

## Influência de cada tipo de prompt

### Prompt de cenário

Este prompt foi o mais eficiente para gerar diversidade de casos. Ele ajudou a cobrir:
- fluxos principais;
- falhas de comunicação;
- desacoplamento entre módulos;
- cenários de recuperação.

Seus limites: ele pode gerar cenários de alto nível sem definir detalhes de API e payload.

### Prompt de dados de teste

Este prompt teve maior impacto na realismo dos testes. Ele permitiu criar entradas que simulam:
- usuários válidos e inválidos;
- payloads incompletos;
- valores fora de faixa;
- problemas de concorrência e idempotência.

Seus limites: exige boa definição do contrato para não gerar dados excessivamente genéricos.

### Prompt de contrato e erro

Este prompt foi decisivo para transformar cenários em critérios de aceite. Ele tornou os testes mais úteis para automação e revisão por QA, pois define:
- status HTTP esperados;
- regras de validação;
- respostas de erro e compensação.

Seus limites: depende da arquitetura do sistema e de convenções internas para ser realmente útil.

## Ajustes necessários para melhores resultados

Os principais ajustes realizados foram:

- informar explicitamente o contexto arquitetural;
- definir quais serviços e integrações são relevantes;
- pedir saídas em formato estruturado;
- incluir Zabbix como critério observável;
- solicitar casos de borda e falha transitória;
- pedir respostas em português e com linguagem de testes realistas.

## Conclusão

Os prompts mais úteis foram aqueles que combinaram:
- contexto técnico;
- detalhamento de regras de negócio;
- definição de saídas esperadas;
- foco em observabilidade.

A combinação desses prompts aumentou muito a qualidade dos casos de teste gerados, trazendo maior cobertura e maior aderência ao ambiente real de integração.
