---
title: Windows Functions - o que são e como funcionam?
layout: post
date: 2023-07-19
image: https://i.imgur.com/TCrZWDp.jpg
tags: [sql, windows-functions]
comments: true
description: Neste artigo, vai ser mostrado o que são as Windows Functions, como utilizá-las de forma eficiente e como elas podem agregar poder e flexibilidade às suas consultas SQL.
---

# Introdução

Neste artigo, vamos mergulhar em um recurso avançado e poderoso oferecido por sistemas de gerenciamento de banco de dados relacionais: as SQL Window Functions, também conhecidas como Funções de Janela. Essa funcionalidade se destaca como uma ferramenta essencial para realizar cálculos e agregações em subconjuntos específicos de dados sem a necessidade de subconsultas complexas ou junções intricadas. Além disso vamos demonstra como elas podem ser empregadas e desafios para você praticar, então vamos para o conteúdo.

Acesse o link abaixo para assistir o conteúdo em forma de vídeo.
{% include elements/video.html id="MzxIhnIaXuY" %}

# Definição

Uma SQL Window Function (Função de Janela) é uma poderosa e avançada funcionalidade disponível em sistemas de gerenciamento de banco de dados relacionais que permite realizar cálculos e agregações em um conjunto de dados específico, sem a necessidade de usar subconsultas ou junções complexas. Essa funcionalidade é uma parte importante da linguagem SQL padrão e é suportada por muitos bancos de dados populares, como PostgreSQL, Oracle, SQL Server e MySQL.

O termo "janela" neste contexto refere-se a um conjunto de registros (linhas) selecionado de acordo com um critério específico. A janela pode ser definida com base em um particionamento dos dados e/ou uma ordenação específica. As funções de janela são aplicadas aos dados dentro dessa janela, permitindo a execução de cálculos e análises sobre um subconjunto específico dos dados.

A grande diferença é que vocÊ vai estar olhando por linhas individuais, essas vc pode realizar alguma algum tipo de operação, uma função de agregação normal retorna somente uma linha pelo grupo de agregação, window function vai retornar todas as linhas e cada uma delas vai possuir o valor calculado que foi definido na janela

Uma grande vantagem das funções de janela é que elas permitem que você trabalhe com valores agregados e não agregados de uma só vez porque as linhas não são recolhidas juntas. 

## Anatomia de uma Window Function

Window function possui três partes essenciais, sendo elas:
1. **Agrupamento**, é o primeiro pilar das SQL Window Functions é o agrupamento. Imagine seus dados como um grande conjunto, e o agrupamento é a maneira de subdividir esse conjunto em partes menores e mais gerenciáveis. A cláusula PARTITION BY desempenha um papel crucial aqui, permitindo que você defina critérios específicos para agrupar seus dados. Cada "janela" resultante se concentra em um subconjunto particular de dados, permitindo análises específicas sem perturbar o panorama geral.
2. **Ordenação**, é o segundo pilar que influencia o comportamento das SQL Window Functions. Pense nisso como a maneira de dispor suas informações para análise. A cláusula ORDER BY determina a ordem em que os dados são processados dentro da janela. Isso é fundamental para análises sequenciais, como cálculos baseados em datas ou eventos consecutivos. A ordenação permite que você siga o fluxo natural dos dados, revelando tendências e insights de maneira contextual.
3. **Intervalo**, é o terceiro pilar, acrescenta um toque de granularidade à sua análise. Usando as cláusulas ROWS ou RANGE, você define quantas linhas antes ou depois da linha atual devem ser incluídas na análise. Isso é especialmente útil para calcular médias móveis ou detectar tendências em dados sequenciais. A escolha entre ROWS e RANGE depende da natureza do seu problema e dos insights que você deseja extrair.

Ao dominar esses três elementos, você estará armado com um conhecimento profundo das SQL Window Functions. Com a capacidade de agrupar, ordenar e definir intervalos com precisão cirúrgica, você poderá criar análises mais ricas e insights mais detalhados. À medida que nos aprofundamos em exemplos práticos e cenários reais, você verá como esses elementos se combinam para proporcionar uma visão mais nítida e holística dos seus dados. Prepare-se para enxergar além do óbvio e descobrir as possibilidades surpreendentes que as SQL Window Functions trazem para a análise de dados.

## Aplicação das Windows Functions

Vamos utilizar um banco de dados hipótetico para que seja possível a criação de cenários para simular a utilização de cada uma das windows functions, é importante ressaltar que não vamos abordar todas elas, até porque cada banco de dados que existe no mercado vai ter uma ou outras que são exclusivos para ele e não existe em outros, mas vamos falar das mais comuns e usuais.

### Window Function: ROW_NUMBER()

Imagine que você seja um analista de dados em uma loja de varejo, buscando otimizar a performance dos produtos. Ao usar a SQL Window Function, como exemplificado abaixo, você pode rapidamente identificar os produtos mais vendidos em cada dia, permitindo ajustes ágeis nos estoques, promoções direcionadas e ações estratégicas para maximizar o impacto das vendas e tomar decisões informadas para impulsionar o sucesso da loja.

