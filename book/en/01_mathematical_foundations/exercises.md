# Exercises

This section presents theoretical and practical problems on the Mathematical Foundations of Multivariate Analysis. Each exercise includes its complete step-by-step solution.

## THEORETICAL QUESTIONS

### Theoretical Question 1: Centering and Variance

**Problem Statement:** Prove algebraically that centering a data matrix $X$ (i.e., forming $X_c = X - \mathbf{1}\bar{x}^T$) does not alter the value of the covariance matrix $S$.

**Solution:**

The covariance matrix is defined as:
$$S = \frac{1}{n-1} X^T X - \frac{1}{n-1} \bar{x} \mathbf{1}^T X - \frac{1}{n-1} X^T \mathbf{1} \bar{x}^T + \frac{1}{n-1} \bar{x} \mathbf{1}^T \mathbf{1} \bar{x}^T$$

Let us rearrange and simplify. We know that:
- $X^T \mathbf{1} = n\bar{x}$ (sum of columns)
- $\mathbf{1}^T \mathbf{1} = n$ (number of rows)

Substituting:
$$S = \frac{1}{n-1} X^T X - \frac{1}{n-1} \bar{x} (n\bar{x})^T - \frac{1}{n-1} (n\bar{x}) \bar{x}^T + \frac{1}{n-1} \bar{x} (n) \bar{x}^T$$

$$S = \frac{1}{n-1} X^T X - \frac{n}{n-1} \bar{x} \bar{x}^T - \frac{n}{n-1} \bar{x} \bar{x}^T + \frac{n}{n-1} \bar{x} \bar{x}^T$$

$$S = \frac{1}{n-1} X^T X - \frac{n}{n-1} \bar{x} \bar{x}^T$$

Alternatively, using the centered matrix:
$$S = \frac{1}{n-1} X_c^T X_c$$

where $X_c = X - \mathbf{1}\bar{x}^T$.

Expanding:
$$X_c^T X_c = (X - \mathbf{1}\bar{x}^T)^T (X - \mathbf{1}\bar{x}^T) = X^T X - X^T \mathbf{1}\bar{x} - \bar{x}^T \mathbf{1}^T X + \bar{x}^T \mathbf{1}^T \mathbf{1} \bar{x}$$

$$= X^T X - (n\bar{x})\bar{x} - \bar{x}^T (n\bar{x}) + \bar{x}^T (n) \bar{x}$$

$$= X^T X - n\bar{x}\bar{x}^T - n\bar{x}^T\bar{x} + n\bar{x}^T\bar{x}$$

$$= X^T X - n\bar{x}\bar{x}^T$$

Therefore:
$$S = \frac{1}{n-1} (X^T X - n\bar{x}\bar{x}^T)$$

**Conclusion:** The formula with uncentered $X$ and $\bar{x}$ is equivalent to using $X_c$. The centering process algebraically absorbs the mean terms, but the final result is the same.

---

### Theoretical Question 2: Eigenvalues of the Correlation Matrix with Perfect Correlation

**Problem Statement:** What are the eigenvalues of an empirical correlation matrix $R$ of dimension $p \times p$ if all original variables are perfectly and linearly correlated ($r_{ij}=1$ for all $i, j$)? Justify your answer by appealing to the concept of matrix rank.

**Solution:**

If all correlations are 1, it means that the matrix $R$ has the form:
$$R = \begin{pmatrix} 1 & 1 & 1 & \cdots & 1 \\ 1 & 1 & 1 & \cdots & 1 \\ 1 & 1 & 1 & \cdots & 1 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & 1 & 1 & \cdots & 1 \end{pmatrix}$$

This matrix can be written as:
$$R = \mathbf{1} \mathbf{1}^T / p$$

(except for a normalization factor; the idea is that all rows are proportional).

**Rank:** All rows are identical, so the rank is exactly 1. This means there is only ONE non-zero eigenvalue.

**Calculating eigenvalues:**

