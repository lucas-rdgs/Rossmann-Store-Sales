# <center>Projeto de Regressão - Rossmann</center>

# <center><img src="https://upload.wikimedia.org/wikipedia/commons/1/15/Dirk_Rossmann_GmbH.jpg" align="center" style="width:70%"/></center>

## 1. Questão de negócio

### 1.1. Sobre a empresa
<p align="justify">A Rossmann é uma das maiores cadeias de drogarias da Europa. Com sua primeira loja aberta em 1972 em Hanôver, na Alemanha, a rede hoje está presente em outros 7 países do continente europeu com mais de 4000 unidades abertas. Seu foco é a venda de produtos de cuidados pessoais e do lar, como dermocosméticos e perfumes, itens de higiene pessoal, produtos de limpeza, utensílios domésticos e decorações, além de comidas e bebidas.</p>

### 1.2. Sobre o projeto
<p align="justify">Buscando a modernização de suas unidades para elevar a experiência de compra de seus clientes, a empresa deseja eleger as melhores lojas para receber reformas e, para isso, foi solicitado ao time de Data um pedido de ajuda com a previsão de vendas de cada loja nas próximas 6 semanas.</p>
<p align="justify">O faturamento de cada unidade pode sofrer influência de diversos fatores como época do ano, presença de promoções e distância de outros concorrentes diretos. Como forma de analisar as influências de cada variável e realizar a previsão das vendas, este projeto realizará uma análise exploratória inicial dos dados históricos de performance das unidades e aplicará um modelo de Machine Learning.</p>
<p align="justify">Desta forma, o objetivo do projeto é, primordialmente:</p>

> - Elencar as unidades da Rossmann em ordem crescente de previsão de vendas nas próximas 6 semanas e;<br/>
> - Desenvolver uma ferramenta útil, efetiva, rápida e descomplicada para visualização dos resultados.

<p align="justify">A metodologia CRISP será base para desenvolvimento do projeto. O CRISP, ou Cross-Industry Standard Process, é um modelo cíclico de desenvolvimento de projetos de dados. Inicialmente empregado em desafios de mineiração de dados, a metodologia fornece um caminho padronizado com seis fases: entendimento do negócio, entendimento dos dados, preparação dos dados, modelagem, avaliação e implantação. Para este trabalho será aplicada uma modificação do CRISP, cujos passos seguidos em cada ciclo é exemplificado na figura abaixo:</p>

<img src="https://github.com/lucas-rdgs/Rossmann-Store-Sales/blob/main/Modelo%20C%C3%ADclico.png" align="center" style="width:70%"/>

<p align="justify">O princípio fundamental e maior vantagem do modelo CRISP é agilizar a entrega de resultados relevantes e pertinentes do projeto, ou seja, todo o ciclo será percorrido elencando premissas e buscando a maneira mais simples e rápida de resolução do desafio. Ao final do ciclo, o público-alvo já terá uma versão inicial perfeitamente usável do projeto e será capaz de avaliar se o produto final atende suas necessidades. Caso contrário, um novo ciclo completo pode ser aplicado para melhorar o produto e nesta nova implementação da metodologia serão feitos procedimentos como escolha de mais ou menos variáveis independentes, implementação de outros parâmetros do modelo de aprendizado de máquina ou ainda o uso de um novo modelo, adaptações da forma de entrega o produto final, entre outros.</p>

### 1.3. Visão geral do conjunto de dados
#### Conjunto de dados bruto
<p align="justify">Foram disponibilizadas três arquivos em formato .csv. A descrição de cada um deles será apresentada abaixo:</p>

<strong>Nome do arquivo:</strong> train.csv<br/>
<strong>Descrição:</strong> contém os dados históricos de vendas de cada loja, estas identificadas por um ID único, assim como atributos temporais.

| **Coluna**    | **Descrição**                                                                                                                                                                                                                                                                              |
|:--------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Store         | um ID único para cada loja                                                                                                                                                                                                                                                                 |
| DayOfWeek     | o dia da semana da data de operação da loja: começando com 1 para segunda-feira                                                                                                                                                                                                            |
| Date          | data de operação da loja, no formato AAAA-MM-DD                                                                                                                                                                                                                                            |
| Sales         | o faturamento de cada dia (esta é a variável que será estimada)                                                                                                                                                                                                                            |
| Customers     | o número de clientes do dia                                                                                                                                                                                                                                                                |
| Open          | um indicador que indica se a loja estava aberta: 0 = fechada, 1 = aberta                                                                                                                                                                                                                  |
| Promo         | indica se a loja estava com uma promoção ativa naquela data                                                                                                                                                                                                                                |
| StateHoliday  | indica um feriado estadual. Normalmente todas as lojas, com poucas exceções, são fechadas durante os feriados estaduais. Perceba que todas as escolas estão fechadas em feriados públicos e durante os finais de semana. a = feriado público, b = feriado da Páscoa, c = Natal, 0 = nenhum |
| SchoolHoliday | indica se (Store, Date) foi afetada pelo fechamento de escolas públicas                                                                                                                                                                                                                    |
<br/>


