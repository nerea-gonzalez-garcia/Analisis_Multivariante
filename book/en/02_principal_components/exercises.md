# Proposed and Solved Exercises

This section presents theoretical and practical problems on Principal Component Analysis. Each exercise includes its complete step-by-step solution.

## THEORETICAL QUESTIONS

### Theoretical Question 1: PCA and Variance Maximization

**Statement:** Demonstrate that the first eigenvector of the correlation matrix $R$ is the one that provides maximum variance when we project the original standardized data onto that vector.

**Solution:**

Let $X_s$ be the matrix of standardized data with dimensions $n \times p$. The variance in the direction of a unit vector $v$ is:

$$\text{Var}(X_s v) = \frac{1}{n-1} (X_s v)^T (X_s v) = \frac{1}{n-1} v^T X_s^T X_s v = v^T \left(\frac{1}{n-1} X_s^T X_s \right) v = v^T R v$$

where $R$ is the correlation matrix.

To maximize $v^T R v$ subject to $\|v\| = 1$, we use Lagrange multipliers:

$$L(v, \lambda) = v^T R v - \lambda(v^T v - 1)$$

Taking derivatives: $2Rv - 2\lambda v = 0 \Rightarrow Rv = \lambda v$

This is the eigenvalue equation. The eigenvalues $\lambda$ are precisely the maximum achievable variances, and the first eigenvector corresponding to the largest eigenvalue produces the maximum possible variance.

**Conclusion:** The first eigenvector of $R$ is the weight vector that maximizes variance.

---

### Theoretical Question 2: Maximum number of components

**Statement:** Why in a dataset with $n=20$ observations and $p=50$ variables, can we obtain at most 19 genuine principal components?

**Solution:**

The maximum number of non-zero principal components is limited by the rank of the centered data matrix $X_c$:

$$\text{rg}(X_c) \leq \min(n-1, p)$$

The constraint $n-1$ (not $n$) comes from the fact that centering the data introduces a mandatory linear dependence via the mean vector.

With $n=20$ and $p=50$:
$$\text{rg}(X_c) \leq \min(20-1, 50) = \min(19, 50) = 19$$

Therefore, there are only 19 strictly positive eigenvalues. The remaining $50-19=31$ eigenvalues are mathematically zero (except for numerical precision errors), representing dimensions with no real variance.

**Conclusion:** The software will report 50 eigenvalues, but only the first 19 are genuine; the rest are algebraic artifacts.

---

### Theoretical Question 3: Orthogonality of components

**Statement:** Prove that two distinct principal components $Y_1 = X_s v_1$ and $Y_2 = X_s v_2$ (with $v_1 \neq v_2$) have zero correlation.

**Solution:**

By construction, the eigenvectors of a symmetric matrix (such as $R$) are orthogonal: $v_1^T v_2 = 0$.

The covariance between the two components is:

$$\text{Cov}(Y_1, Y_2) = \frac{1}{n-1} (X_s v_1)^T (X_s v_2) = \frac{1}{n-1} v_1^T X_s^T X_s v_2 = v_1^T R v_2$$

But we know that $R v_2 = \lambda_2 v_2$, so:

$$v_1^T R v_2 = v_1^T (\lambda_2 v_2) = \lambda_2 (v_1^T v_2) = \lambda_2 \cdot 0 = 0$$

**Conclusion:** Principal components are uncorrelated by algebraic construction.

---

## PRACTICAL PROBLEMS

### Practical Exercise 1: Interpretation of weights, scores, and loadings

**Statement:** In a PCA on the correlation matrix of 3 variables, the following are obtained:

- First eigenvector: $v_1 = (0.577, 0.577, 0.577)^T$
- First eigenvalue: $\lambda_1 = 2.5$
- First standardized individual: $x_1 = (1.5, -0.5, 2.0)^T$

Calculate and interpret:
1. The weight of the first component (already given as $v_1$)
2. The score of the first individual on the first component
3. The factor loading of the first individual on the first component

