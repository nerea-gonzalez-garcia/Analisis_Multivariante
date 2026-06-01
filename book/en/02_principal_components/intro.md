# Chapter 2. Principal Component Analysis

## 2.1 Introduction and Motivation

In the era of *Big Data*, it is not uncommon to encounter data tables composed of tens, hundreds, or thousands of variables ($p$) measured on thousands of observations ($n$). When the number of variables grows, we face the well-known **"curse of dimensionality"**: data become sparse, modeling algorithms become unstable, and graphical visualization of the data as a whole becomes mathematically impossible in the space of $\mathbb{R}^p$.

However, fortunately in nature and in the social sciences, variables rarely operate in a completely independent manner. For example, in anthropometric data, weight, height, and wingspan are strongly correlated. This **correlation implies redundancy**. If several variables move in a coordinated way, the "real" or intrinsic dimensionality of the problem is much lower than the nominal number of variables.

**Principal Component Analysis (PCA)** —initially developed by Karl Pearson (1901) and later formalized by Harold Hotelling (1933)— is the paramount statistical procedure for dimensionality reduction. Its underlying philosophy is elegant: seek a new orthogonal coordinate system (a rotation of the space) where the new axes align naturally with the directions of maximum variance in the data.

## 2.2 Theoretical Development: Mathematical Construction of PCA

To understand the magic of PCA, it is not enough to apply the technique as a "black box". It is essential to understand how the geometric objective of seeking "maximum variability" translates systematically into a classical algebraic optimization problem.

### Formulation of the Optimization Problem

Given a centered data matrix $X_c$ of dimension $n \times p$ with original variables $X_1, X_2, \dots, X_p$. We want to create a **first principal component**, which we will denote as $Y_1$. To make it linearly interpretable, $Y_1$ is constructed as a strict linear combination of the original variables:

$$
Y_1 = v_{11}X_1 + v_{21}X_2 + \dots + v_{p1}X_p = X_c v_1
$$

where $v_1 = (v_{11}, v_{21}, \dots, v_{p1})^T$ is a column vector of weights or "loadings".

**The central objective:** We want this new synthetic variable $Y_1$ to summarize the largest possible amount of empirical information. In statistics, we interpret "information" as "variability" or dispersion. If all individuals had the same value in $Y_1$ (zero variance), the component would be useless for discriminating or studying the sample behavior. Therefore, we desire to **maximize the sample variance of $Y_1$**.

What is the variance of our new component $Y_1$? By leveraging the properties of variance for linear combinations:

$$
Var(Y_1) = Var(X_c v_1) = v_1^T \text{Cov}(X_c) v_1 = v_1^T S v_1
$$

Where $S$ is the sample covariance matrix of dimension $p \times p$. The optimization problem is formulated as follows: find the weight vector $v_1$ that maximizes the quadratic form $v_1^T S v_1$.

### The Unit Norm Constraint and Lagrange Multipliers

At first glance, the problem of maximizing $v_1^T S v_1$ has no finite solution. If we find a vector $v_1$ that gives a variance of 10, we can simply multiply all elements of $v_1$ by 2, and the new variance will be multiplied by 4 (it will be 40). We could artificially increase the variance toward infinity by merely scaling the weights, which is statistically useless.

To solve this problem, we must impose an artificial mathematical constraint that fixes the "scale" of the weight vector without changing its direction. The canonical choice is to require that $v_1$ has Euclidean unit length or norm:

$$ ||v_1||^2 = v_1^T v_1 = 1 $$

Now we have a constrained optimization problem:
> **Maximize:** $f(v_1) = v_1^T S v_1$
> **Subject to:** $g(v_1) = v_1^T v_1 - 1 = 0$

The standard approach in multivariate calculus is to employ the method of **Lagrange multipliers**. We construct the Lagrangian:

$$ L(v_1, \lambda) = v_1^T S v_1 - \lambda (v_1^T v_1 - 1) $$

To find the optimum, we differentiate the Lagrangian with respect to the vector $v_1$ and set it equal to zero:

$$ \frac{\partial L}{\partial v_1} = 2 S v_1 - 2 \lambda v_1 = 0 $$

Dividing by 2 and rearranging terms, we arrive at a monumental expression:

$$ S v_1 = \lambda v_1 $$

```{admonition} Teaching Remark
:class: important
Pay attention to what has just happened! We started with a statistical/geometric problem of variance maximization, and the algebra has returned to us, by strict definition, the characteristic equation of the eigenvalue and eigenvector problem. The direction of maximum variance is none other than an eigenvector of the covariance matrix.
```