<strong>Nome do arquivo:</strong> store.csv<br/>
<strong>Descrição:</strong> contém dados históricos com os atributos de cada loja.

| **Coluna**                | **Descrição**                                                                                                                                                                                                                                             |
|:--------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Store                     | um ID único para cada loja                                                                                                                                                                                                                                |
| StoreType                 | categorização das lojas em 4 diferentes tipos: a, b, c, d                                                                                                                                                                                                 |
| Assortment                | descreve um nível de sortimento: a = básico, b = extra, c = estendido                                                                                                                                                                                     |
| CompetitionDistance       | distância em metros à loja concorrente mais próxima                                                                                                                                                                                                       |
| CompetitionOpenSinceMonth | mês aproximado quando a loja concorrente mais próxima foi inaugurada                                                                                                                                                                                      |
| CompetitionOpenSinceYear  | ano aproximado quando a loja concorrente mais próxima foi inaugurada                                                                                                                                                                                      |
| Promo2                    | Promo2 é uma promoção continuada e consecutiva para algumas lojas: 0 = loja participante, 1 = loja não participante                                                                                                                                       |
| Promo2SinceWeek           | descreve a semana do ano quando a loja iniciou a participação na Promo2                                                                                                                                                                                   |
| Promo2SinceYear           | descreve o ano quando a loja iniciou a participação da Promo2                                                                                                                                                                                             |
| PromoInterval             | descreve os interalos consecutivos quando a Promo2 é iniciada, indicando os meses quando se inicia uma nova Promo2. Por exemplo, "Feb,May,Aug,Nov" significa que cada ciclo começa em fevereiro, maio, agosto e novembro de qualquer ano para aquela loja |

<br/>


<strong>Nome do arquivo:</strong> test.csv<br/>
<strong>Descrição:</strong> contém os dados históricos, com exceção das vendas, das lojas as quais se deseja que sejam feitas as previsões.

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

- O preenchimento de dados faltantes será realizado da seguinte forma:

    - Coluna competition_distance: será atribuído um valor consideravelmente maior que o valor máximo dos dados originais, para facilmente diferenciar esse dado faltante;
    - Coluna competition_open_since_month: será atribuído o valor do mês da data daquele registro;
    - Coluna competition_open_since_year: será atribuído o valor do ano da data daquele registro;
    - Coluna promo2_since_week: será atribuído o valor da semana da data daquele registro;
    - Coluna promo2_since_year: será atribuído o valor do ano da data daquele registro;
    - Coluna promo_interval: será atribuído o valor 0;
    - Coluna month_map: será atribuído o numeral corresponte ao mês da data do registro, iniciando em 1 para janeiro;
    - Coluna is_promo: será atribuído o valor de 1 para os registros em que a coluna month_map corresponda a um mês (valor diferente de 0), caso contrário será atrobuído o valor 0.

- Serão desconsiderados registros em que as lojas estavam fechadas ou que mesmo abertas não apresentam valores de vendas;
- A previsão número de clientes não será trabalhada.
    
## 3. Planejamento da solução
### 3.1 O método SAPE (Saída - Processo - Entrada)
#### Saída (Produto final)
Serão fornecidos:

- Um <i>Jupyter notebook</i> com o desenvolvimento técnico do CRISP para o projeto;
- Um arquivo .csv com as previsões de vendas das lojas desejadas, em ordem decrescente de vendas;
- Uma apresentação de negócios com o desenvolvimento e resultados do projeto;
- Um <i>bot</i> do aplicativo de mensagens Telegram com as previsões de venda das lojas.
    


#### Processo (Passo-a-passo)
<strong>1. Extração dos dados (Extraction)</strong>

