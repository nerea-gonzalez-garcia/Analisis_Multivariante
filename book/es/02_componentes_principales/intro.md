# Capítulo 2. Análisis de Componentes Principales

## 2.1 Introducción y motivación

En la era del *Big Data*, no es infrecuente encontrarse con tablas de datos compuestas por decenas, cientos o miles de variables ($p$) medidas sobre miles de observaciones ($n$). Cuando el número de variables crece, nos enfrentamos a la conocida **"maldición de la dimensionalidad"**: los datos se vuelven dispersos, los algoritmos de modelado se inestabilizan, y la visualización gráfica de los datos en su conjunto resulta matemáticamente imposible en el espacio de $\mathbb{R}^p$.

Sin embargo, afortunadamente en la naturaleza y en las ciencias sociales, las variables rara vez operan de manera totalmente independiente. Por ejemplo, en datos antropométricos, el peso, la altura y la envergadura están fuertemente correlacionados. Esta **correlación implica redundancia**. Si varias variables se mueven de forma coordinada, la dimensionalidad "real" o intrínseca del problema es mucho menor que el número nominal de variables.

El **Análisis de Componentes Principales (ACP)** —desarrollado inicialmente por Karl Pearson (1901) y formalizado posteriormente por Harold Hotelling (1933)— es el procedimiento estadístico rey para la reducción de dimensión. Su filosofía subyacente es elegante: buscar un nuevo sistema de coordenadas ortogonales (una rotación del espacio) donde los nuevos ejes se alineen de forma natural con las direcciones de máxima varianza de los datos.

## 2.2 Desarrollo teórico: Construcción matemática del ACP

Para comprender la magia del ACP, no basta con aplicar la técnica como una "caja negra". Es imprescindible entender cómo el objetivo geométrico de buscar la "máxima variabilidad" se traduce sistemáticamente en un problema clásico de optimización algebraica.

### Formulación del problema de optimización

Dada una matriz de datos centrada $X_c$ de dimensión $n \times p$ con variables originales $X_1, X_2, \dots, X_p$. Queremos crear una **primera componente principal**, que denotaremos como $Y_1$. Para que sea linealmente interpretable, $Y_1$ se construye como una combinación lineal estricta de las variables originales:

$$
Y_1 = v_{11}X_1 + v_{21}X_2 + \dots + v_{p1}X_p = X_c v_1
$$

donde $v_1 = (v_{11}, v_{21}, \dots, v_{p1})^T$ es un vector columna de ponderaciones o "pesos".

**El objetivo central:** Queremos que esta nueva variable sintética $Y_1$ resuma la mayor cantidad posible de información empírica. En estadística, interpretamos "información" como "variabilidad" o dispersión. Si todos los individuos tuvieran el mismo valor en $Y_1$ (varianza cero), la componente no serviría para discriminar o estudiar el comportamiento de la muestra. Por lo tanto, deseamos **maximizar la varianza muestral de $Y_1$**.

¿Cuál es la varianza de nuestra nueva componente $Y_1$? Aprovechando las propiedades de la varianza para combinaciones lineales:

$$
Var(Y_1) = Var(X_c v_1) = v_1^T \text{Cov}(X_c) v_1 = v_1^T S v_1
$$

Donde $S$ es la matriz de covarianzas muestral $p \times p$. El problema de optimización queda planteado de la siguiente manera: encontrar el vector de pesos $v_1$ que maximice la forma cuadrática $v_1^T S v_1$.

### La restricción de norma unidad y Multiplicadores de Lagrange

A simple vista, el problema de maximizar $v_1^T S v_1$ no tiene solución finita. Si encontramos un vector $v_1$ que da una varianza de 10, podemos simplemente multiplicar todos los elementos de $v_1$ por 2, y la nueva varianza se multiplicará por 4 (será 40). Podríamos aumentar artificialmente la varianza hacia infinito tan solo escalando los pesos, lo cual es inútil estadísticamente.

Para resolver este inconveniente, debemos imponer una restricción matemática artificial que fije la "escala" del vector de pesos sin cambiar su dirección. La elección canónica es requerir que $v_1$ tenga longitud o norma unitaria euclidiana:

$$ ||v_1||^2 = v_1^T v_1 = 1 $$

Ahora tenemos un problema de optimización restringida:
> **Maximizar:** $f(v_1) = v_1^T S v_1$
> **Sujeto a:** $g(v_1) = v_1^T v_1 - 1 = 0$

