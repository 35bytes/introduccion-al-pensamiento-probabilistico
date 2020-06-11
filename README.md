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
    - [Ejercicio de Bayes en código](#Ejercicio-de-Bayes-en-código)
    - [Aplicaciones del Teorema de Bayes](#Aplicaciones-del-Teorema-de-Bayes)
- [Mentiras estadísticas](#Mentiras-estadísticas)
    - [Garbage in, garbage out](#Garbage-in,-garbage-out)
    - [Imágenes engañosas](#Imágenes-engañosas)
    - [Cum Hoc Ergo Propter Hoc](#Cum-Hoc-Ergo-Propter-Hoc)
    - [Prejuicio en el muestreo](#Prejuicio-en-el-muestreo)
    - [Falacia del francotirador de Texas](#Falacia-del-francotirador-de-Texas)
    - [Porcentajes confusos](#Porcentajes-confusos)
    - [Falacia de regresión](#Falacia-de-regresión)
- [Introducción a Machine Learning](#Introducción-a-Machine-Learning)
    - [Feature vectors](#Feature-vectors)
    - [Métricas de distancia](#Métricas-de-distancia)
- [Agrupamiento](#Agrupamiento)
    - [Introducción al agrupamiento](#Introducción-al-agrupamiento)
    - [Agrupamiento jerárquico](#Agrupamiento-jerárquico)
    - [Agrupamiento K-means](#Agrupamiento-K-means)
    - [Otras técnicas de agrupamiento](#Otras-técnicas-de-agrupamiento)

# Programación probabilística

## Introducción a la programación probabilística

La **programación probabilística** utiliza _probabilidades_ y _modelos probabilísticos_ para ejecutar cómputos. Se utiliza en una gran cantidad campos: investigación científica, inteligencia artificial, medicina, etc.

Existen lenguajes y librerías especializadas para ejecutar este tipo de cómputo, como _Pyro_ de Uber.

## Probabilidad condicional

La **probabilidad condicional** es la probabilidad de que ocurra un evento _A_, sabiendo que también sucede otro evento _B_. La probabilidad condicional se escribe _P(A|B)_, y se lee _«la probabilidad de A dado B»_.

No tiene por qué haber una relación causal o temporal entre _A_ y _B_. _A_ puede preceder en el tiempo a _B_, sucederlo o pueden ocurrir simultáneamente. _A_ puede causar _B_, viceversa o pueden no tener relación causal. Las relaciones causales o temporales son nociones que no pertenecen al ámbito de la probabilidad. Pueden desempeñar un papel o no, dependiendo de la interpretación que se le dé a los eventos.

La notación para escribir,

_«la probabilidad de A y B suceden»_: <img src="readme_img/paandb.svg" height="15">

_«la probabilidad de B»_: <img src="readme_img/pb.svg" height="15">

Un ejemplo de esto puede ser la probabilidad que una persona **tenga cáncer**, luego de realizar pruebas.

<img src="readme_img/pcancer.svg" height="15">

Otro ejemplo es cual es la probabilidad de que una persona **use drogas**, pero como dato adicional esta persona es músico.

<img src="readme_img/pdrogas.svg" height="15">

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

Como sabemos que <img src="readme_img/pb.svg" height="15"> podemos reemplazarlo en la ecuación y nos quedaría:

<br>
<div align="center">
    <img src="readme_img/bayes-expandido.svg" height="60">
</div>
<br>

En este [enlace](https://www.youtube.com/watch?v=HZGCoVF3YvM&t) _(en inglés)_ podras encontrar un video práctico sobre el **Teorema de Bayes.**


## Ejercicio de Bayes en código

En el siguiente ejercicio implementaremos la posibilidad de tener **síntomas** dado a que una persona tenga **cáncer.**

<div align="center"> 
  <img src="readme_img/cuadro-cancer.png" width="50%">
</div>

```py

# Implementamos la P(B) = P(A)P(B|A) + P(¬A)P(B|¬A)
def prob_b(prob_a, prob_b_dado_a, prob_b_complemento_a):
    calculo = prob_a * prob_b_dado_a + (1-prob_a) * prob_b_complemento_a
    return calculo

# Implementamos la P(A|B) = P(B|A)P(A) / P(B)
def cal_bayes(prob_a, prob_b_dado_a, prob_b_complemento_a):
    prob_evento = prob_b(prob_a, prob_b_dado_a, prob_b_complemento_a)
    calculo = (prob_b_dado_a * prob_a)/prob_evento

    return calculo

if __name__ == "__main__":
    prob_cancer = 1 / 100000
    prob_sintoma_dado_cancer = 1
    prob_sintoma_dado_no_cancer = 10 / 99999
    
    resultado = cal_bayes(prob_cancer, prob_sintoma_dado_cancer, prob_sintoma_dado_no_cancer)

    print(resultado)
```

Vamos a la consola y ejecutamos nuestro programa.

```bash
python3 sintomas.py # Ejecutamos nuestro programa

# Y este sera nuestro resultado.
0.09090909090909091
```

## Aplicaciones del Teorema de Bayes

El Teorema de Bayes es uno de los mecanismos matemáticos más importantes en la actualidad. A grandes rasgos, nos permite medir nuestra certidumbre con respecto a un suceso tomando en cuenta nuestro conocimiento previo y la evidencia que tenemos a nuestra disposición. El Teorema de Bayes permea en tu vida diaria, desde descubrimientos científicos hasta coches autónomos, el Teorema de Bayes es el motor conceptual que alimenta mucho de nuestro mundo moderno.
​
En esta lectura me gustaría darte ejemplos de cómo se utiliza en la vida moderna para que puedas comenzar a implementarlo en tus proyectos, análisis y hasta en tu vida personal.

### **Turing y el código enigma de los Nazis**

Casi todos sabemos que Alan Turing es uno de los padres del cómputo moderno; pocos saben que fue gracias a él que los aliados pudieron tener una ventaja decisiva cuando Turing logró descifrar el código enigma que encriptaba todas las comunicaciones nazis; pero aún menos saben que para romper este código utilizó el Teorema de Bayes.
​
Lo que hizo Turing fue aplicar el Teorema para descifrar un segmento de un mensaje, calcular las probabilidades iniciales y actualizar las probabilidades de que el mensaje era correcto cuando nueva evidencia (pistas) era presentada.

### **Finanzas**

Una de las decisiones más difíciles cuando estás manejando un portafolio de inversión es determinar si un instrumento financiero (acciones, valores, bonos, etc.) se va a apreciar en el futuro y por cuánto, o si, por el contrario se debe vender el instrumento. Los _portafolios managers_ más exitosos utilizan el Teorema de Bayes para analizar sus portafolios.

En pocas palabras, puedes determinar las probabilidades iniciales basándote en el rendimiento previo de tu portafolio o en el rendimiento de toda la bolsa y luego añadir evidencia (estados financieros, proyecciones del mercado, etc.) para tener una mayor confianza en las decisiones de venta o compra.

### **Derecho**

El Derecho es uno de los campos más fértiles para aplicar pensamiento bayesiano. Cuando un abogado quiere defender a su cliente, puede comenzar a evaluar una probabilidad de ganar (basada en su experiencia previa, o en estadísticas sobre el número de juicios y condenados con respecto del tema legal que competa) y actualiza su probabilidad conforme vayan sucediendo los eventos del proceso jurisdiccional.
​
Cada nueva notificación, cada prueba y evidencia que encuentre, etc. sirve para actualizar la confianza del abogado.

### **Inteligencia artificial**

El Teorema de Bayes es central en el desarrollo de sistemas modernos de inteligencia artificial. Cuando un coche autónomo se encuentra navegando en las calles, tiene que identificar todos los objetos que se encuentran en su “campo de visión” y determinar cuál es la probabilidad de tener una colisión. Esta probabilidad se actualiza con cada movimiento de cada objeto y con el propio movimiento del vehículo autónomo. Esta constante actualización de probabilidades es lo que permite que los vehículos autónomos tomen decisiones acertadas que eviten accidentes.

En esta rama existen muchos ejemplos como para cubrirlos todos, pero quiero por lo menos mencionar algunos casos de uso: filtros de spam, reconocimiento de voz, motores de búsqueda, análisis de riesgo crediticio, ofertas automáticas, y un largo etcétera.

Para terminar, me gustaría compartir una cita del famoso economista John Maynard Keynes que resume perfectamente el tipo de pensamiento que quiero que desarrolles: “Cuando los hechos cambian, yo cambio mi opinión. ¿Qué hace usted, señor?”

# Mentiras estadísticas

## Garbage in, garbage out

La calidad de nuestros datos es igual de fundamental que la precisión de nuestros cómputos. Cuando los datos son errados, aunque tengamos un cómputo prístino nuestro resultado serán erróneos.

En pocas palabras: con datos errados las conclusiones serán erradas.

## Imágenes engañosas

Las visualizaciones son muy importantes para entender un conjunto de datos. Sin embargo, cuando se juega con la escala se puede llegar a conclusiones incorrectas.

Nunca se debe confiar en una gráfica sin escalas o etiquetas.

## Cum Hoc Ergo Propter Hoc

Dos variables están positivamente correlacionadas cuando se mueven en la misma dirección y negativamente correlacionadas cuando se mueven en direcciones opuestas. Esta correlación no implica causalidad.

Puede existir variables escondidas que generen la correlación. _Después de esto, eso; entonces a consecuencia de esto, eso._

## Prejuicio en el muestreo

Para que un muestreo pueda servir como base para la inferencia estadística tiene que ser aleatorio y representativo.

El prejuicio en el muestreo elimina la representatividad de las muestras.

A veces conseguir muestras es difícil, por lo que se utiliza a la población de más fácil acceso (caso estudios universitarios).

## Falacia del francotirador de Texas

Esta falacia se da cuando no se toma la aleatoriedad en consideración. También sucede cuando uno se enfoca en las similitudes e ignora las diferencias.

Cuando fallamos al tener una hipótesis antes de recolectar datos estamos en alto riesgo de car en esta falacia (muy común en Data Science).

## Porcentajes confusos

Cuando no sabemos la cuenta total del cual se obtiene un porcentaje tenemos el riesgo de concluir falsos resultados, siempre es importante ver el contexto, y los porcentajes, en vacio, no significan mucho.

## Falacia de regresión

Muchos eventos fluctúan naturalmente, por ejemplo, la temperatura promedio de una ciudad, el rendimiento de un atleta, los rendimientos de un portafolio de inversión, etc.

Cuando algo fluctúa y se aplican medidas correctivas se puede creer que existe un vínculo de causalidad en lugar de una regresión a la media.

# Introducción a Machine Learning

_"Es el campo de estudio que le da a las computadoras la habilidad de aprender sin ser explícitamente programadas."_ - Arthur Samuel, 1959.

- Machine learning se utiliza cuando:
    - Programar un algoritmo es imposible.
    - El problema es muy complejo o no se conocen altoritmos para resolverlo.
    - Ayuda a los humanos a entender patrones (data mining).

- Aprendizaje supervisado vs no supervisado vs semisupervisado.

- Batch vs online learning.

## Feature vectors

Se utilizan para representar características simbólicas o numéricas llamadas _features._ Permiten analizar un objeto desde una perspectiva matemática.

Los algoritmos de machine learning típicamente requieren representaciones numéricas para poder ejecutar el cómputo.

Uno de los _feature vectors_ más conocidos es la representación del color a través de RGB
- color = [R, G, B]
- Procesamiento de imágenes: Gradientes, bordes, áreas, colores, etc.
- Reconocimiento de voz: Distancia de sonidos, nivel de ruido, razón ruido / señal, etc.
- Spam: Dirección IP, estructura del texto, frecuencia de palabras, encabezados, etc.

## Métricas de distancia

Muchos de los algoritmos de machine learning pueden clasificarse como algoritmos de optimización. Lo que desean optimizar es una función que en muchas ocasiones se refiere a la distancia entre features.

Features:

- <img src="readme_img/xab.svg" height="17"> 
- <img src="readme_img/ycd.svg" height="17">

Distancia euclidiana:

<img src="readme_img/euclidiana.svg" height="25">

Distancia de Manhattan:

<img src="readme_img/manhattan.svg" height="25">

# Agrupamiento

## Introducción al agrupamiento

Es un proceso mediante el cual se agrupan objetos similares en clusters que los identifican. Se clasifican como aprendizaje no supervisado, ya que no requiere la utilización de etiquetas.

Permite entender la estructura de los datos y la similitud entre los mismos.

Es utilizado en motores de recomendación, análisis de redes sociales, análisis de riesgo crediticio, clasificación de genes, riesgos médicos, etc.

## Agrupamiento jerárquico

Es un algoritmo que agrupa objetos similares en grupos llamados _clustes_. El algoritmo comienza tratando a cada objeto como un cluster individual y luego realiza los siguientes pasos de manera recursiva:
- Identifica los 2 clusters con menor distancia (lo más similares).
- Agrupa los 2 clusters en 1 nuevo.

El _output_ final es un dendrograma que muestra la relación entre objetos y grupos.

Es importante determinar qué medida de distancia vamos a utilizar y los puntos a utilizar en cada cluster (linkage criteria).

## Agrupamiento K means

Es un algoritmo que agrupa utilizando centroides. El algoritmo funciona asignando puntos al azar (K define el número inicial de clusters) y después:
- En cada iteración el punto se ajusta a su nuevo centroide y cada punto se recalcula con la distancia con respecto de los centroides.
- Los puntos se reasignan al nuevo centro.
- El algoritmo se repite de manera iterativa hasta que ya no existen mejoras.

## Otras técnicas de agrupamiento

El agrupamiento es una técnica de Machine Learning que consiste, en pocas palabras, en dividir una población en grupos con la consecuencia de que los datos en un grupo son más similares entre ellos que entre los otros grupos.

Imagina que eres el dueño de una startup que hace ecommerce y quieres tener estrategias de venta para tus clientes. Es casi imposible diseñar una estrategia por cada individuo, pero se puede utilizar el agrupamiento para dividir a los clientes en grupos que tengan similitudes relevantes y así reducir el problema a unas cuantas estrategias.

Existen dos tipos de agrupamiento:
- **Agrupamiento estricto (hard clustering):** en el cual cada dato pertenece a un grupo u otro. No hay puntos medios.

- **Agrupamiento laxo (soft clustering):** en el cual en lugar de asignar un dato a un grupo, se asigna probabilidades a cada dato de pertenecer o no a un grupo.

Un punto muy importante que debes considerar cuando ejecutas técnicas de agrupamiento es que debes definir muy claro a qué te refieres cuando hablas de similitud entre puntos, porque esto puede ayudarte a definir el algoritmo correcto para tus necesidades particulares.

A grandes rasgos existen cuatro aproximaciones para definir similitud:

- **Modelos conectivos:** Estos modelos asumen que los puntos más similares son los que se encuentran más cercanos en el espacio de búsqueda. Recuerda que este espacio puede ser altamente dimensional cuando tus _feature vectors_ definen muchas características a analizar. Una desventaja de este tipo de modelos es que no escalan para conjuntos de datos grandes (aunque es posible utilizar una muestra y aplicar técnicas de estadística inferencial para obtener resultados).

- **Modelos de centroide:** Este tipo de modelos definen similitud en términos de cercanía con el centroide del grupo. Los datos se agrupan al determinar cuál es el centroide más cercano.

- **Modelos de distribución:** Este tipo de modelos trata de asignar probabilidades a cada dato para determinar si pertenecen a una distribución específica o no (por ejemplo, normal, binomial, Poisson, etc.).

- **Modelos de densidad:** Estos modelos analizan la densidad de los datos en diferentes regiones y dividen el conjunto en grupos. Luego asignan los puntos de acuerdo a las áreas de densidad en las que se haya dividido el dataset.

Acuérdate que no tienes que casarte con un modelo específico. Muchos de los mejores Ingenieros de Machine Learning y Científicos de Datos utilizan varios modelos con el mismo conjunto de datos para analizar el rendimiento de los diversos algoritmos que tienen a su disposición. Así que experimenta y siempre compara tus resultados antes de tomar una decisión.