# RNA Associations Clustering Analysis

##  Overview

This project implements an **end-to-end unsupervised learning pipeline** to analyze and segment associations registered in the **Répertoire National des Associations (RNA)**.

The objective is to identify **homogeneous typologies of active associations** based on their **activity domain, territorial location, and urban context**, using clustering techniques.  
The results are designed to support **public-sector analytics**, territorial studies, and data-driven decision-making.

---

##  Project Objectives

- Segment active associations into meaningful clusters
- Capture structural differences related to:
  - Activity (objet social / objet parent)
  - Commune and urban unit characteristics
  - Urban vs rural environments
- Provide **interpretable cluster profiles** suitable for:
  - Policy analysis
  - Territorial diagnostics
  - Research and academic use

This project is **exploratory and descriptive** in nature and does not aim to predict future outcomes.

---

## 🗂️ Data Sources

### Répertoire National des Associations (RNA)

The RNA is the official French administrative registry of associations, maintained by the French government.

- Platform: data.gouv.fr  
- Dataset: *Répertoire National des Associations*  
- URL: https://www.data.gouv.fr/fr/datasets/repertoire-national-des-associations/

The dataset includes information on:
- Legal identity and status of associations
- Activity classification
- Geographic localization
- Lifecycle dates (creation, publication, dissolution)

---

##  Data Warehouse Context

The RNA data is integrated into a **SQL Server data warehouse (DW_Asso)** using a star schema architecture.


The project assumes **read-only access** to a pre-existing structured data warehouse.

---

##  Technologies & Tools

- **Python 3**
- **SQL Server** (via `pyodbc`)
- **pandas**, **numpy**
- **scikit-learn**
  - K-Means
  - Silhouette Score
  - PCA
- **matplotlib**, **seaborn**

---

##  Methodology

### 1. Data Extraction
- SQL query joining fact and dimension tables
- Association-level dataset with activity, geography, and lifecycle attributes

### 2. Data Cleaning
- Deduplication by association title
- Removal of rows with missing critical fields
- Exclusion of dissolved associations (`position = 'D'`)

### 3. Feature Engineering
- Computation of association age (in years)
- Encoding of urban status
- Use of urban unit size as a structural territorial feature

### 4. Sampling
- Random sample of 50,000 associations
- Ensures computational feasibility while preserving diversity

### 5. Feature Selection
- Activity code (`objet_social`)
- Urban unit size (`taille_unite_urbaine`)
- Urban status (encoded)
- Commune name (top 200 most frequent, others grouped)

### 6. Encoding & Scaling
- One-Hot Encoding for commune names
- Standard scaling of numerical variables

### 7. Clustering
- K-Means clustering
- Optimal number of clusters selected using silhouette analysis
- Final model uses **11 clusters**

### 8. Visualization
- PCA used for 2D visualization of cluster structure
- Scatter plots to assess separation and overlap

### 9. Cluster Profiling
Each cluster is described using:
- Percentage of total associations
- Dominant activity (objet parent)
- Urban unit statistics (mean / median)
- Urban vs rural distribution
- Most frequent communes
- Lifecycle indicators (mean / median age)

---

## 📊 Key Outcomes

- Identification of **11 interpretable association typologies**
- Clear distinction between:
  - Rural vs urban associations
  - Sports vs cultural, educational, and community activities
  - Long-established vs recently created organizations
- Strong relationship between **territorial context and association lifecycle**

Clusters are manually labeled to ensure **interpretability and policy relevance**.



