# 📈 Viés do Ibovespa Diário

> Relatório de leitura qualitativa do mercado brasileiro, gerado automaticamente toda noite pelo **Cowork (Anthropic)** com **Claude** como motor de análise — entregue em PDF antes de cada pregão da B3.

---

## 🏆 Projeto candidato ao prêmio — Melhor Uso do Claude

---

## 🔎 O Problema

Todo dia útil, antes de qualquer decisão de investimento, era necessário garimpar manualmente informações espalhadas em dezenas de fontes — Money Times, InfoMoney, CNN Brasil, Seu Dinheiro, TradingView — para tentar entender o humor do mercado antes da abertura da B3.

Era um processo **demorado, disperso e sem metodologia**:

- ⏱️ **30 a 45 minutos por dia** de pesquisa manual sem estrutura
- 📊 **Dados sem contexto** — saber que o Ibovespa caiu 2% não explica o que fazer amanhã
- 🎲 **Decisões sob pressão** — sem preparo, as escolhas ficavam expostas a ruído e emoção
- 🔁 **Processo repetitivo** — a mesma rotina todo dia útil, ano após ano

> *"O investidor que chega ao pregão sem preparo não toma decisões — reage. E reagir ao ruído do mercado é o caminho mais rápido para o prejuízo."*

---

## 💡 A Solução

O **Viés do Ibovespa Diário** foi construído usando o **Cowork**, ferramenta da Anthropic para automação no desktop, com **Claude** como motor de análise e geração do relatório.

### Como funciona

```
Cowork executa  →  Claude coleta  →  Análise ponderada  →  PDF gerado
    (21h45)          (10+ fontes)       (POS/NEG/NEU)      (local)
```

**1. Cowork executa**
O agente Cowork dispara automaticamente após o fechamento do pregão da B3.

**2. Claude coleta**
Varre as principais fontes de mercado: Money Times, InfoMoney, CNN Brasil, Seu Dinheiro, Gazeta Mercantil, TradingView, entre outras.

**3. Análise ponderada**
Cada manchete é classificada como `POS`, `NEG` ou `NEU`, com o **canal de transmissão** para o mercado explicado — por que aquela notícia importa para o Ibovespa e com qual intensidade.

**4. PDF gerado**
Relatório completo salvo localmente em `D:\Claude\ClaudeViesBovespa\`, pronto para leitura.

---

### Lógica do modelo

| Mecanismo | Descrição |
|-----------|-----------|
| **Classificação POS/NEG/NEU** | Cada manchete recebe viés com canal de transmissão explicado |
| **Lógica antifade** | Quando Wall Street sobe mas o Ibovespa cai, o peso de NY é reduzido pela metade automaticamente |
| **Contagem líquida de sinais** | Todos os sinais somados algebricamente → mapeia para escala 1–5 |
| **Auto-calibração** | A retrospectiva detecta viés sistemático (ex: altismo recorrente) e aplica correção |

### Escala de viés

```
1 — Baixa       (< -1%)
2 — Leve Baixa  (-1% a -0,21%)
3 — Neutro      (-0,20% a +0,20%)
4 — Leve Alta   (+0,21% a +1%)
5 — Alta        (> +1%)
```

---

## 📄 Estrutura do relatório (PDF)

Cada relatório gerado contém **6 seções**:

1. **Viés do pregão** — número de 1 a 5 com justificativa completa
2. **Painel de ativos** — Ibovespa, Dólar/Real, Ouro, Brent, Minério de Ferro, S&P 500
3. **Manchetes classificadas** — até 10 notícias com viés e canal de transmissão
4. **Ventos a favor** — catalisadores positivos para o pregão
5. **Principais riscos** — fatores que podem pressionar o índice
6. **Retrospectiva** — histórico de acertos e erros do modelo com auto-calibração

---

## 📊 Exemplo real — 08 de maio de 2026

**Viés:** `2 — Leve Baixa`

**Justificativa:**
Ibovespa fechou em forte queda de -2,38% (183.218 pts), com pressão concentrada em Bradesco, Itaú, Santander, Petrobras e Vale. Wall Street renovou recorde (S&P 500 e Nasdaq), mas antifade aplicado: o Ibov caiu mesmo com NY em alta — sinal claro de descolamento. Contagem líquida de sinais: **-2,5 → viés 2**.

**Painel de ativos:**

| Ativo | Valor | Variação |
|-------|-------|----------|
| Ibovespa | 183.218 pts | -2,38% |
| Dólar / Real | R$ 4,92 | Estável |
| Ouro (XAU/USD) | ~US$ 4.700/oz | Neutro |
| Petróleo Brent | ~US$ 98/bbl | -3% no dia |
| Minério de Ferro | ~US$ 108/ton | Firme |
| S&P 500 | Máxima histórica | +novo recorde |

**Retrospectiva (últimos 6 pregões):**

| Data | Viés previsto | Resultado | Acerto |
|------|--------------|-----------|--------|
| 07/05 Qui | 4 — Leve Alta | -2,38% | ✗ |
| 06/05 Qua | 4 — Leve Alta | +0,50% | ✓ |
| 05/05 Ter | 3 — Neutro | +0,62% | ✗ |
| 04/05 Seg | 4 — Leve Alta | -0,92% | ✗ |
| 30/04 Qui | 2 — Leve Baixa | +1,39% | ✗ |
| 24/04 Sex | 2 — Leve Baixa | -0,33% | ✓ |

> A retrospectiva é gerada automaticamente no próprio PDF — o modelo registra seus erros publicamente e ajusta a calibração. Transparência total, sem esconder os erros.

---

## 📈 Resultados e impacto

### Em números

| Métrica | Antes | Depois |
|---------|-------|--------|
| Tempo de preparo diário | 30–45 min | ~2 min de leitura |
| Fontes consultadas | Manual, disperso | 10+ consolidadas |
| Estrutura de análise | Nenhuma | Modelo ponderado com escala 1–5 |
| Registro histórico | Não existia | Retrospectiva automática |
| Horas economizadas/ano | — | **+100 horas** (~30 min × 260 pregões) |

### Em comportamento

**Antes:** investidor reativo, que processava informação sob pressão no momento do pregão, exposto a ruído e decisões emocionais.

**Depois:** investidor preparado, que chega ao dia seguinte já sabendo exatamente o que monitorar:
- Futuros do Ibovespa (WINM26) antes das 10h
- ADRs no pré-market (PBR, VALE, ITUB, BBD)
- Brent no pré-market
- Dólar/Real na abertura
- Dados econômicos do dia (payroll, Selic, balanços)

### Em qualidade de decisão

O sistema entrega um diagnóstico estruturado — não uma opinião, mas um **modelo com raciocínio documentado, fontes referenciadas e histórico visível**. Você pode concordar ou discordar, mas a base está clara.

---

## 🛠️ Tecnologia

| Componente | Papel |
|-----------|-------|
| **Cowork** (Anthropic) | Motor de automação no desktop — dispara o processo |
| **Claude** (Anthropic) | Coleta, análise, classificação e geração do relatório |
| **PDF** | Formato de saída — arquivo local, leitura offline |

---

## ⚠️ Disclaimer

> Este material **não é recomendação de investimento**. É uma leitura qualitativa do cenário baseada em notícias públicas. Decisões de alocação são responsabilidade do leitor.

---

## 👤 Autor

**Flavio Renan Sant Anna**
Projeto pessoal de automação financeira com Claude + Cowork (Anthropic).

---

*Gerado pelo Cowork · Anthropic — `D:\Claude\ClaudeViesBovespa\`*
