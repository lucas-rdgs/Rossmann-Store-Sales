# <center>Projeto de Regressão - Rossmann</center>

# <center><img src="https://upload.wikimedia.org/wikipedia/commons/1/15/Dirk_Rossmann_GmbH.jpg" align="center" style="width:70%"/></center>

## 1. Questão de negócio

### 1.1. Sobre a empresa
<p align="justify">A Rossmann é uma das maiores cadeias de drogarias da Europa. Com sua primeira loja aberta em 1972 em Hanôver, na Alemanha, a rede hoje está presente em outros 7 países do continente europeu com mais de 4000 unidades abertas. Seu foco é a venda de produtos de cuidados pessoais e do lar, como dermocosméticos e perfumes, itens de higiene pessoal, produtos de limpeza, utensílios domésticos e decorações, além de comidas e bebidas.</p>

### 1.2. Sobre o projeto
<p align="justify">Buscando a modernização de suas unidades para elevar a experiência de compra de seus clientes, a empresa deseja eleger as melhores lojas para receber reformas e, para isso, foi solicitado ao time de Data um pedido de ajuda com a previsão de vendas de cada loja nas próximas 6 semanas.</p>
<p align="justify">O faturamento de cada unidade é pode sofrer influência de diversos fatores como época do ano, presença de promoções e distância de outros concorrentes diretos. Como forma de analisar as influências de cada variável e realizar a predição das vendas, este projeto realizará uma análise exploratória inicial dos dados históricos de performance das unidades e aplicará um modelo de Machine Learning.</p>
<p align="justify">Desta forma, o objetivo do projeto é, primordialmente:</p>

> - Elencar as unidades da Rossmann em ordem crescente de previsão de vendas nas próximas 6 semanas e;<br/>
> - Desenvolver uma ferramenta útil, efetiva, rápida e descomplicada para visualização dos resultados.

<p align="justify">A metodologia CRISP será base para desenvolvimento do projeto. O CRISP, ou Cross-Industry Standard Process, é um modelo cíclico de desenvolvimento de projetos de dados. Inicialmente empregado em desafios de mineiração de dados, a metodologia fornece um caminho padronizado com seis fases: entendimento do negócio, entendimento dos dados, preparação dos dados, modelagem, avaliação e implantação. Para este trabalho será aplicada uma modificação do CRISP, cujos passos seguidos em cada ciclo é exemplificado na figura abaixo:</p>

<center><img src="/home/lucas/Imagens/Modelo Cíclico.png" align="center" style="width:70%"/></center>

<p align="justify">O princípio fundamental e maior vantagem do modelo CRISP é agilizar a entrega de resultados relevantes e pertinentes do projeto, ou seja, todo o ciclo será percorrido elencando premissas e buscando a maneira mais simples e rápida de resolução do desafio. Ao final do ciclo, o público-alvo já tera uma versão inicial perfeitamente usável do projeto e será capaz de avaliar se o produto final atende suas necessidades. Caso contrário, um novo ciclo completo pode ser aplicado para melhorar o produto e nesta nova implementação da metodologia serão feitos procedimentos como escolha de mais ou menos variáveis independentes, implementação de outros parâmetros do modelo de aprendizado de máquina ou ainda o uso de um novo modelo, adaptações da forma de entrega o produto final, entre outros.</p>

### 1.3. Visão geral do conjunto de dados
#### Conjunto de dados bruto
<p align="justify">Foram disponibilizadas três arquivos em formato .csv. A descrição de cada um deles será apresentada abaixo:</p>

<strong>Nome do arquivo:</strong> train.csv<br/>
<strong>Descrição:</strong> contém os dados de vendas de cada loja, estas identificadas por um ID único, assim como atributos de sazonalidade.

| **Coluna**    | **Descrição**                                                                                                                                                                                                                                                                              |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Store         | um ID único para cada loja                                                                                                                                                                                                                                                                 |
| DayOfWeek     | o dia da semana da data de operação da loja: começando com 1 para segunda-feira                                                                                                                                                                                                            |
| Date          | data de operação da loja, no formato AAAA-MM-DD                                                                                                                                                                                                                                            |
| Sales         | o faturamento de cada dia (esta é a variável que será estimada)                                                                                                                                                                                                                            |
| Customers     | o número de clientes do dia                                                                                                                                                                                                                                                                |
| Open          | um indicador para se a loja estava aberta: 0 = fechada, 1 = aberta                                                                                                                                                                                                                         |
| Promo         | indica se a loja estava com uma promoção ativa naquela data                                                                                                                                                                                                                                |
| StateHoliday  | indica um feriado estadual. Normalmente todas as lojas, com poucas exceções, são fechadas durante os feriados estaduais. Perceba que todas as escolas estão fechadas em feriados públicos e durante os finais de semana. a = feriado público, b = feriado da Páscoa, c = Natal, 0 = nenhum |
| SchoolHoliday | indica se (Store, Date) foi afetada pelo fechamento de escolas públicas                                                                                                                                                                                                                    |
<br/>


