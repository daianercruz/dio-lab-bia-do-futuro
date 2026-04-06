# 🤖 InvestBot — Agente de Investimentos com IA Generativa

## Contexto

Os assistentes virtuais no setor financeiro estão evoluindo de simples chatbots reativos para **agentes inteligentes e proativos**. O InvestBot é um agente financeiro desenvolvido para a **Valore Investimentos** que utiliza IA Generativa para:

- **Antecipar necessidades** ao invés de apenas responder perguntas
- **Personalizar** análises com base no perfil e carteira de cada cliente
- **Cocriar entendimento** financeiro de forma consultiva e educativa
- **Garantir segurança** e confiabilidade nas respostas (anti-alucinação)

---

## O Que Foi Entregue

### 1. Documentação do Agente

Define **o que** o InvestBot faz e **como** ele funciona:

- **Caso de Uso:** Consolidação e análise de carteira de investimentos para pessoa física
- **Persona:** Consultivo, educativo e acolhedor — sem jargões, sem promessas de retorno
- **Arquitetura:** Dados carregados no contexto do system prompt + validação anti-alucinação
- **Segurança:** Respostas baseadas exclusivamente nos dados do cliente

📄 [`docs/01-documentacao-agente.md`](./docs/01-documentacao-agente.md)

---

### 2. Base de Conhecimento

Dados mockados do cliente fictício **João Silva** disponíveis na pasta [`data/`](./data/):

| Arquivo | Formato | Descrição |
|---------|---------|-----------|
| `perfil_investidor.json` | JSON | Perfil, objetivo e tolerância a risco |
| `carteira_ativos.json` | JSON | Posição atual por classe de ativo |
| `historico_aportes.csv` | CSV | Aportes mensais de jan a dez/2024 |
| `benchmarks.json` | JSON | CDI, IPCA+5, Ibovespa e rentabilidade da carteira |

📄 [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md)

---

### 3. Prompts do Agente

- **System Prompt:** Instruções de comportamento, regras anti-alucinação e exemplos few-shot
- **Exemplos de Interação:** 3 cenários reais com entrada e saída esperada
- **Edge Cases:** Previsão de mercado, escopo indevido, dados de terceiros

📄 [`docs/03-prompts.md`](./docs/03-prompts.md)

---

### 4. Aplicação Funcional

Protótipo funcional do InvestBot:

- Chatbot interativo via **Streamlit**
- Integração com **Claude Sonnet** via Anthropic API
- Dados de `data/` carregados no contexto do system prompt a cada sessão

📁 [`src/`](./src/)

---

### 5. Avaliação e Métricas

- 6 cenários de teste estruturados com respostas esperadas
- Métricas de assertividade, segurança e coerência
- Observações de melhoria identificadas durante os testes

📄 [`docs/04-metricas.md`](./docs/04-metricas.md)

---

### 6. Pitch

Roteiro de 3 minutos apresentando o problema, a solução, a demonstração e o diferencial do InvestBot.

📄 [`docs/05-pitch.md`](./docs/05-pitch.md)

---

## Ferramentas Utilizadas

| Categoria | Ferramenta |
|-----------|------------|
| **LLM** | [Claude](https://claude.ai/) (Anthropic) |
| **Desenvolvimento** | [Streamlit](https://streamlit.io/) |
| **Diagramas** | [Mermaid](https://mermaid.js.org/) |

---

## Estrutura do Repositório

```
📁 lab-agente-financeiro/
│
├── 📄 README.md
│
├── 📁 data/
│   ├── benchmarks.json
│   ├── carteira_ativos.json
│   ├── historico_aportes.csv
│   └── perfil_investidor.json
│
├── 📁 docs/
│   ├── 01-documentacao-agente.md
│   ├── 02-base-conhecimento.md
│   ├── 03-prompts.md
│   ├── 04-metricas.md
│   └── 05-pitch.md
│
├── 📁 src/
│   └── app.py
│
├── 📁 assets/
│
└── 📁 examples/
    └── README.md
```

---
