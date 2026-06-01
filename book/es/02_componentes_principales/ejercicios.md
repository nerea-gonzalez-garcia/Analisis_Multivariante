# Ejercicios Propuestos y Resueltos: Análisis de Componentes Principales

Esta sección presenta problemas teóricos e interpretativos sobre el ACP, cada uno con su resolución completa paso a paso. Los ejercicios progresa desde conceptos fundamentales hasta aplicaciones prácticas complejas.

---

## CUESTIONES TEÓRICAS

### Cuestión Teórica 1: Dimensionalidad Intrínseca e Impacto del Rango

**Enunciado:** Se tiene una matriz de datos $X$ de tamaño $n=25$ individuos y $p=300$ genes (genómica). Se centra la matriz (obteniendo $X_c$) y se realiza un ACP.

1. ¿Cuál es el número máximo de componentes principales con varianza estrictamente mayor a 0 que se podrán extraer? Justifica tu respuesta apelando al concepto de rango de una matriz.
2. ¿Qué implica geométricamente este hecho respecto a la verdadera distribución de los 25 pacientes en el espacio genómico de 300 dimensiones?

**Resolución:**

**Apartado 1: Número máximo de componentes con $\lambda_i > 0$**

Para una matriz centrada $X_c$ de dimensión $n \times p$, el álgebra lineal nos garantiza que:
$$\text{rg}(X_c) \leq \min(n-1, p)$$

El rango está limitado por $n-1$ (no $n$) porque al centrar, introducimos una dependencia lineal forzada: cada columna de $X_c$ suma exactamente a 0.

En nuestro caso:
$$\text{rg}(X_c) \leq \min(25-1, 300) = \min(24, 300) = 24$$

Por lo tanto, el número máximo de componentes principales con varianza estrictamente positiva es exactamente **24**.

La matriz de covarianzas $S$ es de dimensión $300 \times 300$, pero tendrá exactamente 24 valores propios $\lambda_i > 0$ y los restantes 276 valores propios serán iguales a 0.

**Apartado 2: Interpretación geométrica**

A pesar de tener datos en un espacio de 300 dimensiones, los 25 pacientes no se distribuyen "aleatoriamente" por todo ese espacio. De hecho, los datos habitaban un **subespacio de dimensión máxima 24**.

Geométricamente, imagina que los 300 genes forman un espacio gigantesco, pero los 25 pacientes están todos concentrados en una "lámina" o "hipersuperficie" de dimensión 24, embebida dentro del espacio de 300 dimensiones. Las 276 dimensiones restantes simplemente no aportan variabilidad: todos los pacientes tienen un comportamiento idéntico en esas 276 direcciones ortogonales.

**Conclusión:** Aunque el investigador midió 300 genes (variables), la verdadera "información" del problema vive en solo 24 dimensiones. El ACP puede capturar esta realidad de forma perfecta: las primeras 24 componentes explicarán el 100% de la varianza, y las restantes 276 componentes tendrán $\lambda = 0$.

---

### Cuestión Teórica 2: Incorrelación de Componentes Principales

**Enunciado:** Demuestra algebraicamente, partiendo de la ecuación $Y = X_c V$ y sabiendo que $S = \frac{1}{n-1} X_c^T X_c$ tiene la descomposición espectral $S = V \Lambda V^T$, que la matriz de covarianzas de las componentes principales $Y$ es estrictamente la matriz diagonal $\Lambda$.

**Resolución:**

Partimos de la matriz de puntuaciones (componentes principales):
$$Y = X_c V$$

La matriz de covarianzas de $Y$ es:
$$\text{Cov}(Y) = \frac{1}{n-1} Y^T Y = \frac{1}{n-1} (X_c V)^T (X_c V) = \frac{1}{n-1} V^T X_c^T X_c V$$

Sabemos que $X_c^T X_c = (n-1) S$, luego:
$$\text{Cov}(Y) = \frac{1}{n-1} V^T ((n-1) S) V = V^T S V$$