And what is the variance obtained? If we multiply the equation $S v_1 = \lambda v_1$ by $v_1^T$ on the left:

$$ v_1^T S v_1 = v_1^T (\lambda v_1) = \lambda (v_1^T v_1) = \lambda (1) = \lambda $$

The algebra reveals that **the maximum possible variance is exactly equal to the eigenvalue $\lambda$ associated with it**. Therefore, to maximize global variance, we choose the eigenvector associated with the **largest eigenvalue** of $S$, that is, $\lambda_1$. This defines the First Principal Component.

The process continues. For the **Second Principal Component** $Y_2 = X_c v_2$, we maximize $v_2^T S v_2$ with the constraint that $v_2^T v_2 = 1$ and, moreover, with the fundamental constraint that this new component must incorporate *new and non-redundant* information with respect to the first, which is enforced by requiring that $v_1$ and $v_2$ be orthogonal ($v_1^T v_2 = 0$). The development with a second Lagrange multiplier leads us to $v_2$ being the eigenvector associated with the second largest eigenvalue, $\lambda_2$. And so on.

### Obtaining via SVD and Relationship with the Spectrum

As we established in Chapter 1, calculating the spectral decomposition of the covariance matrix $S = V \Lambda V^T$ directly provides the weights in $V$ and the variances in $\Lambda$.

However, from the numerical and computational point of view (to avoid numerical instabilities when explicitly forming $X_c^T X_c$), it is highly recommended to perform PCA using the Singular Value Decomposition (SVD) of the original centered data matrix $X_c = U D V^T$.
As we saw:
* The matrix $V$ (right singular vectors) contains the **weights** or coefficients of the principal components.
* The coordinates of the projections (the scores) can be obtained directly as $Y = U D$. (Proof: $Y = X_c V = (U D V^T) V = U D (V^T V) = U D$).

### Geometric Interpretation of Projections

Geometrically, PCA is a **rigid rotation** of the original coordinate system in $\mathbb{R}^p$. The n-dimensional ellipsoid that envelops our point cloud has certain axes of symmetry. PCA simply locates the longest axis of the cloud and converts it into the new X-axis (Component 1). Then it seeks the second longest axis, perpendicular to the first, and converts it into the new Y-axis (Component 2).

Projecting an individual onto these new axes (that is, calculating their factorial coordinates) tells us their position along the principal directions of natural variation of the sample.

## 2.3 Differentiation of Fundamental Matrices

The greatest pedagogical obstacle in PCA is usually the terminological confusion surrounding software statistical outputs (such as R or SPSS). It is mathematically non-negotiable to differentiate with absolute precision the following three elements:

### 1. Weights or Eigenvectors (Weights / Eigenvectors)
Represented by the orthogonal matrix $V$ of dimension $p \times p$. 
* **Mathematical nature:** They are the coefficients of the linear combination model.
* **Basic formula:** $Y = X_c V$
* **Interpretation:** $v_{j1}$ indicates the scalar weighting with which the original variable $X_j$ participates in the synthetic construction of component $Y_1$. They must never be confused with correlations, because their values are artificially forced so that the norm of the vector sums to 1 ($\sum_{j=1}^p v_{j1}^2 = 1$). Their raw numerical value is less intuitive to interpret directly.

### 2. Factorial Scores (Scores)
Represented by the matrix $Y$ of dimension $n \times p$.
* **Mathematical nature:** They are the new synthetic variables, the coordinates of individuals after rotation.
* **Basic formula:** $Y = X_c V$
* **Interpretation:** If a researcher wishes to use PCA as preprocessing to introduce reduced data into a subsequent regression or clustering model, the data they should use are the *scores* corresponding to the first $q$ columns of $Y$. These scores have mean 0 and their variance equals the respective eigenvalue $\lambda_k$.

### 3. Factorial Loadings (Loadings)
Usually represented by the matrix $L$ of dimension $p \times p$.
* **Mathematical nature:** They are the covariances (or correlations if starting from matrix $R$) between the original variables and the generated principal components.
* **Basic formula:** $L = V \Lambda^{1/2}$
* **Interpretation:** It is the key element for **giving name or semantic meaning** to the latent components. If the loading $l_{j1}$ is high and positive, we know that variable $X_j$ is strongly correlated with component 1. Unlike *weights* limited to summing to 1 in squares, loadings reflect standard statistical association metrics.

## 2.4 Contributions and Quality of Representation (cos²)

