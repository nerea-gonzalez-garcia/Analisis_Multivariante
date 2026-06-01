# Matrix Algebra Tools

Multivariate Analysis works simultaneously with many variables. To handle all that information in a compact and efficient way, **matrix algebra** is used — the common mathematical language of all the techniques we will study.

This section reviews the essential concepts you will need throughout the course.

---

## The Multivariate Data Matrix

When we collect data from $n$ individuals on $p$ variables, all the information is organised in a **data matrix** $\mathbf{X}$ of dimension $n \times p$:

$$
\mathbf{X} = \begin{pmatrix}
x_{11} & x_{12} & \cdots & x_{1p} \\
x_{21} & x_{22} & \cdots & x_{2p} \\
\vdots  & \vdots  & \ddots & \vdots  \\
x_{n1} & x_{n2} & \cdots & x_{np}
\end{pmatrix}
$$

where:
- Each **row** $i$ represents an individual or observation.
- Each **column** $j$ represents a variable.
- The element $x_{ij}$ is the value of variable $j$ for individual $i$.

**Example:** If we measure height, weight and age of 5 students, we have a matrix $\mathbf{X}$ of dimension $5 \times 3$.

In R, a data matrix is usually represented as a `data.frame` or a `matrix`:

```r
# Create a data matrix in R
X <- matrix(c(170, 65, 21,
              165, 58, 22,
              180, 75, 23,
              155, 52, 20,
              175, 70, 24),
            nrow = 5, ncol = 3, byrow = TRUE)
colnames(X) <- c("Height", "Weight", "Age")
rownames(X) <- paste0("Stu", 1:5)
print(X)
```

---

## Fundamental Matrix Operations

### Transpose

The **transpose** of a matrix $\mathbf{X}$ (notation: $\mathbf{X}^\top$) swaps rows and columns. If $\mathbf{X}$ is $n \times p$, then $\mathbf{X}^\top$ is $p \times n$.

```r
t(X)   # transpose in R
```

### Matrix product

The **product** $\mathbf{A} \cdot \mathbf{B}$ requires that the number of columns of $\mathbf{A}$ matches the number of rows of $\mathbf{B}$.

```r
A %*% B   # matrix product in R
```

### Inverse matrix

The **inverse** $\mathbf{A}^{-1}$ satisfies $\mathbf{A} \cdot \mathbf{A}^{-1} = \mathbf{I}$ (identity matrix). It only exists if $\mathbf{A}$ is square and non-singular.

```r
solve(A)   # inverse in R
```

### Determinant and trace

```r
det(A)         # determinant
sum(diag(A))   # trace (sum of diagonal elements)
```

---

## The Mean Vector

For each variable $j$, we compute its arithmetic mean over the $n$ individuals:

$$
\bar{x}_j = \frac{1}{n} \sum_{i=1}^{n} x_{ij}
$$

All averages together form the **mean vector** $\bar{\mathbf{x}}$ of dimension $p \times 1$:

$$
\bar{\mathbf{x}} = \begin{pmatrix} \bar{x}_1 \\ \bar{x}_2 \\ \vdots \\ \bar{x}_p \end{pmatrix}
$$

In R:

```r
# Mean vector
x_bar <- colMeans(X)
print(x_bar)
```

---

## Centring the Data

**Centring** the data means subtracting the mean of each variable from each observation. The **centred data matrix** $\tilde{\mathbf{X}}$ is obtained as:

$$
\tilde{\mathbf{X}} = \mathbf{X} - \mathbf{1}_n \bar{\mathbf{x}}^\top
$$

where $\mathbf{1}_n$ is a column vector of ones of length $n$.

Centring is fundamental because it removes the effect of each variable's scale and places the origin of coordinates at the centroid of the point cloud.

```r
# Centre the data in R
X_centred <- scale(X, center = TRUE, scale = FALSE)
print(X_centred)
```

---

## Standardisation

**Standardisation** goes one step further than centring: it also divides by the standard deviation of each variable. This way each variable has mean 0 and standard deviation 1, allowing comparison of variables with different units.

$$
z_{ij} = \frac{x_{ij} - \bar{x}_j}{s_j}
$$

where $s_j$ is the standard deviation of variable $j$.

```r
# Standardise the data in R
X_std <- scale(X, center = TRUE, scale = TRUE)
print(X_std)
```

```{admonition} When to centre and when to standardise?
:class: tip

- **Only centre**: when all variables are on the same scale and units (e.g., all in centimetres).
- **Standardise**: when variables have very different scales or units (e.g., weight in kg, salary in euros, temperature in Celsius). This is the most common option in practice.
```

---

## The Covariance Matrix

