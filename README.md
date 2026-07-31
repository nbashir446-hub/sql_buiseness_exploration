# SQL Business Exploration: ENIAC x Magist Partnership Analysis

## 📌 Project Overview
**ENIAC** is an e-commerce company based in Europe specializing in high-tech products and Apple-compatible accessories. As part of its international expansion strategy into Brazil, ENIAC evaluated a potential partnership with **Magist**—a Brazilian Software as a Service (SaaS) platform connecting merchants to major regional marketplaces.

This data analysis project uses **SQL** to investigate the feasibility of the partnership, focusing directly on ENIAC's two primary operational concerns.


## ❓ Business Questions & Key Concerns

1. **Product Fit:** Is Magist a suitable platform for selling high-end tech products?
2. **Logistics Performance:** Are Magist’s delivery speeds fast and reliable enough to meet ENIAC's brand standards?


## 🛠️ Tech Stack & Tools
 **Database:** MySQL / PostgreSQL (Magist E-Commerce Dataset)
 **Language:** SQL (Data Extraction, Aggregations, Joins, Window Functions)
 **Documentation:** Markdown


## 📊 Key Findings

### 1. Product Fit Analysis
 **Low Tech Volume:** High-tech categories (computers, audio, tech accessories) represent **less than 10–12%** of total order volume on Magist. The platform is dominated by non-tech categories like bed/bath/table and health/beauty.
 **Price Point Mismatch:** Tech products have a significantly higher Average Order Value (AOV) than Magist’s typical catalog. Selling premium products carries higher financial risk due to lower baseline demand for high-end tech on these marketplaces.

### 2. Logistics & Delivery Performance
 **Long Transit Times:** The average delivery time across all Magist orders is **12–15 days**, far exceeding standard European e-commerce benchmarks.
 **Geographic Variance:** Delivery speeds vary drastically by region:
 **Southeast Region (São Paulo / Rio de Janeiro):** ~5–8 days (Acceptable).
 **North / Northeast Regions:** 20–30+ days (High Risk).
**Delivery Delays:** Approximately **8–10% of shipments exceed their estimated delivery date**, which correlates directly with lower customer satisfaction (CSAT) scores for high-value orders.

## 💡 Recommendations for ENIAC

Based on the quantitative analysis of Magist's catalog and logistics data, the following strategic actions are recommended:

### 1. 🛑 Primary Recommendation: Do Not Partner with Magist
**Current Unsuitability:** Magist’s logistics latency (12–15 day averages) and low marketplace share in high-tech products present significant risks to ENIAC’s brand image and customer satisfaction.
**Alternative Channels:** Explore direct entry via dedicated 3PL (Third-Party Logistics) providers based in major metropolitan areas (e.g., São Paulo) or evaluate tech-specialized Brazilian marketplaces like *Kabum!,Mgzine Luiza,Casas Bahia*.

### 2. 🛡️ Secondary Recommendation (If Partnership Moves Forward)
If leadership chooses to move forward with Magist despite the risks, ENIAC should enforce strict operational constraints:
**Geographic Capping:** Restrict fulfillment exclusively to South/Southeast regions to maintain sub-7-day delivery windows.
**Catalog Capping:** Limit initial listings to low-risk, high-margin accessories (cables, cases) rather than expensive core hardware.
**Logistics SLAs:** Require strict contractual SLAs and prioritized fulfillment dispatch windows from Magist.


## 📂 Repository Structure

```text
├── data/              # Dataset documentation & schemas
├── queries/           # SQL scripts used for extraction & analysis
│   ├── product_fit.sql
│   └── delivery_performance.sql
├── reports/           # Final presentation / executive summary
└── README.md          # Project documentation
