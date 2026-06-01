<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

## The Eigen-Decomposition: Eigenvalues and Eigenvectors 

Hervé Abdi[1] 

## **1 Overview** 

_Eigenvectors_ and _eigenvalues_ are numbers and vectors associated to square matrices, and together they provide the _eigen-decomposition_ of a matrix which analyzes the structure of this matrix. Even though the eigen-decomposition does not exist for all square matrices, it has a particularly simple expression for a class of matrices often used in multivariate analysis such as correlation, covariance, or cross-product matrices. The eigen-decomposition of this type of matrices is important in statistics because it is used to find the maximum (or minimum) of functions involving these matrices. For example, principal component analysis is obtained from the eigen-decomposition of a covariance matrix and gives the least square estimate of the original data matrix. 

Eigenvectors and eigenvalues are also referred to as _characteristic vectors and latent roots_ or _characteristic equation_ (in German, “ _eigen_ ” means “specific of” or “characteristic of”). The set of eigenvalues of a matrix is also called its _spectrum_ . 

> 1In: Neil Salkind (Ed.) (2007). _Encyclopedia of Measurement and Statistics._ Thousand Oaks (CA): Sage. Address correspondence to: Hervé Abdi Program in Cognition and Neurosciences, MS: Gr.4.1, The University of Texas at Dallas, Richardson, TX 75083–0688, USA 

_E-mail:_ `herve@utdallas.edu http://www.utd.edu/` _∼_ `herve` 

1 

Hervé Abdi: The Eigen-Decomposition 

**==> picture [360 x 171] intentionally omitted <==**

**----- Start of picture text -----**<br>
Au 1<br>8<br>u 1 u 2 1<br>2<br>1<br>3 12 -1<br>Au<br>-1 2<br>a b<br>**----- End of picture text -----**<br>


Figure 1: Two eigenvectors of a matrix. 

## **2** 

There are several ways to define eigenvectors and eigenvalues, the most common approach defines an eigenvector of the matrix **A** as a vector **u** that satisfies the following equation: 

**==> picture [186 x 10] intentionally omitted <==**

when rewritten, the equation becomes: 

**==> picture [197 x 11] intentionally omitted <==**

where _λ_ is a scalar called the _eigenvalue_ associated to the _eigenvector_ . 

In a similar manner, we can also say that a vector **u** is an eigenvector of a matrix **A** if the length of the vector (but not its direction) is changed when it is multiplied by **A** . 

For example, the matrix: 

**==> picture [190 x 27] intentionally omitted <==**

has the eigenvectors: 

**==> picture [263 x 28] intentionally omitted <==**

2 

Hervé Abdi: The Eigen-Decomposition 

and 

**==> picture [263 x 27] intentionally omitted <==**

We can verify (as illustrated in Figure 1) that only the length of **u** 1 and **u** 2 is changed when one of these two vectors is multiplied by the matrix **A** : 

**==> picture [234 x 27] intentionally omitted <==**

and 

**==> picture [242 x 27] intentionally omitted <==**

For most applications we normalize the eigenvectors ( _i.e.,_ transform them such that their length is equal to one): 

**==> picture [186 x 14] intentionally omitted <==**

For the previous example we obtain: 

**==> picture [199 x 27] intentionally omitted <==**

We can check that: 

and 

**==> picture [283 x 76] intentionally omitted <==**

Traditionally, we put together the set of eigenvectors of **A** in a matrix denoted **U** . Each column of **U** is an eigenvector of **A** . The eigenvalues are stored in a diagonal matrix (denoted **Λ** ), where the diagonal elements gives the eigenvalues (and all the other values are zeros). We can rewrite the first equation as: 

**==> picture [189 x 10] intentionally omitted <==**

3 

Hervé Abdi: The Eigen-Decomposition 

or also as: 

**==> picture [194 x 13] intentionally omitted <==**

For the previous example we obtain: 

**==> picture [56 x 12] intentionally omitted <==**

**==> picture [245 x 76] intentionally omitted <==**

It is important to note that not all matrices have eigenvalues. For example, some matrices do not have eigenvalues. Even when a matrix has eigenvalues and eigenvectors, their computation requires a large number of operations and is therefore better performed by computers. 

## **2.1 Digression: An infinity of eigenvectors for one eigenvalue** 

