# Series de Tiempo con Python
 Curso de Series en Python
Table of Contents
=================

* [Introducción](#introducción)
* [Procesos Estocásticos](#procesos-estocasticos)
    * [Enfoques](#enfoques)
* [Enfoque clásico (descomposición)](#enfoque-clásico)
* [Enfoque de los Alisados o Suavizados](#enfoque-de-los-alisados-o-suavizados)
* [ARIMA](#arima-(autoregresive-integrated-moving-average))
* [SARIMA](#sarima-(seasonal-autoregresive-integrated-moving-average))
* [Enfoque Box-Jenkins](#enfoque-box-jenkins-1)

* [Manejo de datos perdidos en series temporales](#manejo-de-datos-perdidos-en-series-temporales)
* [Series temporales con R](#series-temporales-con-r)
* [Series temporales con alisados, arima, etc. con R](#series-temporales-con-alisados-arima-etc-con-r)
* [Paquetes R para el análisis y tratamiento de Series Temporales:](#paquetes-r-para-el-análisis-y-tratamiento-de-series-temporales)
* [Análisis gráfico de series temporales](#análisis-gráfico-de-series-temporales)

* [Bibliografía](#bibliografía)

## Introducción

Una serie temporal se define como una colección de datos sucesivos que se recopilan, observan o registran cronológicamente en intervalos de tiempo regulares (diario, semanal, semestral, anual, entre otros).Una serie temporal se representa mediante un gráfico temporal, con el valor de la serie en el eje de ordenadas y los tiempos en el eje de abscisas como se muestra a continuación.

![animacion](https://user-images.githubusercontent.com/51028737/123474767-12c0e280-d5c0-11eb-83ca-fbaec64c67bb.gif)

Las series temporales son un caso particular de los procesos estocásticos, ya que un proceso estocástico es una secuencia de variables aleatorias, ordenadas y equidistantes cronológicamente referidas a una característica observable en diferentes momentos.

![Captura de pantalla 2021-06-23 15 08 02](https://user-images.githubusercontent.com/51028737/123475438-0426fb00-d5c1-11eb-95ad-60fec5c6a704.png)


Algunos ejemplos de series temporales vienen de campos como la economía (producto interior bruto anual, tasa de inflación, tasa de desempleo, ...),  la demografía (nacimientos anuales, tasa de dependencia, ...), la meteorología (temperaturas máximas, medias o mínimas, precipitaciones diarias, ...), etc.

El objetivo central de una serie temporal reside en estudiar los cambios en esa variable con respeto al tiempo. De manera que, se pueda predecir sus valores futuros (predicción o proyecciones). Por lo tanto, el análisis de series temporales presenta un conjunto de técnicas estadísticas que permiten construir el comportamiento pasado de la variable, para tratar de predecir el comportamiento futuro para la toma de decisiones.

**Componentes de una serie temporal**

Los componentes que forman una serie temporal son los siguientes:

- Tendencia: Se puede definir como un cambio a largo plazo que se produce en relación al nivel medio, o el cambio a largo plazo de la media. La tendencia se identifica con un movimiento suave de la serie a largo plazo.

![image](https://user-images.githubusercontent.com/51028737/113071715-90708000-9182-11eb-83d1-aca5b977a295.png)

- Estacionalidad: Se la  identifica como un movimiento suave de la serie a largo plazo, es decir, es el comportamiento recursivo o patrón  que responde a las mismas fechas en el tiempo, durante  algunos periodos.

![image](https://user-images.githubusercontent.com/51028737/113071742-9e260580-9182-11eb-8d18-1256b2c4610a.png)


- Ciclo: Es la fluctuación en forma de onda alrededor de la tendencia.Se caracteriza porque su duración es irregular.

![image](https://user-images.githubusercontent.com/51028737/113071770-aed67b80-9182-11eb-868c-ceff1b3ba2c0.png)


- Irregular: Esta componente no responde a ningún patrón o comportamiento sistemático sino que es el resultado de cuestiones  fortuitas implícitas de la serie.

![image](https://user-images.githubusercontent.com/51028737/113071115-55218180-9181-11eb-80b2-a56f7f33a414.png)


## Procesos Estocásticos

Un proceso estocástico \((𝒙_𝒕)\) es una sucesión de variables  aleatorias ordenadas en el tiempo (en el caso de series temporales). Por lo que, las series temporales se definen como un caso particular de los procesos estocásticos.

Lo ideal es tener una serie de tiempo con media y varianza (más o menos) constante.

**Tipos de series temporales**

Las series temporales se pueden dividir en:

- Estacionarias: es aquella en la que las propiedades estadísticas de la serie son estables, no varían con el tiempo, más en concreto su media, varianza y covarianza se mantienen constantes a lo lardo del tiempo. Si una serie temporal tiene una media constante a lo largo del tiempo, decimos que es estacionaria con respecto a la media. Si tiene varianza constante con respecto al tiempo, decimos que es estacionaria en varianza.

- No estacionarias: son aquellas en las que las propiedades estadísticas de la serie sí varían con el tiempo. Estas series pueden mostrar cambio de varianza, tendencia o efectos estacionales a lo largo del tiempo. Una serie es no estacionaria en media cuando muestra una tendencia, y una serie es no estacionaria en varianza cuando la variabilidad de los datos es diferente a lo largo de la serie.

La importancia de esta división reside en que la estacionaridad (en media y en varianza) es un requisito que debe cumplirse para poder aplicar modelos paramétricos de análisis y predicción de series de datos. Ya que con series estacionarias podemos obtener predicciones fácilmente, debido a que como la media es constante se puede estimar con todos los datos y utilizar este valor para predecir una nueva observación. Y también permite obtener intervalos de confianza para las predicciones. 

### Procesos Estocásticos Estacionarios

Un proceso estocástico \((𝒙_𝒕)\) es estacionario en sentido débil cuando su distribución de probabilidad varía de forma más o menos constante a lo largo de cierto periodo de tiempo.

Un tipo especial de serie estacionaria es la serie denominada **ruido blanco**. Un ruido blanco es una serie estacionaria tal que ninguna observación influye sobre las siguientes, es decir, donde los valores son independientes e idénticamente distribuidos a lo largo del tiempo con media y covarianza cero e igual varianza.

![image](https://user-images.githubusercontent.com/51028737/113071563-3ff92280-9182-11eb-8e04-ef9191c282df.png)

Otro tipo especial de serie temporal es la llamada **camino aleatorio**, una serie es un camino aleatorio si la primera diferenciación de la serie es un ruido blanco.

Las series temporales también se pueden dividir según cuántas variables se observan o según su variabilidad:

- Univariante: la serie temporal es un conjunto de observaciones sobre una única caracteristica o variable.
- Multivariante: (o vectorial): la serie temporal es un conjunto de observaciones de varias variables. 

Además se tiene series de tipo:

- Homocedástica: una serie es homocedástica si su variabilidad se mantiene constante a lo largo de la serie.
- Heterocedástica: una serie es heterocedástica cuando la variabilidad de la serie aumenta o disminuye a lo largo del tiempo.

Por otro lado, la variable que se observa en una serie temporal puede ser de tipo:

- Flujo: variable cuya cantidad es acumulada a lo largo del tiempo como la inversión o el ahorro.
- Stock: variable cuya cantidad se mide en un determinado momento del tiempo como la población.

## Enfoques

### Enfoque clásico

El análisis más clásico de las series temporales se basa en la idea de que los valores que toma la variable de observación son la consecuencia de las componentes anteriores (tendencia, estacionalidad, ciclo y aleatoriedad), aunque no siempre aparecen todas. Luego este enfoque descriptivo **determinista** consiste en encontrar componentes que se correspondan a una tendencia a largo plazo, un comportamiento estacional y una parte aleatoria. 

El primer paso a seguir a la hora de realizar un análisis es determinar cómo se combinan los componentes de la serie. Para ello se consideran dos modelos habituales para relacionar los valores de la serie con los componentes anteriores:

- Modelo aditivo: donde cada componente contribuye al comportamiento de la variable de interés en forma aditiva (unidades).
- Modelo multiplicativo: donde cada componente contribuye al comportamiento de la variable de interés en forma multiplicativa (porcentaje).

Si a modelo multiplicativo se le aplica un logaritmo para estabilizarlo, entonces es equivalente a un modelo aditivo. Así pues, una serie temporal se puede descomponer y denotar en su manera aditiva como:

X<sub>t</sub> = T<sub>t</sub> + E<sub>t</sub> + I<sub>t</sub>

ó en su forma multiplicativa como:

X<sub>t</sub> = T<sub>t</sub> x E<sub>t</sub> x I<sub>t</sub>

donde T<sub>t</sub> es la tendencia, E<sub>t</sub> es la componente estacional, que constituyen la señal o parte
determinística, e I<sub>t</sub> es el ruido o parte aleatoria. 

Para conocer qué tipo se adapta mejor a la serie, se pueden seguir los siguientes procedimientos:

- De manera visual:
   - La tendencia y la estacionalidad se mantienen relativamente constantes -> modelo aditivo
   - La tendencia y la estacionalidad varian creciendo o decreciento -> modelo multiplicativo
- De forma matemática:
   - Calcular las series diferencia y cociente, D y C.
   - Calcular el coeficiente de variación para cada serie, CVD y CVC.
   - Comparar sendos coeficientes.
      - Si CVC < CVD -> modelo multiplicativo
      - Si CVC > CVD -> modelo aditivo

Una vez que se conoce la forma en que se relacionan los componentes, se descompone la serie estimando los componentes de tendencia y estacionalidad:

- Componente de tendencia: la forma de la tendencia se puede modelar mediante los siguientes métodos (es importante reseñar que como la finalidad del análisis no es solo describir la serie sino predecir, hay que tener en cuenta cómo continúa la tendencia estimada para valores futuros):
   - Modelos lineales
   - Modelos polinómicos
   - Filtrado (Médias móviles)(no se recomienda ya que no predice, solo describe)
   - Diferenciación (diferencias regulares)
- Componente de estacionalidad: para estimar el efecto estacional se pueden obtener los índices o coeficientes de estacionalidad que representan el valor promedio para cada elemento de la estación (si es anual para cada mes, si es trimestral cada trimestre, esto es, el periodo de la serie)(la suma de los índices estacionales debe de ser igual al número de periodos). Además, la serie original se puede desestacionalizar también mediante una diferenciación estacional de la serie.
   - Médias móviles centradas
   - Diferenciación (diferencias estacionales)

*Se puede diferenciar la parte regular (lag=1) para la tendencia y se puede diferenciar la parte estacional para la estacionalidad (lag=periodo), o ambas. Se seleccionaría aquella diferenciación que minimice la varianza, ya que en una serie sobrediferenciada la varianza aumenta.*

Y por lo tanto, la tendencia y la estacionalidad una vez modelados se pueden eliminar para obtener la componente aleatoria:

I<sub>t</sub> = X<sub>t</sub> − T<sub>t</sub> − E<sub>t</sub>

ó

I<sub>t</sub> = X<sub>t</sub> / (T<sub>t</sub> * E<sub>t</sub>)

En este punto se tiene una descomposición de la serie en componentes que separan tendencia, estacionalidad y ruido. Estos componentes obtenidos de la serie la describen, pero no la predicen. Las predicciones de valores futuros se consiguen usando las componentes T<sub>t</sub> y E<sub>t</sub> con valores de tiempo t+1, t+2, etc. Para ello se realiza un pronóstico futuro de la tendencia, y se le añade la predicción de la estacionalidad (índice de estacionalidad) correspondiente a cada periodo (la componente irregular o aleatorio no es predecible y por lo tanto no se considera).

**Ventajas e inconvenientes**

Los métodos clásicos de análisis de series temporales tienen la ventaja de no ser excesivamente complejos, ya que explican la evolución pasada de una serie en función de pautas simples pero tienen problemas y limitaciones. Aunque son útiles para describir las pautas que sigue una serie temporal, las predicciones que proporcionan suelen ser muy malas (es decir, con un gran error asociado). La razón de esto es que en una serie temporal la observación más reciente depende, en general, de sus valores pasados, pero esta dependencia suele ser más fuerte con los datos más recientes y más débil con los más alejados. 

### Enfoque de los Alisados o Suavizados

Los métodos de suavizado o alisado se basan en modelos paramétricos **deterministas** que se ajustan a la evolución de la serie. Son técnicas de tipo predictivo más que descriptivo (resultan más adecuados para pronosticar). Estos modelos se pueden emplear en:

**Series temporales sin tendencia ni estacionalidad**

Este tipo de series tienen un comportamiento más o menos estable que sigue un patrón subyacente salvo fluctuaciones aleatorias (comportamiento estacionario), a este tipo de series se le pueden aplicar:

- Modelos "naive" o ingenuos: según la importancia que se le de a las observaciones se tiene:
	- Se otorga la misma importancia a todas las observaciones a la hora de predecir, de esta forma la previsión vendrá dada por la media de las observaciones. 
	- Se da importancia únicamente a la última de las observaciones ignorando el resto, de forma que el ajuste de la serie es su “sombra”, es la misma serie pero retardada en una unidad de periodo.
- Modelos de médias móviles: se basan en considerar únicamente las últimas k observaciones. De esta forma se da el mismo peso a los últimos k datos y nada al resto. Este procedimiento no es tan extremo como los anteriores, y al sustituir cada dato por una media de los k últimos la serie se suaviza y se elimina ruido, obteniendo el patrón subyacente de la misma. Cuantas más observaciones relevantes (k) tomemos al aplicar este tipo de ajuste más se suavizará la serie.
- Modelos de suavizado exponencial simple: consisten en dar importancia a todos los datos anteriores, pero concediéndoles diferentes pesos, ya que los datos más relevantes a la hora de efectuar una previsión son los últimos de los que se dispone, disminuyendo la importancia conforme nos alejamos de ellos. De esta manera se sustituye cada dato de la serie por una media ponderada de las observaciones anteriores, considerando que los pesos de las mismas decaen de forma exponencial conforme éstas se alejan en el tiempo (la fórmula del ajuste es recursiva). La cantidad de alisado (de nivel) depende de un parámetro, alpha, que modula la importancia que tienen las observaciones pasadas sobre el presente. Su valor oscila entre 0 y 1. Si alpha toma un valor próximo a 0 las predicciones a lo largo de la serie son muy similares entre sí, y se modifican poco con la nueva información. El caso extremo se produce cuando alpha es cero, lo que implicaría que la predicción es una constante a lo largo del tiempo. Si alpha, por el contrario, toma un valor próximo a 1 la predicción se va adaptando al último valor observado, por lo que se puede decir que los valores alejados en el tiempo no tienen mucha influencia sobre la predicción. El suavizado exponencial simple es el más similar a un modelo ARIMA con cero órdenes de autorregresión, un orden de diferenciación y un orden de media móvil.

**Series temporales no estacionales con tendencia**

En el caso de series temporales con tendencia lineal (creciente o decreciente) pero sin comportamiento estacional, el modelo clásico que más se suele aplicar es el de Holt:

- Modelos de suavizado exponencial de Holt: en estos modelos se aplican un suavizado exponencial simple de manera doble, por lo que también son conocidos como suavizado exponencial doble (en un principio se alisa directamente a la variable objeto de estudio, mientras que en la segunda operación se procede a alisar a la variable alisada previamente obtenida). Estos modelos dependen de dos parámetros, alpha y beta (suavizado de nivel y de tendencia). El parámetro beta modula la importancia que tienen las observaciones pasadas sobre la pendiente estimada en tiempo t. Al igual que para alpha, los valores de beta oscilan entre 0 y 1. Si beta toma un valor próximo a 0 entonces la pendiente es constante o casi constante, es decir, cambia poco a lo largo de la serie temporal. Si beta toma un valor próximo a 1, la predicción de la pendiente se va adaptando al último valor observado y las observaciones de las pendientes más alejadas en el tiempo no tienen apenas influencia sobre la predicción. El modelo de suavizado exponencial de Holt es muy similar a un modelo ARIMA con cero órdenes de autorregresión, dos órdenes de diferenciación y dos órdenes de media móvil.
	- Modelos de suavizado exponencial de Brown: el modelo de Brown es un caso especial del modelo de Holt, en el que sus parámetros de suavizado son el nivel y la tendencia, pero se asumen iguales. 

**Series temporales con tendencia y estacionalidad**

En el caso de series temporales con tendencia lineal (creciente o decreciente) y comportamiento estacional, el modelo clásico que se aplica es el de Holt-Winters:

- Modelo de Holt-Winters: es una extensión del modelo de Holt, solo que además considera estacionalidad, luego ahora el modelo depende de tres parámetros, alpha, beta y gamma (suavizado de nivel, de tendencia y estacional). El parámetro gamma modula la importancia que tienen las observaciones hechas en el mismo periodo de tiempos pasados sobre la predicción en tiempo t. Gamma oscila entre 0 y 1. Si gamma es 0 la predicción en tiempo t va a tomar un valor constante que va a depender de todas las observaciones pasadas dentro de ese mismo periodo. Si gamma es 1 la prediccion en tiempo t va a depender solamente de la observación hecha en tiempo t-p, siendo p la frecuencia (por ejemplo t = 12 para observaciones mensuales). La tendencia y la estacionalidad se pueden combinar de manera aditiva o multiplicativa (el modelo multiplicativo sería más adecuado cuando la amplitud del ciclo va cambiando en el tiempo). El modelo de suavizado exponencial aditivo de Winters es muy similar a un modelo ARIMA con cero órdenes de autorregresión, un orden de diferenciación, un orden de diferenciación estacional y p+1 órdenes de media móvil, donde p es el número de periodos contenidos en un intervalo estacional. Mientras que el modelo de suavizado exponencial multiplicativo de Winters no es similar a ningún modelo ARIMA.

### Enfoque Box-Jenkins

Hasta ahora se han analizado las series temporales desde un punto de vista determinista o clásico, sin tener en cuenta cuál es el mecanismo que genera la serie. Pero ahora con este nuevo enfoque se analizan desde un punto de vista **estocástico**, por lo que el punto de partida para elaborar un modelo a partir de una serie temporal consiste en considerar que dicha serie está generada y es una realización particular de un proceso estocástico.

Pero para poder efectuar inferencias sobre los parámetros de un proceso estocástico, es preciso imponer restricciones a este último. Las restricciones que se imponen habitualmente son que sea estacionario y ergódico. Ya se ha visto cuándo un proceso es estacionario, pero ¿cúando es ergódico?. Antes de explicar un proceso ergódico necesitamos definir la autocorrelación. Se denomina **autocorrelación** de orden k, p<sub>k</sub>, a la correlación (dependencia) de cualesquiera dos variables aleatorias del proceso estocástico (serie temporal), distanciadas k instantes de tiempo. Algunas de sus principales caracteristicas son:
- La autocorrelación de periodo k=0 (p<sub>0</sub>) siempre es 1 por definición.
- La autocorrelación es simétrica p<sub>i</sub>=p<sub>-i</sub>
- La autocorrelación siempre es menor que 1 y mayor que -1 (|p<sub>k</sub>| < 1)
