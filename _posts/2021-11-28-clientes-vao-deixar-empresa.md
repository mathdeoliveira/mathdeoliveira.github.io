---
title: Business Analytics - Quais clientes vão deixar a empresa?
layout: post
date: 2021-11-28
image: https://previews.dropbox.com/p/thumb/ABfovaf9Xq-UrMgJps_CFct-lgs88bSDdx1ku3nkR5uJlBmZdc0fSGByn09N0k_68Uxe61PkNupfvHBOBAoGWOrR0Dvp_EgOo7lNl4O1KzCTysHXJxb2AJR1jIUt5mrN8O4HK4GCrbwXALK7nfa0E39n8AQONFDr_CvlLkU3DZy24jl82iNUBrDzLzKKmfgQ36a3g437vDoTZ3zF2Px0mxL-imXFj1qbGvIwI-buT0kwSirS6oncmij7N_1r7NcCiLn1sZKHVdDmZFz5a4J8HixVh5CTFjNSLxZIfg3w5UCTYVzjOoX7UyUmqpNOjgNvOiO_l4FMy35aVqZVfsQ39TnUT15vIm_Wrr-vTsxZLMgZBw/p.jpeg
tags: [data-science, python]
comments: true
description: O churn é uma métrica que mede a rotatividade de clientes do negócio isso está relacionado com os índices de evasão dos clientes a previsão dessa métrica é de suma importância.
---

O churn é uma métrica que mede a rotatividade de clientes do negócio isso está relacionado com os índices de evasão dos clientes e cancelamento dos serviços do negócio. O churn pode ocorrer de diversas maneiras diferentes e identificando os motivos que fizeram o seu cliente cancelar os seus serviços cria-se a oportunidade de criar estratégias de retenção desses cliente.

O foco desse estudo é usar dados passados para entendermos quais foram os motivos que fizeram o cliente cancelar os serviços dessa empresa, iremos utilizar de algumas técnicas de business analytics para tal e com esse estudo sobre esse caso será possível entender os motivos do churn e podemos levar aos tomadores de decisões informações valiosas sobre o negócio baseado em dados reais.

Irei demonstrar aqui algumas técnicas de business analytics para resolver um problema proposto pela direção do banco, hipotético, eles gostariam de saber mais sobre os clientes que deixaram o banco e para isso teremos que responder a seguinte questão:

> Quais são os motivos mais importantes e que são decisivos para os clientes cancelarem as suas contas?

**Insights da análise exploratória dos dados**

O intuito da análise exploratória dos dados é descobrir mais sobre os nossos dados, aqui vou te mostrar alguns insights que consegui explorando os dados.

