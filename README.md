# <center>Projeto de Regressão - Rossmann</center>

# <center><img src="https://upload.wikimedia.org/wikipedia/commons/1/15/Dirk_Rossmann_GmbH.jpg" align="center" style="width:300.0px;"/></center>

## 1. Questão de negócio

### 1.1. Sobre a empresa
<p align="justify">A Rossmann é uma das maiores cadeias de drogarias da Europa. Com sua primeira loja aberta em 1972 em Hanôver, na Alemanha, a rede hoje está presente em outros 7 países do continente europeu com mais de 4000 unidades abertas.</p>

### 1.2. Sobre o projeto
<p align="justify"></p>

### 1.3. Visão geral do conjunto de dados
#### Conjunto de dados bruto
<p align="justify">.</p>

Estas X colunas são descritas abaixo:

train.csv

| **Coluna**    | **Descrição**                                                                                                                                                                                                                        |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Store         | a unique Id for each store                                                                                                                                                                                                           |
| DayOfWeek     | the day of the week of the store operation date: starting with 1 as Monday                                                                                                                                                           |
| Date          | date of store operation, on YYYY-MM-DD format                                                                                                                                                                                        |
| Sales         | the turnover for any given day (this is what you are predicting)                                                                                                                                                                     |
| Customers     | the number of customers on a given day                                                                                                                                                                                               |
| Open          | an indicator for whether the store was open: 0 = closed, 1 = open                                                                                                                                                                    |
| Promo         | indicates whether a store is running a promo on that day                                                                                                                                                                             |
| StateHoliday  | indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None |
| SchoolHoliday | indicates if the (Store, Date) was affected by the closure of public schools                                                                                                                                                         |

store.csv

| **Coluna**                | **Descrição**                                                                                                                                                                                                              |
|:--------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Store                     | a unique Id for each store                                                                                                                                                                                                 |
| StoreType                 | differentiates between 4 different store models: a, b, c, d                                                                                                                                                                |
| Assortment                | describes an assortment level: a = basic, b = extra, c = extended                                                                                                                                                          |
| CompetitionDistance       | distance in meters to the nearest competitor store                                                                                                                                                                         |
| CompetitionOpenSinceMonth | gives the approximate month of the time the nearest competitor was opened                                                                                                                                                  |
| CompetitionOpenSinceYear  | gives the approximate year of the time the nearest competitor was opened                                                                                                                                                   |
| Promo2                    | Promo2 is a continuing and consecutive promotion for some stores: 0 = store is not participating, 1 = store is participating                                                                                               |
| Promo2SinceWeek           | describes the calendar week when the store started participating in Promo2                                                                                                                                                 |
| Promo2SinceYear           | describes the year when the store started participating in Promo2                                                                                                                                                          |
| PromoInterval             | describes the consecutive intervals Promo2 is started, naming the months the promotion is started anew. E.g. "Feb,May,Aug,Nov" means each round starts in February, May, August, November of any given year for that store |


test.csv

| **Coluna**    | **Descrição**                                                                                                                                                                                                                        |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Id            | an Id that represents a (Store, Date) duple within the test set                                                                                                                                                                      |
| Store         | a unique Id for each store                                                                                                                                                                                                           |
| DayOfWeek     | the day of the week of the store operation date: starting with 1 as Monday                                                                                                                                                           |
| Date          | date of store operation, on YYYY-MM-DD format                                                                                                                                                                                        |
| Open          | an indicator for whether the store was open: 0 = closed, 1 = open                                                                                                                                                                    |
| Promo         | indicates whether a store is running a promo on that day                                                                                                                                                                             |
| StateHoliday  | indicates a state holiday. Normally all stores, with few exceptions, are closed on state holidays. Note that all schools are closed on public holidays and weekends. a = public holiday, b = Easter holiday, c = Christmas, 0 = None |
| SchoolHoliday | indicates if the (Store, Date) was affected by the closure of public schools                                                                                                                                                         |

## 2. Premissas do negócio
<p align="justify">Para a elaboração deste trabalho, as seguintes premissas são adotadas:</p>


## 3. Planejamento da solução
### 3.1 O método SAPE (Saída - Processo - Entrada)
#### Saída (Produto final)
Serão fornecidos 
    


#### Processo (Passo-a-passo)
<strong>1. Extração dos dados (Extraction)</strong>


<strong>2. Transformação dos dados (Transformation)</strong>

2.1. Limpeza dos dados



2.2. Criação de novas colunas






<strong>3. Carregamento dos dados (Loading)</strong>

3.1. Validação de hipóteses

- <strong>H1</strong>: Imóveis que possuem vista para água são em média 30% mais caros;
- <strong>H2</strong>: Imóveis com data de construção menor que 1957 são em média 50% mais baratos;


3.2. Avaliação de insights para o negócio

#### Entrada
- Os dados deste projeto foram retirados do portal Kaggle e estão disponíveis no link:
   

## 4. Teste de hipóteses e insights do negócio

### 4.1. Hipóteses
<p align="justify"> Foram testadas X hipóteses acerca do conjunto de dados dos imóveis, com seus resultados e descrições abaixo:</p>

