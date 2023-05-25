![Rossman](./img/rossmann.png)
 
 <h1 align="center"> PREVISÃO DE VENDAS - LOJAS ROSSMANN </h1>
  
O projeto mencionado é uma iniciativa da comunidade DS (Data Science) com o objetivo de realizar uma previsão de vendas das lojas Rossmann para os próximos 6 meses. Os dados utilizados para esse fim são obtidos do Kaggle, uma plataforma online que reúne conjuntos de dados de diferentes domínios.

Para realizar essa previsão, o projeto utiliza algoritmos de machine learning, que são métodos computacionais capazes de aprender padrões nos dados e fazer previsões com base neles. Esses algoritmos são treinados com os dados históricos de vendas, buscando identificar relações e tendências que possam ajudar a prever as vendas futuras.

Além disso, o projeto segue o método de gerenciamento CRISP, que é uma abordagem amplamente utilizada em projetos de mineração de dados e análise preditiva. O CRISP consiste em uma série de fases iterativas, incluindo compreensão do negócio, compreensão dos dados, preparação dos dados, modelagem, avaliação e implantação. Ao seguir o CRISP, o projeto busca garantir uma abordagem estruturada e sistemática, permitindo a criação de um modelo de previsão de vendas mais preciso e confiável.
 
 ![Crisp](./img/crisp.png)
 
## 1.0. Questão de negócio
A Rossmann opera mais de 3.000 drogarias em 7 países europeus. Atualmente, os gerentes das lojas da Rossmann têm a tarefa de prever suas vendas diárias com antecedência de até seis semanas. As vendas das lojas são influenciadas por diversos fatores, incluindo promoções, concorrência, feriados escolares e estaduais, sazonalidade e localização. Com milhares de gerentes individuais prevendo vendas com base em suas circunstâncias únicas, a precisão dos resultados pode variar bastante.
 
## 2.0. Entendimento do Negócio
Contexto fictício: O CFO (Chief Financial Officer) tem interesse em alocar recursos de forma mais eficiente para as lojas da empresa. Para auxiliar nesse processo de alocação, ele busca realizar uma previsão de vendas das lojas para as próximas 6 semanas.

A previsão de vendas é uma ferramenta valiosa que permite ao CFO ter uma visão antecipada do desempenho esperado de cada loja no curto prazo. Com base nessas previsões, o CFO pode tomar decisões informadas sobre a alocação de recursos financeiros, como investimentos em estoque, contratação de pessoal adicional ou ajuste de despesas.

Para esse projeto será utilizado Aprendizado de Máquina Supervisionada de Regressão - Time Series.
 
## 3.0. Coleta de dados
Na etapa de coleta de dados para esse caso específico, é comum utilizar diferentes métodos, dependendo da fonte dos dados e da disponibilidade de acesso. Para esse caso foi realizado o download dos conjuntos de dados no formato csv por meio da plataforma kaggle.

