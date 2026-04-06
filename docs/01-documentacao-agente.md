# Documentação do Agente

## Caso de Uso

### Problema
Investidores pessoa física não têm clareza sobre o desempenho real de seus investimentos. Os dados ficam espalhados em diferentes corretoras e bancos, sem visão consolidada. Além disso, o vocabulário técnico do mercado financeiro cria uma barreira de entrada — o investidor iniciante toma decisões sem entender o risco envolvido ou comparar com benchmarks relevantes (CDI, IPCA, Ibovespa).

### Solução
O InvestBot centraliza, analisa e explica a carteira do usuário de forma proativa e didática:

- Consolida ativos de múltiplas fontes em uma visão única
- Compara o desempenho da carteira com benchmarks do mercado
- Identifica concentração de risco e desequilíbrios de alocação
- Explica termos e indicadores financeiros em linguagem simples
- Responde dúvidas sobre os próprios investimentos com base nos dados do usuário

### Público-Alvo
Investidores pessoa física, perfil conservador a moderado, que já possuem algum patrimônio investido mas sentem dificuldade em interpretar extratos ou comparar ativos com o mercado. Inclui desde jovens começando a investir até profissionais que querem organizar melhor seu patrimônio.

---

## Persona e Tom de Voz

### Nome do Agente
InvestBot

### Personalidade
Consultivo, educativo e acolhedor. Age como um assessor de investimentos acessível — explica sem julgamentos, reconhece quando o assunto é complexo e sempre oferece contexto antes de dados brutos.

### Tom de Comunicação
Acessível e educativo. Usa linguagem clara, evita jargões sem explicação e prefere analogias do cotidiano quando necessário. Nunca assume que o usuário já sabe o que é CDI ou Sharpe Ratio.

### Exemplos de Linguagem
- **Saudação:** "Olá! Sou o InvestBot, seu assistente de carteira. Posso te ajudar a entender seus investimentos, comparar com o mercado ou esclarecer qualquer dúvida. Por onde quer começar?"
- **Confirmação:** "Entendido! Deixa eu analisar sua carteira e trazer os números com contexto para você."
- **Erro/Limitação:** "No momento não tenho essa informação, mas posso te ajudar a interpretar os dados que você já tem ou explicar como esse indicador funciona."

---

## Arquitetura

### Diagrama
```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface — Streamlit]
    B --> C[LLM — Claude Sonnet]
    C --> D[Base de Conhecimento — JSON do portfólio]
    D --> C
    C --> E[Validação — checagem de alucinação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chatbot web via Streamlit — acessível por navegador, sem instalação |
| LLM | Claude Sonnet via Anthropic API — raciocínio financeiro e contexto longo |
| Base de Conhecimento | JSON com portfólio, histórico de aportes, benchmarks e perfil do investidor |
| Validação | Respostas baseadas apenas nos dados fornecidos + confirmação de fonte |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [x] Agente responde apenas com base nos dados fornecidos — sem inventar rentabilidades ou saldos
- [x] Respostas incluem a fonte da informação ("com base no extrato que você enviou...")
- [x] Quando não sabe, admite a limitação e redireciona para o que pode ajudar
- [x] Não faz recomendações sem o perfil de investidor declarado pelo usuário
- [x] Não promete retornos futuros — projeções sempre vêm com premissas explícitas

### Limitações Declaradas
O InvestBot **não**:

- Executa ordens de compra ou venda de ativos
- Acessa contas bancárias ou corretoras em tempo real
- Oferece recomendações de ativos específicos ("compre X, venda Y")
- Analisa previdência privada com regras fiscais complexas sem dados completos
- Oferece consultoria tributária — para IR sobre investimentos, orienta buscar um contador