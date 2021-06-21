
# Análise exploratória das estatísticas da NBA nas últimas 20 temporadas

Depois de alguns anos namorando a área de análise de dados vendo cursos no datacamp e vídeos no youtube, resolvi perder o medo e colocar em prática meu primeiro projeto de análise de dados usando as bibliotecas Pandas e matplotlib do Python. O meu primeiro projeto envolve as estatísticas dos times na últimas 20 temporadas da NBA.

## Introdução

Nos últimos anos o telespectador assíduo da NBA vem tendo a sensação de que o basquete norte-americano mudou para um jogo maior de perímetro, no qual as equipes estão selecionando mais arremessos de três pontos a cada temporada.

O objetivo da análise é mostrar essa mudança da seleção de arremessos dos times nos últimos 20 anos com os dados e estatísticas que a liga disponibiliza, e apresentar alguns contextos do basquete da NBA nos últimos anos. A análise exploratória apresentará as médias das estatísticas ofensivas dos times por temporada: Arremessos de quadra, arremessos de três pontos arremessos de quadra (FG), aproveitamento de arremessos (FG%), tentativas de três pontos (3PA) e % de aproveitamento de 3 pontos (3P%).  

Para coletar os dados acabei fazendo um webscrapping direto do site da NBA. Sei que existe uma API, mas preferi interagir com a aplicação em um projeto futuro. Para realizar o webscraping, contei muito com a ajuda desse vídeo https://www.youtube.com/watch?v=fAW6AxMHego. Com essas estatísticas construí alguns gráficos simples que apresentam a evolução dos arremessos. Ainda, busquei comparar a evolução dos jogos de temporada regular e de playoffs

Como disclaimer, é um código de alguém com o nível iniciante-intermediário, existem algumas melhorias que eu pretendo implementar e também estou aberto a feedbacks ou outras formas de construção do código. 😊 Como saída do webscraping, tive duas tabelas, uma para os playoffs e outra para a temporada regular. 

Essas tabelas contêm estatísticas gerais do jogo por time e por temporada: porcentagem de vitórias e médias por jogo de arremessos, de aproveitamento de quadra, de rebotes e de assistências. O foco da análise são os arremessos e os pontos: Tentativas de arremessos de quadra, arremessos de quadra convertidos % de aproveitamento, Tentativas de  arremessos três pontos, arremessos de três pontos convertidos e % de aproveitamento. 


# Os passos do projeto são: 

### Webscrapping do site da NBA:
   * Dados de temporada regular
   * Dados de playoffs
   
