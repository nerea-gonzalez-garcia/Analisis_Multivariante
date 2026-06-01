# Capítulo 1. Fundamentos matemáticos para el Análisis Multivariante

## 1.1 Introducción y motivación

El Análisis Multivariante constituye el núcleo analítico de la ciencia de datos moderna. Cuando observamos simultáneamente múltiples características sobre un conjunto de individuos, el análisis aislado (univariante) o por parejas (bivariante) resulta insuficiente. Las variables interactúan, se solapan y, a menudo, esconden estructuras subyacentes que solo se hacen evidentes al analizarlas conjuntamente.

Para abordar esta complejidad, el lenguaje natural es el **álgebra lineal**. La representación de los datos mediante matrices y vectores no es un mero capricho notacional; es una necesidad que nos permite aplicar potentes transformaciones geométricas a la información empírica. 

```{admonition} Comentario Docente
:class: tip
A lo largo de este capítulo, te invitamos a hacer un esfuerzo consciente por traducir cada operación algebraica (sumas, multiplicaciones por escalares, productos matriciales) a su **equivalente geométrico** (traslaciones, homotecias, rotaciones, proyecciones). Un autovector no es solo la solución a una ecuación $Sv=\lambda v$; es un eje rígido en el espacio que no cambia de dirección al transformarlo, sino que actúa como la "columna vertebral" de la nube de datos. Entender esta dualidad álgebra-geometría es el secreto para dominar el Análisis Multivariante.
```

## 1.2 Representación y centrado de los datos

### La matriz de datos

Supongamos que hemos medido $p$ variables aleatorias continuas $X_1, X_2, \dots, X_p$ sobre una muestra de $n$ individuos. Es costumbre organizar esta información en una matriz $X \in \mathcal{M}_{n \times p}(\mathbb{R})$ denominada **matriz de datos**:

$$
X = \begin{pmatrix}
x_{11} & x_{12} & \cdots & x_{1p} \\
x_{21} & x_{22} & \cdots & x_{2p} \\
\vdots & \vdots & \ddots & \vdots \\
x_{n1} & x_{n2} & \cdots & x_{np}
\end{pmatrix} = \begin{pmatrix} x_1^{(ind)} \\ x_2^{(ind)} \\ \vdots \\ x_n^{(ind)} \end{pmatrix} = \begin{pmatrix} X_1 | X_2 | \cdots | X_p \end{pmatrix}
$$

Desde una perspectiva dual, podemos ver a $X$ de dos maneras:
1. **Espacio de los individuos ($\mathbb{R}^p$):** Cada fila $x_i^{(ind)}$ es un punto en un espacio de $p$ dimensiones. El conjunto de las $n$ filas forma la **nube de puntos** de individuos. 
2. **Espacio de las variables ($\mathbb{R}^n$):** Cada columna $X_j$ es un vector en un espacio de $n$ dimensiones. Esta visión será fundamental más adelante para entender la correlación como el ángulo entre vectores.

### Vector de medias y centro de gravedad

El primer paso estadístico natural es resumir la "posición media" de estos datos. Definimos el **vector de medias** $\bar{x} \in \mathbb{R}^p$ como el vector que contiene la media aritmética de cada variable:

$$
\bar{x} = \begin{pmatrix} \bar{x}_1 \\ \bar{x}_2 \\ \vdots \\ \bar{x}_p \end{pmatrix} = \frac{1}{n} X^T \mathbf{1}_n
$$

donde $\mathbf{1}_n$ es un vector columna de $n$ unos y $\bar{x}_j = \frac{1}{n}\sum_{i=1}^n x_{ij}$.

Geométricamente, el vector $\bar{x}$ representa el **centro de gravedad** o centroide de la nube de puntos en $\mathbb{R}^p$. Es el punto de equilibrio donde la suma de los vectores de desviación se anula.

### Matriz centrada y sus propiedades

La posición del origen de coordenadas (el cero absoluto de cada variable) es habitualmente arbitraria y raramente aporta información estructural sobre cómo las variables covarían. Para eliminar este efecto de "escala absoluta", realizamos una operación de **centrado**.

Definimos la **matriz centrada** $X_c$ restando a cada elemento la media de su respectiva columna:

$$
X_c = X - \mathbf{1}_n\bar{x}^T
$$

**Interpretación geométrica:** Restar la media equivale matemáticamente a una **traslación rígida** de toda la nube de puntos. Todos los individuos se mueven exactamente en la dirección y magnitud dadas por $-\bar{x}$. Como resultado, el nuevo centro de gravedad de la nube se ubica en el origen de coordenadas $(0, \dots, 0)$. Las distancias relativas entre los puntos y la forma general de la nube permanecen inalteradas, pero ahora el estudio de la variabilidad (las dispersiones desde el centro) se simplifica algebraicamente.

