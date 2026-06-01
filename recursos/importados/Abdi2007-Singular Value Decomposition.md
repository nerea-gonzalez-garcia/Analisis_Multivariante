<!-- Convertido automáticamente desde PDF. Revisar y corregir formato si es necesario. -->

## Singular Value Decomposition (SVD) 

## and 

## Generalized 

Singular Value Decomposition (GSVD) 

## Hervé Abdi[1] 

## **1 Overview** 

The singular value decomposition (SVD) is a generalization of the eigen-decomposition which can be used to analyze rectangular matrices (the eigen-decomposition is defined only for squared matrices). By analogy with the eigen-decomposition, which decomposes a matrix into two simple matrices, the main idea of the SVD is to decompose a rectangular matrix into three simple matrices: Two orthogonal matrices and one diagonal matrix. 

Because it gives a least square estimate of a given matrix by a lower rank matrix of same dimensions, the SVD is equivalent to principal component analysis (PCA) and metric multidimensional 

> 1In: Neil Salkind (Ed.) (2007). Encyclopedia of Measurement and Statistics. Thousand Oaks (CA): Sage. Address correspondence to: Hervé Abdi Program in Cognition and Neurosciences, MS: Gr.4.1, The University of Texas at Dallas, Richardson, TX 75083–0688, USA 

E-mail: herve@utdallas.edu http://www.utd.edu/∼herve 

1 

Hervé Abdi: The Singular Value Decomposition 

scaling (MDS) and is therefore an essential tool for multivariate analysis. The generalized SVD (GSVD) decomposes a rectangular matrix and takes into account constraints imposed on the rows and the columns of the matrix. The GSVD gives a weighted generalized least square estimate of a given matrix by a lower rank matrix and therefore, with an adequate choice of the constraints, the GSVD implements all linear multivariate techniques ( _e.g.,_ canonical correlation, linear discriminant analysis, correspondence analysis, PLS-regression). 

## **2** 

Recall that a _positive semi-definite_ matrix can be obtained as the product of a matrix by its transpose. This matrix is obviously square and symmetric, but also (and this is less obvious) its eigenvalues are all positive or null, and the eigenvectors corresponding to different eigenvalues are pairwise orthogonal. Let **X** be a positive semi-definite, its eigen-decomposition is expressed as 

**==> picture [192 x 14] intentionally omitted <==**

with **U** being an orthonormal matrix ( _i.e.,_ **U**[T] **U** = **I** ) and **Λ** being a diagonal matrix containing the eigenvalues of **X** . 

The SVD uses the eigen-decomposition of a positive semi-definite matrix in order to derive a similar decomposition applicable to all rectangular matrices composed of real numbers. The idea here is to decompose any matrix into three simple matrices, two orthonormal matrices and one diagonal matrix. When applied to a _positive semi-definite_ matrix, the SVD is equivalent to the eigendecomposition. 

Formally, if **A** is a rectangular matrix, its SVD decomposes it as: 

**==> picture [191 x 15] intentionally omitted <==**

with: 

- **P** : the (normalized) eigenvectors of the matrix **AA**[T] ( _i.e.,_ **P**[T] **P** = **I** ). The columns of **P** are called the _left singular vectors_ of **A** . 

2 

Hervé Abdi: The Singular Value Decomposition 

- **Q** : the (normalized) eigenvectors of the matrix **A**[T] **A** ( _i.e.,_ **Q**[T] **Q** = **I** ). The columns of **Q** are called the _right singular vectors_ of **A** . 

- 1 

- • **∆** : the diagonal matrix of the _singular values_ , **∆** = **Λ** 2 with **Λ** being the diagonal matrix of the eigenvalues of matrix **AA**[T] and of the matrix **A**[T] **A** (they are the same). 

The SVD is a consequence of the eigen-decomposition of a positive semi-definite matrix. This can be shown by considering the eigen-decomposition of the two positive semi-definite matrices that can be obtained from **A** : namely **AA**[T] and **A**[T] **A** . If we express these matrices in terms of the SVD of **A** , we obtain the following equations: 

**==> picture [258 x 15] intentionally omitted <==**

and 

**==> picture [260 x 15] intentionally omitted <==**

This shows that **∆** is the square root of **Λ** , that **P** are the eigenvectors of **AA**[T] , and that **Q** are the eigenvectors of **A**[T] **A** . For example, the matrix: 

**==> picture [225 x 41] intentionally omitted <==**

can be expressed as: 

**==> picture [51 x 14] intentionally omitted <==**

**==> picture [285 x 104] intentionally omitted <==**

3 

Hervé Abdi: The Singular Value Decomposition 

We can check that: 

**==> picture [335 x 104] intentionally omitted <==**

and that: 

**==> picture [304 x 77] intentionally omitted <==**

## **2.1 Technical note: Agreement between signs** 

