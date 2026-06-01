# Práctica guiada en R: ACP de notas de Ciencias y Letras

Esta práctica aplica el ACP al archivo `Ejemplo Ciencias Letras (1).xlsx` facilitado con el curso. El objetivo es reducir siete calificaciones a unas pocas componentes e interpretar qué perfiles académicos distinguen mejor al alumnado.

## 1. Datos del ejemplo

La Tabla 1 recoge las 15 observaciones del archivo original.

**Tabla 1. Calificaciones del ejemplo de Ciencias y Letras.**

| Alumno | Lengua | Matemáticas | Física | Filosofía | Historia | Química | Educación física |
|---|---:|---:|---:|---:|---:|---:|---:|
| Ana | 5 | 5 | 5 | 5 | 5 | 5 | 5 |
| Juan | 7 | 4 | 3 | 4 | 7 | 3 | 8 |
| Manuel | 5 | 8 | 7 | 5 | 6 | 7 | 5 |
| Sara | 7 | 2 | 4 | 7 | 7 | 3 | 6 |
| Paloma | 8 | 9 | 10 | 8 | 7 | 9 | 4 |
| Víctor | 4 | 9 | 8 | 3 | 4 | 7 | 5 |
| Jorge | 6 | 4 | 4 | 5 | 5 | 3 | 7 |
| Susana | 4 | 7 | 8 | 3 | 2 | 8 | 3 |
| María | 5 | 5 | 4 | 6 | 5 | 5 | 1 |
| Javier | 7 | 4 | 5 | 8 | 8 | 4 | 6 |
| Mónica | 7 | 8 | 8 | 7 | 6 | 7 | 9 |
| Lucía | 4 | 3 | 3 | 3 | 2 | 1 | 4 |
| Pablo | 7 | 4 | 4 | 8 | 7 | 4 | 5 |
| Tomás | 3 | 5 | 5 | 3 | 3 | 5 | 7 |
| Pilar | 5 | 6 | 6 | 5 | 5 | 6 | 6 |

La tabla permite observar el punto de partida antes de proyectar los datos: hay asignaturas con escalas comparables, pero perfiles individuales distintos.

```r
notas <- data.frame(
  Lengua = c(5,7,5,7,8,4,6,4,5,7,7,4,7,3,5),
  Matematicas = c(5,4,8,2,9,9,4,7,5,4,8,3,4,5,6),
  Fisica = c(5,3,7,4,10,8,4,8,4,5,8,3,4,5,6),
  Filosofia = c(5,4,5,7,8,3,5,3,6,8,7,3,8,3,5),
  Historia = c(5,7,6,7,7,4,5,2,5,8,6,2,7,3,5),
  Quimica = c(5,3,7,3,9,7,3,8,5,4,7,1,4,5,6),
  Educacion_fisica = c(5,8,5,6,4,5,7,3,1,6,9,4,5,7,6)
)
rownames(notas) <- c(
  "Ana","Juan","Manuel","Sara","Paloma","Victor","Jorge","Susana",
  "Maria","Javier","Monica","Lucia","Pablo","Tomas","Pilar"
)
```

## 2. Explorar y estandarizar

Antes del ACP se revisan medias, desviaciones típicas y correlaciones. Usaremos la matriz de correlaciones porque todas las variables son notas, pero su dispersión no tiene por qué ser idéntica.

```r
round(colMeans(notas), 2)
round(apply(notas, 2, sd), 2)
R <- cor(notas)
round(R, 2)
```

## 3. Obtener las componentes

`prcomp()` centra y estandariza los datos y calcula el ACP mediante SVD.

```r
acp <- prcomp(notas, center = TRUE, scale. = TRUE)
summary(acp)

pesos <- acp$rotation
puntuaciones <- acp$x
varianza <- acp$sdev^2 / sum(acp$sdev^2)

round(pesos[, 1:3], 3)
round(puntuaciones[, 1:3], 3)
round(cbind(varianza, acumulada = cumsum(varianza)), 3)
```

```{admonition} Pregunta de interpretación
:class: tip
Examina los signos y tamaños de los pesos de la primera componente. ¿Qué asignaturas se mueven juntas? Después localiza qué alumnos tienen puntuaciones extremas y vuelve a la Tabla 1 para describir sus perfiles.
```

## 4. Comprobar la relación con la SVD

La práctica conecta con el capítulo anterior: los valores propios de la matriz de correlaciones se obtienen elevando al cuadrado los valores singulares de la matriz estandarizada y dividiendo por $n-1$.

```r
Z <- scale(notas)
descomposicion <- svd(Z)
lambda_svd <- descomposicion$d^2 / (nrow(Z) - 1)
lambda_cor <- eigen(cor(notas))$values

round(cbind(lambda_cor, lambda_svd), 6)
```

## 5. Representaciones gráficas

El gráfico de individuos permite comparar perfiles de estudiantes. El biplot añade las variables para facilitar la interpretación.

```r
plot(
  puntuaciones[, 1], puntuaciones[, 2],
  xlab = "CP1", ylab = "CP2",
  main = "Plano principal de estudiantes"
)
text(puntuaciones[, 1], puntuaciones[, 2], labels = rownames(notas), pos = 3)

biplot(acp, scale = 0, main = "Biplot: estudiantes y asignaturas")
```

## 6. Actividades

1. Calcula cuántas componentes hacen falta para superar el 80 % de varianza explicada.
2. Interpreta las dos primeras componentes a partir de los pesos.
3. Identifica dos estudiantes con perfiles semejantes y dos con perfiles distintos.
4. Repite el ACP sin `scale. = TRUE` y compara los resultados.
5. Explica por qué el signo de una componente puede invertirse sin cambiar su interpretación estadística.
