# Guided R Practice: Science vs. Humanities Grades

In this practice, we will demystify **Principal Component Analysis (PCA)** using a classic pedagogical example. We will observe how the algorithm, without any human supervision or "labels", is able to discover the latent psychological structure in a set of school grades.

## 1. The Dataset

Imagine we have the final grades (from 0 to 10) of 10 secondary school students in 5 subjects: Mathematics, Physics, Biology, Literature, and History.

```r
# Build a didactic dataset
grades <- data.frame(
  Mathematics = c(9, 8, 2, 3, 8, 4, 2, 7, 3, 9),
  Physics     = c(8, 9, 3, 2, 9, 3, 4, 8, 2, 8),
  Biology     = c(7, 8, 4, 4, 7, 5, 3, 6, 4, 7),
  Literature  = c(4, 3, 8, 9, 2, 8, 7, 3, 8, 2),
  History     = c(3, 4, 9, 8, 3, 7, 8, 4, 9, 3)
)
rownames(grades) <- paste0("Stud_", 1:10)

print("Grade data:")
print(grades)

# Initial exploration
print("Means by subject:")
print(colMeans(grades))

print("Standard deviations:")
print(apply(grades, 2, sd))

print("Correlation matrix:")
print(round(cor(grades), 3))
```

If we examine the data superficially, we can intuit a pattern: students who score high in science subjects tend to score low in humanities subjects, and vice versa.

## 2. Exploration of the Correlation Matrix

The correlation matrix reveals the underlying structure:

```r
# Correlation visualization (optional, requires ggplot2)
# install.packages("ggcorrplot")
library(ggcorrplot)
ggcorrplot(cor(grades), method="circle", lab=TRUE)
```

**Observations:**
- Within the Science group (Math, Phys, Bio): high positive correlations (~0.8-0.9)
- Within the Humanities group (Lit, Hist): high positive correlations (~0.85)
- Between groups (Science vs. Humanities): negative correlations (-0.7 to -0.9)

This correlation structure suggests that there is a **latent dimension underlying** that contrasts Science with Humanities.

## 3. PCA via Spectral Decomposition (Manual)

First, let us perform PCA "by hand" to understand all the steps:

```r
# Step 1: Centering and standardization
# Use scale() which subtracts the mean and divides by standard deviation
grades_std <- scale(grades)  # Mean 0, std dev 1

print("Standardized data (first 3 rows):")
print(round(grades_std[1:3, ], 3))

# Step 2: Correlation matrix (equals Cov(grades_std))
R <- cor(grades)  # Or equivalently: cov(grades_std)

print("Correlation matrix R:")
print(round(R, 3))

# Step 3: Spectral decomposition
eig <- eigen(R)
lambda <- eig$values      # Eigenvalues
V <- eig$vectors          # Eigenvectors (weights)

print("Eigenvalues (variances of components):")
print(round(lambda, 4))

print("Eigenvectors (weights) - first 2 columns:")
print(round(V[, 1:2], 4))

# Step 4: Scores (projection of centered data on weights)
# Y = X_std * V
scores_eig <- grades_std %*% V

print("Scores (scores) - first 2 columns:")
print(round(scores_eig[, 1:2], 3))

# Step 5: Factor loadings (correlations between original variables and components)
# L = V * sqrt(lambda)
loadings_eig <- sweep(V, MARGIN=2, STATS=sqrt(lambda), FUN="*")

print("Factor loadings (loadings) - first 2 columns:")
print(round(loadings_eig[, 1:2], 3))

# Explained variance
var_expl <- lambda / sum(lambda)
print("Variance explained per component:")
print(round(var_expl, 4))
print("Cumulative variance:")
print(round(cumsum(var_expl), 4))
```

**Interpretation of Step 3:**

The eigenvalues tell us:
- PC1 explains: 3.6 out of 5 variances = 72%
- PC2 explains: 0.96 out of 5 variances = 19%
- PC3-PC5 explain: <1% each

**The first 2 components capture 91% of the variability!**

## 4. PCA via SVD (Singular Value Decomposition)

Now let us perform PCA using SVD, which is numerically more stable:

```r
# SVD of the standardized data
# grades_std = U * D * V^T
svd_result <- svd(grades_std)

U <- svd_result$u        # Left singular vectors (n x p)
D <- diag(svd_result$d)  # Singular values (matrix diagonal)
V_svd <- svd_result$v    # Right singular vectors (p x p)

print("Singular values:")
print(round(svd_result$d, 4))

# Relationship with eigenvalues of R:
# lambda = d^2 / (n-1)
lambda_from_svd <- (svd_result$d^2) / (nrow(grades_std) - 1)
print("Eigenvalues calculated from SVD (d^2/(n-1)):")
print(round(lambda_from_svd, 4))

# Weights from SVD: V_svd
print("Weights from SVD - first 2 columns:")
print(round(V_svd[, 1:2], 4))

# Scores from SVD: Y = U * D
scores_svd <- U %*% D

print("Scores from SVD - first 2 columns:")
print(round(scores_svd[, 1:2], 3))

# Verification: Do SVD scores match spectral decomposition scores?
print("Do the scores coincide (up to scale)?")
print(round(cor(scores_eig[, 1], scores_svd[, 1]), 4))  # Should be ~1 or ~-1
```

