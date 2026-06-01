# Ejemplos Resueltos

Esta sección ilustra el cálculo paso a paso de los elementos que componen el Análisis de Componentes Principales partiendo de resultados intermedios.

## Ejemplo 1: Cálculo manual de Cargas Factoriales (Loadings)

Supongamos que tras procesar una base de datos con $p=2$ variables (Ingresos y Edad), hemos obtenido su matriz de covarianzas, y el software nos arroja la siguiente descomposición espectral:

**Valores propios ($\lambda$):**
* $\lambda_1 = 9$
* $\lambda_2 = 4$

**Vectores propios ($V$, matriz de pesos):**
$$ V = \begin{pmatrix} 0.8 & -0.6 \\ 0.6 & 0.8 \end{pmatrix} $$

1. ¿Cuál es el porcentaje de varianza explicada por la primera componente principal?
2. Calcula la matriz de Cargas Factoriales (Loadings) $L$.
3. ¿Cuál de las dos variables tiene mayor correlación empírica con la Primera Componente Principal?

```{admonition} Solución
:class: dropdown, tip

**1. Porcentaje de varianza:**
La varianza total es la traza (suma de valores propios): $\lambda_1 + \lambda_2 = 9 + 4 = 13$.
El porcentaje explicado por PC1 es: $\frac{9}{13} \approx 0.692 \implies 69.2\%$.

**2. Matriz de Cargas Factoriales ($L$):**
La fórmula teórica nos dice que $L = V \Lambda^{1/2}$, es decir, multiplicamos cada vector propio por la desviación estándar correspondiente ($\sqrt{\lambda_k}$).
* $\sqrt{\lambda_1} = \sqrt{9} = 3$
* $\sqrt{\lambda_2} = \sqrt{4} = 2$

La matriz $\Lambda^{1/2}$ es diagonal con valores 3 y 2:
$$ L = \begin{pmatrix} 0.8 & -0.6 \\ 0.6 & 0.8 \end{pmatrix} \begin{pmatrix} 3 & 0 \\ 0 & 2 \end{pmatrix} = \begin{pmatrix} (0.8 \times 3) & (-0.6 \times 2) \\ (0.6 \times 3) & (0.8 \times 2) \end{pmatrix} = \begin{pmatrix} 2.4 & -1.2 \\ 1.8 & 1.6 \end{pmatrix} $$

*(Nota: Como partimos de una matriz de covarianzas en lugar de una de correlaciones, las cargas superan el valor de 1. Representan covarianzas entre las variables y las componentes. Si estuviéramos en ACP estandarizado, estarían acotadas entre -1 y 1).*

**3. Correlación máxima con PC1:**
Miramos la primera columna de la matriz $L$.
* Variable 1 (Ingresos) tiene una carga en PC1 de $2.4$.
* Variable 2 (Edad) tiene una carga en PC1 de $1.8$.

La primera variable participa más activamente en la definición de la Componente 1.
```

## Ejemplo 2: Proyección y Puntuaciones (Scores)

Utilizando las matrices del Ejemplo 1, supón que tienes un nuevo individuo cuyos datos *ya centrados* (restada la media muestral) son $x_c = (Ingreso\_centrado=5, Edad\_centrada=-2)$.

1. Calcula las puntuaciones (scores) de este individuo en ambas componentes principales.
2. Comprueba algebraicamente que puedes reconstruir el vector de datos centrado original utilizando sus scores.

```{admonition} Solución
:class: dropdown, tip

**1. Cálculo de scores ($Y$):**
Las puntuaciones se obtienen proyectando los datos centrados sobre la base de vectores propios ($Y = X_c V$).
Tratando al individuo como un vector fila $x_c = (5, -2)$:

$$ y = (5, -2) \begin{pmatrix} 0.8 & -0.6 \\ 0.6 & 0.8 \end{pmatrix} $$
* Score PC1 ($y_1$): $5(0.8) + (-2)(0.6) = 4 - 1.2 = 2.8$
* Score PC2 ($y_2$): $5(-0.6) + (-2)(0.8) = -3 - 1.6 = -4.6$

Las coordenadas del individuo en el nuevo plano factorial son $(2.8, -4.6)$.

**2. Reconstrucción de la matriz:**
La teoría nos dice que $X_c = Y V^T$. Probemos con nuestro individuo fila $y = (2.8, -4.6)$ y la matriz transpuesta $V^T$:

$$ V^T = \begin{pmatrix} 0.8 & 0.6 \\ -0.6 & 0.8 \end{pmatrix} $$

$$ \tilde{x}_c = (2.8, -4.6) \begin{pmatrix} 0.8 & 0.6 \\ -0.6 & 0.8 \end{pmatrix} $$
* Primera coordenada: $2.8(0.8) + (-4.6)(-0.6) = 2.24 + 2.76 = 5.0$
* Segunda coordenada: $2.8(0.6) + (-4.6)(0.8) = 1.68 - 3.68 = -2.0$

Hemos recuperado exactamente el vector original $x_c = (5, -2)$. Esto es posible porque hemos utilizado todas las componentes principales ($p=2$).
```
