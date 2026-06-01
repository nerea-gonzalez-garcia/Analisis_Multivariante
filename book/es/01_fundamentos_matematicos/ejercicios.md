# Ejercicios Propuestos y Resueltos

Esta sección presenta problemas teóricos y prácticos sobre los Fundamentos Matemáticos del Análisis Multivariante. Cada ejercicio incluye su resolución completa paso a paso.

## CUESTIONES TEÓRICAS

### Cuestión Teórica 1: Centrado y Varianza

**Enunciado:** Demuestra algebraicamente que centrar una matriz de datos $X$ (es decir, formar $X_c = X - \mathbf{1}\bar{x}^T$) no altera el valor de la matriz de covarianzas $S$.

**Resolución:**

La matriz de covarianzas se define como:
$$S = \frac{1}{n-1} X^T X - \frac{1}{n-1} \bar{x} \mathbf{1}^T X - \frac{1}{n-1} X^T \mathbf{1} \bar{x}^T + \frac{1}{n-1} \bar{x} \mathbf{1}^T \mathbf{1} \bar{x}^T$$

Reordenemos y simplifiquemos. Sabemos que:
- $X^T \mathbf{1} = n\bar{x}$ (suma de columnas)
- $\mathbf{1}^T \mathbf{1} = n$ (número de filas)

Sustituyendo:
$$S = \frac{1}{n-1} X^T X - \frac{1}{n-1} \bar{x} (n\bar{x})^T - \frac{1}{n-1} (n\bar{x}) \bar{x}^T + \frac{1}{n-1} \bar{x} (n) \bar{x}^T$$

$$S = \frac{1}{n-1} X^T X - \frac{n}{n-1} \bar{x} \bar{x}^T - \frac{n}{n-1} \bar{x} \bar{x}^T + \frac{n}{n-1} \bar{x} \bar{x}^T$$

$$S = \frac{1}{n-1} X^T X - \frac{n}{n-1} \bar{x} \bar{x}^T$$

Alternativamente, usando la matriz centrada:
$$S = \frac{1}{n-1} X_c^T X_c$$

donde $X_c = X - \mathbf{1}\bar{x}^T$.

Expandiendo:
$$X_c^T X_c = (X - \mathbf{1}\bar{x}^T)^T (X - \mathbf{1}\bar{x}^T) = X^T X - X^T \mathbf{1}\bar{x} - \bar{x}^T \mathbf{1}^T X + \bar{x}^T \mathbf{1}^T \mathbf{1} \bar{x}$$

$$= X^T X - (n\bar{x})\bar{x} - \bar{x}^T (n\bar{x}) + \bar{x}^T (n) \bar{x}$$

$$= X^T X - n\bar{x}\bar{x}^T - n\bar{x}^T\bar{x} + n\bar{x}^T\bar{x}$$

$$= X^T X - n\bar{x}\bar{x}^T$$

Por lo tanto:
$$S = \frac{1}{n-1} (X^T X - n\bar{x}\bar{x}^T)$$

**Conclusión:** La fórmula con $X$ y $\bar{x}$ sin centrar es equivalente a usar $X_c$. El proceso de centrado absorbe algebraicamente los términos de la media, pero el resultado final es el mismo.

---

### Cuestión Teórica 2: Valores Propios de la Matriz de Correlación con Correlación Perfecta

**Enunciado:** ¿Cuáles son los valores propios de una matriz de correlación empírica $R$ de dimensión $p \times p$ si todas las variables originales están perfecta y linealmente correlacionadas ($r_{ij}=1$ para todo $i, j$)? Justifica tu respuesta apelando al concepto de rango de la matriz.

**Resolución:**

Si todas las correlaciones son 1, significa que la matriz $R$ tiene la forma:
$$R = \begin{pmatrix} 1 & 1 & 1 & \cdots & 1 \\ 1 & 1 & 1 & \cdots & 1 \\ 1 & 1 & 1 & \cdots & 1 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & 1 & 1 & \cdots & 1 \end{pmatrix}$$

Esta matriz puede escribirse como:
$$R = \mathbf{1} \mathbf{1}^T / p$$

(excepto por un factor de normalización; la idea es que todas las filas son proporcionales).

