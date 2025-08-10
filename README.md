# Telecom-X: Previsão de Evasão de Clientes

Este projeto utiliza técnicas de ciência de dados para prever o churn (evasão) de clientes de uma operadora de telecomunicações. O objetivo é identificar os principais fatores que influenciam a saída dos clientes e propor estratégias para aumentar a retenção.

## Principais Etapas

1. **Extração e Limpeza dos Dados**
   - Os dados são carregados de um arquivo CSV público e tratados para análise.

2. **Análise Exploratória**
   - Visualização da distribuição do churn e análise das variáveis.

3. **Pré-processamento**
   - Codificação de variáveis categóricas com OneHotEncoder.
   - Balanceamento da base usando SMOTE.
   - Seleção das variáveis mais relevantes.
   - Normalização das variáveis numéricas.

4. **Modelagem**
   - Treinamento de modelos de Regressão Logística e Random Forest.
   - Avaliação dos modelos com métricas como acurácia, precisão, recall, F1-score e AUC-ROC.

5. **Interpretação dos Resultados**
   - Identificação dos fatores que mais influenciam o churn:
     - Tempo de contrato
     - Valor total cobrado
     - Fatura digital
     - Perfil familiar (idosos, dependentes, cônjuge)

6. **Recomendações de Retenção**
   - Oferecer benefícios para contratos mais longos.
   - Revisar políticas de cobrança.
   - Acompanhar clientes que recebem fatura digital.
   - Valorizar perfis familiares com programas de fidelidade.

## Como executar

1. Instale as dependências:
   ```
   pip install pandas seaborn matplotlib scikit-learn imbalanced-learn statsmodels
   ```
2. Abra o arquivo `telecom-x_BR.ipynb` no Jupyter Notebook ou VS Code.
3. Execute as células em ordem para reproduzir a análise.

## Resultados

- O modelo Random Forest apresentou melhor desempenho, com acurácia de 82% e AUC-ROC de 0.90.
- Os fatores financeiros e familiares são os principais influenciadores de churn.