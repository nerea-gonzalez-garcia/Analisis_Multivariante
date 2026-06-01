# Práctica guiada en R: Herramientas algebraicas

En esta sección vamos a reproducir matricialmente en R todos los conceptos teóricos desarrollados en el capítulo. R es un lenguaje matricial por excelencia, lo que nos permite traducir directamente el álgebra lineal a código.

## 1. Creación de la matriz de datos

Vamos a simular un pequeño conjunto de datos de $n=5$ individuos observados sobre $p=3$ variables.

```r
# Definir la matriz de datos X (5x3)
set.seed(123)
X <- matrix(c(
   2,  4,  5,
   3,  6,  7,
   4,  5,  6,
   5,  7,  8,
   6,  8,  9
), nrow = 5, byrow = TRUE)

colnames(X) <- c("V1", "V2", "V3")
rownames(X) <- paste0("Ind", 1:5)

print("Matriz de datos X:")
print(X)
```

## 2. Vector de medias y matriz centrada

Calculemos el vector de medias (el centro de gravedad) y centremos la matriz. En álgebra matricial teórica, $X_c = X - \mathbf{1}\bar{x}^T$. En R podemos usar la función `scale()` con `scale = FALSE`, o programarlo directamente:

```r
n <- nrow(X)
p <- ncol(X)

# Vector de medias (colMeans)
x_bar <- colMeans(X)
print("Vector de medias:")
print(x_bar)

# Matriz centrada (manualmente)
# Repetimos el vector de medias en n filas
Matriz_Medias <- matrix(rep(x_bar, each = n), nrow = n)
Xc <- X - Matriz_Medias

print("Matriz centrada Xc:")
print(Xc)

# Verificamos que las nuevas columnas suman 0
print("Suma de las columnas de Xc (debe ser aprox 0):")
print(round(colSums(Xc), 10))
```

## 3. Matriz de covarianzas y correlaciones

Vamos a calcular la matriz de covarianzas manualmente a partir de los dobles productos, y luego verificaremos con la función base `cov()`.

```r
# Matriz de dobles productos (SSCP)
SSCP <- t(Xc) %*% Xc

# Matriz de covarianzas muestral (S)
S_manual <- SSCP / (n - 1)

print("Matriz de covarianzas (Manual):")
print(S_manual)

print("Matriz de covarianzas (Función cov de R):")
print(cov(X))
```

Para la matriz de correlaciones, necesitamos la matriz diagonal de desviaciones típicas.

```r
# Desviaciones típicas (raíz de la diagonal de S)
D_inv_sqrt <- diag(1 / sqrt(diag(S_manual)))

# Correlaciones: R = D^(-1/2) * S * D^(-1/2)
R_manual <- D_inv_sqrt %*% S_manual %*% D_inv_sqrt
rownames(R_manual) <- colnames(R_manual) <- colnames(X)

print("Matriz de correlaciones (Manual):")
print(R_manual)

print("Matriz de correlaciones (Función cor de R):")
print(cor(X))
```

## 4. Descomposición Espectral de S

La función `eigen()` calcula los valores y vectores propios de una matriz cuadrada simétrica.

```r
# Descomposición espectral de la matriz de covarianzas
espectral <- eigen(S_manual)

Lambda <- diag(espectral$values)  # Valores propios (varianzas)
V <- espectral$vectors            # Vectores propios (direcciones)

print("Valores propios (Lambda):")
print(diag(Lambda))

print("Vectores propios (V):")
print(V)

# Reconstrucción de S (S = V * Lambda * V^T)
S_reconstruida <- V %*% Lambda %*% t(V)

print("Reconstrucción espectral de S:")
print(zapsmall(S_reconstruida)) # zapsmall elimina errores de coma flotante
```

## 5. Descomposición en Valores Singulares (SVD)

Finalmente, aplicamos SVD a la matriz de datos centrada original $X_c$ para verificar su profunda conexión con la descomposición espectral de $S$.

```r
# SVD de la matriz centrada
svd_Xc <- svd(Xc)

U <- svd_Xc$u
D <- diag(svd_Xc$d) # Valores singulares
V_svd <- svd_Xc$v

print("Valores singulares de Xc (d):")
print(diag(D))

print("Vectores singulares derechos de Xc (V_svd):")
print(V_svd)
```

```{admonition} Comentario Docente
:class: important
Observa atentamente los resultados que acabas de imprimir en tu consola de R. 
1. ¿Ves la matriz `V_svd`? Compara sus columnas con la matriz `V` de la descomposición espectral. **¡Son exactamente las mismas!** (Puede cambiar el signo de toda la columna, lo cual es matemáticamente equivalente).
2. Toma un valor singular $d_i$ de `svd_Xc$d`, elévalo al cuadrado y divídelo por $n-1$ (es decir, $4$). El resultado será exactamente el valor propio $\lambda_i$ de `espectral$values`.

Has demostrado empíricamente el puente algebraico que sostiene el Análisis de Componentes Principales.
```
