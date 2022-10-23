---
title: Aplicação da álgebra linear em data science - Parte 1 Vetores
layout: post
date: 2022-10-23
image: https://i.imgur.com/4sIezyt.jpg
tags: [data-science, machine-learning]
comments: true
description: Vetores fornecem as bases sobre toda a álgebra linear e suas aplicações em um projeto de data science.
---

# Aplicação de vetores

Vetores fornecem as bases sobre toda a álgebra linear e existem processos onde eles são usados em um projeto de data science e entendê-los onde ele é aplicado é uma boa forma de identificar os motivos para estudar mais sobre.

Na álgebra linear o vetor é uma lista ordenada de números, mas também existem uma álgebra linear abstrata onde o vetor pode incluir outros objetos matemáticos, quando é falado assim pode parecer um pouco abstrato e esotérico e pode até parecer não precisarmos de estudar vetores, porém vamos olhar mais de perto algumas aplicações em data science & machine learning.

## Correlação
Ao decorrer de um projeto de data science chega em um momento onde devemos realizar algumas explorações e a correlação é um método que auxilia nesse processo e é de muita importância essa análise estatística e posteriormente para a aplicação de machine learning. 

O coeficiente de correlação é um número que quantifica o relacionamento linear entre duas variáveis, podendo ter valores entre -1 e +1, onde o valor -1 indica um relacionamento negativo e o +1 um relacionamento positivo e 0 não há relacionamento linear.

<p align="center">
  <img src="https://i.imgur.com/AJJuqN1.png" />
</p>
<p align = "center">
Imagem 1: exemplos de correlações e seus resultados
</p>

Para realizar o cálculo da correlação entre duas variáveis nós utilizamos o produto escalar, ele é uma maneira fundamental de combinar dois vetores. Intuitivamente, o produto escalar é um número que fornece a informação sobre o relacionamento entre dois vetores.

Após o cálculo do coeficiente de correlação é preciso realizar algumas normalizações para que o resultado fique entre o intervalo -1 e +1, sendo elas: (1) Centro médio de cada variável e (2) Divida o produto escalar pelo produto das normas vetoriais.

- 1: O centro médio de cada variável significa subtrair o valor médio de cada valor de dados
- 2: Essa normalização divisiva cancela as unidades de medida e dimensiona a magnitude de correlação máxima possível para |1|.

Sigamos para o cálculo em si da correlação, uma das mais utilizadas é a de Pearson e podemos ver a sua fórmula abaixo:

<p align="center">
  <img src="https://i.imgur.com/X3gmOmZ.png" />
</p>
<p align = "center">
Fórmula 1: coeficiente de correlação de Pearson
</p>

Quando analisamos essa fórmula podemos identificar alguns pontos onde a álgebra linear se faz presente com o produto escalar, que no caso são três, um produto escalar na literatura pode ser indicado por algumas notações, a mais comum se faz da seguinte maneira: $a^T b$, com isso podemos reescrever a fórmula:

<p align="center">
  <img src="https://i.imgur.com/iYniTLT.png" />
</p>
<p align = "center">
Fórmula 2: Correlação de Pearson expressada em álgebra linear, onde x̃ é centro médio(1) de x
</p>

Portanto, a correlação de Pearson é um simples produto escalar entre duas variáveis normalizadas pela magnitude dessas variáveis. Mas vamos realizar uma demonstração passo a passo para exemplificar e facilitar o entendimento.

1. Quando falamos de vetor estamos lidando com uma notação igual a $\vec{v}$, definimos então dois vetores com n valores:

<p align="center">
  <img src="https://i.imgur.com/U76vWO6.png" />
</p>
<p align = "center">
Imagem 2: Vetores x e y definidos 
</p>

2. Defina as médias dos valores de $\vec{x}$ como $\bar x$ e o mesmo para o $\vec{y}$:

<p align="center">
  <img src="https://i.imgur.com/jUIU0r8.png" />
</p>
<p align = "center">
Imagem 3: Exemplo para x para calcular as médias dos valores
</p>

3. Definir então dois novos vetores, $\vec{x^ c}$ e $\vec{y^ c}$, que contém os valores dos vetores com suas respectivas médias subtraídas:

<p align="center">
  <img src="https://i.imgur.com/jO7PBa0.png" />
</p>
<p align = "center">
Imagem 4: Vetores x e y para calcular suas médias subtraídas
</p>

4. Dado isso, precisamos então definir a variância amostral de $\vec{x}$ e $\vec{y}$ como a média dos desvios quadrados da média:

<p align="center">
  <img src="https://i.imgur.com/MuOKVZg.png" />
</p>
<p align = "center">
Imagem 5: Exemplo de definição da variância amostral para x
</p>

5. E com isso podemos calcular o desvio padrão da amostra de $\vec{x}$ e $\vec{y}$:

<p align="center">
  <img src="https://i.imgur.com/aZJ25we.png" />
</p>
<p align = "center">
Imagem 6: Exemplo de definição do desvio padrão da amostra para x
</p>

6. Como dito anteriormente, precisamos realizar a normalização das versões de $\vec{x}$ e $\vec{y}$:

<p align="center">
  <img src="https://i.imgur.com/jJaTYGf.png" />
</p>
<p align = "center">
Imagem 7: Normalização dos vetores x e y
</p>

7. Com isso podemos realizar o cálculo da coeficiente de correlação de Pearson de $\vec{x}$ e $\vec{y}$ que é dado por $\dfrac{1}{n}$ vezes o produto escalar de $\vec{x^ z}$ e $\vec{y^ z}$:

<p align="center">
  <img src="https://i.imgur.com/lkzDXiN.png" />
</p>
<p align = "center">
Imagem 8: Coeficiente de correção de Pearson em forma de produto escalar
</p>

A imagem 8 equivalente em termos de somas em vez de vetores é a mesma mostrada anteriormente na Fórmula 1. E quando nos termos de $\vec{x^ c}$ e $\vec{y^ c}$ temos que:

<p align="center">
  <img src="https://i.imgur.com/jxq8fkY.png" />
</p>
<p align = "center">
Imagem 9: Fórmula reescrita em termos de vetores
</p>

O resultado da fórmula acima rxy é o mesmo mostrado na Fórmula 2. O resultado, como dito anteriormente, é que a correlação de Pearson é um produto escalar entre duas variáveis após a sua normalização para os valores ficam entre -1 e +1.

A correlação não é a única forma de se encontrar similaridade entre duas variáveis, também temos o método de similaridades de cossenos que será assunto para o próximo post aqui do blog fique ligado.

# Bibliografia:

Cohen, M.X. (2022) Practical linear algebra for data science: From core concepts to applications using Python. Beijing: O'Reilly. 

Brett, Matthew. (2022, October). Correlation and projection. [Web log post]. https://matthew-brett.github.io/teaching/correlation_projection.html

Brett, Matthew. (2022, October). Vectors and dot products. [Web log post]. https://matthew-brett.github.io/teaching/on_vectors.html

Lang, S. (2003) Algebra Linear. Rio de Janeiro (RJ): Ciência Moderna.