Beyond analyzing overall impact, when representing data in a suboptimal bidimensional space (e.g., the plane of components 1 and 2), it is essential to know the geometric fidelity of what we are observing to avoid drawing fallacious conclusions.

### Quality of Representation of Individuals (cos²)

Suppose that an individual (point in the original space) is projected onto principal component $k$. The cos² is geometrically defined as the squared cosine of the angle formed by the individual's original position vector with the axis of component $k$.
* **Interpretation:** A cos² close to 1 implies an angle close to 0, which means that the original vector is practically parallel to the component: the projection onto that plane reflects almost perfectly the individual's original profile. 
* If a point has a very low cos² (e.g., 0.05) on the first factorial plane, it means that individual is "orthogonal" to that plane (suspended above or below the plane). Concluding similarities based on their apparent position in the 2D graph would be a projective mirage.

### Contribution to Inertia (Variance Explained by Elements)

* **Contribution of variables to the component:** Of all the variance explained by component $k$ ($\lambda_k$), what fraction comes from variable $j$? It is calculated by taking the squared loading and dividing by $\lambda_k$. This allows objective ranking of variables by their "responsibility" in creating the geometric axis.
* **Contribution of individuals to the component:** There are atypical individuals (outliers) so extreme that they force the variance maximization algorithm to orient the first principal component directly toward them. Evaluating individual contribution prevents biased inferences, warning whether the overall sample variability is being hijacked by a single anomalous case.

## 2.5 Mathematical Properties of PCA

PCA enjoys elegant and rigid theoretical properties derived from spectral algebra, rigorously demonstrable:

1. **Uncorrelation of components:** The empirical covariance matrix of the scores $Y$ is diagonal. $\text{Cov}(Y) = \text{Cov}(X_c V) = V^T \text{Cov}(X_c) V = V^T S V = V^T (V \Lambda V^T) V = I \Lambda I = \Lambda$. The absence of off-diagonal elements mathematically confirms that the new variables are 100% orthogonal (uncorrelated).
2. **Conservation of Total Variance (Trace):** In matrix algebra, the trace (sum of the diagonal) is invariant under cyclic rotations. The original total variance is $\text{tr}(S)$. Knowing that $S = V \Lambda V^T$, we have $\text{tr}(S) = \text{tr}(V \Lambda V^T) = \text{tr}(\Lambda V^T V) = \text{tr}(\Lambda I) = \sum_{k=1}^p \lambda_k$. This property certifies that the orthogonal rotation of PCA neither creates nor destroys information, it merely repackages it along the first axes.
3. **Reconstruction of the Matrix:** If we use all $p$ complete components, we can mathematically recover the original matrix without loss: $X_c = Y V^T$. 
4. **Optimal Low-Rank Approximation (Eckart-Young Theorem):** This is the true justification for PCA as a noise reduction tool. If in the reconstruction we use only the first $q$ principal components ($q < p$), we obtain a reconstructed matrix $\tilde{X}_c = Y_{(q)} V_{(q)}^T$. The Eckart-Young theorem demonstrates that of **all** possible rank-$q$ matrices that exist in the mathematical universe, the matrix $\tilde{X}_c$ constructed with PCA is the one with the smallest possible distance (reconstruction squared error) with respect to the original matrix $X_c$.

## 2.6 Maximum Dimensionality of PCA

A theoretical detail frequently ignored in basic texts is that obtaining $p$ principal components is not always statistically possible. The spectrum of genuine components is governed by the algebraic concept of **matrix rank**, $\text{rg}(X)$.

The covariance matrix $S$ is of size $p \times p$. We might suppose that it always yields $p$ strictly positive eigenvalues. This is **false**. The maximum number of real underlying dimensions is the rank of the original data matrix $X_c$ of dimension $n \times p$.

Algebra stipulates that the rank of a matrix is bounded by its smallest dimension, therefore:
$$ \text{rg}(X_c) \leq \min(n, p) $$
However, when centering the matrix (subtracting the mean vector), we introduce a mandatory linear dependence among the rows (the columns sum to zero by definition). This linear constraint "consumes" an additional dimension, reducing maximum rank:
$$ \text{rg}(X_c) \leq \min(n - 1, p) $$

