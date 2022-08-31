---
title: Vazamento de dados o que devemos saber e como lidar
layout: post
date: 2022-08-31
image: https://i.imgur.com/4sIezyt.jpg
tags: [data-science, machine-learning]
comments: true
description: Existem alguns passos antes mesmo em pensar em aplicar machine learning na empresa.
---

<p align="center" width="60%">
    <img width="60%" src="https://i.imgur.com/4sIezyt.jpg">
</p>

Data leakage se refere ao fenômeno onde dados de fora do conjunto de treinamento é utilizado para criar o modelo, essas mesmas informações não estão disponíveis durante a inferência, podendo acontecer em qualquer passo durante o projeto, seja na geração dos dados, amostragem, divisão entre treino e teste e até no processamento dos dados, portanto é necessário o monitoramento do vazamento de dados em todo ciclo no projeto de machine learning.

Visto que temos um objetivo de prever com a melhor acurácia possível utilizando machine learning o data leakage se torna um desafio, pois:
- O vazamento não é óbvio no primeiro momento
- É perigoso pois pode levar o modelo à falha mesmo após avaliação e testes

Temos que tomar vários cuidados dado que o projeto pode ser um fracasso caso não dêmos a devida atenção ao vazamento, portanto temos aqui algumas causas comuns que devemos ficar de olho.

# Aleatoriamente dividindo dados temporais

Existem inúmeros tutoriais de como aplicar machine learning e eles separam os dados de treino e teste de forma direta, mas temos aqui um possível problema, pois os dados podem ter uma relação com o tempo onde a variável alvo, aquela que queremos prever, é afetada pelo tempo.

Imagina um conjunto que contém dados em um intervalo de um mês, e esses dados são de de valores de ações da bolsa de valores, caso seja feito a divisão dos dados de forma aleatória há o risco de vazamento de dados de dados futuros entrarem nos dados de treinamento.

<p align="center">
  <img src="https://i.imgur.com/Dk49Dmf.png" alt="Sublime's custom image"/>
</p>
<p align = "center">
Quando lidamos com dados com relação ao tempo, ao dividir aleatoriamente pode levar ao vazamento de dados
</p>

Para prevenir de vazar dados futuros para os dados de treinamento e evitar que o modelo tenha uma performance terrível nos dados de teste, e pior nos de produção que não foram vistos, precisamos dividir os dados pelo tempo e não aleatoriamente, como exemplo a imagem abaixo utiliza a variável de tempo para que seja dividido corretamente.

<p align="center">
  <img src="https://i.imgur.com/UpdHZIo.png" alt="Sublime's custom image"/>
</p>
<p align = "center">
Para minimizar o vazamento ou até evitar por completo devemos entender e dividir os dados de forma adequada
</p>

# Transformação antes da divisão

Durante um projeto de machine learning dependendo do algoritmo que será utilizado se faz necessário a transformação dos dados, uma forma é fazer o scaling onde pegamos as estatísticas gerais sendo elas média, mediana, etc. Existem outras como a discretização, normalização e padronização dos dados.

Com essas estatísticas retiradas de todo o conjunto de dados é feita a transformação das variáveis, mas isso se configura em um vazamento de dados, já que estamos pegamos informações globais antes de dividir os dados vazando os dados de teste para o de treinamento. Essas informações não estarão disponíveis no nível de produção onde o modelo terá que prever dado as entradas e com isso a acurácia do modelo terá impacto negativo.

O ideal é realizar a divisão dos dados antes de realizar as transformações, com isso é preciso garantir que está usando as estatísticas ou aprendizados a partir dos dados de treino e transformando os dados de validação e/ou teste. Em algumas literaturas é sugerido que seja feito essa divisão antes mesmo de qualquer análise exploratória e preparação de dados para evitar que não tenhamos informações sobre os dados de testes, já que esse tenta simular os dados de produção.

# Substituindo valores faltantes com dados de teste

Ao decorrer de um projeto podemos ter tido o contato com valores faltantes de algumas colunas e foi definido que será feito a substituição desses valores, existem diversas técnicas a serem utilizadas e uma forma é a substituição pela média.

Quando utilizamos todo o conjunto de dados para calcular a média e substituir os valores faltantes o vazamento de dados pode ocorrer.

Como no ponto anterior, devemos utilizar o conjunto de dados de treino para que não ocorra esse vazamento, assim podemos prevenir que o modelo tenha um impacto dado o vazamento.

# Dados duplicados

Ao percorrer o percurso da modelagem de dados para que o algoritmo tenha mais informações sobre o problema que queremos solucionar em algum ponto seja necessário a junção de dados de fontes diferentes, e nessa junção pode ser gerado dados duplicados sem intenção.

E além disso, caso o problema for uma classificação e se faz necessário a utilização de técnicas de oversampling para expandir a quantidade dados da classe com poucos exemplos também pode ser gerados dados duplicados neste processo. Assim podemos, sem a intenção, ter os mesmos valores duplicados no conjunto, assim o modelo terá um vazamento preocupante, portanto temos sempre que verificar a questão de dados duplicados antes da divisão e também após a divisão dos dados.

# Vazamento de dados em grupos

Ao termos os dados modelados pode acontecer de aparecer o mesmo registro com pouca diferença entre eles mas com o mesmo valor da variável alvo, um dos motivos pode ser que foi gerados em dias diferentes ou tenha algum valor que as diferencia, e com isso temos uma correlação entre as duas e ao realizar a divisão dos dados esse dois valores podem ser direcionados ao treino e também ao teste, se definindo como um vazamento.

Este tipo é difícil de ser identificado sem conhecer a fundo sobre como os dados são gerados, portanto se faz necessário a checagem e também não deixar de lado o conhecimento que as pessoas especializadas no assunto podem contribuir com o projeto.

# Conclusão

Neste post você pode ter descoberto que existem alguns pontos importantes a serem levantados ao decorrer do projeto de machine learning, e o data leakage é somente um deles, ao encontrar em alguns dos pontos anteriores e identificar o vazamento os passos que devemos tomar podem ser:
- Tentar consertar o vazamento
- Identificar, documentar mas não realizar o estudo para arrumar, pois o problema a ser resolvido não tem impacto com o vazamento

O interessante é que, caso seja tomada a direção de arrumar o vazamento, podemos ter identificado somente em uma variável mas ao remover esse vazamento pode ser identificado outros vazamentos de outras variáveis e até criar novos vazamentos. Crie monitoramentos para verificar a adição de novas variáveis, se a adição melhora e muito a performance do modelo no treinamento pode significar que ela é realmente boa e foi acertado a escolha dela ou pode ser um vazamento da variável alvo nos dados de treinamento e isso deteriora a performance do modelo em teste e até em produção.