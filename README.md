# 📊 YouTube India Trending Analysis using Python, SQL & Power BI

Analyze 78,000+ trending YouTube India videos to discover what drives content to trend — using Python for data cleaning, SQL for business logic, and Power BI for dashboard visualization.

---

## 📌 Project Overview

This project is developed as a **Data Analytics portfolio project**.

The objective of this project is to analyze YouTube India trending video data and identify the key factors that influence a video's performance — including upload timing, content category, engagement behaviour, and title optimization.

The project covers the complete Data Analytics workflow including:

- Data Collection
- Data Cleaning
- Feature Engineering
- Exploratory Data Analysis (EDA)
- SQL Business Analysis
- Dashboard Development
- Business Insight Generation

---

## 🎯 Problem Statement

Content creators and media teams need data-backed answers to three critical questions:

- **When** should a video be uploaded for maximum visibility?
- **Which** content categories deliver the best performance?
- **Does** high engagement actually translate into higher views?

The goal is to analyze historical trending data and build an executive dashboard that answers these questions with measurable insights.

---

## 📂 Dataset

**Dataset Name:**

YouTube Trending Video Dataset (India)

🔗 **Download Dataset:** https://www.kaggle.com/datasets/rsrishav/youtube-trending-video-dataset

**Dataset Details:**

| Attribute | Value |
|---|---|
| Region | India (IN) |
| Time Period | 2020 – 2024 |
| Total Records Analyzed | 78,821 videos |
| Total Categories | 14 |

**Features Used:**

- title
- channelTitle
- categoryId
- publishedAt
- trending_date
- view_count
- likes
- comment_count
- tags

**Derived Features Created:**

- engagement_rate
- days_to_trend
- publish_hour_IST
- title_length
- tags_count

> ⚠️ **Data Note:** 2024 records are partial (dataset collection ended mid-year). The decline shown in the yearly trend chart is a data coverage limitation, not an actual performance drop.

---

## 🛠 Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SQL (SQLite via pandasql)
- Power BI
- DAX
- Google Colab

---

## 📚 Project Workflow

### 1. Import Libraries

- Pandas
- NumPy
- Matplotlib
- Seaborn
- pandasql

### 2. Data Loading

- Load CSV dataset from Google Drive
- Load category mapping from JSON file
- Check dataset shape and column information

### 3. Data Cleaning

Performed the following preprocessing steps:

- Removed duplicate video entries
- Converted `trending_date` and `publishedAt` into datetime format
- Mapped `categoryId` to readable category names using JSON
- Removed records with missing category values
- Filtered invalid `days_to_trend` values

### 4. Feature Engineering

Created five new analytical columns:

| Feature | Formula |
|---|---|
| engagement_rate | `(likes + comments) / views × 100` |
| days_to_trend | `trending_date − publishedAt` |
| publish_hour_IST | UTC hour converted to IST (+5:30) |
| title_length | Character count of title |
| tags_count | Count of pipe-separated tags |

### 5. Exploratory Data Analysis (EDA)

Performed:

- Category Performance Analysis
- Engagement Rate Distribution
- Best Upload Hour Analysis
- Title Length Impact Analysis
- Trending Speed Analysis

### 6. SQL Business Analysis

Executed 7 analytical queries using advanced SQL:

| # | Query | SQL Technique |
|---|---|---|
| 1 | Category Performance Ranking | `RANK() OVER` |
| 2 | Best Upload Time Window | `CASE` binning |
| 3 | Consistent Top Channels | `HAVING`, aggregation |
| 4 | Engagement Tier Distribution | Subquery, percentage share |
| 5 | Title Length Optimization | Conditional bucketing |
| 6 | Year over Year Growth | `LAG() OVER` |
| 7 | Content Strategy Scorecard | CTEs + `NTILE(4)` + `RANK()` |

### 7. Dashboard Development

Built an interactive Power BI dashboard containing:

- 4 KPI Cards (Peak Year, Best Upload Window, Total Videos, Best Performing Category)
- Average Views by Category (Bar Chart)
- Best Upload Time Window (Column Chart)
- Engagement Distribution (Donut Chart)
- YouTube India Views Trend (Line Chart)
- Content Strategy Scorecard (Ranked Table with Conditional Formatting)

---

## 💡 Key Insights

### 1. Late Night uploads perform best

Videos uploaded between **12 AM – 6 AM IST** average **19.4 lakh views**, which is **63% higher** than afternoon uploads — despite having the lowest upload volume.

| Time Window | Total Videos | Avg Views |
|---|---|---|
| Late Night | 2,329 | 19,44,788 |
| Evening | 21,971 | 14,61,224 |
| Morning | 24,675 | 12,09,981 |
| Afternoon | 29,846 | 11,87,974 |

### 2. Science & Technology is the strongest overall category

It is the **only category ranking in the top quartile for both views and engagement**.

### 3. High views and high engagement rarely occur together