0. Importação das bibliotecas e funções auxiliares
    - Funções auxiliares:
        - Supressão de avisos
        - Definição do tamanho dos gráficos
        - Cálculos da função de V de Crémer
        - Cálculo das funções de erro
        - Definição da função de Cross Validation
        
    - Carregamento dos dados
        - Dados de treino e dados das lojas
            - Merge dessas bases
        - Dados de teste (retirar)
        
<strong>2. Transformação dos dados (Transformation)</strong>  

1. Descrição dos dados
    - Alteração do título das colunas
    - Conferência do tamanho dos dados
    - Alteração dos tipos de dados
    - Conferência e tratamento de dados faltantes
    - Estatísticas descritivas
        - Variáveis numéricas
            - Tendências central e de dispersão
       - Variáveis categóricas
            - Distribuições (boxplot)
            
2. Feature Engineering
    - Mapa mental de hipóteses
    - Criação das hipóteses
        - Hipóteses Loja
        - Hipóteses Produto
        - Hipóteses Tempo
     - Lista final de hipóteses
    - Feature engineering
        - Criação de colunas
        
3. Filtragem de variáveis
    - Filtragem de linhas, excluindo vendas zeradas e lojas fechadas
    - Filtragem de colunas, excluindo as que não serão utilizadas na análise exploratória de dados
        
4. Análise exploratória de dados
    - Análise Univariada
        - Distribuição da variável resposta
        - Distribuições das variáveis numéricas
        - Contagem e distribuições das variáveis categóricas
    - Análise bivariada
        - Validação das hipóteses elencadas no passo de Feature Engineering
            - Determinação da relevância de cada hipótese
    - Análise multivariada
        - Variáveis numéricas
            - Correlação entre as variáveis pelo método de Pearson
        - Variáveis categóricas
            - Correlações entre as variáveis usando o método V de Cramér
            
5. Preparação dos dados
    - Normalização (não há)
    - Rescaling
    - Transformação
        - Encoding
        - Transformação da variável resposta
        - Transformação de natureza
            - Variáveis cíclicas

6. Seleção de atributos
    - Método Boruta
        - Separação de dados de treino e teste pelas últimas 6 semanas dos dados
        - Random Forest Regressor
        - Seleção das colunas pelo método
        - Seleção manual das colunas obtidas pelo método
        
<strong>3. Carregamento dos dados (Loading)</strong>

7. Modelos de aprendizados de máquina (Machine Learning)
    - Filtragem dos dados usando as colunas selecionadas pelo Boruta
    - Aplicação de modelos
        - Modelo de média - guia inicial
        - Modelo de regressão linear
        - Modelo de regressão linear regularizado tipo Lasso
        - Modelo árvore aleatória (Random Forest)
        - Regressor XGBoost
    - Cross Validation dos modelos de Machine Learning
    - Comparação dos desempenhos individuais e após cross validation
    - Escolha do modelo a ser utilizado para predição, com base em erro, complexidade e tempo de execução. Neste caso, o modelo utilizado será o XGBoost

8. Afinação de hiperparâmetros
    - Determinação de conjuntos de valores arbitrários para os parâmetros do modelo XGBoost
    - Teste de dos parâmetros e continuidade da aplicação do modelo com os melhores parâmetros selecionados
    - Salvamento do modelo com a biblioteca pickle para economizar tempo em próximas execuções

9. Tradução e interpretação do erro
    - Desempenho de negócio, apresentando os erros absolutos e percentuais e aplicando-os aos valores preditos, calculando os melhores e piores cenários do modelo.
    - Desempenho do modelo, plotando os erros e suas taxas
    
10. Implantação do modelo para produção
    - Criação da classe Rossmann com os carregamentos, as transformações e aplicação de modelos
    - Criação do API Handler
    - Criação do API Tester para apresentar os resultados do modelo de maneira útil e rápida

11. Desenvolvimento do Bot do Telegram