<strong>Nome do arquivo:</strong> store.csv<br/>
<strong>Descrição:</strong> contém os atributos de cada loja.

| **Coluna**                | **Descrição**                                                                                                                                                                                                                                             |
|:--------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Store                     | um ID único para cada loja                                                                                                                                                                                                                                |
| StoreType                 | categorização das lojas em 4 diferentes tipos: a, b, c, d                                                                                                                                                                                                 |
| Assortment                | descreve um nível de sortimento: a = básico, b = extra, c = estendido                                                                                                                                                                                     |
| CompetitionDistance       | distância em metros à loja concorrente mais próxima                                                                                                                                                                                                       |
| CompetitionOpenSinceMonth | mês aproximado quando a loja concorrente mais próxima foi inaugurada                                                                                                                                                                                      |
| CompetitionOpenSinceYear  | ano aproximado quando a loja concorrente mais próxima foi inaugurada                                                                                                                                                                                      |
| Promo2                    | Promo2 é uma promoção continuada e consegutiva para algumas lojas: 0 = loja participante, 1 = loja não participante                                                                                                                                       |
| Promo2SinceWeek           | descreve a semana do ano quando a loja iniciou a participação na Promo2                                                                                                                                                                                   |
| Promo2SinceYear           | descreve o ano quando a loja iniciou a participação da Promo2                                                                                                                                                                                             |
| PromoInterval             | descreve os interalos consecutivos quando a Promo2 é iniciada, indicando os meses quando se inicia uma nova Promo2. Por exemplo, "Feb,May,Aug,Nov" significa que cada ciclo começa em fevereiro, maio, agosto e novembro de qualquer ano para aquela loja |

<br/>


<strong>Nome do arquivo:</strong> test.csv<br/>
<strong>Descrição:</strong> contém dados de teste.

| **Coluna**    | **Descrição**                                                                                                                                                                                                                                                                              |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Id            | um ID que representa uma tupla (Store, Date) nos dados de teste                                                                                                                                                                                                                            |
| Store         | um ID único para cada loja                                                                                                                                                                                                                                                                 |
| DayOfWeek     | o dia da semana da data de operação da loja: começando com 1 para segunda-feira                                                                                                                                                                                                            |
| Date          | data de operação da loja, no formato AAAA-MM-DD                                                                                                                                                                                                                                            |
| Open          | um indicador para se a loja estava aberta: 0 = fechada, 1 = aberta                                                                                                                                                                                                                         |
| Promo         | indica se a loja estava com uma promoção ativa naquela data                                                                                                                                                                                                                                |
| StateHoliday  | indica um feriado estadual. Normalmente todas as lojas, com poucas exceções, são fechadas durante os feriados estaduais. Perceba que todas as escolas estão fechadas em feriados públicos e durante os finais de semana. a = feriado público, b = feriado da Páscoa, c = Natal, 0 = nenhum |
| SchoolHoliday | indica se (Store, Date) foi afetada pelo fechamento de escolas públicas                                                                                                                                                                                                                    |

## 2. Premissas do negócio
<p align="justify">Para a elaboração deste trabalho, as seguintes premissas são adotadas:</p>


## 3. Planejamento da solução
### 3.1 O método SAPE (Saída - Processo - Entrada)
#### Saída (Produto final)
Serão fornecidos:

- Um <i>Jupyter notebook</i> com o desenvolvimento técnico do CRISP para o projeto;
- Uma apresentação de negócios com o desenvolvimento e resultados do projeto;
- Um <i>bot</i> do aplicativo de mensagens Telegram com as previsões de venda das lojas.
    


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

    [https://www.kaggle.com/competitions/rossmann-store-sales/data](https://www.kaggle.com/competitions/rossmann-store-sales/data)
   

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
