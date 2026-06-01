<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

## **ANÁLISIS DE COMPONENTES PRINCIPALES (ACP)** 

**OBJETIVO Comprobar la utilidad de las técnicas multivariantes exploratorias de reducción de la dimensión (ACP) para visualizar y descubrir fenómenos latentes en una matriz de datos** 

## **CASO 1 ASIGNATURAS (Ejemplo inicial de teoría)** 

**1.** Importe el archivo de datos de extensión xlsx. 

**==> picture [228 x 105] intentionally omitted <==**

**==> picture [319 x 204] intentionally omitted <==**

Comprobemos que la importación se ha realizado correctamente: 

class(Ejemplo_Ciencias_Letras); dim(Ejemplo_Ciencias_Letras) 

head(Ejemplo_Ciencias_Letras) 

datos<-as.data.frame(Ejemplo_Ciencias_Letras) 

1 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

Almacenaremos los datos en un objeto de tipo matriz, que contenga las variables cuantitativas a analizar, 

row.names(datos)<-datos[,1] 

datos<-datos[,-1] head(datos) 

Datos.ord<-datos[,c(1,5,7,4,2,3,6)] 

**2.** Calcule la matriz de correlaciones R y represéntela gráficamente. 

library(corrplot) 

corrplot(cor(Datos.ord), tl.col="black", tl.srt=45, tl.cex=1) 

**==> picture [295 x 186] intentionally omitted <==**

**3.** Centre la matriz de datos y almacene la nueva matriz en un objeto denominado _datos.center_ 

Primera opción: 

n<-dim(Datos.ord)[1] 

I<-diag(1, nrow=n) #Matriz identidad 

J<-matrix(1, nrow = n, ncol=n) #Matriz unidad 

dt.center2 <- (I-(1/n)*J)%*%as.matrix(Datos.ord) 

2 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

**==> picture [375 x 167] intentionally omitted <==**

colMeans(Datos.ord) #Vector de medias 

**==> picture [469 x 26] intentionally omitted <==**

Segunda opción: 

dt.center<-scale(Datos.ord, scale = F, center=T) 

**==> picture [494 x 163] intentionally omitted <==**

## **¡SON LA MISMA!** 

3 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

**4.** Calcule la Descomposición Espectral de la matriz de covarianzas de _datos.center_ y la Descomposición en Valores Singulares de los datos centrados _datos.center_ . ¿Qué relación observa entre los resultados? 

res.svd<-svd(dt.center) #Descomposición en valores singulares X=UDV[T] 

res.svd$d #Valores singulares 

res.svd$v #vectores singulares derecha V 

**==> picture [435 x 90] intentionally omitted <==**

------------------------------------------------------------------------------------------------------------------ 

cov(dt.center) #Matriz de covarianzas S=VΛV[T] 

res.eigen<-eigen(cov(dt.center)) #Descomposición espectral 

valpropiosL<-res.eigen$values #Valores propios 

vectpropiosV<-res.eigen$vectors #Vectores propios 

**==> picture [412 x 82] intentionally omitted <==**

**5.** Implemente el Análisis de Componentes Principales a partir de la descomposición espectral siguiendo la teoría. 

cargasV<-res.eigen$vectors #Loadings o cargas (V) row.names(cargasV)<-colnames(dt.center) 

colnames(cargasV)<-c("CP1","CP2","CP3","CP4","CP5","CP6","CP7") 

**==> picture [317 x 85] intentionally omitted <==**

4 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

puntY<-dt.center%*%cargasV #Scores o puntuaciones factoriales (Y=XV) 

row.names(puntY)<-row.names(dt.center) 

colnames(puntY)<-colnames(cargasV) 

**==> picture [285 x 174] intentionally omitted <==**

**6.** Implemente el Análisis de Componentes Principales a partir de la función _princomp_ . 

res.acp<-princomp(Datos.ord, cor=F) #Sobre la matriz de covarianzas 

- Obtenga los valores propios y el % de varianza explicada por cada componente. valores.propios<-res.acp$sdev^2 #Varianza explicada 