### Visualização da página:
   
   A página de estatísticas dos times da NBA por temporada pode ser acessada no seguinte endereço: ![image](https://user-images.githubusercontent.com/83252023/122690551-8d74b100-d200-11eb-809b-8ee5dfbf215f.png)


Os filtros que o webscraping irá utilizar são os de temporada e o tipo de temporada. 


# Webscraping e Transformação

### 1) Webscraping:

1. Definir uma lista com as temporadas que eu quero buscar. Cada temporada será utilizada no url para o webscraping.

2. Definir um loop, para cada temporada: 

    * Pegar a URL e o XPATH da tabela com o Selenium 
    * Selecionar cabeçalhos e linhas da tabela
    * Tansformar o cabeçalho e as linhas em um DataFrame, 
    * Transformar o dataframe: selecionar colunas, adicionar coluna da temporada e definir o index
    * Adicionar o resultado do loop ao DataFrame vazio iniciado antes do loop


### 2) Transformação dos dados:

Na transformação dos dados, acabei optando por fazer a maioria das transformações dentro do loop. Primeiro, o loop retorna uma tabela com algumas colunas ocultas, acabei eliminando todas. Já para a análise posterior,  adicionei uma coluna de temporada, uma coluna que mostra a % de arremessos de três pontos dentro dos arremessos de quadra além de adicionar colunas que ranqueiam os times nas estatísticas de conversão de arremessos de três pontos e de % arremessos de 3 pontos dentro dos arremessos de quadra.

* Transformações dentro do loop do código de webscraping:
    * Limpeza de tabelas ocultas no site
    * Inserção da coluna da temporada
    * Inserção de coluna de rank do time da temporada e de 3PSHARE

As alterações nas tabelas que eu realizei fora do loop foram alterações que considerei importante para futuras análises. Primeiramente, peguei de uma página na wikipedia uma lista de times e suas abreviações. 

Acabei fazendo um merge da lista de abreviações para a tabela de estatísticas. Com esse merge, concatenei a coluna de abreviação e a coluna de temporada, para criar um código único nas tabelas de playoffs e de temporada regular.

Por fim, realizei um join entre ambas as tabelas que cria uma coluna na tabela da temporada regular que retorna se aquele time naquela temporada foi para os playoffs ou não (também pretendo utilizar em análises futuras).

 * Transformação fora do loop de webscraping:
   * Webscraping de uma lista de times e suas abreviações
   * Merge da lista de abreviações com os times
   * Join da tabela de temporada regular com a tabela de playoffs para criar coluna na tabela de temporada regular que     retorna se o time foi para os playoffs naquela temporada ou não.
   
   
Como resultado, temos as seguintes saídas:

![image](https://user-images.githubusercontent.com/83252023/122690923-bdbd4f00-d202-11eb-87b3-40ac8aefa20f.png)
![image](https://user-images.githubusercontent.com/83252023/122690928-cdd52e80-d202-11eb-9ac6-5ed29eb8570b.png)

   
## Análise exploratória dos dados
    
Com essas estatísticas construí alguns gráficos simples de linha que apresentam a evolução dos arremessos. Ainda, busquei comparar a evolução dos jogos de temporada regular e de playoffs.

Sendo sincero, após o webscraping eu me sentiria mais confortável utilizando o Power BI para construir os gráficos. Mas como o intuito é aprimorar o uso das biblioteca pandas e matplotlib acabei forçando a parte de transformação das tabelas e de construção dos gráficos no python.


    Gráficos:
    
    * 1. 3P Attempts
    * 2. Field Goal Attempts versus points
    * 3. ThreePoint Share
    * 4. ThreePoint Share vs 2P Share
    * 5. FG% versus 3P%
    * 6. OFfensive Stats


#### 1. Tentativas de arremessos de três pontos


![3PA](https://user-images.githubusercontent.com/83252023/122691158-4be60500-d204-11eb-9c79-202fd486347c.JPEG)


O primeiro gráfico vem para confirmar a sensação que temos nos últimos anos: as equipes passaram a ter mais tentativas de arremessos de três pontos por jogo. No começo do século a média por jogo era de 13.7 tentativas de 3 pontos. Na última temporada regular (2020-21) esse número saltou para 34.6 tentativas de arremessos de 3 por jogo.
    

Interessante notar que a linha dos playoffs se manteve sempre perto e em alguns momentos acima da linha da temporada regular. Geralmente podemos pensar que jogos de playoffs são mais defensivos, mais pegados, com arremessos mais bem selecionados. Porém, pode fazer sentido a média de arremessos de três pontos ser maior nos playoffs se os times que avançam para a pós temporada são os que mais possuem tentativas de arremessos no geral.



Todavia, entender que os times passaram a arremessar mais de três pontos não necessariamente significa que o jogo ficou mais orientado para os arremessos do perímetro. O jogo pode ter se tornando mais ofensivo sem necessariamente os arremessos de três se tornarem dominantes nos playbooks. Para analisarmos isso, o próximo gráfico apresenta que os times passaram a arremessar mais no geral, consequentemente, os arremessos de três pontos também cresceram.

### 2. Evolução da média de Pontos e arremessos por temporada

![FGAversusPoints](https://user-images.githubusercontent.com/83252023/122691227-cca50100-d204-11eb-94a1-aed90cffba75.JPEG)

Esse gráfico já mostra a sensação geral de que nos playoffs o jogo se torna mais defensivo, a linha dos playoffs está mais afastada da linha da temporada regular. 


Como depois de montar os gráficos eu me toquei na questão de que a quantidade de tentativas de arremessos de quadra contemplam os arremessos de três, acabei fazendo uma conta simples pra saber qual o percentual de arremessos de três pontos dentro dos arremessos totais. 

Acredito que essa seja uma comparação mais fiel para mostrar que o jogo no geral vem se tornando mais orientado ao arremesso de três pontos. 

### 3. % de arremessos de três pontos dentro dos arremessos de quadra

![3PSH](https://user-images.githubusercontent.com/83252023/122691262-ff4ef980-d204-11eb-8f12-22748cab945e.JPEG)
![3PSHAREvs3PSHARE](https://user-images.githubusercontent.com/83252023/122691266-05dd7100-d205-11eb-87bd-89780fb7ed1e.JPEG)

Na última temporada regular, os times tiveram em sua seleção de jogadas arremessos de três pontos como quase 40% das escolhas de arremessos de quadra. Na temporada 2000-01 essa % era de 17%

Sabendo que a escolha de arremessos de três cresceu dentro da seleção de arremessos no geral, podemos considerar que o basquete da NBA se tornou mais orientado aos arremessos de 3 pontos. Apenas a quantidade de arremessos de três pontos não explicava que estes estavam se tornando mais comuns, mas apresentava somente a noção de que o jogo se tornou mais ofensivo no geral, com os arremessos de quadra aumentando ao longo do tempo.

Mas o que explica essa mudança? O jogo poderia estar se tornando mais ofensivo, com mais tentativas de arremessos, sem necessariamente os times selecionarem mais arremessos de fora. Uma possível explicação pode estar na ofensividade do jogo no geral e no aproveitamento dos arremessos.

![image](https://user-images.githubusercontent.com/83252023/122691672-8ac98a00-d207-11eb-8b3c-bb9ef9e17d22.png)


![3PvsFG](https://user-images.githubusercontent.com/83252023/122691723-d0865280-d207-11eb-90ef-64f12b968ea0.JPEG)
![Offensive Data](https://user-images.githubusercontent.com/83252023/122691726-d4b27000-d207-11eb-9788-0ca2b6d72629.png)

A premissa estatística dessa mudança é que o aproveitamento dos arremessos de três e de dois pontos são semelhantes, e suas médias por temporada não variam tanto. Portanto, a medida que o volume de jogo aumenta (mais arremessos e mais ataques por partida), vale mais a pena arremessar de três pontos, que o retorna mais, do que arremessar de dois pontos.   A lógica é: já que vamos arremessar mais, que seja mais arremessos de três pontos, pois a recompensa é maior.


Outra explicação (dessa vez esportiva) seria a mudança da posição de armador. Na última década os armadores passaram a ter um volume de jogo maior, se tornando mais explosivos e buscarem mais a cesta dentro de quadra, não sendo mais aquele armador clássico focado nas assistências e em cadenciar o time. Temos vários exemplos: Kyrie Irving,  John Wall, Damian Lillard, Curry, Kemba Walker, James Harden, Russel Westbrook, Donovan Mitchel, Jamal Murray, Trae Young e Devin Booker.

Ainda, houveram mudanças nas regras que tornaram o jogo mais ofensivo. A última mudança significativa foi na temporada 2018-2019, que reduziu o tempo de posse do time que pega um rebote ofensivo de 24 segundos para 14 segundos. 


## Conclusão e próximos passos

A confirmação de que os times passaram a arremessar mais de três pontos traz várias outras dúvidas a serem exploradas.

Uma análise futura é sobre a posição de armador, se a % de aproveitamento não mudou, pois um armador tende a ser um ótimo arremessador. 

Não há como analisar bolas de três e arremessos sem analisar o time do Golde State Warrios a partir da temporada 2012-2013. A minha teoria é que a média de arremessos de três pontos nos jogos de playoffs supera a média da temporada regular desde 2013 por conta do Golden State Warrios. Como nos playoffs são menos times e menos jogos, a média acaba sendo mais sensível a outliers, a ideia é buscar saber qual time impactou nessa mudança.

Por fim, ainda pretendo buscar entender se selecionar mais arremessos de três pontos por jogo se tornou um pré-requisito de sucesso na nba (por isso a coluna se o time foi para a pós temporada e a coluna do ranking do time na estatística).







