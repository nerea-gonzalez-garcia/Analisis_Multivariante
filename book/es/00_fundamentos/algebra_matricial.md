# Herramientas de Álgebra Matricial

El Análisis Multivariante trabaja simultáneamente con muchas variables. Para manejar toda esa información de manera compacta y eficiente se usa el **álgebra matricial**, que es el lenguaje matemático común de todas las técnicas que estudiaremos.

En esta sección repasamos los conceptos esenciales que necesitarás a lo largo del curso.

---

## La Matriz de Datos Multivariante

Cuando recogemos datos de $n$ individuos sobre $p$ variables, toda la información se organiza en una **matriz de datos** $\mathbf{X}$ de dimensión $n \times p$:

$$
\mathbf{X} = \begin{pmatrix}
x_{11} & x_{12} & \cdots & x_{1p} \\
x_{21} & x_{22} & \cdots & x_{2p} \\
\vdots  & \vdots  & \ddots & \vdots  \\
x_{n1} & x_{n2} & \cdots & x_{np}
\end{pmatrix}
$$

donde:
- Cada **fila** $i$ representa un individuo u observación.
- Cada **columna** $j$ representa una variable.
- El elemento $x_{ij}$ es el valor de la variable $j$ para el individuo $i$.

**Ejemplo:** Si medimos la estatura, el peso y la edad de 5 estudiantes, tenemos una matriz $\mathbf{X}$ de dimensión $5 \times 3$.

En R, una matriz de datos se representa habitualmente como un `data.frame` o una `matrix`:

```r
# Crear una matriz de datos en R
X <- matrix(c(170, 65, 21,
              165, 58, 22,
              180, 75, 23,
              155, 52, 20,
              175, 70, 24),
            nrow = 5, ncol = 3, byrow = TRUE)
colnames(X) <- c("Estatura", "Peso", "Edad")
rownames(X) <- paste0("Est", 1:5)
print(X)
```

---

## Operaciones Matriciales Fundamentales

### Traspuesta

La **traspuesta** de una matriz $\mathbf{X}$ (notación: $\mathbf{X}^\top$) intercambia filas por columnas. Si $\mathbf{X}$ es $n \times p$, entonces $\mathbf{X}^\top$ es $p \times n$.

```r
t(X)   # traspuesta en R
```

### Producto de matrices

El **producto** $\mathbf{A} \cdot \mathbf{B}$ requiere que el número de columnas de $\mathbf{A}$ coincida con el número de filas de $\mathbf{B}$.

```r
A %*% B   # producto matricial en R
```

### Matriz inversa

La **inversa** $\mathbf{A}^{-1}$ cumple que $\mathbf{A} \cdot \mathbf{A}^{-1} = \mathbf{I}$ (matriz identidad). Solo existe si $\mathbf{A}$ es cuadrada y no singular.

```r
solve(A)   # inversa en R
```

### Determinante y traza

```r
det(A)    # determinante
sum(diag(A))   # traza (suma de elementos de la diagonal)
```

---

## El Vector de Medias

Para cada variable $j$, calculamos su media aritmética sobre los $n$ individuos:

$$
\bar{x}_j = \frac{1}{n} \sum_{i=1}^{n} x_{ij}
$$

Todos los promedios juntos forman el **vector de medias** $\bar{\mathbf{x}}$ de dimensión $p \times 1$:

$$
\bar{\mathbf{x}} = \begin{pmatrix} \bar{x}_1 \\ \bar{x}_2 \\ \vdots \\ \bar{x}_p \end{pmatrix}
$$

En R:

```r
# Vector de medias
x_bar <- colMeans(X)
print(x_bar)
```

---

## Centrado de los Datos

**Centrar** los datos consiste en restar a cada observación la media de su variable. La **matriz de datos centrada** $\tilde{\mathbf{X}}$ se obtiene como:

$$
\tilde{\mathbf{X}} = \mathbf{X} - \mathbf{1}_n \bar{\mathbf{x}}^\top
$$

donde $\mathbf{1}_n$ es un vector columna de unos de longitud $n$.

Centrar es fundamental porque elimina el efecto de la escala de cada variable y coloca el origen de coordenadas en el centroide de la nube de puntos.

```r
# Centrar los datos en R
X_centrada <- scale(X, center = TRUE, scale = FALSE)
print(X_centrada)
```

---

## Estandarización

La **estandarización** (o tipificación) va un paso más allá del centrado: también divide por la desviación típica de cada variable. Así cada variable tiene media 0 y desviación típica 1, y podemos comparar variables con unidades diferentes.

$$
z_{ij} = \frac{x_{ij} - \bar{x}_j}{s_j}
$$

donde $s_j$ es la desviación típica de la variable $j$.

```r
# Estandarizar los datos en R
X_std <- scale(X, center = TRUE, scale = TRUE)
print(X_std)
```

```{admonition} ¿Cuándo centrar y cuándo estandarizar?
:class: tip

- **Solo centrar**: cuando todas las variables están en la misma escala y unidades (por ejemplo, todas en centímetros).
- **Estandarizar**: cuando las variables tienen escalas o unidades muy distintas (por ejemplo, peso en kg, salario en euros, temperatura en °C). Es la opción más habitual en la práctica.
```

