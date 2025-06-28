# 🧠 SKU-Matching ML Service

A production-ready machine learning microservice for matching messy retail SKU listings to canonical IDs. Built to power real-time dynamic pricing and bundling strategies.

---

## 📑 Table of Contents
- [Overview](#overview)
- [Problem](#problem)
- [Solution](#solution)
- [Technologies Used](#technologies-used)
- [Architecture](#architecture)
- [Key Outcomes](#key-outcomes)
- [Timeline](#timeline)
- [Long-term Impact](#long-term-impact)
- [My Role](#my-role)

---

## Overview

This ML service ingests raw, duplicate-heavy retail item listings and returns the matched canonical SKU ID using a hybrid of LightGBM classification and fastText-based semantic embeddings. The system includes real-time API access, caching, and a human-in-the-loop verification mechanism during early-stage training.

---

## Problem

Retail datasets often include massive amounts of:
- Duplicated SKUs with inconsistent naming
- Vendor-specific spelling, abbreviations, or formatting
- Noisy entries in local food & beverage inventories

Our dataset contained over **6 million items**, many of which were repeated with variations.

Manual cleanup at this scale was inefficient and error-prone.

---

## Solution

We built a **FastAPI-based service** that leverages:
- **fastText embeddings** to convert item names to vectors
- A **LightGBM classifier** trained on pairwise similarity scores
- **Similarity thresholding (80%)** to flag near-matches
- A **human-in-the-loop review** system for early training refinement
- **Redis caching** to accelerate inference
- Scheduled retraining via **Airflow**

---

## Technologies Used

- **Python**
- **LightGBM**
- **fastText**
- **FastAPI**
- **Redis**
- **Docker**
- **Airflow**

---

## Architecture

```text
+--------------------------+
|  External SKU Listings   |
+------------+-------------+
             |
             v
+--------------------------+
|   fastText Embedding     |
+------------+-------------+
             |
             v
+--------------------------+
| LightGBM Similarity Model|
+------------+-------------+
             |
             v
+--------------------------+
| Similarity > 80% ?       |
+------Yes------+---No-----+
|               |          
v               v
Manual Review   No Match
   |              
   v
Model Retraining (via Airflow)
```

---

## Key Outcomes

- 💥 **Manual data-cleaning reduced by 85%**
- ⚡ **Search latency decreased by 30%**
- 🧠 **Enabled 5+ new recommendation features**
  - Dynamic pricing
  - Smart bundling
  - Cross-vendor mapping
  - Input sanitization for dashboards
  - Real-time suggestion in sales tools

---

## Timeline

- 6-week proof of concept
- Production-ready by **week 10**

---

## Long-term Impact

This service now **powers pricing and bundle suggestions** across the product suite. It is a foundational tool for enabling real-time personalization and operational efficiency.

---

## My Role

I led this project as the **Product Manager**, collaborating with a team of data scientists.

- Initiated the project based on repeated internal pain points
- Designed the human-in-the-loop feedback loop
- Defined success metrics and MVP cutoffs
- Aligned stakeholders and oversaw model iteration cycles