It is only through a slight abuse of language that we can talk about _the_ eigenvector associated with _one_ given eigenvalue. Strictly speaking, there is an _infinity_ of eigenvectors associated to each eigenvalue of a matrix. Because any scalar multiple of an eigenvector is still an eigenvector, there is, in fact, an (infinite) family of eigenvectors for each eigenvalue, but they are all proportional to each other. For example, 

**==> picture [177 x 27] intentionally omitted <==**

is an eigenvector of the matrix **A** : 

**==> picture [183 x 27] intentionally omitted <==**

4 

Hervé Abdi: The Eigen-Decomposition 

Therefore: 

**==> picture [251 x 87] intentionally omitted <==**

is also an eigenvector of **A** : 

## **3 Positive (semi-)definite matrices** 

A type of matrices used very often in statistics are called _positive semi-definite_ . The eigen-decomposition of these matrices always exists, and has a particularly convenient form. A matrix is said to be positive semi-definite when it can be obtained as the product of a matrix by its transpose. This implies that a positive semi-definite matrix is always symmetric. So, formally, the matrix **A** is positive 

**==> picture [184 x 14] intentionally omitted <==**

for a certain matrix **X** (containing real numbers). Positive semidefinite matrices of special relevance for multivariate analysis positive semi-definite matrices include correlation matrices. covariance, and, cross-product matrices. 

The important properties of a positive semi-definite matrix is that its eigenvalues are always positive or null, and that its eigenvectors are pairwise orthogonal when their eigenvalues are different. The eigenvectors are also composed of real values (these last two properties are a consequence of the symmetry of the matrix, for proofs see, _e.g.,_ Strang, 2003; or Abdi & Valentin, 2006). Because eigenvectors corresponding to different eigenvalues are orthogonal, it is possible to store all the eigenvectors in an orthogonal matrix (recall that a matrix is orthogonal when the product of this matrix by its transpose is a diagonal matrix). 

This implies the following equality: 

**==> picture [190 x 14] intentionally omitted <==**

5 

Hervé Abdi: The Eigen-Decomposition 

We can, therefore, express the positive semi-definite matrix **A** as: 

**==> picture [190 x 13] intentionally omitted <==**

where **U**[T] **U** _=_ **I** are the normalized eigenvectors; if they are not normalized then **U**[T] **U** is a diagonal matrix. For example, the matrix: 

**==> picture [191 x 27] intentionally omitted <==**

can be decomposed as: 

**==> picture [52 x 12] intentionally omitted <==**

with 

**==> picture [269 x 149] intentionally omitted <==**

## **3.1 Diagonalization** 

When a matrix is positive semi-definite we can rewrite Equation 21 as 

**==> picture [231 x 13] intentionally omitted <==**

This shows that we can transform the matrix **A** into an equivalent _diagonal_ matrix. As a consequence, the eigen-decomposition of a positive semi-definite matrix is often referred to as its _diagonalization_ . 

6 

Hervé Abdi: The Eigen-Decomposition 

## **3.2 Another definition for positive semi-definite matrices** 

A matrix **A** is said to be positive semi-definite if we observe the following relationship for any non-zero vector **x** : 

**==> picture [205 x 14] intentionally omitted <==**

(when the relationship is _≤_ 0 we say that the matrix is negative semi-definite). 

When all the eigenvalues of a symmetric matrix are positive, we say that the matrix is _positive definite_ . In that case, Equation 26 becomes: 

**==> picture [205 x 13] intentionally omitted <==**

## **4 Trace, Determinant, etc.** 

The eigenvalues of a matrix are closely related to three important numbers associated to a square matrix, namely its _trace_ , its _determinant_ and its _rank_ . 

## **4.1 Trace** 

The trace of a matrix **A** is denoted trace { **A** } and is equal to the sum of its diagonal elements. For example, with the matrix: 

**==> picture [200 x 41] intentionally omitted <==**

we obtain: 

**==> picture [224 x 10] intentionally omitted <==**

The trace of a matrix is also equal to the sum of its eigenvalues: 

**==> picture [230 x 23] intentionally omitted <==**

with **Λ** being the matrix of the eigenvalues of **A** . For the previous example, we have: 

**==> picture [238 x 11] intentionally omitted <==**

7 

Hervé Abdi: The Eigen-Decomposition 

We can verify that: 

**==> picture [268 x 23] intentionally omitted <==**

## **4.2 Determinant and rank** 

