# 📊 Social Media Trend Shift Analysis

### 🔍 Overview
This project analyzes **how social media trends evolve over time** — identifying spikes in activity, emerging hashtags, and shifts in platform engagement.  
It integrates **multi-platform datasets** using SQL and Python, performs **time-series and content trend analysis**, and visualizes **platform market share and audience behavior**.

---

## 🚀 Key Objectives
- Detect **trend shifts** and **spike events** across multiple social media platforms.  
- Analyze **daily and monthly posting behavior** using time-series techniques.  
- Identify **emerging and declining hashtags** based on frequency growth rates.  
- Evaluate **platform popularity** and **engagement metrics** (likes, retweets, etc.).  
- Visualize results using interactive and statistical plots.

---

## 🧰 Tools & Technologies
| Category | Tools Used |
|-----------|-------------|
| Programming | Python (Pandas, NumPy) |
| Visualization | Matplotlib, Seaborn, WordCloud |
| Database | MySQL |
| Environment | Jupyter Notebook |
| File Formats | CSV, SQL |

---

## 🗂️ Datasets Used
1. **Book1.csv** — General multi-platform social media data.  
2. **Tweets.csv** — Twitter-specific engagement data (likes, retweets).  
3. **Viral_Social_Media_Trends.csv** — Aggregated viral trends across platforms.  
4. **social_media.sql** — SQL queries used for joins and data exploration.

---

## 🧹 Data Preparation
Performed comprehensive data cleaning and transformation steps:
- `pd.to_datetime()` — Converted timestamps to datetime objects.  
- `dropna()`, `fillna()` — Removed or filled missing values.  
- `str.lower()`, `explode()` — Normalized text and expanded hashtags.  
- Merged datasets using `pd.concat()` into a **master DataFrame**.  
- Extracted date-based features: Year, Month, Day, Hour.

---

## 📈 Exploratory Data Analysis (EDA)

### 1️⃣ Activity Timeline & Spike Detection
- Resampled posts daily with `.resample('D')`.  
- Applied 7-day moving average (`rolling(window=7)`).  
- Detected spikes using **Z-score analysis**.  
- Visualized daily trends and spike markers.

```python
daily = df.set_index("Timestamp").resample("D").size()
daily_ma7 = daily.rolling(7).mean()
zscore = (daily - daily.mean()) / daily.std()
plt.plot(daily_ma7)

2️⃣ Platform Popularity & Growth

Compared posting activity by platform using groupby('Platform').

Visualized total counts and growth using bar plots.

platform_counts = df["Platform"].value_counts()
sns.barplot(x=platform_counts.index, y=platform_counts.values)

3️⃣ Market Share Analysis

Computed each platform’s monthly share of total posts.

Visualized trend shifts with stacked area charts.

monthly = df.set_index("Timestamp").groupby("Platform").resample("ME").size().reset_index()
monthly["share_%"] = monthly["posts"] / monthly.groupby("Timestamp")["posts"].transform("sum") * 100

4️⃣ Hashtag Trend Analysis

Extracted hashtags using .str.split().explode().

Identified top 20 hashtags and growth percentage month-over-month.

Created bar charts and word clouds.

tags = df["Hashtags"].dropna().str.lower().str.split().explode()
tag_counts = tags.value_counts().head(20)
sns.barplot(y=tag_counts.index, x=tag_counts.values)

5️⃣ Engagement Dynamics

Compared average Likes, Retweets, Comments per platform.

Visualized engagement trends over time.

engagement = df.groupby("Platform")[["Likes", "Retweets"]].mean()
sns.barplot(x=engagement.index, y=engagement["Likes"])

6️⃣ Correlation Insights

Calculated correlations between engagement metrics.

Visualized results using a heatmap.

corr = df[["Likes", "Retweets", "Comments"]].corr()
sns.heatmap(corr, annot=True, cmap="coolwarm")

💡 Key Insights

Detected major activity spikes aligned with viral events.

Found that Twitter showed consistent engagement compared to volatile platforms.

Identified emerging hashtags with rapid growth.

Discovered strong correlation between likes and retweets, indicating virality.

📊 Visualization Highlights

Line plots with 7-day smoothing

Stacked area charts for platform share

WordClouds for hashtag prominence

Heatmaps for correlation insights

📚 Learnings & Outcomes

Gained expertise in time-series data analysis using Pandas.

Improved SQL-to-Python data integration.

Enhanced data visualization and storytelling skills.

Built strong understanding of trend detection and growth analytics.

🧠 Future Enhancements

Add NLP-based sentiment analysis.

Implement trend forecasting using ARIMA/Prophet models.

Deploy an interactive dashboard using Streamlit or Power BI.
