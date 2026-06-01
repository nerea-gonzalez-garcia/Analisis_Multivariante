# Análisis Multivariante

Bienvenido/a al manual interactivo de **Análisis Multivariante** de la Universidad de Salamanca.

Este libro está dirigido a los estudiantes del **Grado en Estadística** y de la **Doble Titulación en Estadística e Ingeniería Informática**, y es el material de apoyo oficial para la asignatura.

---

## ¿Qué es el Análisis Multivariante?

Imagina que quieres entender qué factores hacen que un estudiante tenga éxito académico. Tienes datos sobre sus horas de estudio, notas previas, asistencia, uso de recursos digitales, horas de sueño... Hay **muchas variables al mismo tiempo**. ¿Cómo las analizas de forma conjunta sin perder información?

Esa es exactamente la pregunta que responde el **Análisis Multivariante**: un conjunto de técnicas estadísticas diseñadas para estudiar **múltiples variables de forma simultánea**, descubrir patrones ocultos, reducir la complejidad de los datos y tomar mejores decisiones.

En el mundo real, los datos casi nunca vienen solos. Un hospital registra decenas de parámetros por paciente. Una empresa analiza miles de transacciones con múltiples atributos. Un satélite captura imágenes con cientos de bandas espectrales. El Análisis Multivariante es la herramienta para dominar esa complejidad.

---

## ¿Qué técnicas aprenderás?

A lo largo del curso estudiarás las técnicas más potentes y usadas del análisis estadístico moderno:

```{admonition} Técnicas de reducción de dimensionalidad
:class: tip

- **Análisis de Componentes Principales (PCA)**: resume la información de muchas variables en unas pocas componentes sin perder lo esencial.
- **Análisis Factorial**: descubre las variables latentes (no observadas directamente) que explican los datos.
```

```{admonition} Técnicas de clasificación y agrupamiento
:class: tip

- **Análisis Discriminante**: construye reglas para clasificar nuevas observaciones en grupos ya definidos.
- **Análisis de Clúster (Clustering)**: agrupa observaciones similares sin conocer los grupos de antemano.
```

```{admonition} Técnicas para relaciones entre variables
:class: tip

- **Regresión Multivariante**: modela la relación entre varias variables respuesta y varias predictoras.
- **Análisis de Correlación Canónica**: estudia la relación entre dos conjuntos de variables.
- **Modelos de Ecuaciones Estructurales (SEM)**: combina análisis factorial y regresión para modelar relaciones complejas.
```

---

## ¿Para qué sirve en la práctica?

Las aplicaciones del Análisis Multivariante están en todas partes:

| Sector | Aplicación |
|---|---|
| 🏥 **Medicina** | Diagnóstico por grupos de síntomas, segmentación de pacientes, análisis de biomarcadores |
| 💹 **Finanzas** | Detección de fraude, gestión de carteras, análisis de riesgo multidimensional |
| 🤖 **Inteligencia Artificial** | PCA como preprocesado para machine learning, reducción de ruido en datos |
| 🌍 **Ciencias Ambientales** | Análisis de contaminantes, perfiles climáticos, caracterización de ecosistemas |
| 🏪 **Marketing** | Segmentación de clientes, análisis de preferencias, posicionamiento de productos |
| 🧬 **Biología / Genómica** | Clasificación de genes, análisis de expresión diferencial, perfiles moleculares |
| 🏛️ **Ciencias Sociales** | Construcción de índices, análisis de encuestas, perfiles de opinión |

---

## ¿Por qué es importante para ti?

Si estudias Estadística o Ingeniería Informática, el Análisis Multivariante es uno de los pilares de tu formación porque:

- Es **imprescindible** en ciencia de datos y machine learning.
- Está en la base de técnicas como PCA, clustering y análisis discriminante que se aplican con **R** en entornos profesionales y de investigación.
- Te permite pasar de analizar **una variable** a analizar **el mundo real**, donde todo es multidimensional.

---

## Herramienta de trabajo: R y RStudio

A lo largo de este manual utilizaremos **R** como lenguaje de programación estadística y **RStudio** como entorno de desarrollo. R es el estándar de facto en estadística académica y científica, y cuenta con un ecosistema de paquetes especializados en análisis multivariante:

| Paquete | Para qué se usa |
|---|---|
| `FactoMineR` | PCA, Análisis Factorial, Análisis de Correspondencias |
| `factoextra` | Visualización de resultados de PCA y clustering |
| `cluster` | Algoritmos de clustering (k-means, jerárquico, PAM) |
| `MASS` | Análisis Discriminante Lineal y Cuadrático |
| `lavaan` | Modelos de Ecuaciones Estructurales (SEM) |
| `ggplot2` | Visualización de datos de alta calidad |
| `corrplot` | Matrices de correlación visualmente atractivas |

```{admonition} Objetivo de este manual
:class: important

Este libro no es solo teoría. Cada técnica viene acompañada de **ejemplos aplicados con código R**, visualizaciones y ejercicios para que puedas practicar directamente desde RStudio y ver los resultados en tiempo real.
```

---

## Versión PDF

Si prefieres estudiar en formato físico o sin conexión:

- [Descargar PDF en español](../_static/teachbook_es.pdf)
- [Download PDF in English](../_static/teachbook_en.pdf)
