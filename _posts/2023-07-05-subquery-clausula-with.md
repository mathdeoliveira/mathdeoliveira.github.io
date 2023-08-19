---
title: Como usar uma Subquery com WITH no SQL
layout: post
date: 2023-07-19
image: https://i.imgur.com/TCrZWDp.jpg
tags: [sql, database, subquery]
comments: true
description: Neste artigo, vamos trazer pra vocês os tipos de Subquery e a diferença entre elas, em qual momento utilizar cada uma no SQL.
---

# Introdução

No emocionante mundo do SQL, existe uma dupla dinâmica que está pronta para levar suas habilidades de análise de dados a um novo patamar: as subqueries e as Expressões de Tabela Comum, ou CTEs. Neste artigo, vamos mergulhar de cabeça nesses conceitos sem complicação, entender onde e como podemos aplicá-los para fazer mágica com nossas consultas SQL. Vamos desvendar os diferentes tipos de subqueries e descobrir quando é hora de escolher entre elas e as CTEs, tudo isso para tornar sua jornada na manipulação de dados mais fácil, intuitiva e cheia de insights surpreendentes. Prontos? Vamos lá!

Acesse o link abaixo para assistir o conteúdo em forma de vídeo.
{% include elements/video.html id="4xFH7fUTAD8&t" %}

# Subquery
Mas afinal, o que é Subquery? É o seguinte, bem direto, Subquery é uma consulta dentro de outra consulta, assim permite você realizae execuções de comando SQL mais complexos entre tabelas, e por isso você pode utilizar a Subquery nas cláusulas:

1. SELECT
2. WHERE
3. FROM

Então vamos ver exemplos de cada um desses agora:
1. SELECT

```sql
SELECT coluna_1,
       (SELECT coluna_2
       FROM tabela_2)
FROM tabela_1
```

2. WHERE

```sql
SELECT coluna_1
FROM tabela_2
WHERE coluna_3 > (SELECT sum(coluna_2)
                  FROM tabela_2)
```

2. FROM

```sql
SELECT coluna_1
FROM (SELECT coluna_1
      FROM tabela_1)
```

Olhando friamente cada um dos exemplos acima pode ser que não consiga ver possibilidades de uso, mas posso te garantir que saber dessa sintaxa em algum momento você vai lembrar e vai usar, então saber esse conhecimento vai trazer benefícios no futuro, que eu acredito que seja próximo. Você entendeu, certo? Meu intuito aqui é apresentar esse conhecimento para você usar no dia a dia.

# CTE

Bom, continuando aqui nosso conteúdo, vamos para a parte dos CTEs, e de primeira vamos para a definição: É uma forma de construir tabelas de forma temporária para acessar cada uma posteriormente no próprio código SQL, talvez o seu entendimento vai facilitar nos exemplos que vou apresentar logo mais, mas antes gostaria de comentar alguns pontos que utilizando CTE você vai ganhar:
- Facilita a leitura e a compreensão de uma query extensa
- Evita a repetição de queries que são necessárias mais de uma vez

Para utilizar essa funcionalidade é necessário eu te dizer que segue uma sintaxe, essa sintaxe é utilizar a cláusula WITH, e de novo, você vai compreender mais nos exemplos. Visto que temos essas suas possibilidades de Subqueries, quando devemos escolher uma ou outra, a verdade é que não existe uma regra formal e decidida internacionalmente, mas posso te passar alguns pontos.

Escolher subquery para utilizar pode ser uma boa quando você quer usar no filtro, vulgo WHERE, em agregações em conjunto com o GROUP BY e quando você quer retornar uma coluna no seu SELECT.
Escolher o CTE quando você deseja e vá reutilizar a subquery mais de uma vez pois estaremos até diminuindo o consumo no banco, deixar o seu código SQL mais organizado porque é bem possível você desenvolver um comando bastante extenso e um dos poderes do CTE é criar recursividade.

Vamos para a parte onde vemos a mágica dos comandos acontecer, prática :D!

# Colocando o conhecimento em prática
## Subquery
### Select

O comando abaixo é um exemplo na utilização de subquery no Select, ela simplesmente está trazendo uma contagem e enriquecendo sua consulta SQL com informações extras de outra tabela, e sim, o mesmo resultado pode ser alcançado em outra forma, aqui quis te mostrar que é possível utilizar no Select.

<img src="https://i.imgur.com/LObwNlr.png" width="500">

### Where

A outra forma é utilizar no filtro da query, esse confesso que pode vim a ter uma utilização mais comum, pois ali no valor você pode fazer o calculo de qualquer outra tabela e assim filtrar, pode ser uma soma, contagem, média e por ai vai, mostrei que também pode retornar uma lista de valores e filtrar somente por esses valores.

<img src="https://i.imgur.com/HteXVvC.png" width="500">

### From

E o comando no FROM pode ser útil quando você quer fazer uma agregação de agregação, no comando da imagem eu estou primeiro fazendo o somatório agrupando e depois estou tirando a média de todos os valores já somados e assim a subquery foi útil :)

<img src="https://i.imgur.com/BbWPAgA.png" width="500">

### CTE

Vamos aqui demonstrar um código que se utilizar das tabelas temporárias criadas. A regra é a seguinte, você precisa iniciar o comando com a claúsula WITH a seguir dar um nome para a tabela, usa a criatividade aqui, adicionar mais uma claúsula AS, abrir os parênteses, não esqueça de fechar, e dentro dele escrever o seu comando SQL normalmente. Ah, e outra coisa, você não precisa repetir o WITH para uma próxima tabela, só é preciso adicionar uma vírgula e abrir um novo parêntese, como no exemplo.

<img src="https://i.imgur.com/TrQGuFO.png" width="500">

No comando acima dá pra ver que criei duas tabelas e na segunda eu utilizei a primeira, assim aproveitei uma tabela já preparada e depois ao final é necessário você realizar o comando de selecionar alguma das tabelas criadas no CTE e com isso pode realizar o comando que vai devolver o resultado que deseja, inclusive você pode criar subqueries aqui também e cada vez mais você vai aplicando complexidade caso seja necessário no comando.

## Finalização

Bom, espero que tenha te dado bons motivos para você se aprofundar nessa capacidade que o SQL possui, tenho certeza que você aprendendo e colocando em prática você vai dominar o conhecimento e o no seu dia a dia aplicar ele vai ser bastante comum e sem problemas.