# E-commerce Analytics: Data Quality, Performance & Strategic Insights (2023–2025)

## Project Status

| Etapa | Status |
|-------|--------|
| Data Audit | ✅ Concluído |
| Data Cleaning | ✅ Concluído |
| Exploratory Data Analysis | ✅ Concluído |
| Business Insights & Hypothesis Testing | 🔄 Em desenvolvimento |

---

## Contexto de Negócio

Este projeto simula a análise estratégica de um e-commerce com dados corporativos realistas cobrindo o período de **janeiro de 2023 a dezembro de 2025** — 3 anos completos de operação.

A base original contém ruídos comuns em ambientes transacionais reais: inconsistências categóricas, valores ausentes, registros duplicados, preços incorretos e variações de formatação. O pipeline analítico foi construído para tratar esses problemas de forma documentada e rastreável, conectando qualidade de dados, KPIs de performance e tomada de decisão estratégica.

---

## Objetivos do Projeto

1. Realizar auditoria técnica completa da base de dados
2. Identificar e tratar problemas estruturais com decisões documentadas
3. Conduzir análise exploratória orientada a KPIs de negócio
4. Extrair insights estratégicos acionáveis
5. Validar hipóteses com inferência estatística *(em desenvolvimento)*

---

## Estrutura do Projeto

```
ecommerce-analytics/
│
├── data/
│   ├── raw/                        # Base original (13.094 registros)
│   └── processed/                  # Base tratada (12.830 registros válidos)
│
├── notebooks/
│   ├── 01_data_audit.ipynb         # ✅ Auditoria técnica da base
│   ├── 02_data_cleaning.ipynb      # ✅ Limpeza e padronização
│   ├── 03_eda.ipynb                # ✅ Análise exploratória
│   └── 04_business_insights.ipynb  # 🔄 Insights e testes de hipótese
│
├── README.md
└── .gitignore
```

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.x-lightblue)
![Seaborn](https://img.shields.io/badge/Seaborn-0.x-green)
![statsmodels](https://img.shields.io/badge/statsmodels-0.x-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)

- **Python / Pandas / NumPy** — manipulação e transformação de dados
- **Matplotlib / Seaborn** — visualização analítica
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
- Ticket médio cresceu de R$ 2.614 (2023) para R$ 3.722 (2025), indicando crescimento não apenas volumétrico

**Sazonalidade**
- Decomposição da série temporal (modelo multiplicativo) confirmou tendência de crescimento linear após Jan/2024
- **Fevereiro** é consistentemente o mês mais fraco nos três anos
- **Dezembro** é recorrentemente o segundo mês mais fraco — possível antecipação de compras em novembro
- Sazonalidade existente, mas ainda suave — possivelmente mascarada pelo crescimento acelerado da operação

**Mix de Categorias e Produtos**
- **Eletrônicos** representa **59,8%** da receita total; junto com Móveis (16,4%) e Eletrodomésticos (11,3%), concentram **87,5%** do faturamento
- Todos os 10 produtos mais rentáveis pertencem exclusivamente a Eletrônicos
- **22 produtos (11% do portfólio)** respondem por **80% da receita** — concentração típica de curva de Pareto
- Concentração em Eletrônicos representa risco operacional: qualquer queda nessa categoria impacta diretamente o faturamento total

**Formas de Pagamento**
- Distribuição homogênea entre os 4 meios: Cartão de Crédito (27,5%), Pix (24,7%), Débito (24,2%), Boleto (23,6%)
- Ticket médio praticamente uniforme entre os meios (~R$ 3.500), com variação de apenas 4%
- Ausência de diferença estatisticamente relevante — hipótese a ser validada formalmente no próximo notebook

**Correlações**
- **Preço Unitário × Valor Total: 0.79** — principal determinante do faturamento
- **Quantidade Vendida × Valor Total: 0.46** — influência moderada
- **Desconto × Valor Total: −0.06** — impacto praticamente nulo; política de descontos não está direcionada a transações de maior valor

**Geografia**
- São Paulo lidera em receita (11,1%) mas tem o menor ticket médio (R$ 3.420) — crescimento sustentado por volume
- Brasília (R$ 3.745) e Goiânia (R$ 3.708) lideram no ticket médio, indicando potencial para produtos de maior valor agregado
- Mix de categorias homogêneo entre todas as 12 cidades — sem diferenciação regional relevante

---

### 04 · Business Insights *(em desenvolvimento)*

- Testes de hipótese: ticket médio por forma de pagamento, padrões sazonais
- Correlações estatísticas e recomendações estratégicas
- Modelagem preditiva de receita mensal
- Segmentação de clientes (RFM ou clustering)
- Dashboard executivo (Power BI ou Streamlit)

---

## Perguntas Respondidas pela Análise

| Pergunta | Resposta Resumida |
|----------|-------------------|
| Como a qualidade dos dados impacta decisões? | Erro de R$ 510 mil em receita na base original |
| Existe crescimento consistente? | Sim — +553% acumulado em 2 anos |
| Quais categorias impulsionam a receita? | Eletrônicos (59,8%), Móveis (16,4%), Eletrodomésticos (11,3%) |
| O ticket médio varia por pagamento? | Não — variação de apenas ~4% entre os meios |
| Existem padrões sazonais? | Sim, suaves — Fevereiro mais fraco, segundo semestre de 2025 mais forte |
| Onde estão os maiores riscos? | Concentração em Eletrônicos (59,8%) e em 22 produtos (80% da receita) |

---

## Autor

**Bruno Menezes**  
Data Analytics Portfolio Project  
[github.com/brunosmenezes/ecommerce-analytics](https://github.com/brunosmenezes/ecommerce-analytics)
