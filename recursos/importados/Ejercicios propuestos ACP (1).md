<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

**==> picture [35 x 35] intentionally omitted <==**

## **DEPARTAMENTO DE ESTADÍSTICA** 

**==> picture [49 x 44] intentionally omitted <==**

**ANÁLISIS MULTIVARIANTE** – EJERCICIOS ACP PROPUESTOS 

## **EJERCICIO 1: Relación entre Descomposición en Valores y Vectores Propios, Descomposición en Valores Singulares y Análisis de Componentes Principales** 

Consideremos una matriz de datos X de dimensión 𝑛× 𝑝, centrada. 

1. ¿Cómo se relaciona la Descomposición en Valores y Vectores Propios de la matriz de covarianza 𝑋[𝑇] 𝑋 con la Descomposición en Valores Singulares (SVD) de X? 

2. ¿Qué representan los valores propios y vectores propios de la matriz de covarianza en términos del ACP? 

3. ¿Cómo se puede utilizar SVD directamente para calcular las puntuaciones de los individuos en componentes principales, sin necesidad de calcular la matriz de covarianzas y su descomposición espectral? 

## **EJERCICIO 2: Obtención de las componentes principales** 

Considere la siguiente matriz que recoge información de 3 individuos en dos variables 𝑥1, 𝑥2: 

**==> picture [83 x 37] intentionally omitted <==**

Reduzca la dimensión de la siguiente matriz a través del análisis de componentes principales. A partir de ahí: 1) Obtenga el porcentaje de varianza explicada por cada una de las dos componentes principales; 2) A partir de los resultados, construya la matriz de cargas V y escriba la ecuación de la primera componente principal 𝑦1; 3) Obtenga la matriz de puntuaciones de individuos en el espacio de las dos componentes principales. 

## **EJERCICIO 3: Obtención de las componentes principales** 

Considere la matriz de datos (filas = individuos, columnas = variables 𝑋1, 𝑋2, 𝑋3): 

**==> picture [83 x 23] intentionally omitted <==**

Reduzca la dimensión de la matriz anterior mediante Análisis de Componentes Principales (ACP) (trabajando con datos centrados). A partir de ahí: 1) Obtenga el porcentaje de varianza explicada por cada una de las dos primeras componentes principales; 2) Construya la matriz de pesos 𝑽 y escriba la ecuación de la primera componente principal 𝒚𝟏; 3) Obtén la matriz de puntuaciones (scores) de los individuos en el espacio de 1 componente principal. 

1 

**==> picture [35 x 35] intentionally omitted <==**

## **DEPARTAMENTO DE ESTADÍSTICA** 

**==> picture [49 x 44] intentionally omitted <==**

## **ANÁLISIS MULTIVARIANTE** – EJERCICIOS ACP PROPUESTOS 

## **EJERCICIO 4: Obtención de Componentes Principales** 

Considere la siguiente matriz de datos 𝑋, donde las filas representan individuos y las columnas variables cuantitativas: 

**==> picture [83 x 38] intentionally omitted <==**

Se pide reducir la dimensión de la matriz mediante Análisis de Componentes Principales. Trabaje con la matriz de datos centrada. 

1. Centre la matriz de datos y obtenga la matriz 𝑋𝑐. 

2. Calcule la matriz de covarianzas y realice su descomposición espectral para obtener los valores propios. 

3. Obtenga el porcentaje de varianza explicada por cada una de las dos primeras componentes principales. 

4. A partir de los resultados, construya la matriz de pesos 𝑉(matriz de autovectores normalizados) y escriba la ecuación de la primera componente principal 𝑦1. 

5. Obtenga la matriz de puntuaciones de los individuos en el espacio generado por las dos primeras componentes principales. 

## **EJERCICIO 5: Interpretación de Componentes Principales** 

Supongamos que en un análisis de componentes principales realizado sobre un conjunto de datos con 5 variables originales, se obtienen los siguientes autovalores: 

**==> picture [233 x 11] intentionally omitted <==**

¿Cuántos componentes principales recomendarías retener según la **regla de valores propios mayores que 1** ? 

1. ¿Qué porcentaje de la varianza total explican los dos primeros componentes? 

2. Si el tercer componente tuviera una fuerte carga en una variable que consideras importante, ¿lo retendrías en el análisis? Justifica tu respuesta. 

2 

**==> picture [35 x 35] intentionally omitted <==**

## **DEPARTAMENTO DE ESTADÍSTICA** 

**==> picture [49 x 44] intentionally omitted <==**

## **ANÁLISIS MULTIVARIANTE** – EJERCICIOS ACP PROPUESTOS 

## **EJERCICIO 6: Propiedad de centrado de las Componentes Principales** 

Un investigador analiza 5 variables que describen diferentes características de varias ciudades: 

- 𝑋1: densidad de población 

- 𝑋2: precio medio de la vivienda 

- 𝑋3: nivel de tráfico 

- 𝑋4: número de parques 

- 𝑋5: calidad del aire 

Tras realizar un Análisis de Componentes Principales, se obtienen las siguientes cargas de las variables: 

|Variable|CP1|CP2|
|---|---|---|
|Densidadpoblación|0.60|-0.05|
|Precio vivienda|0.58|-0.08|
|Tráfico|0.57|-0.10|
|Parques|-0.02|0.70|
|Calidad aire|-0.05|0.68|



Además, las dos primeras componentes explican 82% de la varianza total. 

1. ¿Qué tipo de características urbanas parece representar la primera componente principal? 

2. ¿Cómo interpretaría la segunda componente principal? 

3. ¿Tiene sentido reducir las 5 variables originales a dos componentes principales? Justifique. 

4. ¿Qué tipo de ciudades cree que tendrían valores altos en CP1? 

5. ¿Qué tipo de ciudades tendrían valores altos en CP2? 

## **EJERCICIO 7: Propiedad de centrado de las Componentes Principales** 

Sea 𝑋una matriz de datos de dimensión 𝑛× 𝑝cuyas columnas representan las variables 𝑋1, … , 𝑋𝑝. Supongamos que las variables están centradas. 

1. Demuestre que la media muestral de cada componente principal 𝑌𝑗es cero. 

2. Interprete este resultado geométricamente en términos de la nube de puntos de los individuos. 

3 

**==> picture [35 x 35] intentionally omitted <==**

## **DEPARTAMENTO DE ESTADÍSTICA** 

**==> picture [49 x 44] intentionally omitted <==**

**ANÁLISIS MULTIVARIANTE** – EJERCICIOS ACP PROPUESTOS 

## **EJERCICIO 8: Reflexión Final y Autoevaluación** 

1. ¿Cómo se relacionan ACP, SVD y Descomposición Espectral? Explica con tus propias palabras. 

2. ¿Qué fue lo más difícil de entender sobre ACP? 

3. Si tuvieras que explicarle ACP a un compañero de primer curso, ¿cómo lo harías en pocas frases? 

4. ¿Cuándo NO es recomendable utilizar ACP en el análisis de datos? 

5. ¿Cuándo es mejor usar la matriz de covarianza en ACP? y¿Cuándo es mejor usar la matriz de correlación y por qué? 

6. ¿Qué representan los valores propios en el ACP? ¿Y cómo se interpretan los vectores propios en el espacio de los datos? 

7. ¿Cómo identificar qué variables están más representadas en cada componente? ¿Qué significa una carga factorial alta en un componente? 

8. ¿Cómo se calculan las puntuaciones factoriales a partir de los datos originales y los autovectores?  ¿Qué significa que un punto esté más alejado en el gráfico de dispersión de los componentes? 

4 