Singular vectors come in pairs made of one left and one right singular vectors corresponding to the same singular value. They could be computed separately or as a pair. Equation 2 requires computing the eigen-decomposition of two matrices. Rewriting this equation shows that it is possible, in fact, to compute only one eigen-decomposition. As an additional bonus, computing only one eigen-decomposition prevents a problem which can arise when the singular vectors are obtained from two separate eigen-decompositions. This problem follows from the fact that the eigenvectors of a matrix are determined up to a multiplication by −1, but that singular vectors being pairs of eigenvectors need to have compatible parities. Therefore, when computed as eigenvectors, a pair of singular vectors can fail to reconstruct the original matrix because of this parity problem. 

This problem is illustrated by the following example: The ma- 

4 

Hervé Abdi: The Singular Value Decomposition 

trix 

**==> picture [225 x 41] intentionally omitted <==**

can be decomposed in two equivalent ways: 

**A** = **P∆Q**[T] 

**==> picture [285 x 166] intentionally omitted <==**

But when the parity of the singular vectors does not match, the SVD will fail to reconstruct the original matrix as illustrated by 

**==> picture [294 x 94] intentionally omitted <==**

By computing only one matrix of singular vectors, we can rewrite Equation 2 in a manner that expresses that one matrix of singular vectors can be obtained from the other: 

**==> picture [241 x 14] intentionally omitted <==**

5 

Hervé Abdi: The Singular Value Decomposition 

For example: 

**==> picture [54 x 14] intentionally omitted <==**

**==> picture [285 x 104] intentionally omitted <==**

## **3 Generalized singular value decomposition** 

For a given _I_ × _J_ matrix **A** , generalizing the singular value decomposition, involves using two positive definite square matrices with size _I_ × _I_ and _J_ × _J_ respectively. These two matrices express constraints imposed respectively on the rows and the columns of **A** . Formally, if **M** is the _I_ × _I_ matrix expressing the constraints for the rows of **A** and **W** the _J_ × _J_ matrix of the constraints for the columns of **A** . The matrix **A** is now decomposed into: 

**==> picture [264 x 13] intentionally omitted <==**

In other words, the generalized singular vectors are orthogonal under the constraints imposed by **M** and **W** . 

This decomposition is obtained as a result of the standard singular value decomposition. We begin by defining the transformed matrix **A** as: 

**==> picture [245 x 15] intentionally omitted <==**

We then compute the standard singular value decomposition of **A** as: 

**==> picture [252 x 15] intentionally omitted <==**

The matrices of the generalized eigenvectors are obtained as: 

**==> picture [236 x 16] intentionally omitted <==**

6 

Hervé Abdi: The Singular Value Decomposition 

The diagonal matrix of singular values is simply equal to the matrix of singular values of **A**: 

**==> picture [178 x 13] intentionally omitted <==**

We verify that: 

**==> picture [51 x 13] intentionally omitted <==**

by substitution: 

**==> picture [70 x 14] intentionally omitted <==**

**==> picture [85 x 16] intentionally omitted <==**

**==> picture [240 x 15] intentionally omitted <==**

To show that Condition 14 holds, suffice to show that: 

and 

**==> picture [253 x 57] intentionally omitted <==**

## **4 Mathematical properties** 

It can be shown that (see, _e.g.,_ Strang, 2003; Abdi & Valentin 2006) that the SVD has the important property of giving an optimal approximation of a matrix by another matrix of smaller rank. In particular, the SVD gives the best approximation, in a least square sense, of any rectangular matrix by another rectangular of same dimensions, but smaller rank. 

Precisely, if **A** is an _I_ × _J_ matrix of rank _L_ ( _i.e.,_ **A** contains _L_ singular values that are not zero), we denote by **P** [ _K_ ] (respectively **Q** [ _K_ ], **∆** [ _K_ ]) the matrix made of the first _K_ columns of **P** (respectively **Q** , 

7 

Hervé Abdi: The Singular Value Decomposition 

**∆** ): 

**==> picture [235 x 14] intentionally omitted <==**

**==> picture [237 x 14] intentionally omitted <==**

**==> picture [237 x 12] intentionally omitted <==**

The matrix **A** reconstructed from the first _K_ eigenvectors is denoted **A** [ _K_ ]. It is obtained as: 

**==> picture [245 x 31] intentionally omitted <==**

(with _`δ` k_ being the _k_ -th singular value). 

The reconstructed matrix **A** [ _K_ ] is said to be optimal (in a least square sense) for matrices of rank _K_ because it satisfies the following condition: 

**==> picture [312 x 21] intentionally omitted <==**

for the set of matrices **X** of rank smaller or equal to _K_ . The quality of the reconstruction is given by the ratio of the first _K_ eigenvalues ( _i.e.,_ the squared singular values) to the sum of all the eigenvalues. This quantity is interpreted as _the reconstructed proportion_ or _the explained variance_ , it corresponds to the inverse of the quantity minimized by Equation 27. The quality of reconstruction can also be interpreted as the squared coefficient of correlation (precisely as the _Rv_ coefficient, see entry) between the original matrix and its approximation. 

