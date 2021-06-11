# EEL891 - 2020.02 - Relatório do Trabalho 2
Regressão Multivariável - estimar o preço de um imóvel a partir de suas características

Aluno: Pedro Boechat



## Organização do Repositório

Nesse repositório podem ser encontrados dois Jupyter Notebooks:

- [`preprocessing.ipynb`](https://github.com/pedroboechat/EEL891_Trabalho2/blob/main/preprocessing.ipynb):

  Contém o código utilizado para realizar o pré-processamento dos conjuntos de treinamento e teste para utilização no modelo regressor.

- [`model.ipynb`](https://github.com/pedroboechat/EEL891_Trabalho2/blob/main/model.ipynb):

  Contém o código utilizado para implementar o modelo regressor e exportar os dados de predição.

e uma pasta [`data`](https://github.com/pedroboechat/EEL891_Trabalho2/tree/main/data) que contém os dados utilizados nos notebooks e os dados submetidos no [Kaggle](https://www.kaggle.com/c/eel891-202002-trabalho-2/).



## Pré-processamento

Por meio da análise dos dados usando a biblioteca `Pandas`, foram identificadas, primeiramente, colunas irrelevantes para o modelo ou com dados inconsistentes, que serão removidas. Em seguida, foi identificada uma coluna com valores binários que necessitavam de conversão de (Pessoa Fisica/Imobiliaria) para (0/1) e colunas com muitos valores não numéricos distintos que necessitavam codificação. Finalmente, foram identificadas colunas com valores numéricos que necessitavam aplicação de padronização. Colunas que não se encaixavam em nenhum dos critérios anteriores foram mantidas sem modificação. Assim, o resumo do pré-processamento dos dados é:

**1. Colunas removidas:**

```
'Id',
'diferenciais'
```

**2. Colunas binarizadas:**

```
'tipo_vendedor'
```

**3. Colunas codificadas (*One-hot Encoding*):**

```
'tipo',
'bairro'
```

**4. Colunas padronizadas:**

```
'quartos',
'suites',
'vagas',
'area_util',
'area_extra',
'preco' (y)
```

**5. Colunas sem modificação:**

```
'churrasqueira',
'estacionamento',
'piscina',
'playground',
'quadra',
's_festas',
's_jogos',
's_ginastica',
'sauna',
'vista_mar'
```



## Implementação do modelo regressor

Com a biblioteca `Pandas`, os dados dos conjuntos de treinamento e teste são importados no formato de DataFrame e depois valores alocados em arrays. No caso do conjunto de treinamento os valores são separados em dois arrays (um para as variáveis independentes e outro para a variável dependente).

Com a biblioteca `SciKit-Learn` vão ser realizadas as ações necessárias em certas colunas, identificadas anteriormente no pré-processamento dos dados. Utiliza-se um *scaler* para padronizar os valores das colunas.

Terminado todo o pré-processamento dos dados, importamos da biblioteca `CatBoost` a classe que implementa o regressor. O `CatBoost` utiliza a técnica de *gradient boosting* para encontrar e treinar o melhor modelo de regressão para os dados que temos. Alimentamos o *fit* do regressor com os dados do conjunto de treinamento.

Com o *fit* do regressor concluído, utilizamos o *cross validation score* do `sklearn` para realizar uma análise preliminar do modelo treinado. Em seguida utilizamos o regressor para predizer os valores do conjunto de teste e exportamos esses para um arquivo CSV, que será enviado no Kaggle.



## Resultados

O modelo encontrou um RMSE de 0.54590 no Kaggle.