El enfoque estándar en cálculo multivariante es emplear el método de los **multiplicadores de Lagrange**. Construimos el Lagrangiano:

$$ L(v_1, \lambda) = v_1^T S v_1 - \lambda (v_1^T v_1 - 1) $$

Para encontrar el óptimo, derivamos el Lagrangiano con respecto al vector $v_1$ y lo igualamos a cero:

$$ \frac{\partial L}{\partial v_1} = 2 S v_1 - 2 \lambda v_1 = 0 $$

Dividiendo entre 2 y reordenando términos, llegamos a una expresión monumental:

$$ S v_1 = \lambda v_1 $$

```{admonition} Comentario Docente
:class: important
¡Fíjate en lo que acaba de suceder! Empezamos con un problema estadístico/geométrico de maximización de varianza, y el álgebra nos ha devuelto, por definición estricta, la ecuación característica del problema de valores y vectores propios. La dirección de máxima varianza no es otra que un vector propio de la matriz de covarianzas.
```

¿Y cuál es la varianza obtenida? Si multiplicamos por la izquierda la ecuación $S v_1 = \lambda v_1$ por $v_1^T$:

$$ v_1^T S v_1 = v_1^T (\lambda v_1) = \lambda (v_1^T v_1) = \lambda (1) = \lambda $$

El álgebra revela que **la varianza máxima posible es exactamente igual al valor propio $\lambda$ asociado**. Por tanto, para maximizar la varianza global, elegimos el autovector asociado al **mayor autovalor** de $S$, es decir, $\lambda_1$. Esto define la Primera Componente Principal.

El proceso continúa. Para la **Segunda Componente Principal** $Y_2 = X_c v_2$, maximizamos $v_2^T S v_2$ con la restricción de que $v_2^T v_2 = 1$ y, además, con la restricción fundamental de que esta nueva componente debe incorporar información *nueva y no redundante* respecto a la primera, lo cual se impone requiriendo que $v_1$ y $v_2$ sean ortogonales ($v_1^T v_2 = 0$). El desarrollo con un segundo multiplicador de Lagrange nos lleva a que $v_2$ debe ser el autovector asociado al segundo mayor autovalor, $\lambda_2$. Y así sucesivamente.

### Obtención mediante SVD y relación con el espectro

Como establecimos en el Capítulo 1, calcular la descomposición espectral de la matriz de covarianzas $S = V \Lambda V^T$ proporciona directamente los pesos en $V$ y las varianzas en $\Lambda$.

Sin embargo, desde el punto de vista numérico y computacional (para evitar inestabilidades numéricas al formar explícitamente $X_c^T X_c$), es altamente recomendable realizar el ACP utilizando la Descomposición en Valores Singulares (SVD) de la matriz de datos original centrada $X_c = U D V^T$.
Como vimos:
* La matriz $V$ (vectores singulares derechos) contiene los **pesos** o coeficientes de las componentes principales.
* Las coordenadas de las proyecciones (los scores) se pueden obtener directamente como $Y = U D$. (Demostración: $Y = X_c V = (U D V^T) V = U D (V^T V) = U D$).

### Interpretación geométrica de las proyecciones

Geométricamente, el ACP es una **rotación rígida** del sistema de coordenadas original en $\mathbb{R}^p$. El elipsoide n-dimensional que envuelve a nuestra nube de puntos tiene ciertos ejes de simetría. El ACP simplemente localiza el eje más largo de la nube y lo convierte en el nuevo Eje X (Componente 1). Luego busca el segundo eje más largo, perpendicular al primero, y lo convierte en el nuevo Eje Y (Componente 2).

Proyectar un individuo sobre estos nuevos ejes (es decir, calcular sus coordenadas factoriales) nos dice su posición a lo largo de las principales direcciones de variación natural de la muestra.

## 2.3 Diferenciación de matrices fundamentales

El mayor obstáculo didáctico en el ACP suele ser la confusión terminológica que rodea a las salidas del software estadístico (como R o SPSS). Es matemáticamente innegociable diferenciar con absoluta precisión los tres elementos siguientes:

### 1. Pesos o Vectores Propios (Weights / Eigenvectors)
Representados por la matriz ortogonal $V$ de dimensión $p \times p$. 
* **Naturaleza matemática:** Son los coeficientes del modelo de combinación lineal.
* **Fórmula base:** $Y = X_c V$
* **Interpretación:** $v_{j1}$ indica la ponderación escalar con la que la variable original $X_j$ participa en la construcción sintética de la componente $Y_1$. No deben confundirse jamás con correlaciones, porque sus valores están forzados artificialmente para que la norma del vector sume 1 ($\sum_{j=1}^p v_{j1}^2 = 1$). Su valor numérico crudo es menos intuitivo de interpretar directamente.