```sql
with venda_por_dia as (SELECT
    produto,
    data_venda,
    sum(valor_venda) as sum_vlr_venda
FROM
    vendas
group by produto, data_venda)
select produto,
       data_venda,
        ROW_NUMBER() OVER (PARTITION BY produto ORDER BY sum_vlr_venda DESC) AS ranking_vendas
from venda_por_dia
```

### Window Function: AVG()

Imagine que você é um analista de mercado em uma empresa de eletrônicos e deseja entender as tendências de vendas de produtos específicos ao longo do tempo. Usando a SQL Window Function mencionada abaixo, você pode calcular a média móvel das vendas diárias para cada produto, considerando os valores das vendas nos últimos três dias. Essa análise ajudará você a identificar padrões sazonais, picos de demanda e flutuações nas vendas, permitindo tomar decisões estratégicas sobre estoque, promoções e lançamentos de novos produtos com base em insights sólidos e em tempo real.

```sql
with venda_por_dia as (SELECT
    produto,
    data_venda,
    sum(valor_venda) as sum_vlr_venda
FROM
    vendas
group by produto, data_venda)
SELECT
    produto,
    data_venda,
    sum_vlr_venda,
    AVG(sum_vlr_venda) OVER (PARTITION BY produto ORDER BY data_venda ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS media_movel
FROM
    venda_por_dia
```

Complementando aqui, a cláusula ROWS BETWEEN 2 PRECEDING AND CURRENT ROW especifica que a janela de cálculo deve incluir as duas linhas anteriores e a linha atual, o que nos dá a média móvel das vendas para o produto em um período de três dias. Isso é útil para identificar tendências ou padrões nas vendas ao longo do tempo para cada produto.

### Window Function: DENSE_RANK()

Suponha que você seja um analista financeiro em uma rede de restaurantes e deseje identificar os produtos mais lucrativos em um período específico. Ao empregar a SQL Window Function abaixo, é possível calcular um ranking de receita total para cada produto com base nas somas das vendas diárias. Isso permitirá que você identifique de forma eficaz os produtos que mais contribuem para a receita total do restaurante, auxiliando nas decisões sobre investimentos, otimização do cardápio e estratégias de promoção para maximizar os ganhos da empresa.

```sql
with venda_por_dia as (SELECT
    produto,
    data_venda,
    sum(valor_venda) as sum_vlr_venda
FROM
    vendas
group by produto, data_venda)
SELECT
    produto,
    data_venda,
    sum_vlr_venda,
    DENSE_RANK() OVER (ORDER BY SUM(sum_vlr_venda) DESC) AS ranking_receita_total
FROM
    venda_por_dia
GROUP BY
    produto, data_venda
```

Essa consulta SQL realiza uma análise detalhada das vendas diárias por produto e, em seguida, calcula o ranking de receita total para cada produto com base na soma total das vendas

### Window Function: LAG()

Suponha que você seja um analista de marketing em uma loja online e deseje entender a variação percentual nas vendas diárias de cada produto em relação ao dia anterior. Utilizando a SQL Window Function abaixo, você pode calcular essa variação percentual para cada produto, o que permitirá avaliar o impacto das estratégias de marketing, promoções e eventos sazonais nas vendas diárias. Esses insights ajudarão você a ajustar suas campanhas de marketing de forma mais precisa e tomar medidas imediatas para otimizar as vendas, mantendo um pulso constante nas mudanças de demanda e comportamento dos clientes.

```sql
WITH venda_por_dia AS (
    SELECT
        produto,
        data_venda,
        SUM(valor_venda) AS sum_vlr_venda
    FROM
        vendas
    GROUP BY produto, data_venda
)
SELECT
    produto,
    data_venda,
    sum_vlr_venda,
    LAG(sum_vlr_venda) OVER (PARTITION BY produto ORDER BY data_venda) AS valor_venda_ultimo_dia,
    (sum_vlr_venda- LAG(sum_vlr_venda) OVER (PARTITION BY produto ORDER BY data_venda)) / sum_vlr_venda * 100 AS variacao_percentual
FROM
    venda_por_dia
```

Além da window function LAG() também temos a LEAD(), a diferença é que você via estar olhando para o registro posterior. Talvez você pode usar essa window function para criar a variável alvo para um modelo de machine learning.

# Finalização
Em resumo, as SQL Window Functions apresentam uma abordagem poderosa para análise e manipulação de dados em sistemas de gerenciamento de banco de dados relacionais. Essa funcionalidade versátil oferece aos profissionais a capacidade de realizar cálculos complexos e análises detalhadas sem a necessidade de subconsultas ou junções complicadas. Seja para identificar tendências de vendas, calcular médias móveis, determinar rankings de receita ou avaliar variações percentuais, as Window Functions proporcionam insights valiosos para a tomada de decisões estratégicas em diversos cenários de negócios. Ao explorar e dominar o uso dessas funções, os profissionais de análise de dados têm em mãos uma ferramenta valiosa para aprimorar suas habilidades e oferecer contribuições ainda mais impactantes no mundo dos dados e do desenvolvimento. Portanto, investir na compreensão e aplicação das SQL Window Functions é um passo fundamental para aprimorar suas análises e aperfeiçoar a forma como você extrai insights valiosos dos seus dados.
