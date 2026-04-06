# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `perfil_investidor.json` | JSON | Personalizar tom e nível de detalhe das respostas, identificar tolerância a risco |
| `carteira_ativos.json` | JSON | Exibir posição atual, calcular rentabilidade e concentração por classe de ativo |
| `historico_aportes.csv` | CSV | Analisar evolução patrimonial e frequência de aportes |
| `benchmarks.json` | JSON | Comparar desempenho da carteira com CDI, IPCA e Ibovespa |

---

## Adaptações nos Dados

Os dados mockados foram expandidos para refletir um perfil de investidor mais realista:

- `perfil_investidor.json` ganhou o campo `objetivo` (ex: aposentadoria, reserva de emergência, renda passiva) para que o agente personalize as análises
- `carteira_ativos.json` foi estruturado por classe de ativo (renda fixa, renda variável, fundos) para facilitar o cálculo de alocação percentual
- `benchmarks.json` foi adicionado do zero, com os retornos acumulados de CDI, IPCA+5 e Ibovespa nos últimos 12 meses, para servir de referência nas comparações

---

## Estratégia de Integração

### Como os dados são carregados?

Todos os arquivos são carregados no início da sessão via Python (`json.load` / `pandas.read_csv`). Os dados são parseados e transformados em um dicionário estruturado em memória, que persiste durante toda a conversa sem necessidade de releitura.

### Como os dados são usados no prompt?

Os dados vão no **system prompt**, formatados como texto estruturado. O agente recebe o contexto completo do cliente logo na instrução inicial, o que evita consultas dinâmicas e reduz latência. Para carteiras muito grandes, apenas o resumo por classe de ativo é incluído — o detalhe por ativo é injetado sob demanda quando o usuário pergunta sobre um item específico.

---

## Exemplo de Contexto Montado
```
Você é o InvestBot, assistente de investimentos da [Empresa].
Responda sempre de forma acessível e educativa. Baseie suas respostas
exclusivamente nos dados abaixo. Se não souber, diga que não tem a informação.

=== PERFIL DO INVESTIDOR ===
Nome: João Silva
Perfil: Moderado
Objetivo: Aposentadoria em 20 anos
Horizonte: Longo prazo
Tolerância a perda: Até 15% ao ano

=== CARTEIRA ATUAL ===
Renda Fixa (60%):
  - Tesouro IPCA+ 2035: R$ 18.000 (30%)
  - CDB 110% CDI: R$ 12.000 (20%)
  - LCI isenção IR: R$ 6.000 (10%)

Renda Variável (30%):
  - ETF BOVA11: R$ 12.000 (20%)
  - Ações WEGE3: R$ 6.000 (10%)

Fundos (10%):
  - Fundo Multimercado XP: R$ 6.000 (10%)

Total investido: R$ 60.000

=== BENCHMARKS (últimos 12 meses) ===
CDI:          10,4%
IPCA+5:       13,1%
Ibovespa:     +8,7%
Sua carteira: +11,2%

=== ÚLTIMOS APORTES ===
- Out/24: R$ 1.500
- Set/24: R$ 1.500
- Ago/24: R$ 800 (aporte menor que o habitual)
```
