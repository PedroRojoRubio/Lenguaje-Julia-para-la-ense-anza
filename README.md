# Lenguaje-Julia-para-la-ense-anza
Ejemplos de uso de Julia como material de apoyo para impartir clases de matemáticas
Vamos a usar un nuevo lenguaje de programación Julia, como herramienta que nos facilite el estudio de la estadística y probabilidad en distintos cursos de la ESO, para ello utilizaremos las facilidades innatas que este nuevo lenguaje proporciona para el uso de procesos y cálculos matemáticos, que incorpora de forma nativa a través de diferentes paquetes.
Asumimos que ya tenemos el entorno apropiado para el uso de Julia, tenemos los siguientes paquetes en nuestro entorno:
-	StatsBase
-	StatsPlots
-	Plots
-	Random
-	DataFrames
-	Distributions
 Lo haremos desde dos enfoques distintos, uso de un entorno de programación tipo “Atom” que nos permite crear programas en Julia y el que usaremos preferentemente “NoteBook” con Jupyter o Pluto,jl.
En este primer contacto introduciremos las nociones básicas de la estadística descriptiva como la media μ, la desviación típica σ, la varianza σ², así como los gráficos básicos como diagramas de barras y de tarta. Veremos cómo podemos usar la potencia de Julia para realizar los distintos cálculos de forma automática, además de su representación gráfica.
Uno de los inconvenientes que se presentan al empezar a trabajar con los temas de estadística es lo aburrido de tener que preparar las tablas de datos a usar como ejemplo en clase, por varios motivos, primero, si se intenta usar muchos datos para que se aproxime más a ejemplos reales se pierde mucho tiempo copiando o recogiendo los posibles datos y entonces los cálculos son muy tediosos, por otro lado,  si se utilizan ejemplos sencillos para poder realizar los cálculos y representarlos, está el inconveniente de que quedan un ejemplos demasiado alejados de la realidad y de poder entender claramente que significa el resumen estadístico. 
Este primer obstáculo es fácil de superar con las facilidades que aportan los lenguajes de programación y en particular Julia, para ello vamos a crear todos los datos simulados que vayamos a necesitar.
Para ello, siendo n = número de datos a generar, usaremos la función “rand” que nos genera números aleatorios, y en este caso nos permite elegir de forma aleatoria entre el siguiente conjunto de datos (0,1,2,3,4) que representan el número de hermanos que tienen los alumnos de nuestro centro. En este caso n=1000 alumnos.
Las siguientes líneas de código nos genera un conjunto de 1000 datos que representan la información recogida en nuestro centro, y que nos permitirá hacer nuestro estudio estadístico. 
n= 1000 
datos = [rand((0,1,2,3,4)) for i in 1:n]
La siguiente línea de código nos proporciona un primer resumen estadístico de los datos generados:
	summarystats(datos)


con la siguiente información:
	Summary Stats:
Length:         1000
Missing Count:  0
Mean:           2.003000
Minimum:        0.000000
1st Quartile:   1.000000
Median:         2.000000
3rd Quartile:   3.000000
Maximum:        4.000000

Para la media μ, la función que nos la da por separado es: mean(datos)
 la desviación típica σ, su función es: std(datos)
 la varianza σ², su función es: var(datos)
la moda, su función es: mode(datos)

Veamos ahora como podemos visualizar esta información, primero vamos ha obtener la frecuencia de cada dato, para ello ejecutamos el siguiente código. 
	datosf=sort(countmap(datos))
que nos devuelve la siguiente estructura en Julia:
OrderedCollections.OrderedDict{Int64,Int64} with 5 entries:
  0 => 195
  1 => 194
  2 => 216
  3 => 203
  4 => 192

Esta orden básicamente lo que hace es contar cuantas ocurrencias hay de cada dato distinto en nuestro conjunto de datos, eso lo hace la función “countmap()”, la función “sort()”, nos lo devuelve en orden. Lo que obtenemos es un diccionario en Julia, que no es más que pares de valores, clave y valor, como en un diccionario, en nuestro caso la clave son los distintos valores que tenemos en nuestra tabla de datos y el valor la frecuencia con que aparece cada dato.
Podemos visualizarlo en forma de tabla creando un “DataFrame” en Julia, que básicamente no es más que una tabla de datos:
dfdatos=DataFrame(nhermanos=collect(keys(datosf)),frecuencia=collect(values(datosf)))

donde la función “keys()” nos devuelve las claves de diccionario, en nuestro caso el número de hermanos, y la función “values()” la frecuencia de cada dato, hay que utilizar la función “collect()” para que esos valores puedan ser usados para crear el DataFarme. 



obtenemos:
5 rows × 2 columns
	nhermanos	frecuencia
	Int64	Int64
1	0	195
2	1	194
3	2	216
4	3	203
5	4	192

Ahora ya podemos generar el gráfico de barras de frecuencias 
@df dfdatos bar(:nhermanos,:frecuencia) 
 

O el gráfico de tarta 
@df dfdatos pie(:nhermanos,:frecuencia)
 

