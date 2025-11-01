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