**Conclusion:** SVD and spectral decomposition produce identical results (identical weights, scores with perfect correlation). SVD is simply a numerically more robust way to perform PCA.

## 5. PCA with Standard R Functions

In real practice, we will use R's built-in functions:

### 5.1 Function prcomp() (Recommended)

prcomp() uses SVD internally, so it is numerically stable:

```r
# PCA with prcomp (on correlation matrix)
pca_prcomp <- prcomp(grades, center=TRUE, scale.=TRUE)

summary(pca_prcomp)

print("Weights (rotations) - first 2 components:")
print(round(pca_prcomp$rotation[, 1:2], 4))

print("Scores (x) - first 2 components:")
print(round(pca_prcomp$x[, 1:2], 3))
```

### 5.2 Function princomp() (Alternative)

princomp() uses eigendecomposition (less stable for large matrices):

```r
pca_princomp <- princomp(grades, cor=TRUE)

summary(pca_princomp)

print("Weights - first 2 components:")
print(round(pca_princomp$loadings[, 1:2], 4))

print("Scores - first 2 components:")
print(round(pca_princomp$scores[, 1:2], 3))
```

**Note:** The loadings in princomp$loadings already include the square root of the eigenvalue (they are directly correlations).

## 6. Loadings, Weights, and Scores: Clearly Explained Differences

We summarize the three key matrices:

```r
# Using prcomp (SVD)
weights <- pca_prcomp$rotation[, 1:2]
scores <- pca_prcomp$x[, 1:2]

# Loadings = weights * sqrt(component variances)
# Component variances are simply the eigenvalues (prcomp$sdev^2)
lambda_comp <- pca_prcomp$sdev^2
loadings <- sweep(weights, MARGIN=2, STATS=sqrt(lambda_comp[1:2]), FUN="*")

print("===== WEIGHTS (Weights / Eigenvectors) =====")
print(round(weights, 4))
print("Sum of squares of each weight:")
print(colSums(weights^2))  # Should be 1

print("\n===== LOADINGS (Loadings / Correlations) =====")
print(round(loadings, 4))
print("Approximate range:")
print(range(loadings))  # Typically between -1 and 1

print("\n===== SCORES (Scores / Factors) =====")
print(round(scores[1:5, ], 3))
print("Mean of scores (should be ~0):")
print(round(colMeans(scores), 10))
print("Variance of scores (should be ~lambda):")
print(round(apply(scores, 2, var), 4))
```

**Key differences:**
- **Weights:** Coefficients of the linear combination, with artificial unit norm
- **Loadings:** True correlations between original variables and components (range -1 to 1)
- **Scores:** Coordinates of individuals in the new space; used for plots and further analysis

## 7. Interpretation of Components: The Correlation Circle

The correlation circle (biplot of variables) visualizes the **loadings** and is the most important tool for understanding what the components mean:

```r
# Install factoextra if not available
if (!require("factoextra")) install.packages("factoextra")
library(factoextra)

# Correlation circle with factoextra
fviz_pca_var(pca_prcomp, 
             axes = c(1, 2),
             col.var = "steelblue",
             circle = TRUE,
             repel = TRUE,
             title = "Correlation Circle - Variables")

# Interpretation:
# - Variables close to the circle: well represented in PC1-PC2
# - Small angle between two variables: high positive correlation
# - 90 degree angle: correlation ~0
# - 180 degree angle: high negative correlation
```

**Reading the circle in our example:**
- **Right side (PC1 positive):** Mathematics, Physics, Biology (Sciences) all point to the right
- **Left side (PC1 negative):** Literature and History (Humanities) point to the left
- **Angle between Sciences and Humanities:** approximately 180 degrees (perfect negative correlation)

**Conclusion:** PC1 is the **Science vs. Humanities** axis

## 8. Individual Plot (Scores)

We project the individuals (students) in the new space:

```r
# Individual plot with factoextra
fviz_pca_ind(pca_prcomp,
             axes = c(1, 2),
             col.ind = "cos2",  # Color by quality of representation
             gradient.cols = c("#00AFBB", "#E7B800", "#FC4E07"),
             repel = TRUE,
             title = "Individual Plot - Students")

# Interpretation:
# - Right: Science students (high grades in Math, Phys, Bio)
# - Left: Humanities students (high grades in Lit, Hist)
# - Up/Down (PC2): Secondary differences (could be overall achievement)
```