Sustituyendo la descomposición espectral $S = V \Lambda V^T$:
$$\text{Cov}(Y) = V^T (V \Lambda V^T) V$$

Como $V$ es ortogonal ($V^T V = I$), tenemos:
$$\text{Cov}(Y) = V^T V \Lambda V^T V = I \Lambda I = \Lambda$$

**Conclusión:** La matriz de covarianzas de las componentes principales es exactamente $\Lambda$, que es diagonal. Esto demuestra matemáticamente que:
- Los elementos de la diagonal son $\lambda_1, \lambda_2, \dots, \lambda_p$ (las varianzas de cada componente)
- Los elementos fuera de la diagonal son todos 0 (no hay covarianza entre componentes)
- Las componentes principales son **100% incorrelacionadas** por construcción

---

### Cuestión Teórica 3: Pesos vs. Cargas

**Enunciado:** Describe en tus propias palabras, y haciendo referencia a su origen algebraico, la diferencia exacta entre un vector propio de peso (weight) y un vector de carga factorial (loading). ¿Por qué el primero está artificialmente acotado en su norma y el segundo no?

**Resolución:**

**Pesos (Weights / Eigenvectors):**

- **Origen algebraico:** Son los vectores propios $v_j$ que satisfacen la restricción $v_j^T v_j = 1$ (norma unitaria). Esta restricción fue introducida artificialmente para resolver el problema de optimización: evitar que la solución divergiera hacia infinito.

- **Interpretación:** Son los coeficientes puros de la combinación lineal. Si $Y_k = v_{1k} X_1 + v_{2k} X_2 + \cdots + v_{pk} X_p$, entonces $v_{jk}$ es el "peso" o "contribución pura" de la variable $X_j$ a la componente $Y_k$.

- **Restricción de norma:** $\sum_{j=1}^p v_{jk}^2 = 1$. Esta es una **restricción artificial, impuesta a priori**, elegida por conveniencia matemática. Cualquier múltiplo escalar de $v_j$ resolvería igualmente bien el problema de maximización, pero elegimos el vector de norma 1 para tener una solución única.

- **Rango de valores:** No están acotados en magnitud individual. Un peso podría ser $v_{1k} = 0.9$ y otro $v_{2k} = 0.1$, sin que esto implique nada particular sobre la importancia relativa de las variables.

**Cargas (Loadings):**

- **Origen algebraico:** Se derivan como $L = V \sqrt{\Lambda}$. Multiplican los pesos por $\sqrt{\lambda_k}$ (la raíz cuadrada de la varianza de la componente).

- **Interpretación:** Son las **correlaciones (o covarianzas si trabajamos con $S$)** entre las variables originales y las componentes principales. El elemento $l_{jk}$ nos dice: "¿Cuánto está correlacionada la variable $X_j$ con la componente $Y_k$?"

- **Significado estadístico:** Una carga alta ($|l_{jk}| \approx 1$) significa que la variable $X_j$ está fuertemente relacionada con la componente $Y_k$. Es directamente interpretable en términos de correlación estándar.

- **Sin restricción artificial:** Las cargas NO tienen una restricción de norma unitaria. Pueden tomar cualquier valor razonable. Su magnitud refleja genuinamente la importancia relativa de las variables en la componente.

**Comparación directa:**

Si los pesos son $v_1 = (0.8, 0.6)^T$ y $\sqrt{\lambda_1} = 2$, entonces:
- Pesos: $(0.8, 0.6)$ — artificialmente restringidos a norma 1
- Cargas: $L = (0.8 \times 2, 0.6 \times 2) = (1.6, 1.2)$ — refleja la varianza de la componente

**Conclusión:** Los pesos son magnitudes algebraicamente "normalizadas" (para resolver el problema de optimización), mientras que las cargas son magnitudes estadísticamente interpretables (correlaciones reales). Para nombrar e interpretar las componentes principales, SIEMPRE se usan las cargas, nunca los pesos.

---

## PROBLEMAS DE INTERPRETACIÓN

### Ejercicio Práctico 1: Calidad de Representación (cos²) e Ilusiones Proyectivas

