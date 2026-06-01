<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

## Herramientas matemáticas el Análisis Multivariante con R para 

## Ana Belén Nieto Librero 

#Vectores 

Para generar un vector: 

```
x<-c(2,3,4)
y<-3:5
z<-seq(from=1,to=6,by=2)
q<-rep(1,3)
x
```

```
##[1]234
```

```
y
```

```
##[1]345
```

```
z
```

```
##[1]135
```

```
q
```

```
##[1]111
```

#Acceso a los elementos de un vector 

```
x[1]
```

```
##[1]2
```

```
x[1:2]
```

```
##[1]23
```

```
x[-1]
```

```
##[1]34
```

#Operaciones con vectores 

1 

```
#Suma
x+y
```

```
##[1]579
```

```
#Diferencia
x-y
```

```
##[1]-1-1-1
```

```
#Multiplicación
x*y
```

```
##[1]61220
```

```
#División
x/y
```

```
##[1]0.66666670.75000000.8000000
```

```
#Restodeunadivisión
x%/%y
```

```
##[1]000
```

```
#Vectortraspuesto
t(x)
```

```
##[,1][,2][,3]
##[1,]234
```

```
#Productointernooescalar
x%*%y
```

```
##[,1]
##[1,]38
```

```
t(x)%*%y
```

```
##[,1]
##[1,]38
```

```
t(y)%*%x
```

```
##[,1]
##[1,]38
```

2 

```
#Longituddeunvector
length(x)
```

```
##[1]3
```

```
#Multiplicacióndeunescalarporunvector
2*x
```

```
##[1]468
```

##Suma de elementos de un vector mediante producto escalar 

```
t(x)%*%rep(1,length(x))
```

```
##[,1]
##[1,]9
```

##Media de un vector mediante producto escalar 

```
n<-length(x)
t(x)%*%rep(1,length(x))/n
```

```
##[,1]
##[1,]3
```

##Suma de cuadrados de los elementos de un vector 

```
t(x)%*%x
```

```
##[,1]
##[1,]29
```

##Varianza 

```
(t(x)%*%x/n)-(t(x)%*%rep(1,length(x))/n)ˆ2
```

```
##[,1]
##[1,]0.6666667
```

#Matrices 

Para generar una matriz: 

```
A<-matrix(data=1:6,nrow=2,ncol=3)
A
```

```
##[,1][,2][,3]
##[1,]135
##[2,]246
```

3 

```
B<-matrix(data=12:17,nrow=2,ncol=3)
B
```

```
##[,1][,2][,3]
##[1,]121416
##[2,]131517
```

Para generar un data frame a partir de vectores: 

```
peso<-c(45,56,78)
altura<-c(156,167,170)
datos<-data.frame(peso,altura)
datos
```

```
##pesoaltura
##145156
##256167
##378170
```

```
#Nombredecolumnas
colnames(datos)
```

```
##[1]"peso""altura"
```

```
#Nombredefilas
rownames(datos)
```

```
##[1]"1""2""3"
```

##Acceso a elementos de una matriz 

```
#Fila
A[2,]
```

```
##[1]246
```

```
#Columna
A[,2]
```

```
##[1]34
```

```
#Columnasinsimplificar
A[,2,drop=FALSE]
```

```
##[,1]
##[1,]3
##[2,]4
```

4 

```
#Elemento
A[2,2]
```

```
##[1]4
```

```
#Subconjuntodeelementos
A[1:2,2:3]
```

```
##[,1][,2]
##[1,]35
##[2,]46
```

```
A[1:2,c(1,3)]
```

```
##[,1][,2]
##[1,]15
##[2,]26
```

```
A[,-1]
```

```
##[,1][,2]
##[1,]35
##[2,]46
```

#Operaciones con matrices 

```
#Suma
A+B
```

```
##[,1][,2][,3]
##[1,]131721
##[2,]151923
#Diferencia
A-B
```

```
##[,1][,2][,3]
##[1,]-11-11-11
##[2,]-11-11-11
```

```
#Multiplicaciónelementoaelemento
A*B
```

```
##[,1][,2][,3]
##[1,]124280
##[2,]2660102
```

5 

```
#Multiplicaciónmatricial(columnasdeA=filasdeB)
A%*%t(B)
```

```
##[,1][,2]
##[1,]134143
##[2,]176188
```

```
#División
A/B
```

```
##[,1][,2][,3]
##[1,]0.083333330.21428570.3125000
##[2,]0.153846150.26666670.3529412
```

```
#Restodeunadivisión
A%/%B
```

```
##[,1][,2][,3]
##[1,]000
##[2,]000
```

```
#Dimensióndeunamatriz
dim(A)
```

```
##[1]23
```

```
##Primernúmeroesnúmerodefilasysegundonúmerodecolumnas
nrow(A)
```

```
##[1]2
```

```
ncol(A)
```

```
##[1]3
```

#Combinar filas y columnas 

```
#Filas
rbind(x,y)
```

```
##[,1][,2][,3]
##x234
##y345
```

```
#columnas
cbind(x,y)
```

6 

```
##xy
##[1,]23
##[2,]34
##[3,]45
```

##Traspuesta 

```
t(A)
```

```
##[,1][,2]
##[1,]12
##[2,]34
##[3,]56
```

##Suma y medias de filas y columnas 

```
#Sumaporfilas
rowSums(A)
```

```
##[1]912
```

```
#Sumaporcolumnas
colSums(A)
```

