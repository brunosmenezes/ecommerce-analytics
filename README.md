# E-commerce Analytics: Data Quality, Performance & Strategic Insights (2023–2025)

## Project Status

| Etapa | Status |
|-------|--------|
| Data Audit | ✅ Concluído |
| Data Cleaning | ✅ Concluído |
| Exploratory Data Analysis | ✅ Concluído |
| Business Insights & Hypothesis Testing | ✅ Concluído |

---

## Contexto de Negócio

Este projeto simula a análise estratégica de um e-commerce com dados corporativos realistas cobrindo o período de **janeiro de 2023 a dezembro de 2025** — 3 anos completos de operação.

A base original contém ruídos comuns em ambientes transacionais reais: inconsistências categóricas, valores ausentes, registros duplicados, preços incorretos e variações de formatação. O pipeline analítico foi construído para tratar esses problemas de forma documentada e rastreável, conectando qualidade de dados, KPIs de performance e tomada de decisão estratégica.

---

## Objetivos do Projeto

1. Realizar auditoria técnica completa da base de dados
2. Identificar e tratar problemas estruturais com decisões documentadas
3. Conduzir análise exploratória orientada a KPIs de negócio
4. Validar hipóteses com inferência estatística
5. Extrair insights estratégicos acionáveis com recomendações priorizadas

---

## Estrutura do Projeto

