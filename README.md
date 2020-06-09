<div align="center">
  <h1>Introducción al Pensamiento Probabilístico</h1>
</div>

<div align="center"> 
  <img src="readme_img/logo-curso.webp" width="15%">
</div>

# Introducción al documento

El contenido de este documento esta basado en el curso del mismo nombre dictado por [David Aroesti](https://github.com/jdaroesti) en [Platzi](https://platzi.com/r/karlbehrens/).

# Tabla de contenido
- [Programación probabilística](#Programación-probabilística)
    - [Introducción a la programación probabilística](#Introducción-a-la-programación-probabilística)
    - [Probabilidad condicional](#Probabilidad-condicional)
    - [Teorema de Bayes](#Teorema-de-Bayes)

# Programación probabilística

## Introducción a la programación probabilística

La **programación probabilística** utiliza _probabilidades_ y _modelos probabilísticos_ para ejecutar cómputos. Se utiliza en una gran cantidad campos: investigación científica, inteligencia artificial, medicina, etc.

Existen lenguajes y librerías especializadas para ejecutar este tipo de cómputo, como _Pyro_ de Uber.

## Probabilidad condicional

La **probabilidad condicional** es la probabilidad de que ocurra un evento _A_, sabiendo que también sucede otro evento _B_. La probabilidad condicional se escribe _P(A|B)_, y se lee _«la probabilidad de A dado B»_.

No tiene por qué haber una relación causal o temporal entre _A_ y _B_. _A_ puede preceder en el tiempo a _B_, sucederlo o pueden ocurrir simultáneamente. _A_ puede causar _B_, viceversa o pueden no tener relación causal. Las relaciones causales o temporales son nociones que no pertenecen al ámbito de la probabilidad. Pueden desempeñar un papel o no, dependiendo de la interpretación que se le dé a los eventos.

La notación para escribir,

_«la probabilidad de A y B suceden»_: `P(A and B) = P(A)P(B|A)`

_«la probabilidad de B»_: `P(B) = P(A)P(B|A) + P(~A)P(B|~A)`

Un ejemplo de esto puede ser la probabilidad que una persona **tenga cáncer**, luego de realizar pruebas.

`P(cancer) = P(positivo)P(cancer|positivo) + P(negativo)P(cancer|negativo)`

Otro ejemplo es cual es la probabilidad de que una persona **use drogas**, pero como dato adicional esta persona es músico.

`P(drogas) = P(músico)P(drogas|músico) + P(~músico)P(drogas|~músico)`

## Teorema de Bayes

El **teorema de Bayes**, en la teoría de la probabilidad, es una proposición planteada por el matemático inglés Thomas Bayes (1702-1761)​ y publicada póstumamente en 1763,​ que expresa la probabilidad condicional de un evento aleatorio _A_ dado _B_ en términos de la distribución de probabilidad condicional del evento _B_ dado _A_ y la distribución de probabilidad marginal de solo _A_.

En términos más generales y menos matemáticos, el teorema de Bayes es de enorme relevancia puesto que vincula la probabilidad de _A_ dado _B_ con la probabilidad de _B_ dado _A_. Es decir, por ejemplo, que sabiendo la probabilidad de tener un dolor de cabeza dado que se tiene gripe, se podría saber (si se tiene algún dato más), la probabilidad de tener gripe si se tiene un dolor de cabeza. Muestra este sencillo ejemplo la alta relevancia del teorema en cuestión para la ciencia en todas sus ramas, puesto que tiene vinculación íntima con la comprensión de la probabilidad de aspectos causales dados los efectos observados.

Sea <img src="readme_img/conjunto-a1-an.svg" height="15"> un conjunto de sucesos mutuamente excluyentes y exhaustivos, y tales que la probabilidad de cada uno de ellos es distinta de cero (0). Sea B un suceso cualquiera del que se conocen las probabilidades condicionales <img src="readme_img/pba.svg" height="15">. Entonces, la probabilidad <img src="readme_img/pab.svg" height="15"> viene dada por la expresión:

<br>
<div align="center">
    <img src="readme_img/bayes.svg" height="60">
</div>
<br>

donde:

- <img src="readme_img/pai.svg" height="15"> son las probabilidades a priori,
- <img src="readme_img/pba.svg" height="15"> es la probabilidad de <img src="readme_img/B.svg" height="12"> en la hipótesis <img src="readme_img/Ai.svg" height="15">,
- <img src="readme_img/pab.svg" height="15"> son las probabilidades a posteriori.


En este [enlace](https://www.youtube.com/watch?v=HZGCoVF3YvM&t) _(en inglés)_ podras encontrar un video práctico sobre el **Teorema de Bayes.**