#### Entrada
- Os dados deste projeto foram retirados do portal Kaggle e estão disponíveis no link:

    [https://www.kaggle.com/competitions/rossmann-store-sales/data](https://www.kaggle.com/competitions/rossmann-store-sales/data)
   

## 4. Teste de hipóteses e insights do negócio

### 4.1. Hipóteses
<p align="justify"> Foram testadas 11 hipóteses acerca do conjunto de dados das lojas no primeiro ciclo do CRISP, com seus resultados e descrições abaixo:</p>

| Hipótese | Validação | Significado para o negócio | Relevância |
|:---------|:----------|:---------------------------|:-----------|
| <strong>H1: </strong>Lojas com maior sortimentos deveriam vender mais | Falsa | Lojas com **maior sortimento** vendem **menos**. | Baixa |
| <strong>H2: </strong>Lojas com competidores mais próximos deveriam vender menos | Falsa | Lojas com **competidores mais próximos** vendem **mais**. | Média |
| <strong>H3: </strong>Lojas com competidores há mais tempo deveriam vender mais | Falsa | Lojas com **competidores há mais tempo** vendem **menos**. | Média |
| <strong>H4: </strong>Lojas com promoções ativas por mais tempo deveriam vender mais | Falsa | O efeito da promoção é positivo até certo ponto, **próximo aos valores mais altos** dos períodos de promoção **as vendas caem**. | Baixa |
| <strong>H5: </strong>Lojas com mais promoções consecutivas deveriam vender mais | Falsa |Lojas com mais promoções consecutivas vendem **menos**. | Baixa |
| <strong>H6: </strong>Lojas abertas durante o feriado de Natal deveriam vender mais | Falsa | Lojas abertas durante o **feriado de Natal** vendem **menos** em relação aos outros feriados. | Média |
| <strong>H7: </strong>Lojas deveriam vender mais ao longo dos anos | Falsa | As lojas estão vendendo **menos** ao longo dos anos. | Alta |
| <strong>H8: </strong>Lojas deveriam vender mais no segundo semestre do ano | Verdadeira | As lojas estão vendendo **mais** no **segundo semestre** do ano. | Alta |
| <strong>H9: </strong>Lojas deveriam vender mais depois do dia 10 de cada mês. | Falsa | Lojas **vendem menos em média depois do dia 10** de cada mês. | Alta |
| <strong>H10: </strong>Lojas deveriam vender menos aos finais de semana | Verdadeira | Lojas **vendem menos** aos **finais de semana**. | Alta |
| <strong>H11: </strong>Lojas deveriam vender menos durante os feriados escolares | Verdadeira | Lojas vendem **menos** durante os **feriados escolares**. Porém, nos meses de julho e agosto as vendas em feriados escolares são equiparáveis e maiores, respectivamente, que as vendas em dias sem feriados escolares, pois nesses meses ocorrem as férias escolares de verão. | Baixa |

### 4.2. Insights
<p align="justify">A análise exploratória dos dados proporciona alguns insights:</p>

#### Insight 1: Distância com competidores
<p align="justify">As lojas com competidores diretos situados até 1km de distância possuem vendas até 9% maiores que aquelas que possuem competidores mais distantes. A tabela abaixo compila as variações das vendas das lojas com relação à distância do competidor mais próximo.</p>

| **Distância do competidor mais próximo** | **Média de vendas por unidade** | **Variação percentual em relação às lojas mais próximas** |
|:----------------------------------------:|:-------------------------------:|:---------------------------------------------------------:|
|                 Até 1 km                 |             7.302,47            |                             -                             |
|                De 1 a 5 km               |             6.836,42            |                          -6,38%                           |
|               De 5 a 10 km               |             6.742,64            |                          -7,67%                           |
|               De 10 a 15 km              |             6.620,98            |                          -9,33%                           |
|               De 15 a 20 km              |             6.845,44            |                          -6,26%                           |
|               Mais de 20 km              |             7.026,72            |                          -3,78%                           |

#### Insight 2: Crescimento das vendas médias durante o feriado de Natal
<p align="justify">O Natal foi o feriado em que houve maior crescimento de vendas médias por loja em 2014 em relação ao ano anterior, de 10,7%. No mesmo período houve crescimento de 9,5% dos feriados regulares e uma redução de 2,4% nas vendas médias no feriado da Páscoa. O Natal, que em 2013 foi o segundo feriado com maior faturamento médio, ocupou a primeira colocação no ano seguinte. O crescimento total das vendas médias nos feriados foi de 6%</p>

#### Insight 3: Vendas a partir do décido dia do mês
<p align="justify">Em média, as lojas vendem mais durante os 10 primeiros dias do mês, quando comparado ao restante do mês. Após o décido dia do mês, as vendas médias por dia são 5,7% do que o período do ínicio dos meses.</p>

## 5. Desempenho do modelo
<p align="justify">Após a aplicação do modelo de Machine Learning nos dados de treino e teste, é essencial que haja uma análise de erros. Variações entre valores reais e previstos por um modelo são inevitáveis, no entanto um bom modelo encontra valores aceitáveis destas diferenças. Esta etapa é essencial para a escolha entre seguir com os resultados obtidos ou continuar com um novo ciclo do CRISP. Nesta etapa usaremos os Erros Médio Absoluto e Percentual Médio Absoluto (leia mais sobre estas métricas aqui); em resumo, estes erros mostram o quanto em média o modelo pode prever além dos valores reais, para cima ou para baixo, em valores absolutos e percentuais.</p>

| **Número de lojas do modelo** | **Previsão de vendas totais** | **Erro Médio Absoluto (MAE)** | **Erro Percentual Absoluto Médio (MAPE)** |
|:-----------------------------:|:-----------------------------:|:-----------------------------:|:-----------------------------------------:|
|              1115             |        $286.911.070,00        |            $744,05            |                   11,15%                  |

<p align="justify">Olhando para os dados do modelo, as vendas totais previstas podem variar em média ±$744,05 ou ±11,15% dos valores reais. A0ssim, podemos determinar quais são as variações totais para mais e para menos dos dados treinados pelo modelo.</p>

| **Cenário**                     |       **Vendas** |
|---------------------------------|-----------------:|
| Pior cenário (Previsão - MAE)   | R$286,078,167.83 |
| Previsão                        | R$286,911,072.00 |
| Melhor Cenário (Previsão + MAE) | R$287,743,976.35 |


<p align="justify">Mas o principal objetido deste projeto é fazer as previsões individuas de cada unidade da Rossmann para que seja decidido sobre o fechamento temporário de cada loja para reformas, então é de grande importância a análise dos erros das previsões de cada loja. O mesmo raciocínio de erro pode ser aplicado em cada uma das lojas.</p>
<p align="justify">O gráfico abaixo mostra os valores dos MAPEs em relação a cada uma das lojas inficivualmente. Algumas unidades possuem MAPEs acima de 0,3, ou seja, 30% de erro medio, com valores máximos ultrapassando os 50%. Porém, a grande maioria de unidades possuem MAPEs abaixo de 20%.</p>

<img src="https://github.com/lucas-rdgs/Rossmann-Store-Sales/blob/main/MAPE_stores.png" style="height: 500px" align="center">

<p align="justify">Para analisar o desempenho do modelo iremos observar quatro gráficos. No primeiro, chamado "Valores reais e previstos pelo modelo", observa-se claramente que os valores reais e previstos seguem a mesma curva de comportamento ou seja, os dois valores seguem as mesmas tendências, por mais que haja erros inerentes ao processo. No próximo, "Taxa de erro (Previsão / Real"), observa-se que os valores das taxas orbitam o valor 1, que indica igualdade entre valores previstos e reais, indicando que o modelo está relativamente próximo da realidade. Já no terceiro gráfico, "Distribuição de erros absolutos", tem-se uma distribuição dos erros absolutos aproximando-se de uma distribuição normal, embora com assimetria à esquerda, mas com maior frequência de erros absolutos próximos a zero. Por fim, o gráfico "Valores dos erros em relação aos erros previstos" mostra novamente que a maioria dos valores preditos possuem erros absolutos tendendo a zero.</p>