**Solution:**

**Part 1: The weights**

The weights are already given: $v_1 = (0.577, 0.577, 0.577)^T$

We verify normalization: $\|v_1\|^2 = 0.577^2 + 0.577^2 + 0.577^2 \approx 1$ ✓

Interpretation: The first component weights all three variables equally (approx. 1/√3 each). This suggests that the first dimension captures a "general level" trend.

**Part 2: The score**

$$y_1 = x_1^T v_1 = (1.5)(0.577) + (-0.5)(0.577) + (2.0)(0.577) = 0.865 - 0.289 + 1.154 = 1.73$$

Interpretation: The first individual has a score of 1.73 on the first component, which is positive and moderate. This indicates that this individual is above average in all three variables.

**Part 3: The loadings**

$$l_1 = v_1 \sqrt{\lambda_1} = (0.577, 0.577, 0.577)^T \cdot \sqrt{2.5} = (0.577, 0.577, 0.577)^T \cdot 1.581 = (0.913, 0.913, 0.913)^T$$

Interpretation: The loadings indicate the correlation between the original standardized variables and the first component. All loadings are high and similar (0.913), indicating that all three variables are equally correlated with PC1.

---

### Practical Exercise 2: Explained variance and decision on number of components

**Statement:** A PCA produces the following eigenvalues:

$$\lambda_1 = 3.5, \quad \lambda_2 = 1.2, \quad \lambda_3 = 0.8, \quad \lambda_4 = 0.3, \quad \lambda_5 = 0.2$$

1. Calculate the percentage of variance explained by each component
2. Calculate the cumulative variance
3. How many components would you retain if your criterion were to capture at least 80% of the variance?

**Solution:**

Total variance: $\sum \lambda_i = 3.5 + 1.2 + 0.8 + 0.3 + 0.2 = 6.0$

**Part 1: Variance per component**

- PC1: $\frac{3.5}{6.0} \times 100 = 58.33\%$
- PC2: $\frac{1.2}{6.0} \times 100 = 20.00\%$
- PC3: $\frac{0.8}{6.0} \times 100 = 13.33\%$
- PC4: $\frac{0.3}{6.0} \times 100 = 5.00\%$
- PC5: $\frac{0.2}{6.0} \times 100 = 3.33\%$

**Part 2: Cumulative variance**

- Up to PC1: 58.33%
- Up to PC2: 58.33% + 20.00% = 78.33%
- Up to PC3: 78.33% + 13.33% = 91.67%
- Up to PC4: 91.67% + 5.00% = 96.67%
- Up to PC5: 96.67% + 3.33% = 100%

**Part 3: Number of components**

To reach at least 80%, we need PC1 and PC2 (78.33% < 80%, but very close). If we want to guarantee ≥80%, we must include PC3, obtaining 91.67%.

In many contexts, if 78.33% is sufficiently close to 80% (difference <2%), retaining only PC1 and PC2 could be acceptable. In other more rigorous contexts, PC1, PC2, and PC3 would be required.

**Conclusion:** Typically, we would retain **3 components** (91.67% of variance), although 2 components (78.33%) could be acceptable depending on the context.

---

## R CODE FOR VERIFICATION

```r
# Comparison of weights, scores, and loadings
lambda <- c(3.5, 1.2, 0.8, 0.3, 0.2)
v1 <- c(0.577, 0.577, 0.577)
x1 <- c(1.5, -0.5, 2.0)

# Score
score <- sum(x1 * v1)
print(paste("Score of individual 1 on PC1:", round(score, 3)))

# Loadings
loading <- v1 * sqrt(lambda[1])
print(paste("Loadings of PC1:", paste(round(loading, 3), collapse=", ")))

# Explained variance
var_total <- sum(lambda)
var_pct <- (lambda / var_total) * 100
var_cum <- cumsum(var_pct)

print("Explained variance (%):")
print(round(var_pct, 2))
print("Cumulative variance (%):")
print(round(var_cum, 2))
```
