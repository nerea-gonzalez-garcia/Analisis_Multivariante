<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Herramientas matemáticas para el Análisis Multivariante** 

Ana Belén Nieto Librero 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

En este tema se introducirán los aspectos básicos del álgebra matricial necesarios para entender los métodos de Análisis Multivariante. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

**Vector** 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Definición** 

Un vector _x_ de dimensión _n ×_ 1 es un conjunto ordenado de _n_ números reales que se denominan escalares y que puede ser expresado como: 

**==> picture [59 x 61] intentionally omitted <==**

Este tipo de vectores se denomina vector columna. Si deseamos expresar un vector en fila sería: 

**==> picture [120 x 19] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Igualdad de vectores** 

Dos vectores _x_ e _y_ de la misma dimensión se dice que son iguales si y sólo si: 

**==> picture [89 x 12] intentionally omitted <==**

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Suma de vectores** 

Si _x_ e _y_ son dos vectores de la misma dimesión, su suma se calcula como: 

**==> picture [205 x 61] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Diferencia de vectores** 

## Análogamente, la diferencia se calcula como: 

**==> picture [205 x 61] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Multiplicación de un vector por un escalar** 

Para obtener la multiplicación de un vector por un escalar se multiplica cada elemento del vector por el escalar. 

**==> picture [129 x 61] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Combinaciones lineales de vectores** 

Si tenemos un conjunto de _p_ vectores _x_ 1 _, x_ 2 _, . . . , xp_ y un conjunto de _p_ escalares _k_ 1 _, k_ 2 _, . . . , kp_ , se denomina combinación lineal a: 

**==> picture [134 x 12] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Producto escalar de vectores** 

Si _x_ e _y_ son dos vectores de la misma dimensión, el producto escalar de ambos se calcula como: 

_n ⟨x , y ⟩_ = _x[t] y_ = _x_ 1 _y_ 1 + _x_ 2 _y_ 2 + _. . ._ + _xnyn_ = suma de _xi yi_ para _i_ = 1, ..., _n_

Si este producto es cero se dice que los vectores son ortogonales. 

## **Propiedades** 

_x[t]_ ( _y_ + _z_ ) = _x[t] y_ + _x[t] z_ ( _x_ + _y_ ) _[t] z_ = _x[t] z_ + _y[t] z x[t]_ ( _ky_ ) = ( _kx[t]_ ) _y_ = _k_ ( _x[t] y_ ) 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Producto escalar de vectores** 

## **Particularidades** 

Los productos _x[t]_ 1 y 1 _[t] x_ son la suma de los elementos del vector. 

Si _x_ representa el vector que contiene los valores de una variable y queremos calcular su media: _x_ ¯ = _n_[1][1] _[t][x]_[=] _n_[1] _[x][t]_[1] Si calculamos el producto escalar de un vector por sí mismo, obtenemos la suma de los cuadrados de los elementos del vector: _x[t] x_ = suma de _x_i_^2 para _i_ = 1, ..., _n_. A partir de esto, la varianza de _x_ se puede calcular como: 

**==> picture [102 x 23] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

**Matriz** 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Definición** 

Una matriz _X_ de dimensión _n × p_ es una tabla rectangular con _n_ filas y _p_ columnas donde se almacenan un conjunto de números reales. El término general se denota por _xij_ . 

**==> picture [179 x 61] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Tipos de matrices** 

## **Matriz rectangular y matriz cuadrada** 

Cuando _n ̸_ = _p_ se dice que la matriz es rectangular. Por el contrario, si _n_ = _p_ , la matriz se denomina cuadrada. En este caso se dice que la matriz es de orden _n_ . 