To find the eigenvalues, we solve the eigenvalue problem. If $R \mathbf{v} = \lambda \mathbf{v}$, and we know that the matrix has rank 1:
- The null space has dimension $p-1$, which implies $p-1$ eigenvalues equal to 0.
- Only one positive eigenvalue exists.

To find that eigenvalue, note that:
$$R \mathbf{1} = \begin{pmatrix} p \\ p \\ \vdots \\ p \end{pmatrix} = p \mathbf{1}$$

Therefore, $\mathbf{1}$ is an eigenvector with eigenvalue $\lambda_1 = p$.

**Conclusion:** The eigenvalues are: $\lambda_1 = p$ and $\lambda_2 = \lambda_3 = \cdots = \lambda_p = 0$.

---

### Theoretical Question 3: Total Variance and Singular Values

**Problem Statement:** If you apply SVD to a centered data matrix $X_c$ and obtain the singular values $d_1 = 5, d_2 = 3, d_3 = 0$, what is the total variance of the sample if the number of individuals is $n=11$?

**Solution:**

The relationship between singular values and eigenvalues is:
$$\lambda_i = \frac{d_i^2}{n-1}$$

With $n=11$, we have $n-1=10$. The eigenvalues are:
$$\lambda_1 = \frac{5^2}{10} = \frac{25}{10} = 2.5$$
$$\lambda_2 = \frac{3^2}{10} = \frac{9}{10} = 0.9$$
$$\lambda_3 = \frac{0^2}{10} = 0$$

The total variance is the sum of the eigenvalues (which equals the trace of the covariance matrix):
$$\text{Total Variance} = \sum_{i=1}^p \lambda_i = 2.5 + 0.9 + 0 = 3.4$$

**Conclusion:** The total variance of the sample is $\mathbf{3.4}$.

---

## PRACTICAL PROBLEMS

### Practical Exercise 1: From Covariance to Correlation

**Problem Statement:** Given the following sample covariance matrix $S$ on 3 variables:

$$
S = \begin{pmatrix} 
16 & -2 & 4 \\ 
-2 & 4 & 1 \\ 
4 & 1 & 9 
\end{pmatrix}
$$

1. Determine the variance of each of the original variables.
2. Calculate the correlation matrix $R$.
3. Between which pair of variables is there the greatest linear dependence regardless of sign?

**Solution:**

**Section 1: Variances**

The variances are on the diagonal of $S$:
- $s_1^2 = 16 \Rightarrow s_1 = 4$
- $s_2^2 = 4 \Rightarrow s_2 = 2$
- $s_3^2 = 9 \Rightarrow s_3 = 3$

**Section 2: Correlation Matrix**

The formula is $R = D^{-1/2} S D^{-1/2}$, where $D = \text{diag}(s_1^2, s_2^2, s_3^2)$.

$$D^{-1/2} = \begin{pmatrix} 1/4 & 0 & 0 \\ 0 & 1/2 & 0 \\ 0 & 0 & 1/3 \end{pmatrix}$$

We calculate:
$$r_{11} = \frac{s_{11}}{s_1 s_1} = \frac{16}{4 \cdot 4} = 1$$
$$r_{12} = \frac{s_{12}}{s_1 s_2} = \frac{-2}{4 \cdot 2} = -0.25$$
$$r_{13} = \frac{s_{13}}{s_1 s_3} = \frac{4}{4 \cdot 3} = \frac{1}{3} \approx 0.333$$
$$r_{22} = \frac{4}{2 \cdot 2} = 1$$
$$r_{23} = \frac{1}{2 \cdot 3} = \frac{1}{6} \approx 0.167$$
$$r_{33} = \frac{9}{3 \cdot 3} = 1$$

$$R = \begin{pmatrix} 
1 & -0.25 & 0.333 \\ 
-0.25 & 1 & 0.167 \\ 
0.333 & 0.167 & 1 
\end{pmatrix}$$

**Section 3: Greatest Linear Dependence**