| Hipótese | Validação | Significado para o negócio |
|:---------|:----------|:---------------------------|
| <strong>H1: </strong>Imóveis com porão possuem em média área total 20% maior | Verdadeira | A média de área total construída dos imóveis com porão é 20,13% maior que aqueles que não possuem este cômodo. Devem ser considerados visto que o aumento de área total é significativo. |
| <strong>H2: </strong>Imóveis com reformas são em média 40% mais caros | Verdadeira | O preço médio dos imóveis que foram reformados é 43% em relação aos que nunca passaram por processos de renovação. É aconselhável comprar imóveis com condições boas para então reformá-los visando lucro na revenda. |
| <strong>H3: </strong>Imóveis com até 2 quartos são em média 30% mais baratos. | Verdadeira | Os imóveis com menos de 2 quartos são em média 30% mais baratos que aqueles que possuem mais dormitórios. Estes imóveis são boa opção de portfólio com preços mais baixos. |
| <strong>H4: </strong>Imóveis que possuem vista para água são em média 30% mais caros | Falsa | Imóveis com vista para a água são em média 214% mais caros. |
| <strong>H5: </strong>Imóveis com data de construção menor que 1957 são em média 50% mais baratos | Falsa | Os imóveis mais antigos possuem pequena variação de preço médio comparado aos mais novos, construídos a partir de 1957, sendo apenas 2.83% mais barato. Quando comparado com outros atributos do portfólio, este possui menor significância. |
| <strong>H6: </strong>O crescimento do preço dos imóveis Year over Year (YoY) é de 10% | Falsa | O preço médio dos imóveis vendidos em 2015 são apenas 0.53% maiores que aqueles vendidos no ano anterior. Assim, este comportamento não deve ser levado em conta no estudo. |
| <strong>H7: </strong>O crescimento do preço dos imóveis Month over Month (MoM) de 15% | Falsa | Entre os meses de maio/2014 e maio/2015, a variação do preço médio dos imóveis variou dentro de um intervalo de -3% e 7% em relação ao mês anterior, nunca alcançando uma variação de 15%. |
| <strong>H8: </strong>Imóveis com condição a partir de 3 são em média 40% mais caros que os imóveis com condição 1. | Falsa | Imóveis com condições acima de 3, ou seja, os imóveis que são considerados "bons" ou melhores, possuem preço médio 60% maiores que aqueles com condições ruins. Portanto, estes imóveis possuem maior valor de mercado. |
| <strong>H9: </strong>Imóveis com porão são em média 5% mais caros. | Falsa | Imóveis com porão, além de maiores em área total, são também 28% mais caros. Consequentemente, são imóveis mais bem avaliados. |
| <strong>H10: </strong>Imóveis são vendidos no verão por um preço médio 15% maior que no inverno. | Falsa | A variação entre os preços médios dos imóveis vendidos no verão e no inverno é de apenas 3%. Ou seja, não há variação significativa entre os preços nas duas estações. |


### 4.2. Insights
<p align="justify" >A análise exploratória dos dados ___ proporciona alguns insights:</p>

#### Insight 1: 
<p align="justify" ></p>

#### Insight 2: 
<p align="justify" </p>

#### Insight 3: 
<p align="justify" ></p>


## 5. Resultados financeiros para o negócio
<p align="justify"</p>

| Número de imóveis | Preço de compra total | Preço de venda total | Faturamento total |
|:-----------------:|:---------------------:|:--------------------:|:-----------------:|
|       3872        | \$1.522.626.895,00    | \$1.959.734.476,70   | \$437.107.581,70  |

<p align="justify" ></p>

## 6. Conclusão
<p align="justify" ></p>

## 7. Próximos passos
<p align="justify" >Este projeto pode ir além nas análises e visualizações já aqui desenvolvidas, incluindo intens como:</p>

## 8. Tecnologias
### Desenvolvimento do código
[<img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" style="height: 50px" align="left"/>](https://jupyter.org/)

[<img src="https://upload.wikimedia.org/wikipedia/commons/1/1d/PyCharm_Icon.svg" style="height: 50px" align="left"/>](https://www.jetbrains.com/pt-br/pycharm/)

[<img src="https://freepikpsd.com/file/2019/10/Python-PNG-File.png" style="height: 50px" align="left"/>](https://www.python.org/)
                                                                                                                  
[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/1200px-Pandas_logo.svg.png" style="height: 50px" align="left"/>](https://pandas.pydata.org/)

[<img src="https://geopandas.org/en/latest/_images/geopandas_logo.png" style="height: 40px" align="left"/>](https://geopandas.org/en/stable/)<br/><br/><br/>

### Construção e publicação dos dashboards
[<img src="https://streamlit.io/images/brand/streamlit-logo-secondary-colormark-darktext.svg" style="height: 50px" align="left"/>](https://streamlit.io/)

[<img src="https://blog.back4app.com/wp-content/uploads/2020/12/O-que-e-o-Heroku.png" style="height: 50px" align="left"/>](http://heroku.com)<br/><br/>

                                                                                                                    
## 9. Sobre o autor
Olá! Meu nome é Lucas Rodrigues.<br/>
Conecte-se comigo no meu [Linkedin](https://www.linkedin.com/in/lucasrodrigues3/).