**==> picture [174 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
x 11 x 12 . . . x 1 n<br> <br>Xn = ( xij ) =  x 21 x 22 . . . x 2 n <br> ... ... ... ... <br> xn 1 xn 2 . . . xnn <br>**----- End of picture text -----**<br>


**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Tipos de matrices** 

## **Matriz diagonal** 

Si la matriz es cuadrada, los elementos _x_ 11 _, x_ 22 _, . . . , xnn_ se denominan diagonal principal. Cuando todos los elementos fuera de la diagonal son nulos, la matriz se llama matriz diagonal. 

**==> picture [141 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
x 11 0 . . . 0<br> <br> 0 x 22 . . . 0 <br>Xn =  <br> ... ... ... ... <br> 0 0 . . . xnn <br>**----- End of picture text -----**<br>


**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Tipos de matrices** 

## **Matriz identidad** 

Si además, todos los elementos de la diagonal son unos, se denomina matriz identidad. 

**==> picture [110 x 61] intentionally omitted <==**

**----- Start of picture text -----**<br>
 1 0 . . . 0 <br> 0 1 . . . 0 <br>In =  <br> ... ... ... ... <br>0 0 . . . 1<br> <br>**----- End of picture text -----**<br>


**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Igualdad de matrices** 

Dos matrices _X_ e _Y_ de la misma dimensión se dice que son iguales si y sólo si: 

_xij_ = _yij_ ( _i_ = 1 _, ..., n, j_ = 1 _, ..., p_ ) 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Suma de matrices** 

La suma de dos matrices de la misma dimensión se obtiene mediante: 

**==> picture [259 x 61] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Diferencia de matrices** 

## Del mismo modo, la diferencia de matrices se obtiene mediante: 

**==> picture [259 x 60] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Multiplicación de una matriz por un escalar** 

También es posible multiplicar una matriz por un escalar: 

**==> picture [167 x 60] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Multiplicación de matrices** 

Si _X_ es una matriz de dimensión _n × p_ e _Y_ una matriz de dimensión _p × m_ , la multiplicación _XY_ es una matriz _Z_ de dimensión _n × m_ cuyo elemento _zij_ se calcula como: 

**==> picture [67 x 31] intentionally omitted <==**

Como se puede apreciar, para que se pueda calcular la multiplicación de matrices, el número de columnas de la primera debe ser igual al número de filas de la segunda. En este caso se dice que las matrices son conformables. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Operaciones estadísticas con matrices** 

## **Ordenación de datos multivariantes** 

Las observaciones de una muestra de tamaño _n_ sobre las que se han medido un conjunto de _p_ variables se puede almacenar en una matriz _n × p_ , donde la fila _i−_ ésima de la matriz corresponde a la observación _i_ y la _j−_ ésima columna recoge los valores de la variable _p_ . 

## **Vector de medias** 

El vector de medias de un conjunto de datos de dimensión _n × p_ se puede obtener mediante: 

¯ _X_ =[1] _n[X][ t]_ **[1]** _[n]_ ¯ _X[t]_ =[1] _n[X] n_ **[1]** _[t]_ 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Operaciones estadísticas con matrices** 

## **Matriz centrada** 

La matriz de datos centrados, es decir, la que se obtiene al restar a cada columna la media de la variable correspondiente, se calcula como: 

**==> picture [130 x 23] intentionally omitted <==**

donde _J_ es una matriz de dimensión _n × n_ con todos los elementos iguales a 1. A la matriz _H_ = _I − n_[1] _[J]_[se][le][denomina][matriz][de] centrado. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Operaciones estadísticas con matrices** 

## **Matriz de dobles productos** 

La matriz de dobles productos o productos cruzados es: 

_P_ = _X[t] X_ 

Si centramos las variables: 

_C_ = _X_[˜] _[t]_[ ˜] _X_ = _X[t] X −_[1] _[−][n]_[ ¯] _[X]_[ ¯] _[X][ t] n_[(] _[X][ t]_[1)(1] _[t][X]_[) =] _[ X][ t][X]_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Operaciones estadísticas con matrices** 

## **Matriz de covarianzas** 

La matriz de covarianzas es aquella matriz cuyo elemento _ij−_ ésimo es: 

_sij_ = _cov_ ( _Xi , Xj_ ) _i_ = _j sii_ = _var_ ( _Xi_ ) _i_ = _j_ 

La matriz de covarianzas se calcula como: 

_S_ =[1] _n[C]_ 1 _S_ = _n −_ 1 _[C]_ 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Operaciones estadísticas con matrices** 

## **Matriz de correlaciones** 

La matriz de correlaciones es aquella matriz cuyo elemento _ij−_ ésimo es: _rij_ = _corr_ ( _Xi , Xj_ ) _i_ = _j rii_ = 1 _i_ = _j_ 

La matriz de correlaciones se calcula como: 

_R_ = _D[−]_[1] _[/]_[2] _SD[−]_[1] _[/]_[2] _S S_ 

donde _DS_ es la matriz diagonal que contiene las varianzas de las variables. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Matriz traspuesta** 

La traspuesta de una matriz _X[t]_ o _X[t]_ se obtiene intercambiando filas y columnas de la matriz _X_ . Es decir: 

**==> picture [35 x 15] intentionally omitted <==**

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Matriz traspuesta** 

|_Xnp_ =|<br><br><br><br><br>|_x_11<br>_x_21<br>...<br>_xn_1|_x_12<br>_x_22<br>...<br>_xn_2|_. . ._<br>_. . ._<br>...<br>_. . ._|_x_1_p_<br>_x_2_p_<br>...<br>_xnp_|<br><br><br><br><br>|
|---|---|---|---|---|---|---|
|_X t_<br>_pn_ =|<br><br><br><br><br>|_x_11<br>_x_12<br>...<br>_x_1_p_|_x_21<br>_x_22<br>...<br>_x_2_p_|_. . ._<br>_. . ._<br>...<br>_. . ._|_x_1_n_<br>_x_2_n_<br>...<br>_xnp_|<br><br><br><br><br>|



**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Matriz traspuesta** 

## **Propiedades** 

( _X[t]_ ) _[t]_ = _X_ 

( _X_ + _Y_ ) _[t]_ = _X[t]_ + _Y[t]_ 

( _XY_ ) _[t]_ = _Y[t] X[t]_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Matriz simétrica** 

Si al calcular la traspuesta de una matriz, el resultado es idéntico a la matriz de partida, se dice que la matriz es simétrica. Obviamente, la matriz debe ser cuadrada. 

_X[t]_ = _X_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Rango de una matriz** 

Para poder definir el rango de una matriz, necesitamos previamente saber el concepto de dependencia e independencia lineal. 

## **Dependencia lineal de vectores** 

Un conjunto de vectores, _x_ 1 _, x_ 2 _, . . . , xn_ se dice que es linealmente dependiente si existe un conjunto de números escalares (constantes) _k_ 1 _, k_ 2 _, . . . , kn_ distintos de cero de tal forma que: 

**==> picture [133 x 10] intentionally omitted <==**

Si no es posible encontrar un conjunto de escalares que satisfagan la ecuación anterior, se dice que los vectores son linealmente independientes. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Rango de una matriz** 

Si la ecuación se satisface, quiere decir que uno de los vectores _xi_ se puede escribir como combinación lineal de los demás. Esto implica que en el conjunto de vectores hay redundancia de información. 

El rango de una matriz se define como el número de filas linealmente independientes de _X_ , o como el número de columnas linealmente independientes de _X_ . 

Si _X_ es una matriz de dimensión _n × p_ , el rango puede ser como máximo el _min_ ( _n, p_ ). En el caso en que sea el _min_ ( _n, p_ ), se dice que la matriz tiene rango completo. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Matriz inversa** 

Si una matriz _X_ es cuadrada y de rango completo, se dice que es no singular y por tanto, tiene una única inversa que se denota por _X[−]_[1] y tiene la propiedad de: 

_XX[−]_[1] = _X[−]_[1] _X_ = _I_ 

Si la matriz no tiene rango completo se dice que es singular y por tanto no existe su inversa. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Matriz inversa** 

Si _X_ es no singular, entonces: _AX_ = _BX → A_ = _B_ . 

## **Propiedad** 

La inversa de la traspuesta de una matriz no singular es la traspuesta de la inversa de dicha matriz. 

( _X[t]_ ) _[−]_[1] = ( _X[−]_[1] ) _[t]_ 

## **Matriz ortogonal** 

Si la inversa de una matriz es igual a su traspuesta se dice que es ortogonal. ( _X_ ) _[−]_[1] = ( _X_ ) _[t]_ 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Determinante de una matriz** 

Llamamos determinante de _X_ , _|X |_ , al número obtenido al sumar todos los diferentes productos de _n_ elementos que se pueden formar con los elementos de dicha matriz, de modo que en cada producto figuren un elemento de cada distinta fila y uno de cada distinta columna, a cada producto se le asigna el signo (+) si la permutación de los subíndices de filas es del mismo orden que la permutación de los subíndices de columnas, y signo (-) si son de distinto orden. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Determinante de una matriz** 

Por ejemplo, para una matriz de orden 3, sería: 

**==> picture [307 x 140] intentionally omitted <==**

**Figure 1:** Cálculo del determinante 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Determinante de una matriz** 

## **Propiedades** 

Si la matriz es diagonal, el determinante es el producto de todos los elementos de la diagonal. _|D|_ = producto de _d_i_ para _i_ = 1, ..., _n_. Si la matriz es no singular, entonces _|X | ̸_ = 0, en caso contrario, _|X |_ = 0. Esta propiedad nos sirve para saber si las variables de nuestro conjunto de datos son linealmente dependientes o no. Si _X_ e _Y_ son dos matrices del mismo orden, entonces: _|XY |_ = _|X ||Y |_ . El determinante de una matriz y de su traspuesta es igual _|X |_ = _|X[t] |_ . 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Determinante de una matriz** 

## **Propiedades** 

El determinante de una matriz es el inverso del de su inversa _|X[−]_[1] _|_ = _|X_ 1 _|_[.] Si el rango de la matriz es completo, entonces el determinante es distinto de cero y existe su inversa. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Traza de una matriz** 

La traza de una matriz cuadrada _tr_ ( _X_ ) es la suma de los elementos de la diagonal. 

_n tr_ ( _X_ ) = suma de _x_ii para _i_ = 1, ..., _n_

## **Propiedades** 

_tr_ ( _X_ + _Y_ ) = _tr_ ( _X_ ) + _tr_ ( _Y_ ) _tr_ ( _XY_ ) = _tr_ ( _YX_ ) _tr_ ( _XX[t]_ ) = _tr_ ( _X[t] X_ ) = suma de _x_ij_^2

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector Matriz** 

**Descomposiciones matriciales** 

**Conceptos geométricos** 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Sistema de coordenadas** 

Geométricamente, un sistema de coordenadas es un sistema que utiliza números para determinar unívocamente la posición de un punto en el espacio. Para la construcción, por ejemplo, de un sistema de coordenadas en tres dimensiones, se necesita: 

El origen de coordenadas que suele ser el punto (0 _,_ 0 _,_ 0). Tres rectas, denominadas ejes coordenados, que pasan por el origen y que son perpendiculares entre sí. Un punto en cada eje distinto del origen que nos dará el sentido negativo o positivo de cada uno de ellos. 

Este concepto es importante en Análisis Multivariante ya que las _n_ observaciones que se han medido en un conjunto de _p_ variables pueden ser vistos como una nube de _n_ puntos en un espacio de dimensión _p_ en el que cada eje represente una variable. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Base canónica** 

Cada vector en el espacio puede ser expresado como combinación lineal de un conjunto de vectores que se denominan base canónica. Dicha base está formada por un conjunto de vectores linealmente independientes y cuyo número es igual a la dimensión del espacio. Por conveniencia, los vectores de la base canónica tienen longitud uno y son ortogonales. En el caso de un espacio tridimensional, la base canónica está formada por los vectores: 

_e_ 1 = (1 _,_ 0 _,_ 0) _e_ 2 = (0 _,_ 1 _,_ 0) _e_ 3 = (0 _,_ 0 _,_ 1) 

Por ejemplo, el vector (6 _,_ 5 _,_ 8) puede ser expresado como combinación lineal de la base canónica: 

(6 _,_ 5 _,_ 8) = 6 _e_ 1 + 5 _e_ 2 + 8 _e_ 3 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Espacio euclídeo** 

Un espacio euclídeo es un espacio vectorial sobre el que se ha definido un producto escalar o producto interno. 

A partir de este producto se pueden definir la norma o longitud de un vector y con él, el concepto de distancia euclídea. 

La dimensión del espacio euclídeo será el número de vectores linealmente independientes que componen la base. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos Descomposiciones matriciales** 

**Vector** 

**Matriz** 

## **Longitud de un vector** 

## La longitud o módulo de un vector se calcula como: 

_n ∥x ∥_ = raíz cuadrada de la suma de _x_i_^2 para _i_ = 1, ..., _n_

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Cosenos directores de un vector** 

Se denominan cosenos directores de un vector a los cosenos de los ángulos que forman el vector con cada eje de coordenadas. 

**==> picture [151 x 156] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticasFigurepara2:el Análisis** Cosenos **Multivariante** directores en un espacio tridimensional 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Cosenos directores de un vector** 

Su calculo sería: 

**==> picture [285 x 30] intentionally omitted <==**

**----- Start of picture text -----**<br>
a 1 a 2 a 3<br>cos α = cos β = cos γ = componentes divididas por la norma del vector.<br>**----- End of picture text -----**<br>


## **Propiedad** 

_cos_[2] _α_ + _cos_[2] _β_ + _cos_[2] _γ_ = 1 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Producto escalar en función del coseno** 

El producto escalar también se puede expresar como: 

_⟨x , y ⟩_ = _x[t] y_ = _∥x ∥∥y ∥_ cos _αxy_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Distancia entre dos vectores** 

La distancia entre dos vectores se calcula como el módulo o la longitud de la diferencia entre ellos. 

_d_ ( _x , y_ ) = _∥x − y ∥_ 

## **Propiedades** 

_d_ ( _x , y_ ) _≥_ 0 _d_ ( _x , y_ ) = 0 _, si x_ = _y d_ ( _x , y_ ) = _d_ ( _y , x_ ) _d_ ( _x , z_ ) _≤ d_ ( _x , y_ ) + _d_ ( _y , z_ ) 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Ángulo entre dos vectores** 

Para calcular el ángulo que forman dos vectores se utiliza el concepto de producto escalar explicado previamente. 

**==> picture [76 x 27] intentionally omitted <==**

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Proyección de vectores** 

En un espacio euclídeo es posible (y será de utilidad en el Análisis Multivariante), proyectar un vector sobre otro. 

Para calcular la proyección de un vector _x_ sobre otro _y_ , se traza la perpendicular a _y_ que pase por el extremo de _x_ . Analíticamente se calcula como: 

**==> picture [64 x 27] intentionally omitted <==**

El vector proyección sería: 

**==> picture [76 x 29] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Cambios de base** 

Aunque hayamos definido la base canónica como sistema de referencia de un espacio euclídeo, cabe destacar que cualquier conjunto de tamaño _n_ de vectores linealmente independientes sirve como base para el espacio, aunque no sean ortogonales y su longitud no sea la unidad. La base que cumple esas propiedades se denomina ortonormal. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Cambios de base** 

En análisis multivariante es frecuente el realizar cambios de base para extraer la máxima información de los datos. Esto se realiza mediante rotaciones de los ejes de coordenadas. 

**==> picture [151 x 141] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas Figurepara el Análisis3: Multivariante** Rotación de una base tridimensional 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposiciones matriciales** 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Definición** 

Para cada matriz cuadrada _A_ existe un escalar _λ_ y un vector no nulo _x_ tal que: 

_Ax_ = _λx_ 

_λ_ se denomina valor propio de _A_ y _x_ vector propio de _A_ correspondiente a _λ_ . 

Para encontrar estos valores se tiene que resolver la siguiente ecuación: 

( _A − λI_ ) _x_ = 0 

**Herramientas matemáticas para el Análisis Multivariante** 

**Ana Belén Nieto Librero** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Definición** 

Si _|A − λI| ̸_ = 0, entonces ( _A − λI_ ) tiene inversa y la única solución a la ecuación es _x_ = 0. Para encontrar vectores propios que no sean nulos, es necesario que _|A − λI|_ = 0. Dicha ecuación se denomina polinomio característico. Si la matriz _A_ es de orden _n_ , el polinomio característico tendrá _n_ raíces, y por lo tanto, _A_ tendrá _n_ valores propios _λ_ 1 _, λ_ 2 _, . . . , λn_ . Los valores propios no tienen porqué ser todos distintos de cero. Solo en caso de que la matriz sea no singular, serán todos no nulos. Una vez encontrados los valores propios, mediante la ecuación ( _A − λI_ ) _x_ = 0 se calculan los vectores propios. 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Propiedad** 

Si en ( _A − λI_ ) _x_ = 0 multiplicamos por un escalar _k_ , se obtiene: 

( _A − λI_ ) _kx_ = _k_ 0 = 0 

Por lo tanto, si _x_ es un vector propio de _A_ , _kx_ también lo es. Para evitar tener infinitos vectores propios se impone la restricción 

**==> picture [37 x 10] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## _− I_ + _A, I A_ 

Si _λ_ es un valor propio de _A_ y _x_ el correspondiente vector propio, se cumple que: 

1 + _λ_ es valor propio de _I_ + _A_ . 

1 _− λ_ es valor propio de _I − A_ . El vector propio _x_ se mantiene. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Traza y determinante** 

Para una matriz cuadrada _A_ con valores propios _λ_ 1 _, λ_ 2 _, . . . , λn_ , se tiene: 

**==> picture [130 x 29] intentionally omitted <==**

Hay que tener en cuenta que no necesariamente _aii_ = _λi_ . 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Matrices simétricas** 

Los vectores propios de una matriz simétrica _A_ son ortogonales entre sí. Esto implica que si normalizamos los vectores propios y los insertamos como columnas de una matriz _C_ , entonces _C_ es una matriz ortogonal. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición Espectral** 

Si _C_ es una matriz que contiene los vectores propios ortogonales de una matriz simétrica _A_ , entonces se cumple: 

_I_ = _CC[t]_ 

Si multiplicamos por _A_ : 

_A_ = _ACC[t]_ 

Si sustituimos _C_ por ( _x_ 1 _, x_ 2 _, . . . , xn_ ): 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición espectral** 

_A_ = _A_ ( _x_ 1 _, x_ 2 _, . . . , xn_ ) _C[t]_ 

= ( _Ax_ 1 _, Ax_ 2 _, . . . , Axn_ ) _C[t]_ = ( _λ_ 1 _x_ 1 _, λ_ 2 _x_ 2 _, . . . , λnxn_ ) _C[t]_ 

= _CDC[t]_ 

## donde: 

**==> picture [127 x 61] intentionally omitted <==**

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición espectral** 

La expresión _A_ = _CDC[t]_ se denomina descomposición espectral de _A_ . 

Dado que _C_ es ortogonal, se cumple _CC[t]_ = _C[t] C_ = _I_ , por lo tanto, _C[t] AC_ = _D_ . Es decir, una matriz simétrica puede ser diagonalizada por una matriz ortogonal formada por sus vectores propios, conteniendo en la diagonal los valores propios de la misma. 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición espectral** 

## **Cuadrado e inversa de matrices** 

Se cumple que si _C_ es una matriz ortogonal que contiene los vectores propios de _A_ y _D_ es una matriz diagonal que contiene los valores propios, entonces: 

_A_[2] = _CD_[2] _C[t] A[−]_[1] = _CD[−]_[1] _C[t]_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición en Valores Singulares** 

De la misma manera que se puede expresar una matriz simétrica en función de sus valores y vectores propios, también se puede expresar cualquier matriz _X_ en función de los valores y vectores propios de _XX[t]_ y _X[t] X_ . Si _X_ es una matriz de dimensión _n × p_ de rango _r_ , la descomposición en valores singulares de _X_ viene expresada como: 

_X_ = _U_ Λ _V[t]_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición en Valores Singulares** 

Donde: 

_U_ es una matriz de dimensión _n × r_ . Contiene en sus columnas los vectores propios normalizados de _XX[t]_ correspondientes a los valores propios ( _λ_ 1 _, λ_ 2 _, . . . , λr_ ). 

Λ es una matriz diagonal de dimensión _r × r_ . Contiene en su diagonal las raíces cuadradas no negativas ( _√λ_ 1 = _α_ 1 _, √λ_ 2 = _α_ 2 _, . . . , √λr_ = _αr_ ) de los valores propios de _XX[t]_ o _X[t] X_ (( _λ_ 1 _, λ_ 2 _, . . . , λr_ )). Estos valores se denominan valores singulares. 

_V_ es una matriz de dimensión _p × r_ .Contiene en sus columnas los vectores propios normalizados de _X[t] X_ correspondientes a los valores propios ( _λ_ 1 _, λ_ 2 _, . . . , λr_ ). 

**Ana Belén Nieto Librero** 

**Herramientas matemáticas para el Análisis Multivariante** 

**Conceptos geométricos** 

**Vector** 

**Matriz** 

**Descomposiciones matriciales** 

## **Descomposición en Valores Singulares** 

Dado que _U_ y _V_ son vectores propios normalizados de una matriz simétrica, se cumple: 

_U[t] U_ = _V[t] V_ = _I_ 

**Ana Belén Nieto Librero Herramientas matemáticas para el Análisis Multivariante** 

