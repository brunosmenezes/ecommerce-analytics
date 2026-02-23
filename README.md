# 📊 Análise de Qualidade de Dados – Vendas de E-commerce

## 📌 Contexto
Este projeto tem como objetivo analisar a qualidade de uma base de dados de vendas de um e-commerce, simulando um cenário real de dados extraídos de um CRM operacional. A base contém informações de transações, produtos, categorias, valores financeiros, localização e forma de pagamento.

O foco do projeto é avaliar a confiabilidade dos dados antes de sua utilização em análises estratégicas, relatórios executivos e modelos analíticos.

---

## 🎯 Objetivos
- Avaliar a qualidade dos dados (completude, consistência, tipagem e integridade de regras de negócio);
- Identificar problemas críticos que impactam métricas financeiras e operacionais;
- Propor ações de limpeza e validação para uso confiável da base;
- Demonstrar boas práticas de Análise Exploratória de Dados (EDA) com foco em qualidade e governança.

---

## 🗂️ Dataset
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

## 🧪 Metodologia
O projeto foi estruturado em três grandes etapas:

1. **Diagnóstico de Qualidade dos Dados**
   - Verificação de valores ausentes;
   - Avaliação de tipagem;
   - Detecção de duplicidades;
   - Identificação de inconsistências semânticas;
   - Validação de regras de negócio (ex: cálculo do valor total da venda).

2. **Análise Exploratória (EDA)**
   - Distribuições de variáveis numéricas;
   - Identificação de outliers;
   - Análises de cardinalidade e fragmentação categórica.

3. **Síntese Executiva**
   - Consolidação dos principais achados críticos;
   - Avaliação de impacto analítico e de negócio;
   - Proposta de ações corretivas e melhorias no pipeline de dados.

---

## 🚨 Principais Achados
- Registros com **inconsistência no valor total da venda** em relação à regra de negócio (Preço Unitário × Quantidade Vendida × (1 − Desconto));
- Presença de **registros duplicados**, impactando métricas de faturamento;
- **Fragmentação semântica** em Localização (múltiplas grafias para a mesma cidade);
- **Valores ausentes** em colunas categóricas relevantes (Categoria e Forma de Pagamento);
- Problemas estruturais de tipagem em campos originalmente importados como string.

---

## 🛠️ Tecnologias Utilizadas
- Python  
- Pandas  
- NumPy  
- Jupyter Notebook  

---

## ▶️ Como Executar o Projeto

1. Navegue até a pasta do projeto:
   ```bash
   cd ecommerce-analytics