```
ecommerce-analytics/
│
├── data/
│   ├── raw/                            # Base original (13.094 registros)
│   └── processed/                      # Base tratada (12.830 registros válidos)
│
├── notebooks/
│   ├── 01_data_audit.ipynb             # ✅ Auditoria técnica da base
│   ├── 02_data_cleaning.ipynb          # ✅ Limpeza e padronização
│   ├── 03_eda.ipynb                    # ✅ Análise exploratória
│   └── 04_business_insights.ipynb     # ✅ Insights e testes de hipótese
│
├── README.md
└── .gitignore
```

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.x-lightblue)
![Seaborn](https://img.shields.io/badge/Seaborn-0.x-green)
![SciPy](https://img.shields.io/badge/SciPy-1.x-orange)
![statsmodels](https://img.shields.io/badge/statsmodels-0.x-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)

- **Python / Pandas / NumPy** — manipulação e transformação de dados
- **Matplotlib / Seaborn** — visualização analítica
- **SciPy / scikit-posthocs** — testes de hipótese e inferência estatística
- **statsmodels** — decomposição de séries temporais
- **Jupyter Notebook** — documentação e narrativa analítica

---

## Pipeline Analítico

### 01 · Data Audit

Auditoria técnica completa da base original com 13.094 registros. Principais achados:

- **ID duplicado:** 131 ocorrências do ID 9484
- **Preço Unitário zerado:** 131 registros com valor = 0
- **Quantidade Vendida inválida:** 264 registros com valor ≤ 0
- **Desconto em formato misto:** valores decimais e strings com `%`
- **Categoria com whitespace:** 14 valores únicos aparentes para 7 categorias reais
- **Forma de Pagamento fragmentada:** 10 variações para 4 meios de pagamento
- **Localização com ruído textual:** 57 variações para 12 cidades
- **Valor Total incorreto:** campo não considerava quantidade vendida
- **Datas com precisão inconsistente:** nanosegundos vs segundos no mesmo campo

---

### 02 · Data Cleaning

Tratamento documentado de todos os problemas identificados na auditoria. Decisões principais:

- Conversão de datas com `format="mixed"` para lidar com inconsistência de precisão temporal
- Padronização de categorias via `strip()`, `lower()` e mapeamento explícito
- Correção de Preço Unitário zero via imputação determinística por produto
- Criação de `id_registro` como chave técnica substituta ao ID duplicado
- Recálculo de `Valor_Total_Corrigido = Preço Unitário × Quantidade × (1 − Desconto)`
- Remoção de 264 registros com `Quantidade Vendida ≤ 0`

**Impacto financeiro da correção:** aproximadamente **R$ 510 mil** em receita subestimada na base original.

**Base analítica final:** 12.830 registros válidos.

---

### 03 · Exploratory Data Analysis

Análise exploratória orientada a KPIs de negócio com foco em receita, sazonalidade, categorias, produtos, formas de pagamento e geografia.

#### Principais Achados

**Receita e Crescimento**
- Receita total do período: **R$ 45,4 milhões**
- Crescimento acumulado de **+553%** entre 2023 (R$ 3,8M) e 2025 (R$ 24,9M)
- Ruptura de patamar em **Jan/2024**: receita mensal saltou de ~R$ 300 mil para ~R$ 1,4 milhão em um único mês
- Ticket médio cresceu de R$ 2.614 (2023) para R$ 3.722 (2025)

**Sazonalidade**
- Decomposição da série temporal (modelo multiplicativo) confirmou tendência de crescimento linear após Jan/2024
- **Fevereiro** é consistentemente o mês mais fraco nos três anos
- **Dezembro** é recorrentemente o segundo mês mais fraco
- Sazonalidade existente mas ainda suave — possivelmente mascarada pelo crescimento acelerado

**Mix de Categorias e Produtos**
- **Eletrônicos** representa **59,8%** da receita total; junto com Móveis (16,4%) e Eletrodomésticos (11,3%), concentram **87,5%** do faturamento
- Todos os 10 produtos mais rentáveis pertencem exclusivamente a Eletrônicos
- **22 produtos (11% do portfólio)** respondem por **80% da receita** — curva de Pareto

**Correlações**
- **Preço Unitário × Valor Total: 0.79** — principal determinante do faturamento
- **Quantidade Vendida × Valor Total: 0.46** — influência moderada
- **Desconto × Valor Total: −0.06** — impacto praticamente nulo

**Geografia**
- São Paulo lidera em receita (11,1%) mas tem o menor ticket médio (R$ 3.420)
- Brasília (R$ 3.745) e Goiânia (R$ 3.708) lideram no ticket médio
- Mix de categorias homogêneo entre todas as 12 cidades

---

### 04 · Business Insights & Hypothesis Testing

Validação estatística das hipóteses levantadas na EDA com recomendações estratégicas priorizadas.

#### Hipóteses Testadas

| Hipótese | Teste | p-valor | Decisão | Conclusão |
|----------|-------|---------|---------|-----------|
| H1 — Ticket médio igual entre formas de pagamento | Kruskal-Wallis | 0,1084 | Não rejeita H0 | Sem diferença significativa |
| H2 — Desconto não influencia o valor da compra | Spearman | < 0,001 | Rejeita H0 | Correlação negativa fraca (ρ = −0,04) |
| H3 — Receita não varia entre os meses | Kruskal-Wallis | 0,9974 | Não rejeita H0 | Sem diferença significativa* |
| H4 — Ticket médio de SP igual ao das demais cidades | Mann-Whitney U | 0,0001 | Rejeita H0 | SP tem ticket menor (−4,4%) |

*Limitação: n=3 por grupo — resultado deve ser interpretado com cautela.

#### Recomendações Estratégicas

🔴 **Alta Prioridade**
- **Revisar política de descontos:** descontos atuais são indiferenciados e não geram aumento de ticket — implementar desconto progressivo por valor de compra
- **Cross-sell e upsell em São Paulo:** maior base de clientes com ticket estatisticamente menor — potencial relevante de aumento de receita

🟡 **Média Prioridade**
- **Monitorar sazonalidade:** padrões de Fevereiro e Dezembro precisam de mais anos de dados para confirmação estatística
- **Avaliar custo de transação por meio de pagamento:** ticket homogêneo entre meios, mas custos de processamento diferem

🟢 **Longo Prazo**
- **Ampliar base histórica:** 5+ anos de dados para análises de sazonalidade e correlações mais robustas

---

## Perguntas Respondidas pela Análise

| Pergunta | Resposta Resumida |
|----------|-------------------|
| Como a qualidade dos dados impacta decisões? | Erro de R$ 510 mil em receita na base original |
| Existe crescimento consistente? | Sim — +553% acumulado em 2 anos |
| Quais categorias impulsionam a receita? | Eletrônicos (59,8%), Móveis (16,4%), Eletrodomésticos (11,3%) |
| O ticket médio varia por pagamento? | Não — confirmado estatisticamente (p = 0,1084) |
| Existem padrões sazonais significativos? | Não confirmado estatisticamente — base insuficiente para conclusão robusta |
| O desconto influencia o valor da compra? | Correlação existe mas é irrelevante na prática (ρ = −0,04) |
| SP tem ticket diferente das demais cidades? | Sim — ticket 4,4% menor, confirmado estatisticamente (p = 0,0001) |

---

## Autor

**Bruno Menezes**  
Data Analytics Portfolio Project  
[github.com/brunosmenezes/ecommerce-analytics](https://github.com/brunosmenezes/ecommerce-analytics)
