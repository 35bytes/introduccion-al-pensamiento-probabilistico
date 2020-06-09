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