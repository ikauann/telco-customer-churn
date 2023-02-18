# Projeto Telco Custumers Churn

## Ciclo 1:

A primeira parte do projeto foi analisar o problema:

> Problema: Uma empresa de telecomunicações deseja melhorar a retenção de clientes, reduzindo o número de cancelamentos de contrato. Eles querem entender quais são as principais razões pelas quais os clientes cancelam seus contratos e como eles podem identificar os clientes que estão em risco de cancelar.

E estudar as informações do dataset:

**Informações do dataset:**

| Coluna          | Descrição                                                                                   |
|----------------|---------------------------------------------------------------------------------------------|
| customerID     | ID exclusivo de cada cliente                                                                 |
| gender         | Gênero do cliente (Masculino ou Feminino)                                                    |
| SeniorCitizen  | Indica se o cliente é idoso (1) ou não (0)                                                  |
| Partner        | Indica se o cliente tem um parceiro (Sim ou Não)                                            |
| Dependents     | Indica se o cliente tem dependentes (Sim ou Não)                                            |
| tenure         | Número de meses que o cliente permaneceu com a empresa                                      |
| PhoneService   | Indica se o cliente tem serviço de telefone (Sim ou Não)                                    |
| MultipleLines  | Indica se o cliente tem várias linhas telefônicas (Sim, Não ou Sem serviço telefônico)      |
| InternetService| Tipo de serviço de internet do cliente (DSL, Fibra Óptica ou Sem serviço de internet)       |
| OnlineSecurity | Indica se o cliente tem segurança online (Sim, Não ou Sem serviço de internet)             |
| OnlineBackup   | Indica se o cliente tem backup online (Sim, Não ou Sem serviço de internet)                |
| DeviceProtection| Indica se o cliente tem proteção de dispositivo (Sim, Não ou Sem serviço de internet)      |
| TechSupport    | Indica se o cliente tem suporte técnico (Sim, Não ou Sem serviço de internet)             |
| StreamingTV    | Indica se o cliente tem serviço de TV por streaming (Sim, Não ou Sem serviço de internet)  |
| StreamingMovies| Indica se o cliente tem serviço de filmes por streaming (Sim, Não ou Sem serviço de internet)|
| Contract       | Tipo de contrato do cliente (Mensal, Dois anos ou Um ano)                                   |
| PaperlessBilling| Indica se o cliente optou pela fatura eletrônica (Sim ou Não)                              |
| PaymentMethod  | Método de pagamento do cliente (Cheque Eletrônico, Cartão de Crédito, Transferência Bancária (automática) ou Pagamento Eletrônico) |
| MonthlyCharges | Valor mensal cobrado do cliente                                                             |
| TotalCharges   | Valor total cobrado do cliente                                                              |
| Churn          | Indica se o cliente cancelou o contrato (Sim ou Não)                                        |

Logo após, importei as bibliotecas necessárias para resolver o problema e fiz uma descrição dos dados. Percebi que não havia outliers nos dados e não precisei fazer nenhum tratamento de dados pesado. Depois dessa parte, fui para a análise de dados. Dividi meu dataset em:

1. Dados demográficos
2. Dados de serviço
3. Dados de informações do usuário.

Analisei os dados demográficos e finalizei o primeiro ciclo com algumas informações:

1. Não há grande diferença entre os dados entre homens e mulheres.
2. A maioria dos clientes não são idosos.
3. A maioria dos clientes não possui filhos.

## Ciclo 2:

Neste ciclo, foram analisados os dados de serviço e informações do usuário.

### Dados de Serviço:

1. A grande maioria usa o serviço de Fibra Óptica, porém mais de 1500 pessoas não possuem serviço de internet. Isso é interessante.
2. A maioria dos clientes não possui suporte técnico. Isso influencia no churn?
3. A maioria das pessoas usa serviço de celular.

### Dados de Informações do Usuário:

1. Fiquei me perguntando: por que há mais pessoas com plano de dois anos do que com um ano?
2. Check Eletrônico é a forma de pagamento que os clientes mais usam.

Finalizando a análise, foram gerados dois heatmaps para analisar as correlações com a variável resposta `Churn`, obtendo-se os seguintes resultados:

1. Não ter suporte técnico impacta no churn.
2. Não ter segurança impacta no churn.
3. Pagamentos mensais impactam no churn.

Após isso, foram preparados os dados para confirmar com o `Boruta` as melhores features para os modelos de aprendizagem. 

Foram utilizadas as técnicas de preparação `MinMaxScaler` e `One-Hot-Encoding`. Cogitou-se em utilizar o `RobustScaler` na coluna "TotalCharge", mas percebeu-se que não havia necessidade.

## Ciclo 3 e 4

No ciclo 3 e 4, meu foco foi analisar as features indicadas pelo Boruta, avaliar se elas faziam sentido com minha análise e observar a correlação. Felizmente, percebi que havia uma correlação significativa.

Removi as colunas que não teriam impacto no churn e usei um modelo randômico para comparar com meu modelo XGBoost.

Meu modelo randômico obteve de 30% a 50% de acurácia, enquanto meu modelo XGBoost alcançou 79%. Entretanto, sabia que a acurácia por si só não era suficiente e por isso utilizei métricas para avaliar sua precisão, que ficou em 65%.

## Ciclo 5

Nesse ciclo apliquei mais 2 modelos e observei as precisões:

1. SVM: obteve 66% de precisão.
2. KNN: obteve 62% de precisão.

Taxa de rotatividade antes do modelo: 27.17% e apos os modelos obtivemos esses resultados:

1. XGBoost reduziu para 21.44% quase 6%.
2. SVM reduziu para 21.82% nos deu 5% de redução.
3. KNN reduziu para 22.62%% o menor até agora.

E finalizei esse ciclo pensando nos próximos passos para o próximo, que é ajustar o hiperparâmetros e testar outros modelos para tentar melhorar a detecção de churn.