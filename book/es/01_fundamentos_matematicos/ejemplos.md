# Ejemplos Resueltos

A continuación, se presentan ejemplos resueltos paso a paso para afianzar los conceptos matemáticos del capítulo. Te recomendamos intentar resolverlos con papel y lápiz antes de mirar la solución.

## Ejemplo 1: Cálculo manual de covarianzas

Dada la siguiente matriz de datos de $n=3$ observaciones y $p=2$ variables:

$$
X = \begin{pmatrix}
2 & 4 \\
4 & 2 \\
6 & 6 
\end{pmatrix}
$$

Se pide:
1. Calcular el vector de medias $\bar{x}$.
2. Calcular la matriz centrada $X_c$.
3. Obtener la matriz de suma de cuadrados y productos cruzados (SSCP).
4. Obtener la matriz de covarianzas muestral $S$.

```{admonition} Solución
:class: dropdown, tip

**1. Vector de medias:**
Calculamos la media de cada columna:
* $\bar{x}_1 = (2 + 4 + 6) / 3 = 12 / 3 = 4$
* $\bar{x}_2 = (4 + 2 + 6) / 3 = 12 / 3 = 4$

Por tanto, $\bar{x} = \begin{pmatrix} 4 \\ 4 \end{pmatrix}$.

**2. Matriz centrada ($X_c$):**
Restamos la media correspondiente a cada columna:
$$
X_c = \begin{pmatrix}
2 - 4 & 4 - 4 \\
4 - 4 & 2 - 4 \\
6 - 4 & 6 - 4
\end{pmatrix} = \begin{pmatrix}
-2 & 0 \\
0 & -2 \\
2 & 2
\end{pmatrix}
$$
Comprobación de seguridad: La suma de cada columna de $X_c$ es cero.

**3. Matriz SSCP ($X_c^T X_c$):**
Multiplicamos la matriz transpuesta por la matriz centrada original:
$$
SSCP = \begin{pmatrix} -2 & 0 & 2 \\ 0 & -2 & 2 \end{pmatrix} \begin{pmatrix} -2 & 0 \\ 0 & -2 \\ 2 & 2 \end{pmatrix}
$$
* Elemento $(1,1) = (-2)(-2) + (0)(0) + (2)(2) = 4 + 0 + 4 = 8$
* Elemento $(1,2) = (-2)(0) + (0)(-2) + (2)(2) = 0 + 0 + 4 = 4$
* Elemento $(2,1) = (0)(-2) + (-2)(0) + (2)(2) = 0 + 0 + 4 = 4$
* Elemento $(2,2) = (0)(0) + (-2)(-2) + (2)(2) = 0 + 4 + 4 = 8$

$$
SSCP = \begin{pmatrix} 8 & 4 \\ 4 & 8 \end{pmatrix}
$$

**4. Matriz de covarianzas ($S$):**
Dividimos la matriz SSCP por los grados de libertad, $n - 1 = 3 - 1 = 2$.
$$
S = \frac{1}{2} \begin{pmatrix} 8 & 4 \\ 4 & 8 \end{pmatrix} = \begin{pmatrix} 4 & 2 \\ 2 & 4 \end{pmatrix}
$$
Interpretación: Ambas variables tienen una varianza de 4, y covarían de forma positiva (covarianza de 2).
```

## Ejemplo 2: Vectores y valores propios

Para la matriz de covarianzas obtenida en el Ejemplo 1, $S = \begin{pmatrix} 4 & 2 \\ 2 & 4 \end{pmatrix}$, halla sus valores propios y vectores propios normalizados.

```{admonition} Solución
:class: dropdown, tip

**1. Obtención de valores propios ($\lambda$):**
Resolvemos la ecuación característica $\det(S - \lambda I) = 0$:
$$
\det \begin{pmatrix} 4-\lambda & 2 \\ 2 & 4-\lambda \end{pmatrix} = (4-\lambda)^2 - 4 = 0
$$
$$
(4-\lambda)^2 = 4 \implies 4-\lambda = \pm 2
$$
Por tanto, los valores propios son:
* $\lambda_1 = 4 + 2 = 6$
* $\lambda_2 = 4 - 2 = 2$

Comprobación (Traza): La traza de $S$ es $4+4=8$. La suma de autovalores es $6+2=8$. Correcto.

**2. Obtención del vector propio para $\lambda_1 = 6$:**
Resolvemos el sistema $(S - 6 I)v = 0$:
$$
\begin{pmatrix} -2 & 2 \\ 2 & -2 \end{pmatrix} \begin{pmatrix} v_{1} \\ v_{2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} \implies -2v_1 + 2v_2 = 0 \implies v_1 = v_2
$$
Un vector propio inicial es $(1, 1)^T$. Para normalizarlo, calculamos su norma: $\sqrt{1^2 + 1^2} = \sqrt{2}$.
El vector propio normalizado es $v_1 = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{pmatrix}$.

**3. Obtención del vector propio para $\lambda_2 = 2$:**
Resolvemos el sistema $(S - 2 I)v = 0$:
$$
\begin{pmatrix} 2 & 2 \\ 2 & 2 \end{pmatrix} \begin{pmatrix} v_{1} \\ v_{2} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \end{pmatrix} \implies 2v_1 + 2v_2 = 0 \implies v_1 = -v_2
$$
Un vector propio inicial es $(1, -1)^T$. Normalizado: $v_2 = \begin{pmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{pmatrix}$.
```