porc<-valores.propios/sum(valores.propios)*100 

porc.acum<-cumsum(porc) 

data.frame(valores.propios,porc, porc.acum) 

**==> picture [223 x 93] intentionally omitted <==**

plot(res.acp, type="lines", ylim=c(0,14), main = "Gráfico de sedimentación") 

**==> picture [182 x 149] intentionally omitted <==**

5 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

- ¿Cuántas componentes principales debemos retener? Ayúdese del scree-plot y del listado de valores propios. 

Autovalores mayores a 1:  3 

Porcentaje de varianza del 75%:  2 

Gráfico de sedimentación: 2 

Decisión del investigador: 2 

- Analice la estructura de la matriz de cargas para las componentes extraídas: 

cargas<-res.acp$loadings 

round(cargas[,1:7],3) 

**==> picture [219 x 121] intentionally omitted <==**

- Realice la representación gráfica de las puntuaciones de los estudiantes en el espacio de dimensión reducida, generado por tantas componentes principales como haya decidido retener. 

scores<-res.acp$scores round(res.acp$scores[,1:2],3) 

**==> picture [165 x 175] intentionally omitted <==**

6 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

plot(res.acp$scores[,1:2], pch=18, xlab="Comp.1 (Ciencias)", ylab="Comp.2 (Letras)") text(res.acp$scores[,1:2]+0.2, label=row.names(Datos.ord), cex=1.25) 

**==> picture [317 x 183] intentionally omitted <==**

7 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

## **CASO 2 PROPUESTO (Prevención del cáncer de cuello uterino)** 

**1.** Importe el archivo de datos de extensión xlsx. 

Importaremos los datos utilizando el menú “Import Dataset” del panel _Environment_ : 

**==> picture [234 x 106] intentionally omitted <==**

**==> picture [327 x 157] intentionally omitted <==**

Antes de comenzar con el análisis de los datos, comprobaremos que la importación se ha realizado correctamente: 

class(sobar_72); dim(sobar_72) colnames(sobar_72); head(sobar_72) sobar_72<-as.data.frame(sobar_72) 

Almacenaremos los datos en un objeto de tipo matriz, que contenga las variables cuantitativas a analizar, 

datos<-as.matrix(sobar_72 [,-20]) dim(datos); class(datos); head(datos) 

8 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

**2.** Calcule la matriz de correlaciones R y represéntela gráficamente. 

- La función _cor_ calcula la matriz de correlaciones de un conjunto de datos y la función corrplot 

de la librería corrplot representa gráficamente la misma. 

**==> picture [72 x 11] intentionally omitted <==**

**----- Start of picture text -----**<br>
R<-cor(datos)<br>**----- End of picture text -----**<br>


**==> picture [348 x 106] intentionally omitted <==**

library(corrplot) 

corrplot(R,  tl.col="black", tl.srt=45,   tl.cex = 0.8, type="upper") 

**==> picture [227 x 201] intentionally omitted <==**

Se observan dos grupos de variables altamente correlacionadas 

**3.** Centre y estandarice la matriz de datos y almacene la nueva matriz en un objeto denominado _datos.est_ . 

La matriz de datos centrada y estandarizada se obtiene mediante la función _scale_ : 

datos.est<-scale(datos, center=T, scale=T) 

**==> picture [527 x 57] intentionally omitted <==**

9 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

**4.** Calcule la Descomposición Espectral de la matriz de covarianzas de _datos.est_ y la Descomposición en Valores Singulares de los datos originales. ¿Qué relación observa entre los resultados? 

A continuación, obtenemos la descomposición espectral de la matriz de covarianzas: 

eigen(cov(datos.est)) 

**==> picture [291 x 173] intentionally omitted <==**

round(cor(datos.est)[,1:3],3) round(cov(datos.est)[,1:3],3) 

**5.** Implemente el Análisis de Componentes Principales a partir de la función _princomp_ en RStudio. Responda a las siguientes cuestiones: 

