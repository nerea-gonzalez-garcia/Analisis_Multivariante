<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

# Herramientas matem´aticas para el An´alisis Multivariante 

## Ejercicio 1: Centrado de una nube de puntos 

**==> picture [231 x 77] intentionally omitted <==**

1. Calcula el **vector de medias** . 

2. Construye la **matriz centrada** . 3. Comprueba que **1** _[t] n[X]_[˜][=] **[ 0]** _[t]_[.] 4. Interpreta geom´etricamente el centrado. 

## Soluci´on 

## **Vector de medias** : 

**==> picture [277 x 83] intentionally omitted <==**

## **Matriz centrada** : 

**==> picture [272 x 78] intentionally omitted <==**

**Comprobaci´on: 1** _[t] n[X]_[˜][=] **[ 0]** _[t]_[.] 

## Interpretaci´on geom´etrica del centrado 

**==> picture [336 x 164] intentionally omitted <==**

**----- Start of picture text -----**<br>
x 2 x 2<br>Original Centrado<br>X ¯<br>x 1 x 1<br>(0 ,  0)<br>−X ¯<br>**----- End of picture text -----**<br>


Centrar = trasladar la nube de puntos para que su media quede en el origen. 

## Ejercicio 2: Dobles productos y covarianzas 

**==> picture [157 x 54] intentionally omitted <==**

1. Calcula el vector de medias. 

2. Calcula la matriz centrada. 

3. Calcula la matriz de dobles productos centrada. 

4. Verifica la identidad del tema: 

**==> picture [91 x 11] intentionally omitted <==**

5. Calcula la matriz de covarianzas. 

6. Cambio de escala: define _Y_ 2 = 10 _X_ 2. Explica qu´e ocurre con _C_ y con _S_ . 

## Soluci´on 

**Medias** (con **1** 4 = (1 _,_ 1 _,_ 1 _,_ 1) _[t]_ ): 

**Centrado** : 

**==> picture [215 x 160] intentionally omitted <==**

## Soluci´on 

**Dobles productos centrados** : 

**==> picture [114 x 28] intentionally omitted <==**

**Verificaci´on** _C_ = _X[t] X − nX_[¯] _X_[¯] _[t]_ : 

**==> picture [310 x 97] intentionally omitted <==**

Soluci´on 

## **Covarianzas** 

**==> picture [207 x 28] intentionally omitted <==**

**Cambio de escala:** _Y_ 2 = 10 _X_ 2 _⇒ y_ ˜ _i_ 2 = 10˜ _xi_ 2. Como 

**==> picture [230 x 16] intentionally omitted <==**

entonces: 

**==> picture [384 x 103] intentionally omitted <==**

Ejercicio 3: Descomposici´on en valores singulares (SVD) peque˜na Considera la matriz rectangular (3 _×_ 2): 

**==> picture [73 x 41] intentionally omitted <==**

Usando las definiciones del tema: 

**==> picture [321 x 38] intentionally omitted <==**

1. Calcula _X[t] X_ . 

2. Halla sus valores propios _λ_ 1 _, λ_ 2 y los valores singulares _α_ 1 _, α_ 2. 

3. Obt´en _V_ a partir de los vectores propios normalizados de _X[t] X_ . 

**==> picture [283 x 25] intentionally omitted <==**

5. Verifica que _U_ Λ _V[t]_ = _X_ . 

## Soluci´on 

**==> picture [200 x 40] intentionally omitted <==**

Por tanto, los valores propios son: 

**==> picture [90 x 11] intentionally omitted <==**

y los valores singulares (del tema: _αi_ = _[√] λi_ ) son: 

La matriz Λ queda: 

**==> picture [112 x 66] intentionally omitted <==**

## Soluci´on 

Como _X[t] X_ = diag(3 _,_ 6), sus vectores propios normalizados son los can´onicos. Ordenando para que _λ_ 1 = 6 vaya primero: 

**==> picture [366 x 103] intentionally omitted <==**

As´ı, la _U_ reducida (3 _×_ 2) es: 

**==> picture [94 x 50] intentionally omitted <==**

**Verificaci´on:** _U_ Λ _V[t]_ = _X_ (al multiplicar, se recuperan las dos columnas de _X_ ). 