[Kaggle dados Rossmann](https://www.kaggle.com/competitions/rossmann-store-sales)

Dados | descrição
------- | ---------
train.csv | dados históricos, incluindo as vendas
test.csv | dados históricos, excluindo as vendas
sample_submission.csv | um arquivo de exemplo de submissão no formato correto
store.csv | informações adicionais sobre as lojas


Campos de dados
A maioria dos campos é autoexplicativa. A seguir, estão as descrições para aqueles que não são:

Colunas | descrição
------- | ---------
Id | um ID que representa um par (Loja, Data) no conjunto de testes
Store | um ID único para cada loja
Sales | a receita para um determinado dia (isso é o que você está prevendo)
Customers | o número de clientes em um determinado dia
Open | um indicador se a loja estava aberta: 0 = fechada, 1 = aberta
StateHoliday | indica um feriado estadual. Normalmente, todas as lojas, com poucas exceções, estão fechadas em feriados estaduais. Observe que todas as escolas estão fechadas em feriados públicos e fins de semana. a = feriado público, b = feriado de Páscoa, c = Natal, 0 = Nenhum
SchoolHoliday | indica se (Loja, Data) foi afetada pelo fechamento de escolas públicas
StoreType | diferencia entre 4 modelos diferentes de loja: a, b, c, d
Assortment | descreve o nível de variedade: a = básico, b = extra, c = estendido
CompetitionDistance | distância em metros até a loja concorrente mais próxima
CompetitionOpenSince[Month/Year] | fornece o ano e mês aproximados da abertura da loja concorrente mais próxima
Promo | indica se a loja está executando uma promoção naquele dia
Promo2 | Promo2 é uma promoção contínua e consecutiva para algumas lojas: 0 = loja não está participando, 1 = loja está participando
Promo2Since[Year/Week] | descreve o ano e semana do calendário em que a loja começou a participar da Promo2
PromoInterval | descreve os intervalos consecutivos em que a Promo2 é iniciada, nomeando os meses em que a promoção é iniciada novamente. Por exemplo, "Fev, Mai, Ago, Nov" significa que cada rodada começa em fevereiro, maio, agosto e novembro de qualquer ano para aquela loja.
 
## 4.0. Limpeza dos dados
Durante a etapa de limpeza dos dados, foi realizado um tratamentos para lidar com valores vazios ou ausentes. A substituição desses valores vazios é uma prática importante para garantir a qualidade e consistência dos dados utilizados no projeto de previsão de vendas.

Existem várias abordagens que podem ser adotadas para tratar os valores vazios, e a escolha depende do contexto dos dados e da natureza do problema em questão. O método usado para substituir valores vazios foram com preenchimento com um valor padrão: Nesse caso, os valores vazios são substituídos por um valor específico ou um valor médio ou mediano dos dados existentes.
  
## 5.0. Exploração dos dados
Na etapa de exploração dos dados, o objetivo principal é obter um entendimento mais profundo do negócio por meio da análise dos dados disponíveis. Essa etapa envolve identificar padrões, relacionamentos e insights relevantes que possam ajudar a compreender melhor o comportamento dos dados e a tomar decisões embasadas. A seguir, são apresentadas algumas etapas comuns durante a exploração dos dados:

### 5.1. Análise descritiva 
Inicia-se com uma análise descritiva das variáveis disponíveis, como a média, mediana, desvio padrão, valores mínimos e máximos. Essa análise fornece uma visão geral do intervalo de valores, identificando possíveis discrepâncias ou anomalias nos dados.


attributes |	min |	max	| range	| mean	| median	| std	| skew	| kurtosis
---------- | --- | --- | ----- | ---- | ------ | --- | ---- | --------
store	| 1.0 |	1115.0 |	1114.0	| 558.429727 |	558.0 |	321.908493 |	-0.000955 |	-1.200524
day_of_week	| 1.0	| 7.0	| 6.0	| 3.998341 |	4.0 |	1.997390 |	0.001593 |	-1.246873
sales	| 0.0 |	41551.0 |	41551.0	| 5773.818972 |	5744.0	| 3849.924283 |	0.641460	| 1.778375
customers |	0.0	| 7388.0 |	7388.0 |	633.145946 |	609.0 |	464.411506 |	1.598650 |	7.091773
open |	0.0 |	1.0 |	1.0 |	0.830107 |	1.0 |	0.375539 |	-1.758045 |	1.090723
promo |	0.0 |	1.0 |	1.0 |	0.381515 |	0.0 |	0.485758 |	0.487838 |	-1.762018
school_holiday |	0.0 |	1.0 |	1.0 |	0.178647 |	0.0 |	0.383056 |	1.677842	| 0.815154
competition_distance |	20.0 |	200000.0 |	199980.0 |	5935.442677 |	2330.0	| 12547.646829 |	10.242344 |	147.789712
competition_open_since_month |	1.0 |	12.0 |	11.0 |	6.786849 |	7.0 |	3.311085 |	-0.042076 |	-1.232607
competition_open_since_year |	1900.0 |	2015.0 |	115.0 |	2010.324840 |	2012.0 |	5.515591 |	-7.235657 |	124.071304
promo2 |	0.0 |	1.0 |	1.0 |	0.500564 |	1.0 |	0.500000 |	-0.002255 |	-1.999999
promo2_since_week |	1.0 |	52.0 |	51.0 |	23.619033 |	22.0 |	14.310057 |	0.178723 |	-1.184046
promo2_since_year |	2009.0 |	2015.0 |	6.0 |	2012.793297 |	2013.0 |	1.662657 |	-0.784436 |	-0.210075
is_promo |	0.0 |	1.0 |	1.0 |	0.155231 |	0.0 |	0.362124 |	1.904152 |	1.625796


### 5.2. Visualização dos dados 
Utilizando gráficos e visualizações, é possível explorar as relações entre as variáveis e identificar tendências ou padrões. Histogramas, gráficos de dispersão, gráficos de linhas e box plots são algumas das ferramentas comumente utilizadas para essa análise visual.
 
 <h1 align="center"> Variável numérica </h1>
 
![](./img/variavel_numerica.png)

 <h1 align="center"> Variável Categórica </h1>
 
![](./img/variavel_categorica.png)

### 5.3. Correlação entre variáveis
É importante analisar a correlação entre as variáveis para identificar possíveis relações e dependências. A matriz de correlação ou gráficos de dispersão podem ajudar a entender se as variáveis estão positivamente, negativamente ou não correlacionadas entre si.

### 5.4. Criação de hipóteses
Com base na análise dos dados, é possível criar hipóteses sobre os fatores que influenciam o comportamento dos dados. Essas hipóteses podem ser testadas posteriormente ou fornecer insights para direcionar a modelagem e as estratégias de previsão.

### 5.5 Extração de insights 
Durante a exploração dos dados, é fundamental extrair insights relevantes que possam ser aplicados ao negócio. Isso envolve identificar padrões interessantes, relações inesperadas ou oportunidades de melhoria.
 
 
## 6.0. Modelagem dos dados
Na etapa de modelagem dos dados, o objetivo é preparar os dados de forma adequada para que os algoritmos de machine learning possam ser aplicados. Essa etapa envolve uma série de processos, como codificação de variáveis categóricas em variáveis numéricas, transformações de dados e separação dos dados em conjuntos de treinamento e teste. Aqui estão algumas das principais etapas envolvidas na modelagem dos dados:

### 6.1. Codificação de variáveis categóricas 
Os algoritmos de machine learning geralmente trabalham melhor com variáveis numéricas. Portanto, é necessário codificar as variáveis categóricas em valores numéricos. Isso pode ser feito usando técnicas como codificação one-hot (dummy encoding), onde cada categoria se torna uma nova variável binária, ou a codificação de rótulos (label encoding), onde cada categoria é atribuída a um número inteiro.

### 6.2 Transformações de variáveis 
Em alguns casos, pode ser necessário aplicar transformações em variáveis para tornar sua distribuição mais adequada para os algoritmos de machine learning. Por exemplo, aplicar logaritmo em variáveis com distribuição assimétrica ou utilizar transformações polinomiais para capturar relações não lineares.

### 6.3 Separação de dados de treinamento e teste 
É necessário dividir os dados em conjuntos separados para treinamento e teste. O conjunto de treinamento é utilizado para treinar os algoritmos de machine learning, enquanto o conjunto de teste é usado para avaliar o desempenho do modelo.
 
## 7.0. Algoritmos de Machine Learning
Na etapa de implementação de algoritmos de machine learning, o objetivo é selecionar e aplicar diferentes algoritmos para resolver o problema de previsão de vendas e determinar qual deles apresenta o melhor desempenho para o caso em questão.
 
 ## 8.0. Avaliação do Algoritmo
Após treinar cada modelo, é necessário avaliar seu desempenho com o subconjunto de validação. Métricas apropriadas para avaliação de modelos de previsão podem incluir erro médio absoluto (MAE), erro médio quadrático (MSE), coeficiente de determinação (R²) e outros. Com base nas métricas de desempenho, é possível comparar e identificar qual algoritmo apresenta os melhores resultados.

Ajuste de hiperparâmetros: É possível que cada algoritmo possua hiperparâmetros que afetam seu desempenho. Por meio de técnicas como pesquisa em grade (grid search) ou otimização bayesiana, é possível ajustar esses hiperparâmetros e realizar testes adicionais para encontrar a combinação ideal que maximize o desempenho do modelo.

Seleção do melhor modelo: Ao finalizar a implementação dos algoritmos e avaliar seu desempenho, é possível selecionar o modelo que apresenta o melhor desempenho de acordo com as métricas escolhidas. Esse modelo será utilizado para fazer as previsões de vendas futuras com base nos dados disponíveis.
 
## 9.0. Modelo em produção
Na etapa de colocar o modelo em produção, foi desenvolvido um dashboard utilizando a plataforma Streamlit. No entanto, uma implementação adicional que traria benefícios para o CFO seria disponibilizar as informações através de um bot no Telegram, proporcionando uma forma mais conveniente e acessível de acessar os dados de previsão de vendas.