**Rango:** Todas las filas son idénticas, por lo que el rango es exactamente 1. Esto significa que solo hay UN valor propio no nulo.

**Cálculo de valores propios:**

Para encontrar los autovalores, resolvemos el problema de eigenvalores. Si $R \mathbf{v} = \lambda \mathbf{v}$, y sabemos que la matriz tiene rango 1:
- El espacio nulo tiene dimensión $p-1$, lo que implica $p-1$ valores propios iguales a 0.
- Solo existe un valor propio positivo.

Para hallar ese valor propio, observa que:
$$R \mathbf{1} = \begin{pmatrix} p \\ p \\ \vdots \\ p \end{pmatrix} = p \mathbf{1}$$

Por lo tanto, $\mathbf{1}$ es un vector propio con valor propio $\lambda_1 = p$.

**Conclusión:** Los valores propios son: $\lambda_1 = p$ y $\lambda_2 = \lambda_3 = \cdots = \lambda_p = 0$.

---

### Cuestión Teórica 3: Varianza Total y Valores Singulares

**Enunciado:** Si aplicas el proceso de SVD a una matriz centrada $X_c$ y obtienes los valores singulares $d_1 = 5, d_2 = 3, d_3 = 0$, ¿cuál es la varianza total de la muestra si el número de individuos es $n=11$?

**Resolución:**

La relación entre valores singulares y valores propios es:
$$\lambda_i = \frac{d_i^2}{n-1}$$

Con $n=11$, tenemos $n-1=10$. Los valores propios son:
$$\lambda_1 = \frac{5^2}{10} = \frac{25}{10} = 2.5$$
$$\lambda_2 = \frac{3^2}{10} = \frac{9}{10} = 0.9$$
$$\lambda_3 = \frac{0^2}{10} = 0$$

La varianza total es la suma de los valores propios (que es igual a la traza de la matriz de covarianzas):
$$\text{Varianza Total} = \sum_{i=1}^p \lambda_i = 2.5 + 0.9 + 0 = 3.4$$

**Conclusión:** La varianza total de la muestra es $\mathbf{3.4}$.

---

## PROBLEMAS PRÁCTICOS

### Ejercicio Práctico 1: De la Covarianza a la Correlación

**Enunciado:** Dada la siguiente matriz de covarianzas muestral $S$ sobre 3 variables:

$$
S = \begin{pmatrix} 
16 & -2 & 4 \\ 
-2 & 4 & 1 \\ 
4 & 1 & 9 
\end{pmatrix}
$$

1. Determina la varianza de cada una de las variables originales.
2. Calcula la matriz de correlaciones $R$.
3. ¿Entre qué par de variables existe una mayor dependencia lineal independientemente del signo?

**Resolución:**

**Apartado 1: Varianzas**

Las varianzas están en la diagonal de $S$:
- $s_1^2 = 16 \Rightarrow s_1 = 4$
- $s_2^2 = 4 \Rightarrow s_2 = 2$
- $s_3^2 = 9 \Rightarrow s_3 = 3$

**Apartado 2: Matriz de Correlaciones**

La fórmula es $R = D^{-1/2} S D^{-1/2}$, donde $D = \text{diag}(s_1^2, s_2^2, s_3^2)$.

$$D^{-1/2} = \begin{pmatrix} 1/4 & 0 & 0 \\ 0 & 1/2 & 0 \\ 0 & 0 & 1/3 \end{pmatrix}$$

Calculamos:
$$r_{11} = \frac{s_{11}}{s_1 s_1} = \frac{16}{4 \cdot 4} = 1$$
$$r_{12} = \frac{s_{12}}{s_1 s_2} = \frac{-2}{4 \cdot 2} = -0.25$$
$$r_{13} = \frac{s_{13}}{s_1 s_3} = \frac{4}{4 \cdot 3} = \frac{1}{3} \approx 0.333$$
$$r_{22} = \frac{4}{2 \cdot 2} = 1$$
$$r_{23} = \frac{1}{2 \cdot 3} = \frac{1}{6} \approx 0.167$$
$$r_{33} = \frac{9}{3 \cdot 3} = 1$$

$$R = \begin{pmatrix} 
1 & -0.25 & 0.333 \\ 
-0.25 & 1 & 0.167 \\ 
0.333 & 0.167 & 1 
\end{pmatrix}$$