---

## La Matriz de Covarianzas

La **matriz de covarianzas** $\mathbf{S}$ (dimensión $p \times p$) resume la variabilidad y las relaciones lineales entre todas las variables:

$$
\mathbf{S} = \frac{1}{n-1} \tilde{\mathbf{X}}^\top \tilde{\mathbf{X}}
$$

Su elemento $(j, k)$ es:

$$
s_{jk} = \frac{1}{n-1} \sum_{i=1}^{n} (x_{ij} - \bar{x}_j)(x_{ik} - \bar{x}_k)
$$

- Los elementos de la **diagonal** ($s_{jj}$) son las **varianzas** de cada variable.
- Los elementos **fuera de la diagonal** ($s_{jk}$, $j \neq k$) son las **covarianzas** entre pares de variables.

```r
# Matriz de covarianzas en R
S <- cov(X)
print(S)

# Visualizar con corrplot
library(corrplot)
corrplot(cov2cor(S), method = "color", type = "upper",
         addCoef.col = "black", tl.col = "black")
```

```{admonition} Propiedades de la matriz de covarianzas
:class: note

- Es **simétrica**: $\mathbf{S} = \mathbf{S}^\top$.
- Es **semidefinida positiva**: todos sus autovalores son $\geq 0$.
- La diagonal contiene las varianzas (siempre $\geq 0$).
```

---

## La Matriz de Correlaciones

La **matriz de correlaciones** $\mathbf{R}$ estandariza las covarianzas dividiéndolas por las desviaciones típicas de cada par de variables:

$$
r_{jk} = \frac{s_{jk}}{s_j \cdot s_k}
$$

Así, todos los valores están entre $-1$ y $1$:
- $r_{jk} = 1$: correlación lineal positiva perfecta.
- $r_{jk} = -1$: correlación lineal negativa perfecta.
- $r_{jk} = 0$: ausencia de correlación lineal.

```r
# Matriz de correlaciones en R
R <- cor(X)
print(R)

# Visualización atractiva
library(corrplot)
corrplot(R, method = "color", type = "upper",
         addCoef.col = "black", tl.col = "black",
         col = colorRampPalette(c("#2166AC", "white", "#D6604D"))(200),
         title = "Matriz de correlaciones", mar = c(0,0,1,0))
```

La Tabla 1 resume la diferencia entre covarianza y correlación.

**Tabla 1. Comparación entre covarianza y correlación.**

| Característica | Covarianza ($s_{jk}$) | Correlación ($r_{jk}$) |
|---|---|---|
| Rango de valores | $(-\infty, +\infty)$ | $[-1, 1]$ |
| Depende de la escala | Sí | No |
| Interpretación | Dirección de la relación | Dirección e intensidad |
| Cuándo usarla | Variables en misma escala | Comparación entre variables |

---

## Autovalores y Autovectores

Algunos métodos como el **PCA** o el **Análisis Discriminante** requieren calcular los **autovalores** ($\lambda_i$) y **autovectores** ($\mathbf{v}_i$) de la matriz de covarianzas o correlaciones.

Un autovector $\mathbf{v}$ y su autovalor $\lambda$ satisfacen:

$$
\mathbf{S} \mathbf{v} = \lambda \mathbf{v}
$$

Los autovalores indican cuánta varianza captura cada dirección; los autovectores indican en qué dirección del espacio original se proyectan los datos.

```r
# Autovalores y autovectores en R
ev <- eigen(S)
cat("Autovalores:\n"); print(ev$values)
cat("Autovectores (columnas):\n"); print(ev$vectors)

# Proporcion de varianza explicada por cada autovalor
prop_var <- ev$values / sum(ev$values)
cat("Proporcion de varianza explicada:\n"); print(round(prop_var, 4))
```

```{admonition} Conexión con el temario
:class: important

Los autovalores y autovectores de $\mathbf{S}$ o $\mathbf{R}$ son **exactamente** lo que calcula el PCA en el siguiente tema. Entender este apartado es clave para comprender por qué el PCA funciona.
```

---

## Resumen

La tabla 2 recoge los conceptos matriciales más importantes del curso y su función en el Análisis Multivariante.

**Tabla 2. Conceptos matriciales clave y su uso en el curso.**

| Concepto | Notación | Para qué se usa |
|---|---|---|
| Matriz de datos | $\mathbf{X}$ ($n \times p$) | Almacena todas las observaciones |
| Vector de medias | $\bar{\mathbf{x}}$ ($p \times 1$) | Centroide de la nube de puntos |
| Datos centrados | $\tilde{\mathbf{X}}$ | Base para calcular $\mathbf{S}$ y para PCA |
| Datos estandarizados | $\mathbf{Z}$ | Elimina efecto de escala |
| Matriz de covarianzas | $\mathbf{S}$ ($p \times p$) | Variabilidad y relaciones entre variables |
| Matriz de correlaciones | $\mathbf{R}$ ($p \times p$) | Intensidad de relaciones sin efecto escala |
| Autovalores / Autovectores | $\lambda_i$ / $\mathbf{v}_i$ | PCA, Análisis Discriminante, SEM |
