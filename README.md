# divvy-tripdata
Primeiro Captstone Project do Google Analytics Course on Coursera

A **Cyclistic** é uma companhia fictícia de bicicletas compartilhadas de Chicago. O diretor de marketing acredita que o futuro 
sucesso da companhia depende da maximização do número de membros anuais. Portanto, o time quer entender como ciclistas 
casuas e membros usam as bicicletas da companhia diferentemente. Destes insigths, o time desenhará uma nova estratégia 
de marketing para converter ciclistas casuis em membros. Mas primeiro, os executivos da companhia precisam aprovar 
as recomendações, logo eles precisam estar amparados por informações e visualizações profissionais de dados.

Personagens e time

Cyclistic: é um programa de bicicletas compartilhadas com mais de 5.800 bicicletas e 600 estações de ancoragem.
Lily Moreno: é a diretora de marketing. A companhia se destaca oferecendo bicicletas reclináveis, tríciclos e bicicletas de
carga, fazendo-a mais inclusiva para pessoas com deficiências e ciclistas que não podem usar o padrão duas rodas.
A maioria dos ciclistas optam pela tradicional, cerca de 8% usam a opção assistiva. Usuários são mais provável usá-las para lazer,
no entanto 30% fazem uso para rotina profissional.
Marketing da Cyclistic: é o time de dados responsável por coletar, analizar e reportar os dados que auxiliam a estratégia de marketing da empresa.
Executvos da Cyclistic: time orientado a ados que decidirá se aprovará as recomendações do time de marketing.

Sobre a Companhia

Em 2016, Cyclistic lançou com sucesso uma oferta de compartilhamento de bicicletas. Desde então a compahia crsce para uma frota 
5.824 bicicletas que são monitoradas e ancoradas em uma rede de 692 estações pela cidade de Chicago. As bicicletas podem ser
desbloqueadas de uma estação e retornadas a qualquer outra estação do sistema a qualquer momento.

Até agora, a estratégia do time de marketing contou com a conscientização geral para atrair todos os segmentos de consumidores.
Um método que ajudou a fazer tudo ser possível foi a flexibilidade dos planos de pagamentos: passeio único, dia completo, e membros
anuais. Consumidores que compram o passeio único ou dia completo são considerados ciclistas casuais. Cientes que compram o plano
anual são considerados membros.

O time de finanças concluiu que membros anuais trazem mais lucros para empresa do que os casuais. Apesar da flexibilidade
de preços ajudar a Cyclistic a atrair mais consumidores, Moreno acredita que a maximização dos números de membros anuais irá 
ser a chave para o futuro crescimento. Ao invés de criar uma campnha de marketing que almeje todos os consumidores alvos, 
Moreno acredita que há uma boa chance de converter ciclistas casuais em membros. Ela notou que os usuários casuais estão
conscientes do programa e escolheram a empresa para a sua mobilidade.

Questionamentos

1. Como os membros casuais e anuais comportam-se diferentemente?
2. Por que os casuais adeririam ao plano anual?
3. Como pode a companhia usar as midias digitais para influenciar os casuais a adesão do plano anual?
4. 

O objetivo da análise é trazer daos que amparem a uma futura tomada de decisão pelos executivos da Cyclistic.