### 2. Puntuaciones Factoriales (Scores)
Representadas por la matriz $Y$ de dimensión $n \times p$.
* **Naturaleza matemática:** Son las nuevas variables sintéticas, las coordenadas de los individuos tras la rotación.
* **Fórmula base:** $Y = X_c V$
* **Interpretación:** Si un investigador desea usar el ACP como pre-procesamiento para introducir los datos reducidos en un modelo de regresión posterior o cluster, los datos que debe utilizar son los *scores* correspondientes a las primeras $q$ columnas de $Y$. Estos scores tienen media 0 y su varianza es igual al respectivo valor propio $\lambda_k$.

### 3. Cargas Factoriales (Loadings)
Representadas habitualmente por la matriz $L$ de dimensión $p \times p$.
* **Naturaleza matemática:** Son las covarianzas (o correlaciones si se parte de matriz $R$) entre las variables originales y las componentes principales generadas.
* **Fórmula base:** $L = V \Lambda^{1/2}$
* **Interpretación:** Es el elemento clave para **dar nombre o significado semántico** a las componentes latentes. Si la carga $l_{j1}$ es alta y positiva, sabemos que la variable $X_j$ está fuertemente correlacionada con la componente 1. A diferencia de los *weights* limitados a sumar 1 en cuadrados, las cargas reflejan métricas estándar estadísticas de asociación.

## 2.4 Contribuciones y calidad de representación (cos²)

Más allá de analizar el impacto general, al representar datos en un espacio subóptimo bidimensional (ej. el plano de las componentes 1 y 2), es indispensable conocer la fidelidad geométrica de lo que estamos observando para no extraer conclusiones falaces.

### Calidad de representación de individuos ($\cos^2$)

Supongamos que un individuo (punto en el espacio original) se proyecta sobre la componente principal $k$. El $\cos^2$ se define geométricamente como el coseno al cuadrado del ángulo que forma el vector de posición original del individuo con el eje de la componente $k$.
* **Interpretación:** Un $\cos^2$ cercano a 1 implica un ángulo cercano a 0, lo que significa que el vector original es prácticamente paralelo a la componente: la proyección sobre ese plano refleja casi a la perfección el perfil original del individuo. 
* Si un punto tiene un $\cos^2$ sumamente bajo (ej. 0.05) en el primer plano factorial, significa que ese individuo es "ortogonal" a ese plano (está suspendido por encima o por debajo del plano). Concluir similitudes basadas en su posición aparente en el gráfico 2D sería un espejismo proyectivo.

### Contribución a la inercia (Varianza explicada por elementos)

* **Contribución de variables a la componente:** De toda la varianza que explica la componente $k$ ($\lambda_k$), ¿qué fracción proviene de la variable $j$? Se calcula tomando la carga al cuadrado y dividiendo por $\lambda_k$. Esto permite ranquear objetivamente a las variables por su "responsabilidad" en la creación del eje geométrico.
* **Contribución de individuos a la componente:** Existen individuos atípicos (outliers) tan extremos que obligan al algoritmo de maximización de varianza a orientar la primera componente principal directamente hacia ellos. Evaluar la contribución individual previene inferencias sesgadas, advirtiendo si la variabilidad general de la muestra está siendo secuestrada por un único caso anómalo.

## 2.5 Propiedades matemáticas del ACP

El ACP goza de elegantes y rígidas propiedades teóricas derivadas del álgebra espectral, demostrables rigurosamente:

1. **Incorrelación de componentes:** La matriz de covarianzas empírica de las puntuaciones $Y$ es diagonal. $\text{Cov}(Y) = \text{Cov}(X_c V) = V^T \text{Cov}(X_c) V = V^T S V = V^T (V \Lambda V^T) V = I \Lambda I = \Lambda$. La falta de elementos fuera de la diagonal confirma matemáticamente que las nuevas variables son $100\%$ ortogonales (incorrelacionadas).
2. **Conservación de la varianza total (Traza):** En álgebra matricial, la traza (suma de la diagonal) es invariante ante rotaciones cíclicas. La varianza total original es $\text{tr}(S)$. Sabiendo que $S = V \Lambda V^T$, se cumple $\text{tr}(S) = \text{tr}(V \Lambda V^T) = \text{tr}(\Lambda V^T V) = \text{tr}(\Lambda I) = \sum_{k=1}^p \lambda_k$. Esta propiedad certifica que la rotación ortogonal del ACP no crea ni destruye información, tan solo la re-empaqueta en los primeros ejes.
3. **Reconstrucción de la matriz:** Si utilizamos los $p$ componentes completos, podemos recuperar matemáticamente la matriz original sin pérdida: $X_c = Y V^T$. 
4. **Aproximación óptima de rango reducido (Teorema de Eckart-Young):** Esta es la verdadera justificación del ACP como herramienta de reducción de ruido. Si en la reconstrucción utilizamos únicamente los primeros $q$ componentes principales ($q < p$), obtenemos una matriz reconstruida $\tilde{X}_c = Y_{(q)} V_{(q)}^T$. El teorema de Eckart-Young demuestra que de **todas** las posibles matrices de rango $q$ que existen en el universo matemático, la matriz $\tilde{X}_c$ construida con ACP es la que tiene la menor distancia posible (error cuadrático de reconstrucción) respecto a la matriz original $X_c$.

## 2.6 Dimensionalidad máxima del ACP

Un detalle teórico frecuentemente ignorado en textos básicos es que la obtención de $p$ componentes principales no siempre es posible estadísticamente. El espectro de componentes genuinas está gobernado por el concepto algebraico de **rango de una matriz**, $\text{rg}(X)$.

La matriz de covarianzas $S$ es de tamaño $p \times p$. Podríamos suponer que siempre arrojará $p$ autovalores estrictamente positivos. Esto es **falso**. El número máximo de dimensiones reales subyacentes es el rango de la matriz de datos original $X_c$ de dimensión $n \times p$.

El álgebra estipula que el rango de una matriz está acotado por su menor dimensión, por tanto:
$$ \text{rg}(X_c) \leq \min(n, p) $$
Sin embargo, al centrar la matriz (restar el vector de medias), introducimos una dependencia lineal obligatoria entre las filas (las columnas suman cero por definición). Esta restricción lineal "consume" una dimensión adicional, reduciendo el rango máximo:
$$ \text{rg}(X_c) \leq \min(n - 1, p) $$

**Implicaciones prácticas de alta dimensionalidad ($p > n$):**
Existen áreas como la genómica (microarrays) o la espectrometría donde es habitual tener una muestra de $n=50$ pacientes medidos sobre $p=10.000$ genes. En esta situación extrema:
* El rango máximo de la matriz de covarianzas es $\min(50 - 1, 10.000) = 49$.
* Aunque la matriz de covarianzas calculada será gigantesca ($10.000 \times 10.000$), el software computará **a lo sumo 49 valores propios estrictamente positivos** ($\lambda_1, \dots, \lambda_{49} > 0$).
* Los restantes 9.951 valores propios ($\lambda_{50}, \dots, \lambda_{10.000}$) serán matemáticamente iguales a cero (salvo artefactos de precisión en coma flotante computacional). Las componentes asociadas a esos valores nulos son "espejismos" hiperplanares que explican literalmente un 0% de la variabilidad, demostrando que el volumen de datos habitaba realmente en un subespacio ínfimo encajado dentro de $\mathbb{R}^{10.000}$.

## 2.6b Obtención sucesiva de componentes principales y restricción de ortogonalidad

Hemos visto que la Primera Componente Principal $Y_1$ se obtiene eligiendo el autovector asociado al mayor autovalor. La construcción del resto de componentes sigue un procedimiento jerárquico riguroso.

**Segunda Componente Principal ($Y_2$):**

Una vez extraída la dirección de máxima varianza $v_1$, deseamos encontrar la segunda dirección de máxima varianza. Sin embargo, no podemos elegir simplemente el autovector correspondiente a $\lambda_2$, porque sería **linealmente dependiente** de $v_1$, incorporaría información redundante y violaría el principio fundamental de que cada componente debe aportar información nueva.

Para evitar esta redundancia, imponemos la **restricción de ortogonalidad**:

$$v_1^T v_2 = 0$$

Geométricamente, esto significa que $v_2$ debe ser perpendicular a $v_1$. Algebraicamente, el método de los multiplicadores de Lagrange con esta restricción adicional conduce a que $v_2$ es el autovector correspondiente al segundo mayor autovalor, $\lambda_2$.

**Componentes Principales Sucesivas ($Y_3, Y_4, \dots$):**

