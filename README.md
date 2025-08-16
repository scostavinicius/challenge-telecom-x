# Análise de Evasão de Clientes na Telecom X

## Introdução

Este notebook contém uma análise exploratória de dados com o objetivo de entender os fatores que levam à evasão de clientes (Churn) em uma empresa de telecomunicações. A análise explora as relações entre o Churn e diversas características dos clientes, como tipo de contrato, serviço de internet, método de pagamento, custos e tempo de permanência.

## Processos Principais

### 1. Extração de Dados

O notebook começa com a importação de bibliotecas essenciais como `pandas` e `numpy`. Os dados são carregados a partir de um arquivo JSON hospedado em um repositório do GitHub.

### 2. Tratamento e Limpeza de Dados

A fase de tratamento de dados foi crucial para preparar o conjunto de dados para a análise. Os passos incluem:

- **Normalização**: O arquivo JSON continha dados aninhados em colunas como `customer`, `phone`, `internet` e `account`. A função `pd.json_normalize` foi utilizada para expandir essas colunas, criando um DataFrame com uma estrutura mais plana.
- **Reorganização de Colunas**: Os nomes das colunas normalizadas foram renomeados para uma melhor legibilidade. Por exemplo, `customer.gender` foi alterado para `gender`. A coluna `customerID` foi definida como o índice do DataFrame.
- **Padronização e Conversão de Tipos**:
  - Foram removidas linhas onde a coluna `Churn` estava vazia.
  - Valores categóricos binários (`Yes`, `No`, `True`, `False`, `1`, `0`) foram padronizados para o tipo booleano (`True` ou `False`).
  - Valores incoerentes, como `'No phone service'` e `'No internet service'`, foram tratados e mapeados para `False` nas colunas relevantes.
  - Valores em branco na coluna `Charges.Total` foram removidos e a coluna foi convertida para o tipo numérico `float`.
- **Criação de Novas Colunas**: Uma nova coluna, `Contas_Diarias`, foi criada para representar o custo médio diário do serviço, calculada a partir do custo mensal.

### 3. Análise Exploratória de Dados

Esta seção foca na identificação de padrões e relações entre a evasão de clientes e outras variáveis.

- **Cálculo de Índices Estatísticos**: Foram calculados a média, mediana e desvio padrão para as colunas numéricas de `Charges.Monthly` (Custos Mensais) e `tenure` (Meses de Contrato) para obter uma visão geral da distribuição dos dados.
- **Visualização de Distribuição de Churn**: Gráficos de barras e histogramas foram utilizados para visualizar a distribuição do Churn em relação a variáveis categóricas e numéricas, como:
  - `Gênero x Evasão`
  - `Tipo de Contrato x Evasão`
  - `Serviço de Internet x Evasão`
  - `Método de Pagamento x Evasão`
  - `Custo Mensal x Evasão`
  - `Meses de Contrato x Evasão`

### 4. Conclusões e Recomendações

Com base na análise exploratória, foram tiradas as seguintes conclusões e feitas recomendações:

- **Tempo de Contrato**: Clientes com contratos de curto prazo (mês a mês) têm uma taxa de Churn significativamente maior. Recomenda-se a criação de ofertas e incentivos para que os clientes optem por contratos mais longos.
- **Serviço de Internet**: O serviço de fibra óptica está associado a uma alta taxa de Churn, sugerindo que há insatisfação específica com este serviço. É recomendado investigar a qualidade e os problemas relacionados a este serviço.
- **Método de Pagamento**: Clientes que usam cheque eletrônico são os que mais cancelam. A empresa deve analisar as causas por trás da insatisfação desses clientes, podendo ser problemas no processo de pagamento ou outros fatores que influenciam sua decisão.