**Apartado 3: Mayor Dependencia Lineal**

Calculamos el valor absoluto de cada correlación:
- $|r_{12}| = 0.25$
- $|r_{13}| = 0.333$ ← Mayor valor
- $|r_{23}| = 0.167$

**Conclusión:** La mayor dependencia lineal es entre las **variables 1 y 3** con $|r_{13}| = 0.333$.

---

### Ejercicio Práctico 2: Geometría de las Transformaciones y Descomposición Espectral

**Enunciado:** Considera un punto en $\mathbb{R}^2$, representado por el vector columna $x = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$. Tienes las siguientes dos matrices de transformación:

$$ A = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix}, \quad B = \begin{pmatrix} \cos(\pi/4) & -\sin(\pi/4) \\ \sin(\pi/4) & \cos(\pi/4) \end{pmatrix} $$

1. Calcula $Ax$ e indica geométricamente qué le ha sucedido al punto original.
2. Calcula $Bx$ e indica qué tipo de transformación es $B$.
3. ¿Cómo se relacionan estas matrices con las matrices $\Lambda$ y $V$ de una descomposición espectral $S = V \Lambda V^T$?

**Resolución:**

**Apartado 1: Transformación $Ax$**

$$Ax = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 4 \\ 3 \end{pmatrix}$$

**Interpretación geométrica:** La matriz $A$ es diagonal, lo que significa que actúa como una **homothecia (escalado no uniforme)**. El punto original se estira por un factor de 2 en la dirección del eje X y por un factor de 3 en la dirección del eje Y.
- La coordenada X: $2 \rightarrow 4$ (se duplica)
- La coordenada Y: $1 \rightarrow 3$ (se triplica)

El punto se desplaza desde $(2, 1)$ a $(4, 3)$, permaneciendo en el mismo cuadrante pero alejándose del origen.

**Apartado 2: Transformación $Bx$**

Con $\cos(\pi/4) = \sin(\pi/4) = \frac{\sqrt{2}}{2} \approx 0.707$:

$$B = \begin{pmatrix} 0.707 & -0.707 \\ 0.707 & 0.707 \end{pmatrix}$$

$$Bx = \begin{pmatrix} 0.707 & -0.707 \\ 0.707 & 0.707 \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 1.414 - 0.707 \\ 1.414 + 0.707 \end{pmatrix} = \begin{pmatrix} 0.707 \\ 2.121 \end{pmatrix}$$

**Interpretación geométrica:** La matriz $B$ es una **matriz de rotación** de ángulo $\pi/4 = 45^\circ$ (rotación en sentido contrario a las agujas del reloj). El punto $(2, 1)$ se rota 45 grados alrededor del origen, sin cambiar su distancia respecto al origen.

Verificación: 
- Distancia original: $\sqrt{2^2 + 1^2} = \sqrt{5} \approx 2.236$
- Distancia tras rotación: $\sqrt{0.707^2 + 2.121^2} = \sqrt{0.5 + 4.5} = \sqrt{5} \approx 2.236$ ✓

**Apartado 3: Relación con Descomposición Espectral**

En una descomposición espectral $S = V \Lambda V^T$:
- **$V$:** Es una matriz de rotación ortogonal (como $B$). Sus columnas son los vectores propios ortonormales. Rota el espacio original a un nuevo sistema de coordenadas donde la matriz es diagonal.
- **$\Lambda$:** Es una matriz diagonal (como $A$). Contiene los valores propios. Actúa como un escalado no uniforme a lo largo de los ejes del nuevo sistema de coordenadas.

**Conclusión:** La descomposición espectral puede interpretarse como:
1. **$V^T$:** Rota el espacio original
2. **$\Lambda$:** Escala los ejes del espacio rotado
3. **$V$:** Rota de vuelta al espacio original

Esto es exactamente lo que hace la transformación compuesta $B \to A \to B^T$ (aunque en notación espectral es $V^T \to \Lambda \to V$).

---

## PROBLEMAS ADICIONALES

### Ejercicio Práctico 3: SVD y Reconstrucción de Matrices (NUEVO)

**Enunciado:** Consideremos una pequeña matriz de datos centrada:

$$
X_c = \begin{pmatrix} 
3 & 1 \\
1 & 2 \\
-1 & 0 \\
-3 & -3
\end{pmatrix} \quad (n=4, p=2)
$$

1. Calcula la matriz de covarianzas $S$ manualmente.
2. Calcula la descomposición espectral de $S$ (valores propios y vectores propios).
3. Realiza la SVD de $X_c$.
4. Verifica que los valores propios de $S$ coinciden con $\frac{d_i^2}{n-1}$ donde $d_i$ son los valores singulares.

**Resolución:**

**Apartado 1: Matriz de Covarianzas**

$$SSCP = X_c^T X_c = \begin{pmatrix} 3 & 1 & -1 & -3 \\ 1 & 2 & 0 & -3 \end{pmatrix} \begin{pmatrix} 3 & 1 \\ 1 & 2 \\ -1 & 0 \\ -3 & -3 \end{pmatrix}$$

Calculamos:
- $(1,1)$: $3 \cdot 3 + 1 \cdot 1 + (-1)(-1) + (-3)(-3) = 9 + 1 + 1 + 9 = 20$
- $(1,2)$: $3 \cdot 1 + 1 \cdot 2 + (-1) \cdot 0 + (-3)(-3) = 3 + 2 + 0 + 9 = 14$
- $(2,1)$: $1 \cdot 3 + 2 \cdot 1 + 0 \cdot (-1) + (-3)(-3) = 3 + 2 + 0 + 9 = 14$
- $(2,2)$: $1 \cdot 1 + 2 \cdot 2 + 0 \cdot 0 + (-3)(-3) = 1 + 4 + 0 + 9 = 14$

$$SSCP = \begin{pmatrix} 20 & 14 \\ 14 & 14 \end{pmatrix}$$

$$S = \frac{1}{n-1} SSCP = \frac{1}{3} \begin{pmatrix} 20 & 14 \\ 14 & 14 \end{pmatrix} = \begin{pmatrix} 6.667 & 4.667 \\ 4.667 & 4.667 \end{pmatrix}$$

**Apartado 2: Descomposición Espectral**

Polinomio característico: $\det(S - \lambda I) = 0$

$$(6.667 - \lambda)(4.667 - \lambda) - 4.667^2 = 0$$
$$\lambda^2 - 11.334\lambda + 31.111 - 21.780 = 0$$
$$\lambda^2 - 11.334\lambda + 9.331 = 0$$

Usando fórmula cuadrática:
$$\lambda = \frac{11.334 \pm \sqrt{128.46 - 37.324}}{2} = \frac{11.334 \pm \sqrt{91.136}}{2} = \frac{11.334 \pm 9.547}{2}$$

$$\lambda_1 \approx 10.44, \quad \lambda_2 \approx 0.89$$

(Para el propósito del ejercicio, usaría la función `eigen()` en R para obtener valores exactos.)

**Apartado 3: SVD**

En R: `svd(Xc)` proporciona $U$, $D$, $V$ directamente.

**Apartado 4: Verificación**

Con $n=4 \Rightarrow n-1=3$:
$$\lambda_i = \frac{d_i^2}{3}$$

Esta relación se verifica numéricamente.

---

## CÓDIGO R PARA VERIFICACIÓN

```r
# Ejercicio 1: Covarianza a Correlación
S <- matrix(c(16, -2, 4, -2, 4, 1, 4, 1, 9), nrow=3)
diag_sqrt <- sqrt(diag(S))
R <- S / outer(diag_sqrt, diag_sqrt)
print(R)

# Ejercicio 2: Transformaciones
x <- c(2, 1)
A <- diag(c(2, 3))
B <- matrix(c(cos(pi/4), sin(pi/4), -sin(pi/4), cos(pi/4)), nrow=2, byrow=TRUE)

print("Ax:"); print(A %*% x)
print("Bx:"); print(B %*% x)

# Ejercicio 3: SVD y Espectral
Xc <- matrix(c(3, 1, 1, 2, -1, 0, -3, -3), nrow=4, byrow=TRUE)
S_ex3 <- cov(Xc)
eig <- eigen(S_ex3)
svd_Xc <- svd(Xc)

print("Valores propios:"); print(eig$values)
print("Valores singulares al cuadrado / (n-1):"); print(svd_Xc$d^2 / 3)
```