La función princomp permite obtener los resultados del Análisis de Componentes Principales de nuestro conjunto de datos: 

pca.res<-princomp(datos.est, cor=T) 

summary(pca.res) 

- Obtenga los valores propios y el % de varianza explicada por cada componente. 

Los valores propios obtenidos para cada componente principal son: 

valores.propios<-pca.res$sdev^2 

**==> picture [278 x 28] intentionally omitted <==**

Y a partir de ellos calculamos el porcentaje de varianza explicada por cada componente como: 

(valores.propios[1]/sum(valores.propios))*100 

(valores.propios[2]/sum(valores.propios))*100 

La primera componente principal explica el 28,71% de la variabilidad de los datos, y la segunda el 18.61%. 

10 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

- ¿Cuántas componentes principales debemos retener? Ayúdese del scree-plot y del listado de valores propios. 

Para obtener el gráfico de sedimentación o _scree plot_ es suficiente con: 

plot(pca.res, type="lines", ylim=c(0,6),main = "Gráfico de sedimentación") 

**==> picture [231 x 231] intentionally omitted <==**

Así: 

Autovalores mayores a 1: 5 Porcentaje de varianza del 75%: 6 Gráfico de sedimentación: 3 Decisión del investigador: 3 

- Analice la estructura de la matriz de cargas para las componentes extraídas: 

pca.res$loadings[,1:3] 

**==> picture [206 x 165] intentionally omitted <==**

11 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

Así, las primeras componentes principales vienen dadas por la combinación lineal de las variables originales estandarizadas: 

𝑌1 = 0,1 ∙𝑧𝑆𝑅 + 0.002 ∙𝑧𝐸𝑎𝑡 + 0.2 ∙𝑧𝑃𝐻𝑦𝑔 + ⋯+  0,381 ∙𝑧𝑎𝑏𝑖 + 0,352 ∙𝑧𝐷𝑒𝑠 

𝑌2 = 0,066 ∙𝑧𝑆𝑅 −0.017 ∙𝑧𝐸𝑎𝑡 + 0.179 ∙𝑧𝑃𝐻𝑦𝑔 + ⋯+  0,012 ∙𝑧𝑎𝑏𝑖 −0,07 ∙𝑧𝐷𝑒𝑠 𝑌3 = 0,25 ∙𝑧𝑆𝑅 −0.512 ∙𝑧𝐸𝑎𝑡 −0.278 ∙𝑧𝑃𝐻𝑦𝑔 + ⋯+  0,060 ∙𝑧𝑎𝑏𝑖 + 0,020 ∙𝑧𝐷𝑒𝑠 

- Realice la representación gráfica de las puntuaciones de los individuos en el espacio generado por las dos primeras componentes principales. 

Las puntuaciones de las observaciones en el espacio de componentes principales son: 

pca.res$scores[,1:3] 

**==> picture [142 x 208] intentionally omitted <==**

Para obtener el gráfico de puntuaciones en el espacio de las componentes: 

colors <- c(rep("#E69F00",21), rep("#999999",51)) 

plot(pca.res$scores[,1:2], pch=19, #col=as.factor(Arqueologia2$Type), 

main="Espacio de puntuaciones en las Componentes Principales",col=colors) text(pca.res$scores[,1:2]+0.1, label=cervix, cex=0.6 ) 

**==> picture [177 x 174] intentionally omitted <==**

12 

**ANÁLISIS DE COMPONENTES PRINCIPALES EN R** Análisis Multivariante – Grado en Estadística 

O incluso puede representarse en un espacio tridimensional: 

library(scatterplot3d) 

scatterplot3d(pca.res$scores[,1:3], pch=19, angle = 60, color=colors) 

**==> picture [257 x 236] intentionally omitted <==**

Preguntas propuestas: 

- 1- ¿Las componentes principales obtenidas son variables incorrelacionadas? 

- 2- ¿Qué relación hay ahora entre la matriz de covarianzas y de correlaciones? ¿Y entre los resultados del ACP y la descomposición espectral? 

13 