The **covariance matrix** $\mathbf{S}$ (dimension $p \times p$) summarises the variability and linear relationships between all variables:

$$
\mathbf{S} = \frac{1}{n-1} \tilde{\mathbf{X}}^\top \tilde{\mathbf{X}}
$$

Its element $(j, k)$ is:

$$
s_{jk} = \frac{1}{n-1} \sum_{i=1}^{n} (x_{ij} - \bar{x}_j)(x_{ik} - \bar{x}_k)
$$

- The **diagonal** elements ($s_{jj}$) are the **variances** of each variable.
- The **off-diagonal** elements ($s_{jk}$, $j \neq k$) are the **covariances** between pairs of variables.

```r
# Covariance matrix in R
S <- cov(X)
print(S)

# Visualise with corrplot
library(corrplot)
corrplot(cov2cor(S), method = "color", type = "upper",
         addCoef.col = "black", tl.col = "black")
```

```{admonition} Properties of the covariance matrix
:class: note

- It is **symmetric**: $\mathbf{S} = \mathbf{S}^\top$.
- It is **positive semi-definite**: all eigenvalues are $\geq 0$.
- The diagonal contains variances (always $\geq 0$).
```

---

## The Correlation Matrix

The **correlation matrix** $\mathbf{R}$ standardises covariances by dividing by the standard deviations of each pair of variables:

$$
r_{jk} = \frac{s_{jk}}{s_j \cdot s_k}
$$

All values are between $-1$ and $1$:
- $r_{jk} = 1$: perfect positive linear correlation.
- $r_{jk} = -1$: perfect negative linear correlation.
- $r_{jk} = 0$: absence of linear correlation.

```r
# Correlation matrix in R
R <- cor(X)
print(R)

# Attractive visualisation
library(corrplot)
corrplot(R, method = "color", type = "upper",
         addCoef.col = "black", tl.col = "black",
         col = colorRampPalette(c("#2166AC", "white", "#D6604D"))(200),
         title = "Correlation matrix", mar = c(0,0,1,0))
```

Table 1 summarises the difference between covariance and correlation.

**Table 1. Comparison between covariance and correlation.**

| Feature | Covariance ($s_{jk}$) | Correlation ($r_{jk}$) |
|---|---|---|
| Range of values | $(-\infty, +\infty)$ | $[-1, 1]$ |
| Scale dependent | Yes | No |
| Interpretation | Direction of relationship | Direction and strength |
| When to use | Variables on same scale | Comparing across variables |

---

## Eigenvalues and Eigenvectors

Some methods such as **PCA** or **Discriminant Analysis** require computing the **eigenvalues** ($\lambda_i$) and **eigenvectors** ($\mathbf{v}_i$) of the covariance or correlation matrix.

An eigenvector $\mathbf{v}$ and its eigenvalue $\lambda$ satisfy:

$$
\mathbf{S} \mathbf{v} = \lambda \mathbf{v}
$$

Eigenvalues indicate how much variance each direction captures; eigenvectors indicate in which direction of the original space the data is projected.

```r
# Eigenvalues and eigenvectors in R
ev <- eigen(S)
cat("Eigenvalues:\n"); print(ev$values)
cat("Eigenvectors (columns):\n"); print(ev$vectors)

# Proportion of variance explained by each eigenvalue
prop_var <- ev$values / sum(ev$values)
cat("Proportion of variance explained:\n"); print(round(prop_var, 4))
```

```{admonition} Connection with the syllabus
:class: important

The eigenvalues and eigenvectors of $\mathbf{S}$ or $\mathbf{R}$ are **exactly** what PCA computes in the next topic. Understanding this section is key to understanding why PCA works.
```

---

## Summary

Table 2 collects the most important matrix concepts of the course and their role in Multivariate Analysis.

**Table 2. Key matrix concepts and their use in the course.**

| Concept | Notation | Purpose |
|---|---|---|
| Data matrix | $\mathbf{X}$ ($n \times p$) | Stores all observations |
| Mean vector | $\bar{\mathbf{x}}$ ($p \times 1$) | Centroid of the point cloud |
| Centred data | $\tilde{\mathbf{X}}$ | Basis for computing $\mathbf{S}$ and for PCA |
| Standardised data | $\mathbf{Z}$ | Removes scale effect |
| Covariance matrix | $\mathbf{S}$ ($p \times p$) | Variability and relationships between variables |
| Correlation matrix | $\mathbf{R}$ ($p \times p$) | Relationship strength without scale effect |
| Eigenvalues / Eigenvectors | $\lambda_i$ / $\mathbf{v}_i$ | PCA, Discriminant Analysis, SEM |