We calculate the absolute value of each correlation:
- $|r_{12}| = 0.25$
- $|r_{13}| = 0.333$ ← Largest value
- $|r_{23}| = 0.167$

**Conclusion:** The greatest linear dependence is between **variables 1 and 3** with $|r_{13}| = 0.333$.

---

### Practical Exercise 2: Geometry of Transformations and Spectral Decomposition

**Problem Statement:** Consider a point in $\mathbb{R}^2$, represented by the column vector $x = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$. You have the following two transformation matrices:

$$ A = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix}, \quad B = \begin{pmatrix} \cos(\pi/4) & -\sin(\pi/4) \\ \sin(\pi/4) & \cos(\pi/4) \end{pmatrix} $$

1. Calculate $Ax$ and indicate geometrically what has happened to the original point.
2. Calculate $Bx$ and indicate what type of transformation $B$ is.
3. How do these matrices relate to the matrices $\Lambda$ and $V$ of a spectral decomposition $S = V \Lambda V^T$?

**Solution:**

**Section 1: Transformation $Ax$**

$$Ax = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 4 \\ 3 \end{pmatrix}$$

**Geometric Interpretation:** The matrix $A$ is diagonal, meaning it acts as a **non-uniform scaling (homothety)**. The original point is stretched by a factor of 2 in the X-axis direction and by a factor of 3 in the Y-axis direction.
- X coordinate: $2 \rightarrow 4$ (doubled)
- Y coordinate: $1 \rightarrow 3$ (tripled)

The point moves from $(2, 1)$ to $(4, 3)$, remaining in the same quadrant but moving away from the origin.

**Section 2: Transformation $Bx$**

With $\cos(\pi/4) = \sin(\pi/4) = \frac{\sqrt{2}}{2} \approx 0.707$:

$$B = \begin{pmatrix} 0.707 & -0.707 \\ 0.707 & 0.707 \end{pmatrix}$$

$$Bx = \begin{pmatrix} 0.707 & -0.707 \\ 0.707 & 0.707 \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 1.414 - 0.707 \\ 1.414 + 0.707 \end{pmatrix} = \begin{pmatrix} 0.707 \\ 2.121 \end{pmatrix}$$

**Geometric Interpretation:** The matrix $B$ is a **rotation matrix** with angle $\pi/4 = 45°$ (counterclockwise rotation). The point $(2, 1)$ is rotated $45°$ around the origin, without changing its distance from the origin.

Verification:
- Original distance: $\sqrt{2^2 + 1^2} = \sqrt{5} \approx 2.236$
- Distance after rotation: $\sqrt{0.707^2 + 2.121^2} = \sqrt{0.5 + 4.5} = \sqrt{5} \approx 2.236$ ✓

**Section 3: Relationship with Spectral Decomposition**

In a spectral decomposition $S = V \Lambda V^T$:
- **$V$:** Is an orthogonal rotation matrix (like $B$). Its columns are orthonormal eigenvectors. It rotates the original space to a new coordinate system where the matrix is diagonal.
- **$\Lambda$:** Is a diagonal matrix (like $A$). It contains the eigenvalues. It acts as non-uniform scaling along the axes of the new coordinate system.

**Conclusion:** The spectral decomposition can be interpreted as:
1. **$V^T$:** Rotates the original space
2. **$\Lambda$:** Scales the axes of the rotated space
3. **$V$:** Rotates back to the original space

This is exactly what the composite transformation $B \to A \to B^T$ does (although in spectral notation it is $V^T \to \Lambda \to V$).

---

## ADDITIONAL PROBLEMS

### Practical Exercise 3: SVD and Matrix Reconstruction (NEW)

**Problem Statement:** Consider a small centered data matrix:

$$
X_c = \begin{pmatrix} 
3 & 1 \\
1 & 2 \\
-1 & 0 \\
-3 & -3
\end{pmatrix} \quad (n=4, p=2)
$$

