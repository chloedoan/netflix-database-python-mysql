
# 📊 Netflix SQL & Python Analysis

This project explores Netflix’s content library using a combination of SQL and Python data processing. It focuses on extracting business insights from a cleaned and normalized version of the original Netflix dataset, further enriched with external IMDb ratings data.

Tableau Dashboard Link: https://public.tableau.com/app/profile/chloe.doan/viz/Netflix_17516218459510/overview

---

## 🗃️ Dataset Overview

The dataset has been processed and split into multiple normalized tables:

- **titles**: Central table containing metadata for each show (e.g., `show_id`, `title`, `type`, `duration`, `date_added`).
- **director**: Names of directors linked by `show_id`.
- **country_cleaned**: Cleaned country data for each title.
- **listed_in**: Genre or category information (e.g., "Comedy", "International Movies").
- **rating_description**: Descriptions and explanations of rating labels.

All tables are connected through the `show_id` field, except for `rating_description` which links through the `rating` field to `titles`.

---

## 📁 Tableau Dashboard

### 🛠️ Tableau Public Link: 

[Netflix Analysis](https://public.tableau.com/app/profile/chloe.doan/viz/Netflix_17516218459510/overview)

### 🔍 Overview
<img width="1383" height="822" alt="Screenshot 2025-07-27 at 8 24 46 AM" src="https://github.com/user-attachments/assets/535ea6ca-c67b-4541-a6c3-e01509ee8139" />

#### Key Insights

- **Total Titles**: 8,807 Netflix releases (as of Sep 25, 2021)
  - 📈 2,020 titles added between Sep 2020 – Sep 2021
- **Top Producing Country**: 🇺🇸 United States with 3,690 titles
- **Most Released Genre**: 🌍 *International* – 4,103 titles
- **Top Director**: 🎬 Rajiv Chilaka – 22 titles
- **Release Year Trends**:
  - Peak in **2019** with **1,628** new releases
  - Significant growth from 2015 to 2019
- **Average Duration Trends**:
  - 🎞️ Movies peaked at ~206 mins around 1965, then declined gradually
  - 📺 TV Shows hit highest average (~9.3 seasons) in early 1990s
- **Global Reach**:
  - Strong content contributions from North America, Europe, and South Asia (visualized via world map)

### 🧾 Type

<img width="1376" height="820" alt="Screenshot 2025-07-27 at 8 27 02 AM" src="https://github.com/user-attachments/assets/ada383c9-7321-4c8b-8c4c-82f1421acbe8" />

<div align="center">
<img width="757" height="268" alt="Screenshot 2025-07-27 at 8 27 44 AM" src="https://github.com/user-attachments/assets/04a56637-f53e-4a8a-8aad-be630e3fc216" />
</div>

#### Key Insights

- **Growth by Type**:  
  - Steady increase in both **movies** and **TV shows** since 2015, with movies dominating until 2021.
  - By 2021, TV shows accounted for **53%** of new releases (a shift from only 17% in 2008).

- **Content Suitability**:
  - Majority of titles are **not suitable for children**:
    - Top ratings include **TV-MA**, **TV-14**, and **R**, making up the largest share.
  - Content for children (e.g. TV-Y, G, PG) forms a much smaller portion.

- **Top IMDb Titles (Weighted)**:
  - Includes classics like *The Lord of the Rings*, *Inception*, *Pulp Fiction*, *Schindler’s List*.
  - Weighted score method used to highlight high-rating + high-vote films.

- **Top IMDb Titles (Raw)**:
  - Best-rated based on raw IMDb score (e.g., *Everybody Knows*, *The CEO*, *Lens*) — with scores up to **9.7/10**.

- **Example Highlighted Title**:
  - *1 Mile to You* (TV-14, Drama/Romantic/Sports), directed by Leif Tilden, with a score of **6.3/10** based on 2,918 votes.

### 📽️ Genre

<img width="1381" height="817" alt="Screenshot 2025-07-27 at 8 28 01 AM" src="https://github.com/user-attachments/assets/65bdc9ba-db70-4aa1-93ba-799dba298810" />

<img width="1034" height="284" alt="Screenshot 2025-07-27 at 8 28 12 AM" src="https://github.com/user-attachments/assets/8691e8b9-1e1b-4cb3-a56c-1b8be5ca8a25" />

#### Key Insights

- **Releases by Type**  
  - Movies consistently dominate over TV shows across all genres.  
  - The donut chart highlights a strong preference for **movie** releases on Netflix.

- **Releases by Country**  
  - The **United States** leads significantly in total content production.  
  - Other top countries include **Canada**, **India**, and the **United Kingdom**.

- **IMDb Ratings**  
  - Highest-rated content categories include **Children & Family**, **Reality TV**, and **International**.  
  - Average IMDb scores generally range between **6.0 and 7.5**, with some subgenres exceeding that.

- **Release Volume Over Time (2008–2021)**  
  - Sharp growth in releases started around **2015**.  
  - **International**, **Dramas**, and **Comedies** consistently top the yearly release counts.

- **Genre Evolution**  
  - **International** content remained dominant across all years.  
  - Mid-tier genres like **Action & Adventure** and **Romantic** fluctuated in popularity after 2017.

---

## 📁 Python Data Enrichment (IMDb Integration)

To enrich the Netflix dataset with **average user ratings** and **number of votes**, a Python data pipeline was developed using IMDb’s non-commercial datasets. 

### 🔗 Data Sources

- **[Netflix Movies and TV Shows on Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)**  

- **[IMDb Non-Commercial Datasets](https://datasets.imdbws.com/)**  
   
  - `title.akas.tsv.gz`: Localized and alternative titles.
  - `title.basics.tsv.gz`: Title types, start years, genres.
  - `title.ratings.tsv.gz`: Average ratings and number of votes.

### 🛠️ Python Processing Steps

- Joined IMDb files on `tconst` to compile a dataset with:
  - Primary title
  - Average rating
  - Number of votes
- Matched IMDb titles to Netflix titles to attach ratings information.
- Produced a final enriched dataset with:
  - `show_id` (from Netflix)
  - `title` (from Netflix)
  - `averageRating` (from IMDb)
  - `numVotes` (from IMDb)

This dataset will be used in Tableau for advanced visualization, such as comparing Netflix content by popularity and rating metrics.

---

## 📈 Key Analyses

The combined SQL + Python dataset allows us to answer key business and strategic questions, including:

- **Top Countries & Directors**: Identifies the countries and directors with the highest number of releases on the platform.
- **Genre Duration Trends**: Analyzes average duration of movies across different genres.
- **Seasonal Release Patterns**: Examines how release volumes vary by month and genre, to identify optimal release timings.
- **Market Segmentation**: Breaks down releases by content type and country for a detailed market view.
- **User Ratings Insights** *(via Python integration)*: Highlights the highest-rated Netflix content and correlates user engagement metrics.

---

## 💡 Purpose

This combined analysis can help content strategists and data analysts:

- Understand regional and genre trends on Netflix.
- Optimize content planning based on seasonal and categorical data.
- Gain insight into director and country contributions to Netflix’s library.
- Leverage user rating data for quality-focused content decisions.

---

## 🛠️ Tools

- **MySQL Workbench** – Writing and testing SQL queries
- **Python (Pandas, NumPy)** – Data cleaning and integration with IMDb ratings
- **Tableau Public** – For visualizations and dashboards (not included in this repo)

---

## 📁 Contents

- `Databse_queries`: SQL file containing all queries used for analysis
- `create_table`: SQL file containing the original dataset
- `dim_tables`: SQL file containing dimension tables after extraction
- `final_table`: SQL file containing the final joined table
- `imdb_merge.ipynb`: Jupyter notebook for Python data enrichment with IMDb
- `README.md`: Project overview and documentation

---

---
📬 Contact

Author: Chloe Doan
Email: lqchloe.doan@gmail.com 
Portfolio Repository: [GitHub Link](https://github.com/chloedoan/netflix-database-mysql)

