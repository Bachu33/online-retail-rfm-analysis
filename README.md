# 🛒 Online Retail RFM Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Bachu33/online-retail-rfm-analysis/blob/main/rfm.ipynb)

A customer segmentation project using **Recency-Frequency-Monetary (RFM)** analysis on the UCI Online Retail dataset. Built in Google Colab, customers are scored across three behavioural dimensions and grouped into actionable business segments.

---

## 📌 Project Overview

**RFM analysis** is a proven marketing technique that ranks customers based on three key behaviours:

| Dimension | Description |
|---|---|
| **Recency (R)** | How recently did the customer make a purchase? |
| **Frequency (F)** | How often do they buy? |
| **Monetary (M)** | How much do they spend in total? |

Each customer receives a score from **1 (worst) to 5 (best)** on each dimension, which are then combined to assign them to a meaningful business segment.

---

## 📂 Dataset

- **Source:** [UCI Machine Learning Repository – Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail)
- **Description:** Transactional data from a UK-based online retail company (Dec 2010 – Dec 2011)
- **Records:** ~541,000 rows before cleaning
- **Key columns:** `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, `Country`

---

## 🔧 Methodology

### 1. Data Cleaning
- Removed rows with missing `CustomerID` (~25% of data)
- Dropped cancellation orders (invoices starting with `C`)
- Removed negative quantities and zero/negative unit prices
- Removed duplicate rows
- Converted `InvoiceDate` to datetime and `CustomerID` to integer

### 2. Feature Engineering
- `TotalPrice = Quantity × UnitPrice` computed per line item

### 3. RFM Calculation
- **Recency:** Days since a customer's last purchase (relative to the day after the final transaction)
- **Frequency:** Number of unique invoices per customer
- **Monetary:** Total spend per customer

### 4. Scoring
- Each dimension is split into quintiles (1–5) using `pd.qcut`
- Recency is scored inversely (lower days = higher score)
- Ties in Frequency and Monetary are broken using rank-based quantile cuts

### 5. Segmentation
Customers are assigned to one of **8 segments** based on their R, F, and M scores:

| Segment | Criteria | Business Interpretation |
|---|---|---|
| **Champions** | R≥4, F≥4, M≥4 | Best customers — reward and retain |
| **Loyal Customers** | R≥3, F≥3, M≥3 | Buy regularly and spend well — upsell opportunities |
| **Promising** | R≥4, F≤2 | Recent buyers not yet frequent — nurture with welcome offers |
| **Potential Loyalists** | R≥3, F≤2 | Show some loyalty — offer membership programs |
| **At Risk** | R≤2, F≥3, M≥3 | Were good customers but fading — send win-back campaigns |
| **Cannot Lose Them** | R≤2, F≥4, M≥4 | Former top customers — re-engage immediately |
| **Needs Attention** | (other mid-range) | Going quiet — limited-time promotions to re-activate |
| **Lost** | R=1, F=1 | Lowest scores across all dimensions — minimal effort |

---

## 📊 Visualisations

The notebook produces the following charts:

- Top 10 countries by transaction volume
- Distributions of Recency, Frequency, and Monetary values
- Distribution of R, F, M scores across customers
- Customer count per segment (horizontal bar chart)
- Average spend per segment (bar chart)
- Heatmap of average RFM scores by segment

---

## 🚀 Getting Started

### Option 1 — Run in Google Colab (Recommended)
Click the badge at the top of this README, or go directly to:

**[Open in Google Colab](https://colab.research.google.com/github/Bachu33/online-retail-rfm-analysis/blob/main/rfm.ipynb)**

1. Click **Runtime → Run all** (or press `Ctrl+F9`)
2. The first cell will automatically download and extract the dataset from the UCI repository — no setup needed

> **Note:** The Colab session needs to stay active during the dataset download (~23MB). If the session times out, simply reconnect and re-run.

### Option 2 — Run Locally
1. Clone this repository:
```bash
git clone https://github.com/Bachu33/online-retail-rfm-analysis.git
cd online-retail-rfm-analysis
```
2. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn openpyxl
```
3. Launch the notebook:
```bash
jupyter notebook rfm.ipynb
```

---

## 📁 Repository Structure

```
├── rfm.ipynb          # Main analysis notebook
└── README.md          # Project documentation
```

---

## 🎯 Success Criteria

✅ RFM metrics calculated per customer  
✅ Customers scored 1–5 on each dimension  
✅ 8 meaningful customer segments produced  
✅ Business interpretation provided for each segment  
✅ Visualisations supporting segment analysis  

---

## 📚 References

- Daqing Chen, Sai Liang Sain, and Kun Guo (2012). *Data mining for the online retail industry: A case study of RFM model-based customer segmentation using data mining.* Journal of Database Marketing and Customer Strategy Management.
- [UCI Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail)