| Category | Avg Views | Engagement | Interpretation |
|---|---|---|---|
| Music | 19,56,834 | 8.25% | Maximum reach |
| Gaming | 10,54,363 | 10.45% | Loyal, active community |
| Entertainment | 13,07,070 | 4.41% | High volume, passive audience |

### 4. Shorter titles receive more views

Titles under 30 characters averaged **20.8 lakh views**, which is **71% higher** than titles over 70 characters.

### 5. 2022 was the peak performance year

Average views grew **+15.52%** in 2021 and **+3.31%** in 2022 before declining.

---

## 🔬 Methodology Highlights

### Sample Size Bias Handling

**Pets & Animals** initially ranked **#1** by average views (34 lakh) — but contained only **30 videos** compared to Entertainment's 33,798. A single viral video was distorting the entire average.

**Solution:** Categories with fewer than **100 trending videos** were excluded from all comparative rankings.

### Percentile-Based Scoring

Fixed thresholds were replaced with quartile-based classification using `NTILE(4)`:

```sql
NTILE(4) OVER (ORDER BY avg_views DESC)      AS views_quartile
NTILE(4) OVER (ORDER BY avg_engagement DESC) AS engagement_quartile
```

Both quartiles are summed into a **combined score (2–8)** that determines the strategy tier:

| Combined Score | Strategy Tier | Categories |
|---|---|---|
| 2 – 3 | High Priority | Science & Technology, Music, Comedy |
| 4 – 5 | Growth Potential | Film & Animation, Sports, People & Blogs, Gaming, Travel & Events |
| 6 | Stable | Entertainment, Education |
| 7 – 8 | Needs Improvement | News & Politics, Howto & Style, Autos & Vehicles |

**Advantage:** Thresholds are derived from the data itself and automatically adjust if the dataset is updated.

---

## 📸 Project Screenshots

### Power BI Dashboard

![Dashboard](screenshots/dashboard.png)

### Average Views by Category

![Category Views](screenshots/category_views.png)

### Engagement Rate by Category

![Engagement](screenshots/engagement_by_category.png)

### Best Upload Hour Analysis

![Upload Hour](screenshots/best_upload_hour.png)

### Title Length Impact

![Title Length](screenshots/title_length_impact.png)

### Trending Speed by Category

![Trending Speed](screenshots/trending_speed.png)

---

## 📁 Project Structure

```
YouTube_India_Trending_Analysis/
│
├── Notebooks/
│   ├── youtube_data_analysis.py
│   └── youtube_sql_analysis.py
│
├── SQL_Query/
│   ├── sql_q1_category_rank.csv
│   ├── sql_q2_upload_time.csv
│   ├── sql_q3_top_channels.csv
│   ├── sql_q4_engagement_tier.csv
│   ├── sql_q5_title_length.csv
│   ├── sql_q6_yearly_growth.csv
│   └── sql_q7_strategy.csv
│
├── Dashboard/
│   ├── Youtube_Dashboard.pbix
│   ├── YTDASHBOARD.pdf
│   └── youtube_clean_data.csv
│
├── Screenshots/
│   ├── dashboard.png
│   ├── category_views.png
│   ├── engagement_by_category.png
│   ├── best_upload_hour.png
│   ├── title_length_impact.png
│   └── trending_speed.png
│
└── README.md
```

---

## ▶️ How to Run

**1. Clone Repository**

```
git clone https://github.com/mohit-kanojiya/YouTube_India_Trending_Analysis.git
```

**2. Download Dataset**

Download `IN_youtube_trending_data.csv` and `IN_category_id.json` from the Kaggle link above and place them in your working directory.

**3. Install Dependencies**

```
pip install pandas numpy matplotlib seaborn pandasql
```

**4. Run Python Analysis**

```
python notebooks/youtube_data_analysis.py
python notebooks/youtube_sql_analysis.py
```

**5. Open Dashboard**

Open `dashboard/youtube_dashboard.pbix` in **Power BI Desktop**, or view the static export `dashboard/youtube_dashboard.pdf`.

---

## 🎯 Business Recommendations

1. **Prioritize Science & Technology, Music, and Comedy** — the only categories in the top performance tier
2. **Schedule uploads during late night IST hours** — 63% higher average views with lower competition
3. **Keep video titles under 30 characters** — measurably correlated with higher view counts
4. **Treat Gaming as a community strategy, not a reach strategy** — highest engagement but mid-tier views
5. **Reassess News & Politics investment** — lowest engagement rate (2.34%) and bottom-quartile views

---

## ⚠️ Limitations & Future Scope

| Limitation | Detail |
|---|---|
| Deduplication approach | Each video counted once at first trending appearance |
| Dislikes excluded | YouTube removed public dislike counts in December 2021 |
| Partial 2024 data | YoY decline reflects incomplete data coverage |
| Static dashboard | Future version will use a single fact table with star schema to enable slicers and cross-filtering |

---

## 👨‍💻 Author

**Mohit Kanojiya**

GitHub: https://github.com/mohit-kanojiya

---

⭐ If you found this project useful, don't forget to **Star** this repository.