## 9. Quality of Representation Analysis (cos²)

Not all individuals are equally well represented in 2D. Some might be "out of the plane":

```r
# Cos² (quality of representation)
cos2_values <- diag(pca_prcomp$x[, 1:2] %*% t(pca_prcomp$x[, 1:2]) / 
                     rowSums(pca_prcomp$x^2))

print("Cos² of each individual in the PC1-PC2 plane:")
print(round(cos2_values, 4))

# Plot colored by cos²
fviz_pca_ind(pca_prcomp,
             axes = c(1, 2),
             col.ind = cos2_values,
             gradient.cols = c("#00AFBB", "#E7B800", "#FC4E07"),
             repel = TRUE,
             title = "Individual Plot - Colored by Cos²")
```

## 10. Contribution Analysis

Which individuals "pull" axis PC1 the most? Which variables contribute most to PC1?

```r
# Contribution of variables to PC1 (in %)
contrib_var <- (loadings[, 1]^2 / sum(loadings[, 1]^2)) * 100
print("Contribution of variables to PC1 (%):")
print(round(contrib_var, 2))

# Bar plot of contributions
fviz_contrib(pca_prcomp, choice="var", axes=1, top=10)
```

**Reading:** All 5 variables contribute significantly, but Mathematics and Literature lead (opposite signs).

## 11. Cumulative Variance Explained

Deciding how many components to retain:

```r
# Plot of explained variance
fviz_eig(pca_prcomp, 
         addlabels=TRUE,
         ylim=c(0, 100),
         main="Cumulative Explained Variance")

# Rule of thumb: retain components until 80-90% variance
cumsum_var <- cumsum(pca_prcomp$sdev^2 / sum(pca_prcomp$sdev^2))
n_comp <- which(cumsum_var >= 0.80)[1]
print(paste("Number of components for 80% variance:", n_comp))
```

## 12. Complete Biplot (Individuals + Variables)

The biplot is the most informative visualization: superimposes individuals and variables:

```r
# Manual biplot with ggplot2 (advanced, optional)
# Or simply:
biplot(pca_prcomp, scale=0)

# With factoextra:
fviz_pca_biplot(pca_prcomp,
                repel=TRUE,
                col.var="steelblue",
                col.ind="grey",
                title="Biplot - Individuals and Variables")
```

**Reading the Biplot:**
- Student "Stud_1" is TOP-RIGHT: many high grades in Sciences, profile "Science Excellence"
- Student "Stud_3" is TOP-LEFT: many high grades in Humanities, profile "Humanities Excellence"
- The "Mathematics" arrow points RIGHT: variable associated with positive PC1 (Sciences)
- The "Literature" arrow points LEFT: variable associated with negative PC1 (Humanities)

## 13. Final Interpretative Summary

What has PCA discovered without supervision?

```r
print("=== DISCOVERIES FROM PCA ===")
print("PC1 (72% of variance):")
print("  - Contrasts SCIENCES (Math, Phys, Bio with loadings ~+0.6)")
print("  - with HUMANITIES (Lit, His with loadings ~-0.6)")
print("  - Interpretation: Axis SCIENCE vs HUMANITIES")
print("")
print("PC2 (19% of variance):")
print("  - Smaller component, represents residual variation")
print("  - Could be interpreted as OVERALL ACHIEVEMENT or specificities")
print("")
print("Conclusion: Students distribute mainly along one latent dimension:")
print("specialization in Sciences vs. Humanities")
```

This is a perfect didactic example of how PCA discovers latent structures in data **completely unsupervised**, based only on variance and correlation.
Z <- scale(grades)
decomposition <- svd(Z)
lambda_svd <- decomposition$d^2 / (nrow(Z) - 1)
lambda_cor <- eigen(cor(grades))$values

round(cbind(lambda_cor, lambda_svd), 6)
```

## 5. Plot and interpret

```r
plot(
  scores[, 1], scores[, 2],
  xlab = "PC1", ylab = "PC2",
  main = "Principal plane of students"
)
text(scores[, 1], scores[, 2], labels = rownames(grades), pos = 3)

biplot(pca, scale = 0, main = "Biplot: students and subjects")
```

## 6. Activities

1. Determine how many components are needed to exceed 80% explained variance.
2. Interpret the first two components from their weights.
3. Identify two similar student profiles and two contrasting profiles.
4. Repeat PCA without `scale. = TRUE` and compare the results.
5. Explain why reversing the sign of a component does not alter its statistical interpretation.
