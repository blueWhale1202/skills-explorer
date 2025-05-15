# 🧠 HIRELENS

A web-based platform to **analyze and visualize in-demand job skills** across thousands of job descriptions from online recruitment sites.

> Supports **multi-filter queries** by job title, location, seniority level, and posting date. Returns **ranked skills** with real-time frequency analysis.

---

## 📊 Features

* 🔍 **Search by job title** (e.g. `Backend Developer`)
* 🎯 **Filter by**:

  * Experience level: `Intern`, `Junior`, `Senior`, etc.
  * Location: `Ho Chi Minh City`, `Hanoi`, etc.
  * Updated date: Filter job postings by recency (e.g., after `2025-01-01`)
  * Skill type:

    * **Soft Skills** (e.g. `Communication`, `Teamwork`)
    * **Technical Skills** (e.g. `Python`, `SQL`, `AWS`)
* 📈 **Get skill frequency** (e.g. `Python - 84.3%` of matched jobs)
* ⚡ Handles **big data** (over **1 million** job descriptions)

---

## 📂 How It Works

1. **Normalize user intent** using `keyword_alias` to map search input to canonical job words.
2. **Filter** by `location`, `seniority_level`, and `posted_date` (default: last 6 months).
3. **Match jobs** using a 3-tier strategy:

   * Full-text search on canonical `job_word`
   * Fallback full-text search on raw user input
   * Fuzzy match on tokenized job title (similarity ≥ 0.3)
4. **Aggregate and compute** skill frequency based on matched jobs.

---

## 🧰 Tech Stack

| Component       | Technology                  |
| --------------- | --------------------------- |
| Framework       | **Next.js 15 (App Router)** |
| Client Fetching | TanStack Query              |
| Database        | PostgreSQL (Raw SQL)        |
| Caching         | Redis                       |
| Validation      | Zod                         |
| UI Framework    | Tailwind CSS, shadcn/ui     |

---

## ✨ Example Query Output

* **Search**: `Data`
* **Filter**: `4 levels`, `2 locations`, `Updated after: 2024-11-15`
* **Result**: `Matched 911 jobs`, `Top Skills:`

  * `Analytical skills (Soft)` - 90.8%
  * `SQL (Technical)` - 84.4%
  * `Python (Technical)` - 84.3%
  * `Teamwork (Soft)` - 51.3%

---

## 🚀 Performance Note

* Optimized for **large-scale data** (1M+ rows) using materialized views and indexed full-text search.
* Redis caching is applied to first-page queries for **faster retrieval** (TTL: 30 minutes).

---

## 📅 Last Updated

* **Data last updated**: `15/05/2025`
* **Query time sample**: `~492ms`

---

## 🚀 Future Roadmap

### 🔍 Search Optimization

* **Scalable Infrastructure**: As data volume grows, transition backend processing to distributed systems such as **Apache Spark**, **Hadoop**, or adopt **cloud-native data pipelines** to ensure high-throughput analytics.
* **Smarter Search Engine**: Replace PostgreSQL-based fuzzy search with **semantic search technologies** like **Elasticsearch** or **Vector DBs**, enabling faster, context-aware, and scalable matching of job titles and user queries.

### 🌱 Feature Expansion

* **CV Skill Gap Analyzer**: Empower users to upload their CVs and select a desired job role. The system will **analyze current skill sets**, compare them with market demands, and **highlight missing or underdeveloped skills**.
* **Smart Career Suggestions**: For users without a defined target role, the platform will **analyze their CVs** and provide **personalized career path recommendations** based on their existing skills and market trends.
