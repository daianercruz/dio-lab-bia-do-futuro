# Exemplos e Referências

Esta pasta contém exemplos de implementação para cada etapa do desafio.

## Estrutura do Projeto

```
├── assets/
├── data/
│   ├── benchmarks.json
│   ├── carteira_ativos.json
│   ├── historico_aportes.csv
│   └── perfil_investidor.json
├── docs/
│   ├── 01-documentacao-agente.md
│   ├── 02-base-conhecimento.md
│   ├── 03-prompts.md
│   ├── 04-metricas.md
│   └── 05-pitch.md
├── examples/
│   └── README.md
├── src/
└── README.md
```

## Documentação

| Arquivo | Descrição |
|---------|-----------|
| `docs/01-documentacao-agente.md` | Caso de uso, persona, arquitetura e segurança do agente |
| `docs/02-base-conhecimento.md` | Dados utilizados, adaptações e estratégia de integração |
| `docs/03-prompts.md` | System prompt, exemplos de interação e edge cases |
| `docs/04-metricas.md` | Cenários de teste, resultados e métricas avançadas |
| `docs/05-pitch.md` | Roteiro do pitch de 3 minutos |

## Base de Conhecimento

Os arquivos na pasta `data/` representam o cliente fictício **João Silva** — perfil moderado, 35 anos, R$ 60.000 investidos, objetivo de aposentadoria em 20 anos:

| Arquivo | Descrição |
|---------|-----------|
| `perfil_investidor.json` | Perfil, objetivo e tolerância a risco |
| `carteira_ativos.json` | Posição atual por classe de ativo |
| `historico_aportes.csv` | Aportes mensais de janeiro a dezembro/2024 |
| `benchmarks.json` | CDI, IPCA+5, Ibovespa e rentabilidade da carteira |

## Exemplo de Implementação

Confira na pasta `src/` um exemplo básico de estrutura de aplicação usando Streamlit.