**Enunciado:** En un estudio de marcas de vehículos basado en 10 atributos de seguridad y confort, se aplica un ACP y se decide retener únicamente las componentes PC1 y PC2. Al revisar los diagnósticos, observamos que para el individuo (marca) "Volvo", la calidad de representación en el primer plano factorial es:
- $\cos^2(\text{Volvo}, \text{PC1}) = 0.05$
- $\cos^2(\text{Volvo}, \text{PC2}) = 0.10$

1. ¿Cuál es el $\cos^2$ total de Volvo en el plano principal?
2. Si un analista junior presenta un gráfico de puntos 2D (plano PC1-PC2) argumentando que Volvo y Honda están muy cerca en ese dibujo y, por tanto, son coches casi idénticos estadísticamente, ¿por qué deberías rechazar tajantemente esa conclusión?

**Resolución:**

**Apartado 1: $\cos^2$ Total**

El $\cos^2$ total es simplemente la suma de los $\cos^2$ individuales en el plano 2D:
$$\cos^2_{\text{total}} = \cos^2(\text{Volvo}, \text{PC1}) + \cos^2(\text{Volvo}, \text{PC2}) = 0.05 + 0.10 = 0.15$$

Esto significa que el **15%** de la variabilidad de Volvo se representa en el plano 2D.

**Apartado 2: Crítica de la Conclusión del Analista Junior**

El argumento del analista junior es completamente **falso por la siguiente razón:**

La proximidad espacial en el gráfico 2D es un **espejismo de proyección**. El punto de Volvo está representado con solo el 15% de fidelidad. Es decir, el 85% de la información sobre Volvo está "fuera del plano", en las dimensiones 3, 4, ..., 10 que no se visualizan.

**Ejemplo concreto:** Imagina que Volvo vive en un espacio 10-dimensional. Si proyectamos Volvo sobre el plano PC1-PC2 con un $\cos^2 = 0.15$, es como si intentaras describir una ciudad mirando solo desde arriba (vista aérea). Una vez que bajas al nivel del suelo (explores las otras dimensiones), la ciudad es completamente distinta. Dos puntos que se ven cercanos desde el aire podrían estar en barrios completamente distintos en la realidad.

**Cálculo del ángulo de proyección:**
$$\cos^2_{\text{total}} = 0.15 \Rightarrow \cos(\theta) = \sqrt{0.15} \approx 0.387 \Rightarrow \theta \approx 67^\circ$$

Volvo forma un ángulo de aproximadamente 67 grados con el plano principal. El punto se proyecta MUY lejos de su posición real.

**Conclusión correcta:** Es posible que Volvo y Honda estén cercanos en PC1-PC2 pero sean **extremadamente distintos** en las otras dimensiones. Necesitarías verificar también los $\cos^2$ de Honda y, idealmente, examinar sus valores en las componentes 3 y posteriores para hacer una comparación justa.

---

### Ejercicio Práctico 2: Interpretación de Cargas Factoriales y Nombrado de Componentes

**Enunciado:** En un estudio psicológico con adolescentes, se miden 4 variables: Ansiedad (A), Estrés (E), Horas de Deporte (D) y Horas de Sueño (S). El ACP sobre la matriz de correlaciones arroja los siguientes *loadings* para la PC1:

* $L(A, \text{PC1}) = 0.85$
* $L(E, \text{PC1}) = 0.88$
* $L(D, \text{PC1}) = -0.75$
* $L(S, \text{PC1}) = -0.80$

1. Bautiza/nombra la componente PC1 basándote en estos *loadings*.
2. Si un individuo tiene un *score* en PC1 extremadamente negativo ($y_1 = -5.0$), ¿cómo es su perfil psicológico esperado en términos de Ansiedad y Sueño?

**Resolución:**

**Apartado 1: Nombrado de la Componente**

Analizamos las cargas:
- **Cargas positivas altas:** Ansiedad (0.85) y Estrés (0.88)
- **Cargas negativas altas:** Horas de Deporte (-0.75) y Horas de Sueño (-0.80)