## 1.3 Medidas de variabilidad e información

### Matriz de dobles productos

Una vez que la nube de puntos orbita alrededor del origen, nos interesa medir cómo se distribuye su dispersión. Introducimos la matriz de suma de cuadrados y productos cruzados (SSCP):

$$
SSCP = X_c^T X_c
$$

Si analizamos el elemento genérico de esta matriz de dimensión $p \times p$, observamos que:
* Elemento diagonal $(j, j)$: $\sum_{i=1}^n (x_{ij} - \bar{x}_j)^2$, que es la desviación cuadrática total de la variable $j$.
* Elemento fuera de la diagonal $(j, k)$: $\sum_{i=1}^n (x_{ij} - \bar{x}_j)(x_{ik} - \bar{x}_k)$, que es la suma de productos cruzados entre las variables $j$ y $k$.

### Matriz de covarianzas

Si dividimos la matriz SSCP por los grados de libertad $n-1$, obtenemos el estimador insesgado de la **matriz de covarianzas muestral** $S$:

$$
S = \frac{1}{n-1} X_c^T X_c
$$

```{admonition} Comentario Docente
:class: note
¿Por qué $n-1$ en lugar de $n$? Al estimar el centro de gravedad $\bar{x}$ a partir de la muestra, hemos "consumido" un grado de libertad. Es decir, conociendo $n-1$ residuos centrados, el último queda automáticamente fijado porque la suma de los residuos debe ser cero. Dividir por $n-1$ corrige el leve sesgo a la baja introducido al usar la media muestral en lugar de la media poblacional real.
```

**Interpretación geométrica:** La matriz $S$ es el "carnet de identidad" de la forma de la nube de puntos. 
* Los elementos de la diagonal (las varianzas $s_j^2$) indican cuánto se estira la nube a lo largo de cada uno de los ejes cartesianos originales.
* Los elementos fuera de la diagonal (covarianzas $s_{jk}$) indican el grado de *tendencia diagonal* de la nube. Si $s_{jk} > 0$, la nube se inclina hacia el primer y tercer cuadrante del plano $(X_j, X_k)$.

### Matriz de correlaciones

La magnitud de la covarianza está severamente afectada por las unidades de medida. Para estandarizar esta medida, definimos la **matriz de correlaciones** $R$:

$$
R = D^{-1/2} S D^{-1/2}
$$

donde $D = \text{diag}(s_1^2, s_2^2, \dots, s_p^2)$. El elemento genérico de $R$ es el coeficiente de correlación de Pearson $r_{jk} = \frac{s_{jk}}{s_j s_k} \in [-1, 1]$.

**Relación entre correlación y orientación:** Si la nube de puntos es esférica o circular, $R$ será aproximadamente la matriz identidad (no hay correlaciones). Si la nube tiene forma de elipsoide alargado ("balón de rugby"), $R$ contendrá valores alejados de cero. La correlación mide cómo de concentrada está la nube de puntos alrededor de una línea recta teórica.

## 1.4 Herramientas algebraicas fundamentales

Es vital observar que $S = \frac{1}{n-1} X_c^T X_c$. Por construcción, cualquier matriz de la forma $A^T A$ tiene dos propiedades estructurales profundas:
1. **Es simétrica:** $S = S^T$.
2. **Es semidefinida positiva:** Para cualquier vector $v \in \mathbb{R}^p$, la forma cuadrática $v^T S v \geq 0$. (Demostración: $v^T S v = \frac{1}{n-1} v^T X_c^T X_c v = \frac{1}{n-1} (X_c v)^T (X_c v) = \frac{1}{n-1} ||X_c v||^2 \geq 0$). 

Estas dos propiedades abren la puerta al Teorema Espectral, la piedra angular del análisis multivariante.

### Valores y vectores propios

Dada una matriz cuadrada $S$, un escalar $\lambda \in \mathbb{R}$ es un **valor propio** (autovalor) y un vector no nulo $v \in \mathbb{R}^p$ es un **vector propio** (autovector) asociado a $\lambda$ si satisfacen la ecuación fundamental:

$$
S v = \lambda v
$$

**Intuición del proceso:** Multiplicar una matriz $S$ por un vector cualquiera $x$ produce un nuevo vector $y = Sx$. En general, $y$ apuntará en una dirección distinta a $x$. Sin embargo, existen unas direcciones "mágicas" en el espacio que, al multiplicarlas por $S$, no sufren ningún cambio de dirección, tan solo un estiramiento o contracción. Estas direcciones inmutables son los vectores propios. El factor de estiramiento es el valor propio $\lambda$.

### Descomposición espectral