**Practical Implications of High Dimensionality ($p > n$):**
There are areas such as genomics (microarrays) or spectrometry where it is common to have a sample of $n=50$ patients measured over $p=10,000$ genes. In this extreme situation:
* The maximum rank of the covariance matrix is $\min(50 - 1, 10,000) = 49$.
* Although the calculated covariance matrix will be gigantic ($10,000 \times 10,000$), the software will compute **at most 49 strictly positive eigenvalues** ($\lambda_1, \dots, \lambda_{49} > 0$).
* The remaining 9,951 eigenvalues ($\lambda_{50}, \dots, \lambda_{10,000}$) will be mathematically equal to zero (except for floating-point computational precision artifacts). The components associated with these null values are "mirages" hyperplanar that explain literally 0% of the variability, demonstrating that the data volume actually inhabited a minuscule subspace embedded within $\mathbb{R}^{10,000}$.

## 2.6b Successive Obtaining of Principal Components and Orthogonality Constraint

We have seen that the First Principal Component $Y_1$ is obtained by choosing the eigenvector associated with the largest eigenvalue. The construction of the remaining components follows a rigorous hierarchical procedure.

**Second Principal Component ($Y_2$):**

Once the direction of maximum variance $v_1$ has been extracted, we wish to find the second direction of maximum variance. However, we cannot simply choose the eigenvector corresponding to $\lambda_2$, because it would be **linearly dependent** on $v_1$, would incorporate redundant information, and would violate the fundamental principle that each component must provide new information.

To avoid this redundancy, we impose the **orthogonality constraint**:

$$v_1^T v_2 = 0$$

Geometrically, this means that $v_2$ must be perpendicular to $v_1$. Algebraically, the method of Lagrange multipliers with this additional constraint leads to $v_2$ being the eigenvector corresponding to the second largest eigenvalue, $\lambda_2$.

**Successive Principal Components ($Y_3, Y_4, \dots$):**

The same reasoning applies recursively. The $k$-th principal component $Y_k = X_c v_k$ is obtained by maximizing $v_k^T S v_k$ under the constraints:
1. $v_k^T v_k = 1$ (unit norm)
2. $v_k^T v_j = 0$ for all $j < k$ (orthogonality with respect to the previous ones)

This makes $v_k$ the eigenvector associated with the $k$-th largest eigenvalue $\lambda_k$.

**Final Result:** If we order the eigenvalues as $\lambda_1 \geq \lambda_2 \geq \dots \geq \lambda_p \geq 0$ and their corresponding eigenvectors form the columns of $V$, then:
- The weight matrix is $V = (v_1 | v_2 | \cdots | v_p)$
- The scores are $Y = X_c V$
- The $p$ components are **mutually orthogonal** (uncorrelated) by construction

---

## 2.6c Deep Geometric Interpretation: The Point Cloud and Principal Axes

To truly understand PCA, it is essential to visualize what happens in the geometric space $\mathbb{R}^p$.

**The Point Cloud as an Ellipsoid:**

Imagine that our set of $n$ individuals (points in $\mathbb{R}^p$) forms a cloud. If this cloud is "spherical", it means that variability is uniform in all directions. If it is "elongated" (cigar-shaped) or "flat" (pancake-shaped), it means that there is preferential variability in certain directions.

Mathematically, the shape of this cloud is encoded in the covariance matrix $S$ (or the correlation matrix $R$). The spectral decomposition $S = V \Lambda V^T$ tells us:
- The eigenvectors $v_1, v_2, \dots, v_p$ are the **principal axes of the ellipsoid** (perpendicular to each other)
- The eigenvalues $\lambda_1, \lambda_2, \dots, \lambda_p$ are the **"semi-lengths" of the axes** (they measure the "width" of the ellipsoid in each direction)

**The Coordinate Rotation:**

PCA is a process of **rigid rotation** of the space. We take the original coordinate system (the axes of variables $X_1, X_2, \dots, X_p$) and rotate it so that:
1. The first axis of the new system points exactly in the direction $v_1$ (direction of the longest axis of the ellipsoid)
2. The second axis points in the direction $v_2$ (perpendicular to the first, second most elongated direction)
3. And so on

In this new system, the covariance matrix becomes the diagonal matrix $\Lambda$, with no off-diagonal elements. This means that in the new system, the variables (components) are **completely independent**.

---

## 2.6d PCA via Spectral Decomposition and SVD: Two Equivalent Approaches

There are two computationally equivalent ways to perform PCA. Both give the same result, but have distinct advantages and disadvantages.

### Approach 1: Spectral Decomposition of $S$ or $R$

**Procedure:**
1. Center (and optionally standardize) the data matrix
2. Calculate the covariance matrix (or correlations): $S = \frac{1}{n-1} X_c^T X_c$
3. Calculate the spectral decomposition: $S = V \Lambda V^T$
4. The weights are the columns of $V$
5. The scores are $Y = X_c V$
6. The loadings are $L = V \sqrt{\Lambda}$