<img src="https://github.com/lucas-rdgs/Rossmann-Store-Sales/blob/main/model_performance.png" style="height: 500px" align="center">

<p align="justify">Com estas análises de erro pode-se concluir que o modelo possui bom desempenho. Cabe a uma análise posterior decidir se a magnitude desses erros é satisfatória para responder a questão de negócio ou se será necessária a aplicação de um novo ciclo do CRISP.</p>

## 6. Resultados financeiros para o negócio
<p align="justify">Os valores médios e totais das previsões das 856 lojas da Rossmann para as próximas semanas estão apresentados abaixo:</p>

| Número de lojas | Venda média por loja nas próximas 6 semanas | Vendas total nas próximas semanas |
|:---------------:|:-------------------------------------------:|:---------------------------------:|
|       856       |                 $276.908,15                 |          $237.033.377,31          |

<p align="justify">Abaixo está uma tabela com as 5 lojas com maiores vendas previstas para as próximas 6 semanas. A tabela completa está carregada nos arquivos deste trabalho</p>

| **store** | **store_type** | **assortment** | **prediction** |
|:---------:|:--------------:|:--------------:|:--------------:|
|    262    |        b       |      basic     |   $878.736,57  |
|    1114   |        a       |    extended    |   $877.711,62  |
|    562    |        b       |    extended    |   $852.243,01  |
|    733    |        b       |      extra     |   $737.265,82  |
|    251    |        a       |    extended    |   $704.585,78  |