El mismo razonamiento se aplica recursivamente. La $k$-ésima componente principal $Y_k = X_c v_k$ se obtiene maximizando $v_k^T S v_k$ bajo las restricciones:
1. $v_k^T v_k = 1$ (norma unitaria)
2. $v_k^T v_j = 0$ para todo $j < k$ (ortogonalidad respecto a las anteriores)

Esto hace que $v_k$ sea el autovector asociado al $k$-ésimo mayor autovalor $\lambda_k$.

**Resultado final:** Si ordenamos los autovalores como $\lambda_1 \geq \lambda_2 \geq \dots \geq \lambda_p \geq 0$ y sus autovectores correspondientes forman las columnas de $V$, entonces:
- La matriz de pesos es $V = (v_1 | v_2 | \cdots | v_p)$
- Las puntuaciones son $Y = X_c V$
- Las $p$ componentes son **mutuamente ortogonales** (incorrelacionadas) por construcción

---

## 2.6c Interpretación geométrica profunda: La nube de puntos y los ejes principales

Para entender verdaderamente el ACP, es imprescindible visualizar qué ocurre en el espacio geométrico $\mathbb{R}^p$.

**La nube de puntos como un elipsoide:**

Imagina que nuestro conjunto de $n$ individuos (puntos en $\mathbb{R}^p$) forma una nube. Si esta nube es "esférica", significa que la variabilidad es uniforme en todas las direcciones. Si es "alargada" (un cigarro) o "plana" (una tortilla), significa que existe variabilidad preferencial en ciertas direcciones.

Matemáticamente, la forma de esta nube está codificada en la matriz de covarianzas $S$ (o la matriz de correlaciones $R$). La descomposición espectral $S = V \Lambda V^T$ nos dice:
- Los vectores propios $v_1, v_2, \dots, v_p$ son los **ejes principales del elipsoide** (perpendiculares entre sí)
- Los valores propios $\lambda_1, \lambda_2, \dots, \lambda_p$ son los **"semilargos" de los ejes** (miden el "ancho" del elipsoide en cada dirección)

**La rotación de coordenadas:**

El ACP es un proceso de **rotación rígida** del espacio. Tomamos el sistema de coordenadas original (los ejes de las variables $X_1, X_2, \dots, X_p$) y lo rotamos de forma que:
1. El primer eje del nuevo sistema apunta exactamente en la dirección $v_1$ (dirección del eje más largo del elipsoide)
2. El segundo eje apunta en la dirección $v_2$ (perpendicular al primero, segunda dirección más alargada)
3. Y así sucesivamente

En este nuevo sistema, la matriz de covarianzas se convierte en la matriz diagonal $\Lambda$, sin elementos fuera de la diagonal. Esto significa que en el nuevo sistema, las variables (componentes) son **completamente independientes**.

---

## 2.6d ACP mediante descomposición espectral y SVD: Dos aproximaciones equivalentes

Existen dos formas computacionalmente equivalentes de realizar el ACP. Ambas dan el mismo resultado, pero tienen ventajas y desventajas distintas.

### Aproximación 1: Descomposición Espectral de $S$ o $R$

**Procedimiento:**
1. Centrar (y opcionalmente estandarizar) la matriz de datos
2. Calcular la matriz de covarianzas (o correlaciones): $S = \frac{1}{n-1} X_c^T X_c$
3. Calcular la descomposición espectral: $S = V \Lambda V^T$
4. Los pesos son las columnas de $V$
5. Las puntuaciones son $Y = X_c V$
6. Las cargas son $L = V \sqrt{\Lambda}$

**Ventajas:**
- Conceptualmente muy clara: se ve directamente la estructura de la matriz de covarianzas
- Los valores propios son directamente las varianzas de las componentes

**Desventajas:**
- Si $p$ es muy grande, formar explícitamente $X_c^T X_c$ puede causar inestabilidad numérica
- Computacionalmente más lento para matrices grandes

### Aproximación 2: Descomposición en Valores Singulares de $X_c$

**Procedimiento:**
1. Centrar (y opcionalmente estandarizar) la matriz de datos
2. Calcular la SVD de $X_c$: $X_c = U D V^T$
3. Los pesos son las columnas de $V$ (vectores singulares derechos)
4. Las puntuaciones son $Y = U D$ (o equivalentemente, $Y = X_c V$)
5. Las cargas son $L = V \sqrt{\frac{D^2}{n-1}}$