**Interpretación:** Esta componente contrasta:
- **Lado positivo (altos valores de PC1):** Adolescentes ansiosos y estresados, que duermen poco y hacen poco deporte
- **Lado negativo (bajos valores de PC1):** Adolescentes tranquilos, que duermen mucho y hacen mucho deporte

**Nombre sugerido:** **"Bienestar Psicofísico"** o **"Equilibrio Mental-Físico"**

Alternativamente, según la perspectiva: **"Estrés vs. Autocuidado"** (enfatizando el eje positivo/negativo) o **"Salud Mental"** (si la ansiedad es la variable dominante).

**Apartado 2: Perfil de un Individuo con Score Negativo Extremo**

Un individuo con $y_1 = -5.0$ está **extremadamente en el lado negativo** de la componente, lo opuesto al lado de ansiedad/estrés.

Recordamos la relación: $Y = X_c V$. Para un score muy negativo, esperamos:
- $y_1 = 0.85 \cdot z_A + 0.88 \cdot z_E - 0.75 \cdot z_D - 0.80 \cdot z_S = -5.0$

Para que esta suma sea muy negativa, necesitamos:
- $z_A$ (ansiedad estandarizada) **baja** (menos ansiedad)
- $z_E$ (estrés estandarizado) **bajo** (menos estrés)
- $z_D$ (deporte) **alto** (más deporte)
- $z_S$ (sueño) **alto** (más sueño)

**Conclusión del perfil esperado:**
- **Ansiedad:** Muy baja (el individuo es relativamente tranquilo)
- **Estrés:** Muy bajo
- **Horas de Deporte:** Muy altas (por encima de la media)
- **Horas de Sueño:** Muy altas (por encima de la media)
- **Descripción cualitativa:** "Un adolescente mentalmente equilibrado, que duerme bien, hace mucho ejercicio físico y no sufre ansiedad ni estrés significativos"

---

## PROBLEMAS COMPUTACIONALES

### Ejercicio Práctico 3: Cálculo Manual de Componentes Principales (NUEVO)

**Enunciado:** Consideremos un pequeño dataset de $n=4$ estudiantes evaluados en $p=3$ asignaturas (Matemáticas, Física, Literatura). Los datos centrados son:

$$
X_c = \begin{pmatrix}
2 & 1 & -2 \\
1 & 2 & -1 \\
-1 & -1 & 1 \\
-2 & -2 & 2
\end{pmatrix}
$$

1. Calcula manualmente la matriz de covarianzas $S$.
2. Encuentra los autovalores y autovectores de $S$ (puedes usar aproximaciones numéricas).
3. Determina los pesos, puntuaciones y cargas para las primeras dos componentes.
4. ¿Qué porcentaje de varianza explican las dos primeras componentes?

**Resolución:**

**Apartado 1: Matriz de Covarianzas**

$$SSCP = X_c^T X_c = \begin{pmatrix} 2 & 1 & -1 & -2 \\ 1 & 2 & -1 & -2 \\ -2 & -1 & 1 & 2 \end{pmatrix} \begin{pmatrix} 2 & 1 & -2 \\ 1 & 2 & -1 \\ -1 & -1 & 1 \\ -2 & -2 & 2 \end{pmatrix}$$

Calculamos elemento por elemento:
- $(1,1)$: $2(2) + 1(1) + (-1)(-1) + (-2)(-2) = 4 + 1 + 1 + 4 = 10$
- $(1,2)$: $2(1) + 1(2) + (-1)(-1) + (-2)(-2) = 2 + 2 + 1 + 4 = 9$
- $(1,3)$: $2(-2) + 1(-1) + (-1)(1) + (-2)(2) = -4 - 1 - 1 - 4 = -10$
- (simetría...) $(2,2) = 10$, $(2,3) = -9$, $(3,3) = 10$

$$SSCP = \begin{pmatrix} 10 & 9 & -10 \\ 9 & 10 & -9 \\ -10 & -9 & 10 \end{pmatrix}$$