Acesse [aqui](https://github.com/lucas-rdgs/Rossmann-Store-Sales/blob/main/predicted_sales.csv) um arquivo do tipo .csv com todas as previsões de venda por loja.

## 7. Bot no aplicativo de mensagens Telegram
<p align="justify">Atendendo ao segundo objetivo deste projeto – descrito na seção 1.2 Sobre o projeto –, foi desenvolvido um bot no aplicativo de mensagens Telegram em que o usuário pode digitar o código da loja que deseja receber a previsão de vendas, recebendo a previsão de vendas automaticamente.</p>

Para acessar o bot, [clique aqui](https://t.me/rossmann_lr_bot) ou copie e cole o seguinte endereço no seu navegador: https://web.telegram.org/k/#@rossmann_lr_bot.

<p align="justify">A utilização do aplicativo de mensagens Telegram é demonstrada abaixo:</p>

![](https://github.com/lucas-rdgs/Rossmann-Store-Sales/blob/main/telegram_bot.gif)

## 8. Conclusão
<p align="justify">Este projeto, conforme seus objetivos iniciais, desenvolve uma análise exploratória dos dados de um conjunto de unidades de farmácias da rede Rossmann, aplica modelos de machine learning e prevê as vendas de cada loja nas 6 semanas seguintes ao fim dos dados temporais, provendo ainda uma ferramenta rápida e simples de visualização dessas previsões através de um bot no aplicativo de mensagens Telegram.</p>

<p align="justify">Após testes de alguns modelos, o escolhido para realizar as previsões foi o XGBoost. Assim, se prevê que as 856 lojas da rede Rossmann venderão em média $276.908,15 cada, totalizando $237.033.377,31 ao fim de 6 semanas. Os valores previstos por loja possuem erro percentual médio (MAPE) de 11,15%.</p>

O desenvolvimento do projeto no Jupyter notebook pode ser acessado [aqui](https://github.com/lucas-rdgs/Rossmann-Store-Sales/blob/main/Previsoes_Vendas_Rossmann.ipynb).

## 9. Próximos passos
<p align="justify">Um novo ciclo do CRISP pode ser desenvolvido para aperfeiçoar o desempenho do modelo e reduzir o erro da previsão das vendas das lojas da Rossmann. Várias abodagens podem ser adotadas, porém pontos importantes não podem ser ignorados pois fornecem melhoras consideráveis na execução do projeto. Uma ordem decrescente de importância de técnicas é apresentada abaixo:</p>

> - Seleção de diferentes atributos que influenciam as vendas das lojas;
> - Teste de novos modelos de Machine Learning;
> - Refinamento de hiperparâmetros, com novos parâmetros.

<p align="justify">Além das melhorias no modelo de Machine Learning, podem ser feitas modificações no bot do Telegram, tornando a experiência do usuário mais intuitiva e visualmente prazerosa, adotando funcionalidades como:</p>

> - Função de ajuda;
> - Possibilidade de solicitar as previsões de mais de uma loja na mesma mensagem;
> - Teclado personalizado com as funções da aplicação.

## 10. Tecnologias
### Desenvolvimento do código
[<img src="https://upload.wikimedia.org/wikipedia/commons/3/38/Jupyter_logo.svg" style="height: 50px" align="left"/>](https://jupyter.org/)

[<img src="https://upload.wikimedia.org/wikipedia/commons/1/1d/PyCharm_Icon.svg" style="height: 50px" align="left"/>](https://www.jetbrains.com/pt-br/pycharm/)

[<img src="https://freepikpsd.com/file/2019/10/Python-PNG-File.png" style="height: 50px" align="left"/>](https://www.python.org/)
                                                                                                                  
[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/1200px-Pandas_logo.svg.png" style="height: 50px" align="left"/>](https://pandas.pydata.org/)<br/><br/><br/>


### Desenvolvimento da API
[<img src="https://blog.back4app.com/wp-content/uploads/2020/12/O-que-e-o-Heroku.png" style="height: 50px" align="left"/>](http://heroku.com)

[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/82/Telegram_logo.svg/2048px-Telegram_logo.svg.png" style="height: 50px" align="left"/>](https://core.telegram.org/bots)<br/><br/>

                                                                                                                    
## 11. Sobre o autor
Olá! Meu nome é Lucas Rodrigues.<br/>
Conecte-se comigo no meu [Linkedin](https://www.linkedin.com/in/lucasrodrigues3/).
