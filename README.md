# 🧭 Travel Review Clustering using Hierarchical Clustering

Unsupervised machine-learning project that groups travellers into clusters based on the average ratings they gave to **24 categories of tourist places** (churches, beaches, parks, museums, restaurants, gyms, etc.) using **Agglomerative (Hierarchical) Clustering with Ward linkage**.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-orange)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Dataset](#-dataset)
3. [Tech Stack](#-tech-stack)
4. [Project Structure](#-project-structure)
5. [Workflow](#-workflow)
6. [Key Results](#-key-results)
7. [Installation & Usage](#-installation--usage)
8. [Limitations & Future Work](#-limitations--future-work)
9. [Author](#-author)

---

## 📖 Project Overview

Travel platforms collect ratings from thousands of users. This project explores whether those users naturally fall into distinct groups according to *how they rate* different place categories. The notebook:

- cleans and prepares the Google review ratings data,
- explores rating behaviour with visualisations,
- builds a **dendrogram** to decide the number of clusters,
- fits an **Agglomerative Clustering** model (Ward linkage, Euclidean distance),
- visualises the resulting clusters with a pair plot.

## 📂 Dataset

- **Source:** Google Reviews Ratings dataset (UCI Machine Learning Repository – *Travel Review Ratings / Google reviews*).
- **File:** `google_review_ratings.csv` (place it in the project root; it is not included in this repo).
- **Size:** 5,456 users × 26 columns (25 after dropping a redundant empty column).

| Column | Description |
|---|---|
| `User` | Unique user id |
| `Category 1 … Category 24` | Average rating given by the user to a category (churches, resorts, beaches, parks, theatres, museums, malls, zoo, restaurants, pubs/bars, local services, burger/pizza shops, hotels/lodgings, juice bars, art galleries, dance clubs, swimming pools, gyms, bakeries, beauty & spas, cafes, view points, monuments, gardens) |
| `Unnamed: 25` | Empty column – dropped |

## 🛠 Tech Stack

- **Language:** Python 3
- **Libraries:** pandas, NumPy, Matplotlib, Seaborn, SciPy, scikit-learn
- **Environment:** Jupyter Notebook

## 🗂 Project Structure

```
travel-review-clustering/
│
├── Hierarchical_Clustering_Travel_Review_Clustering.ipynb   # Main notebook
├── google_review_ratings.csv                                # Dataset (add yourself)
├── images/                                                  # Output figures
│   ├── hist.png
│   ├── reviews_per_cat.png
│   ├── cats_vs_reviews.png
│   ├── avg_rating.png
│   ├── dendrogram.png
│   ├── dendrogram_cut.png
│   └── pairplot_small.jpg
├── requirements.txt
├── .gitignore
└── README.md
```

## 🔄 Workflow

1. **Import packages** – pandas, numpy, matplotlib, seaborn.
2. **Read data** – load `google_review_ratings.csv`.
3. **Data types & dimensions** – inspect `info()` and `shape` (5456 × 26).
4. **Data manipulation** – drop `Unnamed: 25`, rename columns to meaningful names, fix the invalid `local_services` value (`'2\t2.'`) and convert it to numeric.
5. **Statistical summary** – `describe()` for numeric and categorical features.
6. **Missing values** – fill the few missing values with the column mean.
7. **Exploratory Data Analysis** – histograms, reviews per category, categories rated per user, average rating per category.
8. **Hierarchical clustering** – Ward linkage → dendrogram → choose cut-off (`max_d = 80000`) → `AgglomerativeClustering(n_clusters=2)`.
9. **Visualise & conclude** – pair plot coloured by cluster; clusters mapped to labels.

## 📊 Key Results

- All **11 categories** (parks, theatres, museums, malls, zoo, restaurants, pubs/bars, local services, burger/pizza shops, hotels/lodgings, juice bars) were rated by every user (minimum rating > 0).
- ~**3,725 users** rated all 24 categories; the minimum number of categories rated by a user is **15**.
- Lowest average ratings: **gyms (~0.82), swimming pools (~0.95), cafes (~0.97), bakeries (~0.97)**.
- The dendrogram (cut at height 80,000) suggests **2 clusters**.

### Sample Figures

| Dendrogram with cut-off | Average rating per category |
|---|---|
| ![dendrogram](images/dendrogram_cut.png) | ![avg](images/avg_rating.png) |

## ⚙️ Installation & Usage

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/travel-review-clustering.git
cd travel-review-clustering

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add the dataset
#    Download google_review_ratings.csv and place it in the project folder

# 5. Launch the notebook
jupyter notebook Hierarchical_Clustering_Travel_Review_Clustering.ipynb
```

**`requirements.txt`**
```
pandas
numpy
matplotlib
seaborn
scipy
scikit-learn
jupyter
```

## ⚠️ Limitations & Future Work

- Features were **not scaled** before clustering; applying `StandardScaler` could change results.
- The derived `id` column is currently part of the feature set passed to the model; it should be excluded since it is an identifier, not a rating.
- The final labels *Positive / Negative* are an interpretation of the two clusters – verify by comparing the cluster-wise mean ratings.
- Evaluate cluster quality with **silhouette score**, and compare with **K-Means / DBSCAN**.
- Build a **recommender system** for users who rated fewer categories.

---
⭐ If you found this project useful, please give it a star!