Os dados foram obtidos através do serviço da nuvem da Amazon Web Services. A fonte de dados é confiável, por assim dizer, os dados
são formatados da maneira correta, completo e livre de dados duplicados. É original, ou seja, é possível localizá-lo em sua fonte de
dados (https://divvy-tripdata.s3.amazonaws.com/index.html). E, por último, os dados são compreensíveis e atuais.

São 24 planilhas referentes aos meses de abril de 2020 até abril de 2022. Cada planilha contém dados referente ao uso de cada
mês de referência. São 13 colunas: ride_id: identificação do passeio; rideable_type: tipo de bicicleta adotada;
started_at: horário de início; ended_at: horário de término; start_station_name: nome da estação de início; start_station_id: 
identificador da estação de início; end_station_name: nome da estação de término; end_station_id: identificador da estação de 
término, start_lat: latitude do início do passeio; start_lng: longitude do início do passeio; end_lat: latitude do final do passeio,
end_lng: longitude do final do passeio, member_casual: tipo de membro.

As ferramentas utilizadas foram a linguagem de programação Python e a ferramenta de Visualizações  Pandas e Numpy para limpeza e manuseamento dos dados, Glob para união dos 24 planilhas em dataset
único, Datetime para trabalho com séries temporais, Matplotlib, Seaborn e Tableau para visualizações, Profilling para EDA e Folium para
análises geográficas.

Devido a união de 24 planilhas com mais de 7 milhões de observações estar muito além do processamento que minha máquina pode dispensar,
opto por realizar a técnica estatística de amostramento randômico estratificado, a qual é realizada através do tomamento de amostra
de cada estrato da população visando manter a representatividade dos dados.

Opto em continuar com 1 milhão de dados já que com essa dimensão a minha análise seria possível, embora o cálculo estatístico 
indique que teria 99% de confiança e 1% de margem de erro com 16.543 observações.

Já num primeiro momento decido não utilizar as colunas 'ride_id', 'start_station_id', 'end_station_name', 'end_station_id', 
'end_lat', 'end_lng' visto que essas colunas apresentavam pouco valor de análise. Por conseguinte, da coluna 'started_at' 
extraio a informação do dia da semana que o passeio aconteceu. Transformo as colunas 'rideable_type' e 'start_station_name' do 
tipo objeto para o tipo categórico, visando a economia de de processamento de dados e utilidade em posterior análise. Da subtração
da coluna 'ended_at' e 'started_at' extraio a duração dos passeios. Da coluna 'started_at' extraio as informações dos meses e com
eles construo uma variável de estações do ano. Posteriormente, realizo a extração de dados discrepantes (outliers)
com a técnica estatítica de alcance interquartílico (interquartile range (IQR)). E, por final, realizo a tradução das colunas 
e valores.

Após essas tranformações, com a Análise possuindo 90.036 obervações, após a retirada dos outliers, e 9 colunas, após as transformações necessárias.

# Visualizaçãoes

O dataset é formado por 58,91% de usuários membros e 41,09% de usuários casuais: 

![2022_06_05_12_19_18_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172057900-4c3f4ef1-cd4a-4d69-afcb-9faa415dcabe.png)

Com o gráfico seguinte é possível notar que a preferência entre os usuários se assemelham. No entanto, os números de bicicletas clássicas é muito mais usado pelos membros anuais.

![2022_06_05_12_30_05_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172058201-d93776e0-9441-4ca3-8816-f526c414abd0.png)

Um dos fatores que diferenciam os usuários é os dias que estes escolhem para consumir o serviço da empresa. É possível notar que a distribuição possui uniformidade entre os dias da semana para os anuais, no entanto para os casuais o uso é mais intenso nos dias que abrangem os finais de semana:

![2022_06_05_12_33_03_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172058396-33321372-729a-4d81-8eed-3cc1dfb3bc21.png)

Outra característica semelhante entre eles é refletido nas estações do ano. Devido Chicago estar localizada na região Norte dos Estados Unidos, a prevalência de temperaturas mais baixas é comum nos meses de Dezembro a Maio, os quais estão contidos as estações Inverno e Primavera. Fonte: [https://www.ncei.noaa.gov/]

![2022_06_05_12_38_10_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172058866-278ea988-b5da-4284-b22e-56f053d74fa6.png)

O gráfico a seguir demonsta a distruibuição da duração dos passeios realizados pelos membros anuais:

![2022_06_05_12_51_28_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172059330-cb534e37-2043-4580-9c3a-2e1dd9719136.png)


A análise estátisca nos diz que a média de duração destes membros é de aproximadamente 14 Min e metade da distribuição se encontra até aprox.10 Min. Por outro lado, os casuais: 

![24841616](https://user-images.githubusercontent.com/50409048/172059389-4f1773ed-416b-4414-82b0-d1b84fe28336.png)

Usam em média durante 20 Min e a mediana dos dados em 16 Min, aambos aproximadamente. 

O gráfico a seguir demonstra o uso durante o tempo para os usuários membros, e nesse intervalo encontra-se também o ponto de mais atenção na pandemia de Covid-19:

![2022_06_05_13_08_11_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172059897-38a39bdc-cfd1-4172-9ffc-f9fc2a67debd.png)

Nota-se que a emergência sanitária não alterou os costumes adotados por estes. E por outro lado: 

![2022_06_05_13_13_30_trip_análise_Jupyter_Notebook](https://user-images.githubusercontent.com/50409048/172059997-3d4e5a32-d640-47cb-8692-572704d72f36.png)

Entre os casuais, é possível considerar que houve um aumento de popularidade durante o ano de 2021.

Diante dessa popularização entre os usuários alvos e a emergência sanitária global. Pode-se hipotetizar que estes usuários se sentiram cerceados com as medidas de restrições adotadas ou passaram a adotar hábitos mais saudáveis de vida. E munido desse fato, um estudo sistematizado concluiu que há redução de 20% de risco de mortalidade em todas as doenças em relação aos não ciclistas. Fonte: [Health benefits of cycling: a systematic review, https://onlinelibrary.wiley.com/doi/epdf/10.1111/j.1600-0838.2011.01299.x]

# Considerações Finais

* As medidas de conversão de usuários casuais para membros pode ser adotada focando nos finais de semana.
* Estações do ano como o Inverno merece investigação mais profunda no sentido da lucratividade da operação, visto que apresenta grande disparidade em relação as outras estações e menor número de usuários casuais para captação de novos membros.
* É  possível notar que a duração dos itinerários casuais é maior que a dos membros. Isso possibilitaria a adesão de campanhas explicativas de como seria mais vantajoso a adesão dos planos de adesão contínua nos postos de embarques mais frequentados.
* No período em análise é possível notar que no Verão de 2021 houve um aumento nítido de popularidade que não se converteu em adesão. É preciso investigar mais a fundo as razões desse aumento. É possível supôr que que esse período corresponda as normas de restrições à Covid-19, caso em que muitos lugares adotaram o trabalho remoto e isso possibilitou um aumento populacional ocioso.
* Munido de estudos acadêmicos, a Cyclistic pode adotar campanhas e profissionais da saúde que corroborem as informações e construir uma campanha com esse foco.


