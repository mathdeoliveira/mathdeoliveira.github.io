---
name: Web app com machine learning
tools: [python, machine-learning, heroku]
image: https://previews.dropbox.com/p/thumb/ABdqeIgjskmZd1n2foi_s4KjNTxipz5lP6QLeySqAm9n5OO5rYwwrkgKHxxSkgEwn21bPfthZyfTg0jS-W2_HSmC1nMLErqIJ0VtPgeAqIwY_GiiyobSCQV4_eH-LTLH0NiJbVc8Z--svCceHMAC1w95ZMjHXr0YeN-YHUAEX-d4vFS5FfFlJTDxyddQRdZthWs4QDQESWYGLRkGxos6k8Jcvp-GitlUAGXAyJ9o9DY_ZRhonN_KdZ80eYVp6UYAjrDq6y2Dx7kgku2xx_7L3JrKO1R3t1AiYFTaLCcohKinkcCXI8LxG_AQhdUfCDvC46KTCblrf1V7G9UaRKVuxEl8OhImxvdqo28RAM-vGIDcZQ/p.jpeg
description: Algoritmo de machine learning aplicado em um web app
---

# Introdução
Vamos ver como podemos aplicar um modelo de Machine Learning em um projeto, esse projeto tem como intuito prever o valor de um imóvel na cidade de São Paulo, dado as suas características. Então, com dados do passado disponibilizados no Kaggle podemos criar um modelo de Machine Learning irá aprender e vai ajudar essa previsão.