**Ventajas:**
- Numéricamente más estable: evita formar explícitamente $X_c^T X_c$
- Computacionalmente más eficiente para matrices grandes

**Desventajas:**
- La interpretación directa de $D$ requiere recordar que $\lambda_i = \frac{d_i^2}{n-1}$

**Relación entre ambas:** Como demostramos en el Capítulo 1, la matriz $V$ de la SVD de $X_c$ es exactamente la matriz $V$ de la descomposición espectral de $S$. Los valores propios se relacionan mediante $\lambda_i = \frac{d_i^2}{n-1}$.

---

## 2.6e ACP sobre Matriz de Covarianzas vs. ACP sobre Matriz de Correlaciones

Una decisión crítica en la práctica es si realizar el ACP sobre $S$ (matriz de covarianzas) o sobre $R$ (matriz de correlaciones). Esta elección tiene implicaciones profundas en los resultados.

### ACP sobre Matriz de Covarianzas ($S$)

**Cuándo usar:**
- Variables medidas en la misma unidad (ej. todas en metros, o todas en euros)
- Queremos que el ACP privilegie las variables con mayor varianza original

**Efecto:**
- Las variables con varianzas grandes "tiran" del análisis hacia ellas
- Una variable con desviación estándar de 1000 tendrá mucho más peso que una con desviación estándar de 0.1
- Las primeras componentes estarán dominadas por las variables que naturalmente tienen más dispersión

**Ejemplo:** Si analizamos antropometría combinando "peso en kg", "altura en cm" y "edad en años", el peso (varianza ~2000) y la altura (varianza ~400) dominarán completamente, mientras que la edad (varianza ~500) será marginada, aunque todas sean estadísticamente relevantes.

### ACP sobre Matriz de Correlaciones ($R$)

**Cuándo usar:**
- Variables medidas en unidades distintas (ej. euros, metros, horas)
- Queremos que el ACP trate a todas las variables con igual importancia estadística

**Efecto:**
- Al estandarizar ($s_j = 1$ para todo $j$), todos los pesos se equilibran
- Las primeras componentes reflejan patrones de asociación entre variables, no simplemente patrones de varianza "cruda"

**Ejemplo:** Si queremos comparar precios de viviendas, superficie, antigüedad y distancia a centro, estandarizar primero (con $R$) evita que el precio (rango 200.000-800.000) domine sobre la antigüedad (rango 0-100 años).

**Nota teórica:** Trabajar con $R$ es equivalente a estandarizar las variables originales (restar media, dividir por desviación estándar) y luego realizar ACP sobre la matriz de covarianzas de los datos estandarizados.

---

## 2.7 Resumen de conceptos clave

| Concepto | Definición | Fórmula | Rango |
|----------|-----------|---------|-------|
| **Pesos (Loadings en algunos textos)** | Coeficientes que definen las combinaciones lineales | $V$ (ortogonal) | Restringidos: $\sum v_{ji}^2 = 1$ |
| **Puntuaciones (Scores)** | Coordenadas de los individuos en el nuevo espacio | $Y = X_c V$ | Media 0, varianza $= \lambda_i$ |
| **Cargas (Loadings)** | Correlaciones entre variables originales y componentes | $L = V \sqrt{\Lambda}$ | Sin restricción de norma |
| **Valor propio $\lambda_i$** | Varianza de la $i$-ésima componente | Diagonal de $\Lambda$ | $\lambda_1 \geq \cdots \geq \lambda_p \geq 0$ |
| **Valor singular $d_i$** | Relaciona con valor propio | $\lambda_i = d_i^2 / (n-1)$ | $d_i \geq 0$ |
| **Rango máximo** | Dimensiones no redundantes | $\min(n-1, p)$ | Fijo para una muestra dada |

---

## 2.8 Material Complementario

En las siguientes secciones se abordará la resolución práctica de la técnica:
* Se presentará el proceso computacional empleando el lenguaje estadístico R, con ejemplos de cálculo manual paso a paso
* Desarrollaremos el caso clásico de notas de alumnos de Educación Secundaria (Ciencias vs. Letras), ilustrando cómo el ACP descubre automáticamente estas dimensiones latentes
* Se mostrarán visualizaciones del círculo de correlaciones (variables) y los gráficos de individuos (scores)
* Se hará mención de la proyección biplot, que constituye la visualización simultánea de *scores* (individuos) y *loadings* (variables) sobre el mismo espacio plano, técnica que se analizará rigurosamente en capítulos venideros