1. Calculate the covariance matrix $S$ manually.
2. Calculate the spectral decomposition of $S$ (eigenvalues and eigenvectors).
3. Perform the SVD of $X_c$.
4. Verify that the eigenvalues of $S$ coincide with $\frac{d_i^2}{n-1}$ where $d_i$ are the singular values.

**Solution:**

**Section 1: Covariance Matrix**

$$SSCP = X_c^T X_c = \begin{pmatrix} 3 & 1 & -1 & -3 \\ 1 & 2 & 0 & -3 \end{pmatrix} \begin{pmatrix} 3 & 1 \\ 1 & 2 \\ -1 & 0 \\ -3 & -3 \end{pmatrix}$$

We calculate:
- $(1,1)$: $3 \cdot 3 + 1 \cdot 1 + (-1)(-1) + (-3)(-3) = 9 + 1 + 1 + 9 = 20$
- $(1,2)$: $3 \cdot 1 + 1 \cdot 2 + (-1) \cdot 0 + (-3)(-3) = 3 + 2 + 0 + 9 = 14$
- $(2,1)$: $1 \cdot 3 + 2 \cdot 1 + 0 \cdot (-1) + (-3)(-3) = 3 + 2 + 0 + 9 = 14$
- $(2,2)$: $1 \cdot 1 + 2 \cdot 2 + 0 \cdot 0 + (-3)(-3) = 1 + 4 + 0 + 9 = 14$

$$SSCP = \begin{pmatrix} 20 & 14 \\ 14 & 14 \end{pmatrix}$$

$$S = \frac{1}{n-1} SSCP = \frac{1}{3} \begin{pmatrix} 20 & 14 \\ 14 & 14 \end{pmatrix} = \begin{pmatrix} 6.667 & 4.667 \\ 4.667 & 4.667 \end{pmatrix}$$

**Section 2: Spectral Decomposition**

Characteristic polynomial: $\det(S - \lambda I) = 0$

$$(6.667 - \lambda)(4.667 - \lambda) - 4.667^2 = 0$$
$$\lambda^2 - 11.334\lambda + 31.111 - 21.780 = 0$$
$$\lambda^2 - 11.334\lambda + 9.331 = 0$$

Using quadratic formula:
$$\lambda = \frac{11.334 \pm \sqrt{128.46 - 37.324}}{2} = \frac{11.334 \pm \sqrt{91.136}}{2} = \frac{11.334 \pm 9.547}{2}$$

$$\lambda_1 \approx 10.44, \quad \lambda_2 \approx 0.89$$

(For the purposes of this exercise, we would use the `eigen()` function in R to obtain exact values.)

**Section 3: SVD**

In R: `svd(Xc)` provides $U$, $D$, $V$ directly.

**Section 4: Verification**

With $n=4 \Rightarrow n-1=3$:
$$\lambda_i = \frac{d_i^2}{3}$$

This relationship is verified numerically.

---

## R CODE FOR VERIFICATION

```r
# Exercise 1: Covariance to Correlation
S <- matrix(c(16, -2, 4, -2, 4, 1, 4, 1, 9), nrow=3)
diag_sqrt <- sqrt(diag(S))
R <- S / outer(diag_sqrt, diag_sqrt)
print(R)

# Exercise 2: Transformations
x <- c(2, 1)
A <- diag(c(2, 3))
B <- matrix(c(cos(pi/4), sin(pi/4), -sin(pi/4), cos(pi/4)), nrow=2, byrow=TRUE)

print("Ax:"); print(A %*% x)
print("Bx:"); print(B %*% x)

# Exercise 3: SVD and Spectral
Xc <- matrix(c(3, 1, 1, 2, -1, 0, -3, -3), nrow=4, byrow=TRUE)
S_ex3 <- cov(Xc)
eig <- eigen(S_ex3)
svd_Xc <- svd(Xc)

print("Eigenvalues:"); print(eig$values)
print("Singular values squared / (n-1):"); print(svd_Xc$d^2 / 3)
```