Temos o problema definido, que é prever o valor do imóvel na cidade de São Paulo, vamos agora conseguir os dados para que possamos treinar os algoritmos e eles aprenderem com o passado. Os dados utilizado neste projeto foram obtidos [neste link](https://www.kaggle.com/argonalyst/sao-paulo-real-estate-sale-rent-april-2019) e esse conjunto de dados contém aproximadamente 13.000 apartamentos para venda e aluguel para cidade de São Paulo, e só tem dados para a data de Abril de 2019.

# Análise Exploratória dos Dados
Esta etapa tem por objetivo criar uma consciência situacional inicial e permitir um entendimento de como os dados estão estruturados, primeiramente vamos criar um dicionário para cada variável do nosso conjunto de dados, retirado do Kaggle.

Dicionário das variáveis

- Price - Preço final anunciado em reais (R$)
- Condo - Preço do condomínio
- Size - Tamanho da propriedade em m²
- Rooms - Número de quartos
- Toilets - Número de banheiros
- Suites - Número de quartos com banheiro privativo
- Parking - Número de vagas de garagem
- Elevator - Se tem ou não elevador
- Furnished - Se a propriedade é mobiliada ou não
- Swimming Pool - Se a propriedade tem ou não piscina
- New - Se a propriedade é nova ou não
- District - Nome do bairro e cidade onde a propriedade está localizada
- Negotiation Type - Se a propriedade está para venda ou aluguel
- Property Type - Tipo da propriedade
- Latitude - Localização geográfica
- Longitude - Localização geográfica

Vamos iniciar mostrando alguns gráficos que representam o nosso conjunto de dados. Para mais informações, por favor entre no [notebook](http://bit.ly/2Qq2ngF).

![alt text](https://previews.dropbox.com/p/thumb/ABeRIYuN54-nazLubzbqW4k9-zr8-gbW7MTDFxcBLYVsYPNn3YcjK26MSOHBlgqTl87OaiRoN7sOCBE4HfgbK4HXiCWNVlcGCvxdAtse8yT9xvAAxDXz46phrdBw6jMM0h4LAIl9TMYshFMKdQb3OSohQ60UlOhAZCxkVwxHVMZ4trtWQYrNDCEVSPSZ_oc7xlh-z4yGm_btjmT0zlImHtwsnVeNOLgvZkHgcLuTgDVXpJs4REZw6dezbjbl1cdW4dn24gkev8Ut3qe8wXafcSDnc6FiotXfrkupTnKQbCCrlCa8ex5Dw4sbQ9CMUNR0IryxLSp26Z6zEW4fsZPvrSIvNPa3QZxkHH9voyb9s9Fxtg/p.png)

Com o gráfico acima podemos evidenciar que a grande maioria dos aptos anunciados tem dois quartos. É interessante sabermos disso pois assim sabemos que a maioria dos aptos são construídos com dois quartos estão à venda, com essa informação podemos levar às construtoras dizendo que com esse número de quartos podem atrair mais compradores. Claro que, não podemos fixar essa informação como verdade única, temos outras variáveis que vão levar ou não a compra e não podemos deixar de lado.

![alt text](https://previews.dropbox.com/p/thumb/ABf4TacJRiwL5LnL6KMjiYP6o_Pu3sA-aAB43tTa70yEiMBxU41tgFVFCDVzUC4LjXm-dKsdgsYgER89YLJ3IB1c3UkFFdIpgrPdHe7UMs0oARo6hZliQBzjIiLwQ5JwRuEV0snfs3r22EdrOGPUzS020XYrBEYui9-EiSwylh9qHkSzxqPRbAQljRQnbHEtq0BkB2WFpUEz9DsCC4-mF23NFvnsRbCWjp8KENmQ_scsJgxbHM3Ejcugrd-IYejrrnEVVojuuJGL_eFk1Kr-j8e8IWK0iViULKryLayT88nFNbVCNKUTkOUpcSbR5rHNriaGq_I7acoygergsjbafJHjizf41J-ri3JysgKXUrk85w/p.png)

Sabemos que os imóveis anunciados são somente da cidade de São Paulo, com o gráfico acima, podemos descobrir a localização de cada um dos aptos anunciado, e vamos evidenciar no gráfico o preço de cada um deles, onde as cores mais escura dos pontos tem o maior preço e os pontos com cores mais claras tem o menor preço.

Feito essa rápida análise vamos iniciar o processo anterior aos algoritmos de Machine Learning. Lembrando que, para ver todo código usado, por favor entre no [notebook](http://bit.ly/2Qq2ngF).

#   Pré Processamento
Vamos iniciar um pré-processamento, vamos retirar algumas variáveis que não me interessa para o nosso modelo, já fiz alguns testes e essas variáveis não faz com que o nosso modelo seja mais eficiente, mas para o futuro seria interessante adicionar as variáveis elevator, furnished, swimming_pool, new e.Nesse primeiro projeto iremos manter mais simples.

Após isso, vamos usar o LabelEncoder para transformar a variável district de categórica para númerica. Então, esse processo transforma, por exemplo, o valor categórico 'Carrão' será transformado para o valor número '19', e o nosso modelo de ML irá usar isso para poder prever os futuros dados. E após isso, dividimos o nosso conjunto de dados em dois, o de treino e o de teste.

O intuito do modelo é a previsão do valor do preço de venda de um imóvel, com isso já sei que vamos usar os algoritmos de **regressão**, existe vários algoritmos de regressão, vou escolher alguns para ver como eles se saem com os nosso dados. As métricas de avaliação dos modelos que escolhi, foram: r2_score, mean_squared_erros e mean_absolute_erros.

A explicação do funcionamento de cada modelo e dos parâmetros fica para um próximo momento, ficaria bastante extenso o notebook. Não entrei também no processo de tunning dos parâmetros, em um projeto real devemos fazer todo esse processo, mas aqui o projeto é tem como intuito o treino/estudo, vamos manter um pouco mais simples.

# Machine Learning
Os algoritmos escolhidos para o nosso problema, foram: XGBoost, LASSO Regression, Random Forest Regression, Linear Regression e Gradient Boosting Regressor.

Usamos cada um desses algoritmos e vimos o retorno das métricas para cada um deles, tivemos que o GBRegressor teve os melhores valores para os nossos dados.

Para os nosso conjunto de dados, o algoritmo GB teve o melhor score de previsão, vamos usar a r2_score para a avaliação, o algoritmo alcançou 88.76%, que é um bom resultado, no futuro podemos incluir mais variáveis para melhorar o modelo e também começar o processo de tunning dos parâmetros. Mas por hora, esse modelo será o escolhido pois teve uma melhor performance em comparação aos outros.

# Aplicando o modelo em um WebApp
Após o treino do modelo escolhido, devemos achar um jeito de usar esse modelo, nesse projeto vamos utiliza Python, HTML, Flask e o Heroku para subir para produção para utilização.

Todos os arquivos usado para a criação do projeto está no meu GitHub, mais especificamente nesse [portfólio](https://github.com/mathdeoliveira/project_predict_house_prices).

![alt text](https://previews.dropbox.com/p/thumb/ABdpiAI2oN1kE-HjqlHQgZTLmMQORErJ9VV-kksC0u4kyXMcTsDD1ag6Nlb8NlnrJ2wjxPqRsKgU3ZLlruJJA_8vPIiuWqO__w8PAQCwgYOgZTSX_Gg-STPXxrsAvXVqsvPhZiQ6hdKzuJCldFHbuLz_gyuCS_1AU3RJ6H-TR2ZMXaeJjLI7hyF2lJsHrl0LDbaik094UPTnXhKB6seHYaAkJ1Th4YqL9aCBO64pM-uQ3QKZWGUMeK4XU9o-HUuGs98TFbbZsu-DeAn_IBlOklNp2Fgkm2mNp_AvCNpnPc9grWXMpBrVIGHDeublVXWh4BozdHBxiJtuO5t_VPcZXco-ixmnEFL40kXs1WgyO77s-g/p.png)

Para ver o aplicar o modelo, eu criei de forma bem simples, um WebApp que podemos entrar com valores reais e com isso prever o valor com os dados de entrada, usando o modelo GB treinado. A imagem ao lado mostra uma forma de como podemos implantar um modelo de Machine Learning, assim o usuário entra com os dados das características do apartamento e ele conseguir calcular a previsão do preço do imóvel.

Então o que acontece, de forma bem simplória, o usuário deseja saber quanto possa custar o apto, acessa o site e ele entra com as caraterísticas do apto o modelo recebe esses dados e, como ele já está treinado, ele consegue prever um valor do apto, a página HTML recebe os dados e mostra o valor retornado pelo modelo para o usuário.

Quer testar você mesmo? Eu disponibilizei por meio do Heroku o webapp para o acesso, [clique aqui](https://datascience-mathdeoliveira.herokuapp.com/).

# Conclusão
Vimos neste artigo uma forma de utilizar Machine Learning para um projeto e o conjunto de dados aqui estudado é um bastante conhecido e com isso podemos aplicar vários modelos para aprender sobre eles, fizemos uma rápida análise de exploração dos dados e descobrimos algumas coisas interessantes. Partimos para criar modelos de Machine Learning onde o intuito é conseguir criar um modelo que possa prever o valor de um apartamento na cidade de São Paulo.

Colocamos em um ambiente de produção, onde o algoritmo usa dados reais para prever o valor do imóvel, com isso podemos ter uma visão do que é possível criar aplicações com Machine Learning para problemas reais.