Começando com o gênero dos clientes, conseguimos perceber que os clientes do gênero feminino são os clientes que mais deixaram de ser clientes. ![alt text](https://previews.dropbox.com/p/thumb/ABemkg0haW8dAAjGNhETaUbVJsaIwS5-SYhPWTB9rBTlAPtf63mJxcTQf9xgGW5FlWp6w5KKyKLLQGT6FgIqhCvW14chRMcVvvS4nbTQZlxfUybn4cQBiUM2PklodTcKJabsfLFVIunI_L-SWwdXI8lB7hLliuPXrRRlauZULu_qwMzY-JqskRqhc3idlw8OXkwQwJQBBCsUQSYfYILfPIz_I_9RsBziYb82MW1mj7TCOJpEoc9_l4JzkhQGuE3IPtMUC5BAJkuKDW-J5utCfnwPgS5cbyJiiDDbeBhd71G-576YeTbc3aL1KKVYxfP5ssANYMNNIaoY6N3V51mi65Fr5eD8ybRR5VqzFm0lkE24aw/p.png)

Continuando, temos uma variável que mostra se o cliente tem ou não um cartão de crédito, representado por 0 e 1. A tabela nos mostra que os clientes que possuem cartão de crédito são a maioria que deixaram de ser clientes do banco. ![alt text](https://previews.dropbox.com/p/thumb/ABdd0aiFT8VMuDsAtO0H2yKmy-T25RCkPziSfx7072TTD3yhUSyif2n8y3dWb6Qns52cM_7dgYVPpI7Bj8TSQZ7Vvdwy8ozJKF8h0IBQVKkzCZERrxLeLydzLZUbjXewdFTutrlCaiPG2NGSPuYjl3PgPamTgOV7ToIcYrUMf97abWPQpybabJILguIFjTwwr6Bw0vrYCdPv5V-zvaKo7uHP3cAhmgIFtUa0FPPx7LYqua40g01EHM1GWN8dGkVNt_KbbWTH_gKuhaY3cG3ZXkbU4p_LuE4yJNphN_QDGNeO4ewF7y6q-np2SeT6STY_GYJJM-KBUb6Uqs3F1bgY5bMoVwjgip4MuAQNlwSnpkEKnA/p.png)

Convido você a entrar no notebook para ver toda a análise dos dados feita, [clique aqui.](https://bit.ly/2O0cJSI)

**Algoritmos de machine learning**

Vamos utilizar de algoritmos de machine learning para auxiliar na resolução do nosso problema. Sabemos que se trata de um problema de classificação, portanto vamos utilizar os algoritmos com essa finalidade.

Um dos algoritmos escolhido é Regressão Logística, para termos uma visão estatística vamos usar a biblioteca *statsmodels*. Tivemos o seguinte resultado:

Para um intervalo de confiança de 95%, temos que alguns coeficientes não foram estaticamente significativos, poderiam ser removidos do modelo. Esses coeficientes podem ser interpretados em termos de aumento ou diminuição da chance do cliente deixarem ou não de ser cliente, pois estão em escala logarítmica.

Interpretando alguns dados temos que, os clientes do sexo Male possuem menos chances de deixarem de ser clientes do que do sexo Feminino. Os clientes que são mais velhos tem mais chances de deixarem de ser clientes do banco. Quanto mais tempo sendo cliente do banco menor serão as chances do cliente deixar de ter conta no banco. Os clientes da Alemanha são os que tem mais chances de deixarem de ser cliente do banco.

Temos que para esse modelo algumas variáveis importantes, sendo elas **Geography, Gender, Age, Balance e IsActiveMember.**

Para fazer uma comparação com a Regressão Logística, usaremos o Random Forest Classifier, que é um algoritmo baseado em árvores. ![alt text](https://previews.dropbox.com/p/thumb/ABdEvUfrlfB8Kh4RFLKlDSiizlQp696HBjrDjQmKyo0qGYC9fSMkZSFXjbPscRoXqK1GzIX-pGo9ePBkWF7sdP5z2aufUBz2w58sNZecYYtjWyen0N1g1Z8t0WiB6PTGM26fx2P9VpNAY23DGxuR8g20Rd7jOzRQxEHbrxLFygoNxi_zU6cLSu9AC_lGfL8cPNpVjJhAZ7blPLv7cUxByD_E3kBGJsB170OLIuLh4I_26IAZxlmCcWbhYLux-0BoPqljBOauJIn84eewntADeV7h1VBQrAlM3sL5NTEb64XA1_cnp88YlXT7mAeBnlzGXYt7E4BqMQsR0kH6vUd-eDsggC0ZUSgE8idwUCUUUH-ScQ/p.png)

Para tal, o modelo, de acordo com o gráfico acima, tivemos que as variáveis importantes foram: **Age, EstimatedSalary, Balance e CreditScore.**

**Conclusão**
Fizemos uma boa análise do nosso problema, desde o entendimentos dos dados com a análise exploratória dos dados, onde tivemos alguns insights interessantes até a utilização de algoritmos para auxiliar na resolução do problema e agora podemos voltar na pergunta de negócio, definida anteriormente, e com isso podemos responder com mais convicção e baseado nos dados.

1. Quais são os motivos mais importantes e que são decisivos para os clientes cancelarem as suas contas?

Fizemos dois modelos, onde os dois tiveram resultados um pouco diferente, qual está certo? Os dois estão certos, ainda há um grande trabalho a ser feito, mas podemos responder à essa pergunta com:

**R. A idade é de fato uma variável decisiva e o saldo em conta também tem uma importância. Outros resultados foram mostrados e devem ser levados em conta, já que tiveram uma considerada importância, as variáveis: localização, gênero, score do cartão de crédito e empresa ativa são variáveis que aparecerem como uma importância e devem ser consideradas. Essas são os motivos mais decisivos que levam os clientes a cancelarem as suas contas ou não.**

Todo o trabalho foi feito pautado em dados, portanto pode ser que seja necessário a aquisição de mais dados, criação de mais variáveis e trabalhar melhor com as transformações, aqui o estudo foi feito com intuito de rapidamente entregar um resultado aos tomadores de decisão que irá trazer um impacto positivo ao banco, pois são aspectos que deverão ser trabalhados para a retenção dos clientes.

