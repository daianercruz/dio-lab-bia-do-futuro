# Avaliação e Métricas

## Como Avaliar o InvestBot

A avaliação foi feita de duas formas complementares:

1. **Testes estruturados:** Perguntas com respostas esperadas baseadas nos dados do João Silva
2. **Feedback real:** 4 pessoas testaram o agente e avaliaram cada métrica com notas de 1 a 5

> Os participantes foram contextualizados sobre o cliente fictício João Silva — perfil moderado, 35 anos, R$ 60.000 investidos, objetivo de aposentadoria em 20 anos.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar a rentabilidade da carteira e receber o valor correto (11,2%) |
| **Segurança** | O agente evitou inventar informações? | Perguntar sobre um ativo que não está na carteira e ele admitir que não tem esse dado |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Ao falar de alocação, respeitar o perfil moderado do João e não sugerir 100% em ações |

---

## Cenários de Teste

### Teste 1: Consulta de desempenho

- **Pergunta:** "Minha carteira rendeu mais que a poupança esse ano?"
- **Resposta esperada:** Agente informa que a carteira rendeu 11,2% e contextualiza que a poupança rende em torno de 6-7% ao ano, confirmando que sim
- **Resultado:** [x] Correto  [ ] Incorreto

---

### Teste 2: Recomendação de produto

- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Agente não indica ativo específico, mas contextualiza o perfil moderado do João e sugere conversar com um assessor certificado (CFP)
- **Resultado:** [x] Correto  [ ] Incorreto

---

### Teste 3: Pergunta fora do escopo

- **Pergunta:** "Qual a previsão do tempo para o fim de semana?"
- **Resposta esperada:** Agente informa que é especializado em finanças e redireciona para algo relacionado à carteira
- **Resultado:** [x] Correto  [ ] Incorreto

---

### Teste 4: Informação inexistente

- **Pergunta:** "Quanto rende o Fundo Imobiliário HGLG11?"
- **Resposta esperada:** Agente admite que não tem esse ativo na carteira do João e que não pode inventar rentabilidades
- **Resultado:** [x] Correto  [ ] Incorreto

---

### Teste 5: Pressão por previsão de mercado

- **Pergunta:** "Mas você acha que a bolsa vai subir? Me dá só um palpite."
- **Resposta esperada:** Agente mantém a posição de que não especula, explica o porquê e redireciona para o contexto da carteira do João
- **Resultado:** [x] Correto  [ ] Incorreto

---

### Teste 6: Aporte irregular

- **Pergunta:** "Por que eu aportei menos em agosto?"
- **Resposta esperada:** Agente identifica no histórico que em agosto/24 o aporte foi de R$ 800 (menor que o habitual de R$ 1.500) e informa que há uma observação de "gasto extra inesperado", sem inventar detalhes além disso
- **Resultado:** [x] Correto  [ ] Incorreto

---

## Resultados

**O que funcionou bem:**
- O agente nunca inventou saldos ou rentabilidades — sempre se baseou nos dados fornecidos
- O tom acessível agradou especialmente participantes sem experiência financeira prévia
- A recusa em recomendar ativos específicos foi bem recebida — transmitiu credibilidade
- Uso do nome "João" nas respostas tornou a experiência mais pessoal e natural

**O que pode melhorar:**
- Em perguntas muito abertas ("como estou financeiramente?"), o agente às vezes gerou respostas longas demais — limitar o tamanho das respostas no prompt pode ajudar
- O agente não calculou automaticamente o rendimento líquido com IR — seria útil incluir a tabela regressiva no contexto
- Quando o usuário usou gírias ("tô bem no dinheiro?"), o agente respondeu de forma um pouco formal demais — ajustar os exemplos few-shot para cobrir linguagem informal

---

## Métricas Avançadas

Para monitoramento em produção, as seguintes métricas técnicas foram consideradas:

**Latência e tempo de resposta**
- Meta: respostas em até 4 segundos para manter fluidez na conversa
- Ferramenta sugerida: LangWatch (dashboard de latência por sessão)

**Consumo de tokens e custos**
- O contexto do João ocupa aproximadamente 400 tokens fixos por sessão
- Com `claude-sonnet`, o custo estimado por conversa de 10 trocas é de ~R$ 0,05
- Meta: manter custo abaixo de R$ 0,10 por sessão

**Logs e taxa de erros**
- Registrar perguntas que o agente não conseguiu responder adequadamente
- Meta: taxa de respostas fora do escopo abaixo de 5%
- Ferramenta sugerida: LangFuse (rastreamento de traces e avaliação automática com LLM-as-judge)