**Advantages:**
- Conceptually very clear: the structure of the covariance matrix is directly visible
- The eigenvalues are directly the variances of the components

**Disadvantages:**
- If $p$ is very large, explicitly forming $X_c^T X_c$ can cause numerical instability
- Computationally slower for large matrices

### Approach 2: Singular Value Decomposition of $X_c$

**Procedure:**
1. Center (and optionally standardize) the data matrix
2. Calculate the SVD of $X_c$: $X_c = U D V^T$
3. The weights are the columns of $V$ (right singular vectors)
4. The scores are $Y = U D$ (or equivalently, $Y = X_c V$)
5. The loadings are $L = V \sqrt{\frac{D^2}{n-1}}$

**Advantages:**
- Numerically more stable: avoids explicitly forming $X_c^T X_c$
- Computationally more efficient for large matrices

**Disadvantages:**
- The direct interpretation of $D$ requires remembering that $\lambda_i = \frac{d_i^2}{n-1}$

**Relationship between both:** As we demonstrated in Chapter 1, the matrix $V$ from the SVD of $X_c$ is exactly the matrix $V$ from the spectral decomposition of $S$. The eigenvalues are related by $\lambda_i = \frac{d_i^2}{n-1}$.

---

## 2.6e PCA on Covariance Matrix vs. PCA on Correlation Matrix

A critical decision in practice is whether to perform PCA on $S$ (covariance matrix) or on $R$ (correlation matrix). This choice has profound implications for the results.

### PCA on Covariance Matrix ($S$)

**When to use:**
- Variables measured in the same unit (e.g., all in meters, or all in euros)
- We want PCA to privilege variables with larger original variance

**Effect:**
- Variables with large variances "pull" the analysis toward them
- A variable with standard deviation of 1000 will have much more weight than one with standard deviation of 0.1
- The first components will be dominated by variables that naturally have more dispersion

**Example:** If we analyze anthropometry combining "weight in kg", "height in cm", and "age in years", weight (variance ~2000) and height (variance ~400) will completely dominate, while age (variance ~500) will be marginalized, although all are statistically relevant.

### PCA on Correlation Matrix ($R$)

**When to use:**
- Variables measured in different units (e.g., euros, meters, hours)
- We want PCA to treat all variables with equal statistical importance

**Effect:**
- By standardizing ($s_j = 1$ for all $j$), all weights are balanced
- The first components reflect patterns of association between variables, not simply patterns of "raw" variance

**Example:** If we want to compare house prices, surface area, age, and distance to center, standardizing first (with $R$) prevents the price (range 200,000-800,000) from dominating over age (range 0-100 years).

**Theoretical Note:** Working with $R$ is equivalent to standardizing the original variables (subtract mean, divide by standard deviation) and then performing PCA on the covariance matrix of the standardized data.

---

## 2.7 Summary of Key Concepts

| Concept | Definition | Formula | Range |
|----------|-----------|---------|-------|
| **Weights (Loadings in some texts)** | Coefficients that define linear combinations | $V$ (orthogonal) | Restricted: $\sum v_{ji}^2 = 1$ |
| **Scores (Scores)** | Coordinates of individuals in the new space | $Y = X_c V$ | Mean 0, variance $= \lambda_i$ |
| **Loadings (Loadings)** | Correlations between original variables and components | $L = V \sqrt{\Lambda}$ | No norm restriction |
| **Eigenvalue $\lambda_i$** | Variance of the $i$-th component | Diagonal of $\Lambda$ | $\lambda_1 \geq \cdots \geq \lambda_p \geq 0$ |
| **Singular value $d_i$** | Relates to eigenvalue | $\lambda_i = d_i^2 / (n-1)$ | $d_i \geq 0$ |
| **Maximum rank** | Non-redundant dimensions | $\min(n-1, p)$ | Fixed for a given sample |

---

## 2.8 Supplementary Material

In the following sections we will address the practical resolution of the technique:
* We will present the computational process using the statistical language R, with examples of manual step-by-step calculation
* We will develop the classic case of grades of Secondary Education students (Sciences vs. Humanities), illustrating how PCA automatically discovers these latent dimensions
* Visualizations will be shown of the correlation circle (variables) and individual graphs (scores)
* Mention will be made of the biplot projection, which constitutes the simultaneous visualization of *scores* (individuals) and *loadings* (variables) on the same flat space, a technique that will be analyzed rigorously in forthcoming chapters