Another classic quantity associated to a square matrix is its _determinant_ . This concept of determinant, which was originally defined as a combinatoric notion, plays an important rôle in computing the inverse of a matrix and in finding the solution of systems of linear equations (the term _determinant_ is used because this quantity determines the existence of a solution in systems of linear equations). The determinant of a matrix is also equal to the product of its eigenvalues. Formally, if _|_ **A** _|_ the determinant of **A** , we have: 

**==> picture [298 x 22] intentionally omitted <==**

For example, the determinant of matrix **A** (from the previous section), is equal to: 

**==> picture [240 x 10] intentionally omitted <==**

Finally, the _rank_ of a matrix can be defined as being the number of non-zero eigenvalues of the matrix. For our example: 

**==> picture [195 x 11] intentionally omitted <==**

For a positive semi-definite matrix, the rank corresponds to the dimensionality of the Euclidean space which can be used to represent the matrix. A matrix whose rank is equal to its dimensions is called a _full rank_ matrix. When the rank of a matrix is smaller than its dimensions, the matrix is called _rank-deficient_ , _singular_ , or _multicolinear_ . Only full rank matrices have an inverse. 

## **5 Statistical properties of the eigen-decomposition** 

The eigen-decomposition is important because it is involved in problems of optimization. For example, in principal component 

8 

Hervé Abdi: The Eigen-Decomposition 

analysis, we want to analyze an _I × J_ matrix **X** where the rows are observations and the columns are variables describing these observations. The goal of the analysis is to find row _factor scores_ , such that these factor scores “explain” as much of the variance of **X** as possible, and such that the sets of factor scores are pairwise orthogonal. This amounts to defining the factor score matrix as 

**==> picture [184 x 10] intentionally omitted <==**

under the constraints that 

**==> picture [201 x 13] intentionally omitted <==**

is a diagonal matrix ( _i.e.,_ **F** is an orthogonal matrix) and that 

**==> picture [183 x 14] intentionally omitted <==**

( _i.e.,_ **P** is an orthonormal matrix). There are several ways of obtaining the solution of this problem. One possible approach is to use the technique of the Lagrangian multipliers where the constraint from Equation 38 is expressed as the multiplication with a diagonal matrix of Lagrangian multipliers denoted **Λ** in order to give the following expression 

**==> picture [192 x 21] intentionally omitted <==**

(see Harris, 2001; and Abdi & Valentin, 2006; for details). This amount to defining the following equation 

**==> picture [281 x 21] intentionally omitted <==**

In order to find the values of **P** which give the maximum values of _L_ , we first compute the derivative of _L_ relative to **P** : 

**==> picture [214 x 26] intentionally omitted <==**

and then set this derivative to zero: 

**==> picture [242 x 14] intentionally omitted <==**

9 

Hervé Abdi: The Eigen-Decomposition 

Because **Λ** is diagonal, this is clearly an eigen-decomposition problem, and this indicates that **Λ** is the matrix of eigenvalues of the positive semi-definite matrix **X**[T] **X** ordered from the largest to the smallest and that **P** is the matrix of eigenvectors of **X**[T] **X** associated to **Λ** . Finally, we find that the factor matrix has the form 

**==> picture [186 x 15] intentionally omitted <==**

The variance of the factors scores is equal to the eigenvalues: 

**==> picture [218 x 16] intentionally omitted <==**

Taking into account that the sum of the eigenvalues is equal to the trace of **X**[T] **X** , this shows that the first factor scores “extract” as much of the variances of the original data as possible, and that the second factor scores extract as much of the variance left unexplained by the first factor, and so on for the remaining factors. 1 Incidently, the diagonal elements of the matrix **Λ** 2 which are the standard deviations of the factor scores are called the _singular values_ of matrix **X** (see entry on singular value decomposition). 

## **References** 

- [1] Abdi, H. (2003). Multivariate analysis. In M. Lewis-Beck, A. Bryman, & T. Futing (Eds): _Encyclopedia for research methods for the social sciences_ . Thousand Oaks: Sage. 

- [2] Abdi, H., Valentin, D. (2006). _Mathématiques pour les sciences cognitives (Mathematics for cognitive sciences)._ Grenoble: PUG. 

- [3] Harris, R.j. (2001). _A primer of multivariate statistics_ . Mahwah (NJ): Erlbaum. 

- [4] Strang, G. (2003). _Introduction to linear algebra_ . Cambridge (MA): Wellesley-Cambridge Press. 

10 

