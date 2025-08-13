# Telecom-X: Previsão de Evasão de Clientes

Este projeto utiliza técnicas de ciência de dados para prever o churn (evasão) de clientes de uma operadora de telecomunicações. O objetivo é identificar os principais fatores que influenciam a saída dos clientes e propor estratégias para aumentar a retenção.


## Estrutura do Projeto

- `telecom-x_BR.ipynb`: Notebook principal com todo o fluxo de análise, modelagem e visualizações.
- `TelecomX_Dados_Limpos.csv`: Arquivo CSV com os dados tratados e prontos para análise.

## Preparação dos Dados

1. **Classificação das Variáveis**
   - **Categóricas**: Exemplo — gênero, contrato, método de pagamento, serviços adicionais.
   - **Numéricas**: Exemplo — tempo de contrato, cobrança total.

2. **Codificação e Normalização**
   - Variáveis categóricas são codificadas com `OneHotEncoder`.
   - Variáveis numéricas são normalizadas com `StandardScaler`.

3. **Balanceamento**
   - Utilização do SMOTE para equilibrar as classes de churn.

<p align="center">
  <img src="img/distribuicao_churn.png" alt="Distribuição Churn" width="45%" />
  <img src="img/distribuicao_churn_balanceado.png" alt="Distribuição Churn Balanceado" width="45%" />
</p>

4. **Separação dos dados**
   - Divisão em conjuntos de treino e teste (70% treino, 30% teste) para garantir avaliação justa dos modelos.

**Justificativas**
   - Codificação facilita o uso dos algoritmos de machine learning.
   - Normalização melhora o desempenho dos modelos lineares.
   - Balanceamento evita viés para a classe majoritária.


## Modelagem


- ### **Avaliação**:
  - Métricas: acurácia, precisão, recall, F1-score, AUC-ROC.
  - Random Forest apresentou melhor desempenho (acurácia de 82%, AUC-ROC de 0.90).

- ### **Principais variáveis**:
  - Tempo de contrato
  - Valor total cobrado
  - Fatura digital
  - Perfil familiar (idosos, dependentes, cônjuge)


  Relacionamento das principais variáveis com o churn
  <p align="center">
  <img src="img/cobranca_total_churn.png" alt="Cobrança Total x Churn" width="45%" />
  <img src="img/tempo_contrato_churn.png" alt="Tempo Contrato x Churn" width="45%" />
</p>

- ### **Modelos utilizados**:
#### 1) Regressão Logística

Análise das variáveis mais relevantes:

<div style="text-align: center;">
  <table style="border-collapse: collapse; margin: auto;">
    <thead>
      <tr>
        <th style="border-right: 1px solid #ccc; padding: 8px; text-align: center;">Variável</th>
        <th style="padding: 8px; text-align: center;">Coeficientes</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">tempo_de_contrato</td>
        <td style="padding: 8px; text-align: right;">-2.511658</td>
      </tr>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">cobranca_total</td>
        <td style="padding: 8px; text-align: right;">1.528867</td>
      </tr>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">fatura_digital_1</td>
        <td style="padding: 8px; text-align: right;">0.837263</td>
      </tr>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">idoso_1</td>
        <td style="padding: 8px; text-align: right;">0.835703</td>
      </tr>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">dependentes_1</td>
        <td style="padding: 8px; text-align: right;">-0.348092</td>
      </tr>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">genero_Masculino</td>
        <td style="padding: 8px; text-align: right;">-0.006404</td>
      </tr>
      <tr>
        <td style="border-right: 1px solid #ccc; padding: 8px;">tem_conjuge_1</td>
        <td style="padding: 8px; text-align: right;">0.002767</td>
      </tr>
    </tbody>
  </table>
</div>

OBSERVAÇÕES  
`tempo_de_contrato`: Coeficiente negativo, indica que clientes com maior tempo de contrato têm menor probabilidade de camcelamento.  
`cobranca_total`: Coeficiente positivo, sugere que cobranças totais mais altas aumentam a chance de churn.  
`fatura_digital`: Coeficiente positivo, indica que clientes que recebem fatura digital tendem a evadir mais.  
`idoso`: Coeficiente negativo, mostra que idosos têm menor propensão ao churn.  
`dependentes` e `tem_conjuge`: Ambos negativos, sugere que clientes com dependentes ou cônjuge são mais fiéis. 


#### 2) Random Forest

Analisando a importânicia das principais variáveis  

<p align="left">
    <img src="img/rd_variaveis.png" alt="Cobrança Total x Churn" width="60%" />
</p>

OBSERVAÇÕES

`tempo_de_contrato`: Altíssima importância, reforçando o papel do tempo de contrato na retenção.  
`cobranca_total`: Também muito relevante, indicando que valores altos de cobrança estão associados ao churn.  
`fatura_digital`: Importante para o modelo, sugerindo que o método de recebimento da fatura influencia a evasão.  
`idoso`, `dependentes`, `tem_conjuge`: Todas aparecem entre as mais relevantes, alinhando-se com os resultados da regressão logística.

**Recomendações de Retenção**
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