```
##[1]3711
```

```
#Mediaporfilas
rowMeans(A)
```

```
##[1]34
```

```
#Mediaporcolumnas
colMeans(A)
```

```
##[1]1.53.55.5
```

##Determinante 

```
C<-matrix(data=c(1,5,6,3,8,6,2,3,1),nrow=3,ncol=3)
det(C)
```

```
##[1]-7
```

##Traza 

```
traza<-function(X)
{
traza<-0
for(iin1:dim(X)[1])
traza<-traza+X[i,i]
return(traza)
}
traza(C)
```

7 

```
##[1]10
```

#Extraer elementos de la diagonal de una matriz cuadrada 

```
diag(C)
```

```
##[1]181
```

```
##Traza
sum(diag(C))
```

```
##[1]10
```

##Inversa 

```
solve(C)
```

```
##[,1][,2][,3]
##[1,]1.428571-1.2857141
##[2,]-1.8571431.571429-1
##[3,]2.571429-1.7142861
```

##Vector de medias 

```
n<-nrow(A)
vector_medias<-(t(A)%*%rep(1,n))/n
vector_medias
```

```
##[,1]
##[1,]1.5
##[2,]3.5
##[3,]5.5
```

##Matriz centrada 

```
J<-matrix(rep(1,nˆ2),nrow=n,ncol=n)
J
```

```
##[,1][,2]
##[1,]11
##[2,]11
```

```
A_cent<-A-(J%*%A)/n
A_cent
```

```
##[,1][,2][,3]
##[1,]-0.5-0.5-0.5
##[2,]0.50.50.5
```

##Matriz de dobles productos 

8 

```
P<-t(A)%*%A
P
##[,1][,2][,3]
##[1,]51117
##[2,]112539
##[3,]173961
```

```
#Conlasvariablescentradas
C<-t(A_cent)%*%A_cent
C
```

```
##[,1][,2][,3]
##[1,]0.50.50.5
##[2,]0.50.50.5
##[3,]0.50.50.5
CC<-t(A)%*%A-n*vector_medias%*%t(vector_medias)
CC
```

`## [,1] [,2] [,3] ## [1,] 0.5 0.5 0.5 ## [2,] 0.5 0.5 0.5 ## [3,] 0.5 0.5 0.5` ##Matriz de varianzas-covarianzas 

```
S<-CC/(n-1)
S
```

`## [,1] [,2] [,3] ## [1,] 0.5 0.5 0.5 ## [2,] 0.5 0.5 0.5 ## [3,] 0.5 0.5 0.5` ##Matriz de correlaciones `Ds<-` **`diag`** `(` **`diag`** `(S)` **`ˆ`** `(1` **`/`** `2)) Ds` 

```
##[,1][,2][,3]
##[1,]0.70710680.00000000.0000000
##[2,]0.00000000.70710680.0000000
##[3,]0.00000000.00000000.7071068
```

```
R<-solve(Ds)%*%S%*%solve(Ds)
R
```

```
##[,1][,2][,3]
##[1,]111
##[2,]111
##[3,]111
```

9 

##Descomposición espectral (matrices cuadradas) 

```
eigen(S)
```

```
##eigen()decomposition
##$values
##[1]1.500000e+004.440892e-160.000000e+00
##
##$vectors
##[,1][,2][,3]
##[1,]-0.57735030.81649660.0000000
##[2,]-0.5773503-0.4082483-0.7071068
##[3,]-0.5773503-0.40824830.7071068
```

##Descomposición en valores singulares (matrices rectangulares) 

```
svd(A)
```

```
##$d
##[1]9.52551810.5143006
##
##$u
##[,1][,2]
##[1,]-0.6196295-0.7848945
##[2,]-0.78489450.6196295
##
##$v
##[,1][,2]
##[1,]-0.22984770.8834610
##[2,]-0.52474480.2407825
##[3,]-0.8196419-0.4018960
```

```
X3<-matrix(c(1,1,
1,1,
1,-2),ncol=2,byrow=TRUE)
X3
##[,1][,2]
##[1,]11
##[2,]11
##[3,]1-2
```

```
n3<-nrow(X3)
p3<-ncol(X3)
```

```
XtX<-t(X3)%*%X3
XtX
```

```
##[,1][,2]
##[1,]30
##[2,]06
```

10 

```
eig<-eigen(XtX)
lambda<-eig$values
V<-eig$vectors
lambda
```

```
##[1]63
```

```
V
```

```
##[,1][,2]
##[1,]0-1
##[2,]10
```

```
alpha<-sqrt(lambda)
alpha
```

```
##[1]2.4494901.732051
```

```
Sigma<-diag(alpha)
Sigma_inv<-diag(1/alpha)
U<-X3%*%V%*%Sigma_inv
U
```

```
#(pxp)
#(pxp),aquíalpha>0
#(nxp)
```

```
##[,1][,2]
##[1,]0.4082483-0.5773503
##[2,]0.4082483-0.5773503
##[3,]-0.8164966-0.5773503
```

```
t(U)%*%U
```

```
##[,1][,2]
##[1,]10
##[2,]01
```

```
t(V)%*%V
```

```
##[,1][,2]
##[1,]10
##[2,]01
```

```
X3_rec<-U%*%Sigma%*%t(V)
X3_rec
```

```
##[,1][,2]
##[1,]11
##[2,]11
##[3,]1-2
```

11 

```
all.equal(X3,X3_rec)
```

```
##[1]TRUE
```

12 