$$S = \frac{1}{n-1} SSCP = \frac{1}{3} \begin{pmatrix} 10 & 9 & -10 \\ 9 & 10 & -9 \\ -10 & -9 & 10 \end{pmatrix} = \begin{pmatrix} 3.33 & 3.00 & -3.33 \\ 3.00 & 3.33 & -3.00 \\ -3.33 & -3.00 & 3.33 \end{pmatrix}$$

**Apartado 2: Autovalores y Autovectores (Aproximados)**

(En práctica real usarías `eigen()` en R. Aquí presentamos el concepto.)

Resolviendo $\det(S - \lambda I) = 0$:
$$\lambda_1 \approx 9.0, \quad \lambda_2 \approx 1.0, \quad \lambda_3 \approx 0.0$$

Autovectores ortonormalizados:
$$v_1 \approx \begin{pmatrix} 0.577 \\ 0.577 \\ -0.577 \end{pmatrix}, \quad v_2 \approx \begin{pmatrix} 0.707 \\ -0.707 \\ 0 \end{pmatrix}, \quad v_3 \approx \begin{pmatrix} 0.408 \\ 0.408 \\ 0.816 \end{pmatrix}$$

**Apartado 3: Pesos, Puntuaciones y Cargas**

**Pesos (Matriz $V$):**
$$V = (v_1 | v_2 | v_3) = \begin{pmatrix} 0.577 & 0.707 & 0.408 \\ 0.577 & -0.707 & 0.408 \\ -0.577 & 0 & 0.816 \end{pmatrix}$$

**Puntuaciones (Matriz $Y = X_c V$):**
$$Y \approx \begin{pmatrix} 2.31 & 0.71 \\ 1.55 & 1.41 \\ -1.55 & -0.71 \\ -2.31 & -1.41 \end{pmatrix} \quad \text{(primeras 2 columnas)}$$

**Cargas (Matriz $L = V \sqrt{\Lambda}$):**
$$\sqrt{\lambda_1} = 3.00, \quad \sqrt{\lambda_2} = 1.00$$

$$L = \begin{pmatrix} 0.577 \times 3.00 & 0.707 \times 1.00 \\ 0.577 \times 3.00 & -0.707 \times 1.00 \\ -0.577 \times 3.00 & 0 \times 1.00 \end{pmatrix} = \begin{pmatrix} 1.73 & 0.71 \\ 1.73 & -0.71 \\ -1.73 & 0 \end{pmatrix}$$

**Apartado 4: Varianza Explicada**

Varianza total: $\text{tr}(S) = 3.33 + 3.33 + 3.33 = 10$

- PC1 explica: $\lambda_1 / 10 = 9.0 / 10 = 90\%$
- PC2 explica: $\lambda_2 / 10 = 1.0 / 10 = 10\%$

**Conclusión:** Las primeras dos componentes explican el **100%** de la varianza (porque $\lambda_3 \approx 0$). En realidad, los datos viven en 2 dimensiones, no en 3.

---

## CÓDIGO R PARA VERIFICACIÓN

```r
# Ejercicio 3: Cálculo Manual de ACP
Xc <- matrix(c(2,1,-2, 1,2,-1, -1,-1,1, -2,-2,2), nrow=4, byrow=TRUE)
colnames(Xc) <- c("Mat", "Fis", "Lit")

# Matriz de covarianzas
S <- cov(Xc)
print("Matriz de covarianzas S:"); print(S)

# Descomposición espectral
eig <- eigen(S)
lambda <- eig$values
V <- eig$vectors

print("Autovalores:"); print(lambda)
print("Autovectores:"); print(V)

# Puntuaciones
Y <- Xc %*% V
print("Puntuaciones (scores):"); print(Y)

# Cargas
L <- sweep(V, MARGIN=2, STATS=sqrt(lambda), FUN="*")
print("Cargas (loadings):"); print(L)

# Varianza explicada
var_exp <- lambda / sum(lambda)
print("Varianza explicada:"); print(var_exp)
print("Varianza acumulada:"); print(cumsum(var_exp))
```
