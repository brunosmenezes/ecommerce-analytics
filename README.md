# 📊 Qualidade e Preparação de Dados – Vendas de E-commerce

## 1. 📌 Contexto  
Este projeto tem como objetivo avaliar e preparar uma base de dados de vendas de um e-commerce, simulando um cenário real de dados extraídos de um CRM operacional. A base contém informações de transações, produtos, categorias, valores financeiros, localização e forma de pagamento.

O foco do projeto é garantir a **confiabilidade dos dados antes de sua utilização em análises estratégicas, relatórios executivos e modelos analíticos**, contemplando desde o diagnóstico de qualidade até a geração de uma base analítica final pronta para uso.

---

## 2. 🎯 Objetivos  
- Avaliar a qualidade dos dados (completude, consistência, tipagem e integridade de regras de negócio);  
- Identificar problemas críticos que impactam métricas financeiras e operacionais;  
- Aplicar regras de limpeza, validação e padronização dos dados;  
- Construir uma **base analítica final consistente e confiável** para análises subsequentes;  
- Demonstrar boas práticas de preparação de dados e governança analítica.

---

## 3. 🗂️ Dataset  
Base de vendas de um e-commerce com registros de transações contendo, entre outros campos:  
- ID da Venda  
- Data da Venda  
- Produto e Categoria  
- Preço Unitário  
- Quantidade Vendida  
- Desconto  
- Valor Total  
- Localização  
- Forma de Pagamento  

> ⚠️ Observação: O dataset utilizado foi propositalmente “sujo” para simular problemas reais encontrados em bases de dados operacionais.

---

## 4. 🧪 Metodologia  

O projeto foi estruturado em três grandes etapas:

### 4.1 Diagnóstico de Qualidade dos Dados (`01_diagnostico_qualidade.ipynb`)  
- Verificação de valores ausentes;  
- Avaliação de tipagem;  
- Detecção de duplicidades;  
- Identificação de inconsistências semânticas;  
- Validação de regras de negócio (ex: cálculo do valor total da venda).

### 4.2 Limpeza e Preparação dos Dados (`02_limpeza_e_preparacao.ipynb`)  
- Conversão e padronização de tipos de dados;  
- Tratamento de outliers em variáveis operacionais (quantidade vendida);  
- Padronização de campos categóricos (categoria, forma de pagamento e localização);  
- Validação e recálculo do faturamento com base na regra de negócio;  
- Definição de chave técnica e tratamento de registros duplicados;  
- Geração da **base analítica final versionada**.

### 4.3 Síntese Executiva e Base Final  
- Consolidação dos principais achados críticos;  
- Avaliação do impacto das etapas de limpeza nos KPIs;  
- Geração de uma base limpa em `data/processed/ecommerce_base_final.csv`, pronta para análises exploratórias, construção de indicadores e etapas analíticas futuras.

---

## 5. 🚨 Principais Achados  
- Registros com **inconsistência no valor total da venda** em relação à regra de negócio (Preço Unitário × Quantidade Vendida × (1 − Desconto));  
- Presença de **registros duplicados** (~5–6% da base), impactando métricas de faturamento;  
- **Fragmentação semântica** em Localização (múltiplas grafias para a mesma cidade);  
- **Valores ausentes** em colunas categóricas relevantes (Categoria e Forma de Pagamento);  
- Problemas estruturais de tipagem em campos originalmente importados como string;  
- Impacto mensurável da limpeza dos dados em métricas de volume e faturamento.

---

## 6. 📦 Entregáveis  
- `data/raw/vendas_loja_crm_sujo.csv` → base bruta original  
- `01_diagnostico_qualidade.ipynb` → diagnóstico de qualidade  
- `02_limpeza_e_preparacao.ipynb` → pipeline de limpeza e preparação  
- `data/processed/ecommerce_base_final.csv` → **base analítica final pronta para uso**

---

## 7. 🛠️ Tecnologias Utilizadas  
- Python  
- Pandas  
- NumPy  
- Matplotlib / Seaborn  
- Jupyter Notebook  

---

## 8. ▶️ Como Executar o Projeto  

1. Navegue até a pasta do projeto:  
   ```bash
   cd ecommerce-analytics