Por ser $S$ simétrica y semidefinida positiva, el Teorema Espectral nos garantiza que:
1. Todos sus $p$ valores propios son reales y no negativos ($\lambda_1 \geq \lambda_2 \geq \dots \geq \lambda_p \geq 0$).
2. Sus vectores propios forman una base ortogonal de $\mathbb{R}^p$.

Esto nos permite factorizar (descomponer) la matriz $S$ como:

$$
S = V \Lambda V^T
$$

Donde:
* $V$ es una matriz ortogonal ($V^T V = I$) cuyas columnas son los $p$ vectores propios ortonormales.
* $\Lambda$ es una matriz diagonal con los valores propios en orden descendente.

```{admonition} Comentario Docente
:class: important
La descomposición espectral revela la verdadera anatomía de la matriz de covarianzas. Geométricamente, $S$ describe un elipsoide de variabilidad. Los vectores propios de $V$ son los **ejes principales** de dicho elipsoide (que por definición son perpendiculares entre sí), y los valores propios de $\Lambda$ representan la varianza (el ancho) de la nube a lo largo de esos nuevos ejes. El eje asociado a $\lambda_1$ es siempre la dirección en la que la nube de datos es más alargada.
```

### Descomposición en Valores Singulares (SVD)

Mientras que la descomposición espectral se aplica a matrices cuadradas y simétricas (como $S$ o $R$), la SVD es una técnica universal que puede aplicarse a *cualquier* matriz rectangular, incluida nuestra matriz de datos centrada original $X_c$ de dimensión $n \times p$.

La SVD afirma que toda matriz $X_c$ puede factorizarse como:

$$
X_c = U D V^T
$$

Donde:
* $U$ (dimensión $n \times p$) tiene columnas ortonormales ($U^T U = I$) denominadas vectores singulares izquierdos.
* $D$ (dimensión $p \times p$) es diagonal y contiene los **valores singulares** $d_i \geq 0$.
* $V$ (dimensión $p \times p$) es ortogonal ($V^T V = I$) y contiene los vectores singulares derechos.

**Interpretación en tres actos:** La SVD nos enseña que cualquier matriz transforma el espacio en tres pasos aislados:
1. $V^T$: Rota el espacio de entrada $\mathbb{R}^p$.
2. $D$: Escala (estira o encoge) a lo largo de los ejes coordenados.
3. $U$: Mapea el resultado en el espacio de salida $\mathbb{R}^n$.

### Relación entre Descomposición Espectral y SVD

¿Por qué estudiar ambas descomposiciones? Porque representan dos caras de la misma moneda estadística. Vamos a demostrar su profunda interconexión algebraica.

Partiendo de la SVD de $X_c$, construyamos la matriz de dobles productos $X_c^T X_c$:

$$
X_c^T X_c = (U D V^T)^T (U D V^T)
$$
Recordando que $(AB)^T = B^T A^T$, obtenemos:
$$
X_c^T X_c = V D^T U^T U D V^T
$$
Como $U$ es ortonormal ($U^T U = I$) y $D$ es diagonal ($D^T = D$):
$$
X_c^T X_c = V D I D V^T = V D^2 V^T
$$

Si dividimos por $n-1$, obtenemos la matriz de covarianzas $S$:

$$
S = V \left( \frac{1}{n-1} D^2 \right) V^T
$$

Si comparamos esta expresión resultante con la descomposición espectral $S = V \Lambda V^T$, llegamos a un resultado teórico monumental:

1. **La matriz $V$ es idéntica en ambas:** Los vectores singulares derechos de la matriz de datos original son exactamente los vectores propios de la matriz de covarianzas.
2. **Relación de valores:** Los valores propios $\lambda_i$ de $S$ están ligados directamente a los valores singulares $d_i$ de $X_c$ mediante la expresión:
   $$ \lambda_i = \frac{d_i^2}{n-1} $$

## 1.5 Conexión con la reducción de la dimensión

Todo este esfuerzo teórico tiene un propósito práctico claro. Si observamos que en nuestro elipsoide de datos (descrito por $\Lambda$ o $D$) la gran mayoría de la variabilidad se concentra en unos pocos ejes principales (los primeros $\lambda_i$ son grandes), mientras que en las direcciones ortogonales restantes el elipsoide es extremadamente "plano" (los últimos $\lambda_i$ son cercanos a cero), podemos atrevernos a proyectar la nube de puntos sobre el subespacio definido únicamente por las direcciones importantes.

Esta proyección eliminará las dimensiones de varianza casi nula (posiblemente ruido o redundancias) perdiendo una cantidad estadísticamente insignificante de información, pero ganando una enorme simplicidad al reducir drásticamente el valor de $p$. Este mecanismo geométrico y algebraico es exactamente el fundamento del **Análisis de Componentes Principales (ACP)**, cuya derivación rigurosa exploraremos en el Capítulo 2.