The GSVD minimizes an expression similar to Equation 27, namely 

**==> picture [265 x 21] intentionally omitted <==**

for the set of matrices **X** of rank smaller or equal to _K_ . 

8 

Hervé Abdi: The Singular Value Decomposition 

## **4.1 SVD and General linear model** 

It can be shown that the SVD of a rectangular matrix gives the PCA of this matrix, with, for example, the factor scores being obtained as **F** = **P∆** . 

The adequate choice of matrices **M** and **W** makes the GSVD a very versatile tool which can implement the set of methods of linear multivariate analysis. For example, correspondence analysis (see entry) can be implemented by using a probability matrix ( _i.e.,_ made of positive or null numbers whose sum is equal to 1) along with two diagonal matrices **M** = **Dr** and **W** = **Dc** representing respectively the relative frequencies of the rows and the columns of the data matrix. The other multivariate techniques ( _e.g.,_ discriminant analysis, canonical correlation analysis, discriminant analysis) can be implemented with the proper choice of the matrices **M** and **W** (see, _e.g.,_ Greenacre, 1984). 

## **5 An example of singular value decomposition: Image compression** 

**==> picture [268 x 84] intentionally omitted <==**

Figure 1: The matrix of Equation 28 displayed as a picture. 

The SVD of a matrix is equivalent to PCA. We illustrate this property by showing how it can be used to perform image compression. Modern technology use digitized pictures, which are equivalent to a matrix giving the gray level value of each pixel. For example, the 

9 

Hervé Abdi: The Singular Value Decomposition 

**==> picture [338 x 225] intentionally omitted <==**

Figure 2: A picture corresponding to a matrix in the order of 204 × 290 = 59610 pixels. 

matrix: 

**==> picture [310 x 86] intentionally omitted <==**

corresponds to the image in Figure 1. 

In general, pictures coming from natural images have rather large dimensions. For example, the picture shown in Figure 2 corresponds to a matrix with 204 rows and 290 columns (therefore 204 × 290 = 59610 pixels). To avoid the problem of transmitting or storing the numerical values of such large images we want to represent the image with fewer numerical values than the original number of pixels. 

Thus, one way of compressing an image is to compute the singular value decomposition and then to reconstruct the image by 

10 

Hervé Abdi: The Singular Value Decomposition 

**==> picture [338 x 225] intentionally omitted <==**

Figure 3: The picture in Figure 2 built back with 25 pairs of singular vectors. (compression rate of ≈ 80%) 

an approximation of smaller rank. This technique is illustrated in Figures 4 and 5, which show the terms used in the approximation. As can be seen in Figure 4, the image is reconstructed almost perfectly (according to the human eye) by a rank 25 approximation. This gives a compression ratio of: 

**==> picture [285 x 25] intentionally omitted <==**

## **References** 

- [1] Abdi, H. (2003). Multivariate analysis. In M. Lewis-Beck, A. Bryman, & T. Futing (Eds): _Encyclopedia for research methods for the social sciences_ . Thousand Oaks: Sage. 

- [2] Abdi, H., Valentin, D. (2006). _Mathématiques pour les sciences cognitives (Mathematics for cognitive sciences)._ Grenoble: PUG. 

- [3] Greenacre, M.J. (1984). _Theory and applications of correspondence analysis_ . London: Academic Press. 

11 

Hervé Abdi: The Singular Value Decomposition 

**==> picture [357 x 458] intentionally omitted <==**

Figure 4: Reconstruction of the image in Figure 2. The percentages of explained variance are: 0.9347; 0.9512; 0.9641; 0.9748; 0.9792; 0.9824; 0.9846; 0.9866; 0.9881; 0.9896; 0.9905; 0.9913; 0.9920; 0.9926; 0.9931; 0.9936; 0.9940; 0.9944; 0.9947; 0.9950; 0.9953; 0.9956; 0.9958; 0.9961; 0.9963; 

12 

Hervé Abdi: The Singular Value Decomposition 

**==> picture [376 x 439] intentionally omitted <==**

Figure 5: The terms **p** _k_ **q** _k_ used to reconstruct the image in Figure 2 (see Figure 4). The eigenvalues (squared singular values) associated to each image are: 0.9347; 0.0166; 0.0129; 0.0107; 0.0044; 0.0032; 0.0022; 0.0020; 0.0015; 0.0014; 0.0010; 0.0008; 0.0007; 0.0006; 0.0005; 0.0005; 0.0004; 0.0004; 0.0003; 0.0003; 0.0003; 0.0003; 0.0002; 0.0002; 0.0002. 

13 

Hervé Abdi: The Singular Value Decomposition 

- [4] Strang, G. (2003). _Introduction to linear algebra_ . Cambridge (MA): Wellesley-Cambridge Press. 

14 

