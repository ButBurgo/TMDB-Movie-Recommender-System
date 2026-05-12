# TMDB 5000 Movie Dataset Title Recommendation System

This project was developed for the **Massive Data Mining** exam at the **University of Salerno** (Master's Degree in Data Science and Innovation Management). 

## Exam Assignment
The task required the development of a recommendation system based on the [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata/). 
**Requirement:** Given a movie title (even if approximate) or a simple descriptive string, the system must return the top 10 most relevant candidates found in the dataset.

## Project Overview
The system provides a robust search experience by comparing traditional string matching with modern deep learning techniques. It identifies the most effective way to retrieve films based on different types of user queries.

### Key Features
* **Fuzzy Search:** Handles typos and partial titles using Levenshtein distance through the `TheFuzz` library.
* **Semantic Search:** Understands the "meaning" of descriptive queries using the `all-mpnet-base-v2` transformer model.
* **Adaptive Scoring:** A weighted system that switches priorities between title matching and semantic relevance based on query type.
* **Bonus Weights:** Extra points are awarded for results matching specific actors or genres mentioned explicitly in the query.

## Repository Structure
The project is organized into two main notebooks to separate the analytical phase from the implementation phase:

* **`EDA.ipynb`**: Contains the complete Exploratory Data Analysis, visualizations, and statistical insights of the TMDB dataset.
* **`Main.ipynb`**: Contains the core logic of the recommendation system, the encoding process, the search functions, and the final validation.
* **`environment.yml` / `requirements.txt`**: Configuration files for environment reproducibility.
* **`data/`**: Directory containing the `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv` files.

## Tech Stack
* **Language:** Python 3.10.20
* **Data Processing:** `pandas`, `numpy`, `ast`
* **NLP & AI:**
    * `sentence-transformers`: Using the **all-mpnet-base-v2** model.
    * `thefuzz`: For Levenshtein-based string matching.
    * `scikit-learn`: For calculating **Cosine Similarity**.
* **Visualization:** `matplotlib`, `seaborn`, `plotly.express`, `collections.Counter`.

## EDA Highlights (from `EDA.ipynb`)
* **Market Trends:** Strong positive correlation (0.71) between budget and revenue.
* **Profitability:** Documentaries, Music, and Horror genres yield the highest **Return on Investment (ROI)**.
* **Industry Data:** USA leads production with 2,906 films; Robert De Niro is the most frequent actor (45 films).

## Methodology
The system operates in two main modes defined in `Main.ipynb`:
1.  **Title Mode:** Prioritizes string similarity when a query closely matches an existing title (Threshold > 0.65).
2.  **Descriptive Mode:** Prioritizes semantic meaning (Cosine Similarity) for conceptual queries.

## Validation Results
The models were evaluated using **Mean Reciprocal Rank (MRR)** and **Hit@K** metrics across 25 test queries.

| Metric | Fuzzy Matching (Winner) | Cosine Similarity |
| :--- | :---: | :---: |
| **MRR** | **0.8247** | 0.7536 |
| **Hit@1** | **0.76** | 0.72 |
| **Hit@5** | **0.96** | 0.80 |
| **Hit@10** | **1.00** | 0.84 |

## Installation & Usage

### Using Conda (Recommended)
```bash
conda env create -f environment.yml
conda activate movie-recommender
```

### Using Pip
```bash
pip install -r requirements.txt
```

## Author
* **Name:** Bruno Maria Di Maio
* **Academic Year:** 2026