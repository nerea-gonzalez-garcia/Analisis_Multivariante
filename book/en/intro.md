# Multivariate Analysis

Welcome to the interactive manual for **Multivariate Analysis** at the University of Salamanca.

This book is aimed at students of the **Degree in Statistics** and the **Double Degree in Statistics and Computer Engineering**, and is the official support material for the course.

---

## What is Multivariate Analysis?

Imagine you want to understand which factors contribute to a student's academic success. You have data on study hours, previous grades, attendance, use of digital resources, sleep hours... There are **many variables at the same time**. How do you analyse them jointly without losing information?

That is exactly the question that **Multivariate Analysis** answers: a set of statistical techniques designed to study **multiple variables simultaneously**, discover hidden patterns, reduce data complexity and make better decisions.

In the real world, data almost never comes alone. A hospital records dozens of parameters per patient. A company analyses thousands of transactions with multiple attributes. A satellite captures images with hundreds of spectral bands. Multivariate Analysis is the tool to master that complexity.

---

## What techniques will you learn?

Throughout the course you will study the most powerful and widely used techniques in modern statistical analysis:

```{admonition} Dimensionality reduction techniques
:class: tip

- **Principal Component Analysis (PCA)**: summarises information from many variables into a few components without losing the essentials.
- **Factor Analysis**: discovers latent variables (not directly observed) that explain the data.
```

```{admonition} Classification and clustering techniques
:class: tip

- **Discriminant Analysis**: builds rules to classify new observations into predefined groups.
- **Cluster Analysis**: groups similar observations without knowing the groups in advance.
```

```{admonition} Techniques for relationships between variables
:class: tip

- **Multivariate Regression**: models the relationship between several response variables and several predictors.
- **Canonical Correlation Analysis**: studies the relationship between two sets of variables.
- **Structural Equation Models (SEM)**: combines factor analysis and regression to model complex relationships.
```

---

## What is it used for in practice?

The applications of Multivariate Analysis are everywhere:

| Sector | Application |
|---|---|
| 🏥 **Medicine** | Diagnosis by symptom groups, patient segmentation, biomarker analysis |
| 💹 **Finance** | Fraud detection, portfolio management, multidimensional risk analysis |
| 🤖 **Artificial Intelligence** | PCA as preprocessing for machine learning, data noise reduction |
| 🌍 **Environmental Sciences** | Pollutant analysis, climate profiles, ecosystem characterisation |
| 🏪 **Marketing** | Customer segmentation, preference analysis, product positioning |
| 🧬 **Biology / Genomics** | Gene classification, differential expression analysis, molecular profiles |
| 🏛️ **Social Sciences** | Index construction, survey analysis, opinion profiles |

---

## Why is it important for you?

If you study Statistics or Computer Engineering, Multivariate Analysis is one of the pillars of your training because:

- It is **essential** in data science and machine learning.
- It underpins techniques such as PCA, clustering and discriminant analysis applied with **R** in professional and research environments.
- It allows you to move from analysing **one variable** to analysing **the real world**, where everything is multidimensional.

---

## Working tool: R and RStudio

Throughout this manual we will use **R** as the statistical programming language and **RStudio** as the development environment. R is the de facto standard in academic and scientific statistics, and has a specialised ecosystem of packages for multivariate analysis:

| Package | Purpose |
|---|---|
| `FactoMineR` | PCA, Factor Analysis, Correspondence Analysis |
| `factoextra` | Visualisation of PCA and clustering results |
| `cluster` | Clustering algorithms (k-means, hierarchical, PAM) |
| `MASS` | Linear and Quadratic Discriminant Analysis |
| `lavaan` | Structural Equation Models (SEM) |
| `ggplot2` | High-quality data visualisation |
| `corrplot` | Visually appealing correlation matrices |

```{admonition} Goal of this manual
:class: important

This book is not just theory. Each technique is accompanied by **applied examples with R code**, visualisations and exercises so you can practise directly from RStudio and see the results in real time.
```

---

## PDF version

If you prefer to study in physical format or offline:

- [Download PDF in English](../_static/teachbook_en.pdf)
- [Descargar PDF en español](../_static/teachbook_es.pdf)
