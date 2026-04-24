# Supply-Chain-Analysis

The dataset is too large to upload directly but if you're interested you can download from here: https://drive.google.com/file/d/1lDOwB-Yk3iDawmLH3zXfijalduxSH2Iw/view?usp=drive_link.

# 📦 Supply Chain Delivery Performance Report

> **End-to-End Order Fulfillment Analysis & Predictive Insight**

![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Orders](https://img.shields.io/badge/Orders%20Analyzed-172%2C765-blue)
![Model](https://img.shields.io/badge/Model-Random%20Forest-orange)
![Accuracy](https://img.shields.io/badge/Accuracy-74%25-yellow)

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [Business Context \& Objectives](#business-context--objectives)
- [Key Performance Indicators](#key-performance-indicators)
- [Profitability Analysis](#profitability-analysis)
- [Bottleneck Detection](#bottleneck-detection)
- [Root Cause Analysis](#root-cause-analysis)
- [Time-Based Delay Patterns](#time-based-delay-patterns)
- [Machine Learning Model Results](#machine-learning-model-results)
- [Strategic Recommendations](#strategic-recommendations)
- [Conclusion \& Target State](#conclusion--target-state)

---

## Executive Summary

This report presents a comprehensive analysis of delivery operations for a global e-commerce company managing end-to-end order fulfillment across multiple regions. The analysis covers **172,765 orders** spanning **January 2015 – January 2018**, focusing on identifying root causes of chronic late deliveries, quantifying their financial impact, and establishing a data-driven framework for improvement.

**The headline finding is stark: 54.71% of all orders are delivered late**, costing the business **$2.1M** in eroded profitability on delayed orders alone. A Random Forest predictive model achieved **74% accuracy** in identifying at-risk orders before they become late.

| Key Finding | Metric |
|:---|:---|
| Overall Late Delivery Rate | **54.71%** |
| On-Time Delivery Rate | 45.29% |
| Total Orders Analyzed | 172,765 |
| Total Profit (profitable orders) | $7.5M |
| Profit at Risk (delayed orders) | $2.1M |
| Predictive Model Accuracy (RF) | 74% |

---

## Business Context & Objectives

The company operates a global e-commerce platform selling products across categories including **sporting goods, fitness equipment, outdoor gear, footwear, and apparel** across multiple international regions.

### Core Business Problem

Actual shipping times frequently deviate from scheduled delivery windows, creating:

- Eroded customer trust
- Reduced order profitability
- Inability to make reliable commitments to buyers at point of purchase

### Analytical Objectives

1. Understand the current state of delivery performance across all dimensions (region, mode, time, segment)
2. Quantify the financial impact of delays on order profitability
3. Identify the primary operational bottlenecks driving late deliveries
4. Build a predictive model to flag high-risk orders before they are shipped
5. Deliver actionable recommendations to improve on-time delivery and profitability

---

## Key Performance Indicators

The following KPIs were computed directly from the cleaned dataset to establish a performance baseline.

| 172,765 | 94,523 | 54.71% | 45.29% |
|:---:|:---:|:---:|:---:|
| Total Orders | Late Deliveries | Late Delivery % | On-Time Delivery % |

| $7.5M | $2.1M | 3 days | $22.03 |
|:---:|:---:|:---:|:---:|
| Total Profit | Profit at Risk | 90th Percentile Delay | Avg Order Profit |

### Key Takeaways

- **Late Delivery Rate (54.71%):** More than half of all orders arrive late — this is not an edge-case problem; it is the default experience for the majority of customers.
- **$2.1M Profit at Risk:** Orders that experienced delays collectively generated $2.1M in profit that is under constant pressure from further operational deterioration.
- **90th Percentile Delay = 3 Days:** Even the most extreme cases are contained within 3 days of lateness, suggesting the problem is systemic and process-driven rather than catastrophic.

---

## Profitability Analysis

### Profitability Distribution

Order-level profitability was classified into three tiers based on Order Profit Per Order. While **80.7%** of orders are profitable, the **18.7%** loss-making share represents a meaningful drag that is disproportionately concentrated among delayed shipments.

| Tier | Definition | Share |
|:---|:---|:---:|
| ✅ Profit | Order Profit Per Order > 0 | **80.7%** |
| ❌ Loss | Order Profit Per Order < 0 | **18.7%** |
| ➖ Break-even | Order Profit Per Order = 0 | **0.6%** |

### Delay Distribution & Profit vs. Delay Days

- **31.0%** of all orders arrive exactly **1 day late** — the single largest cohort.
- Orders delayed by **1–4 days** account for **54.7%** of all order volume, directly mapping to the overall late delivery rate.
- Mean profit per order remains stable at approximately **$20–$23** across all delay levels — the profitability problem is driven by **volume** of delayed orders, not individual order economics, making systemic throughput improvement the highest-leverage intervention.

---

## Bottleneck Detection

Delay percentage was computed across six key operational dimensions. The findings reveal where the fulfillment process breaks down most severely.

| Dimension | Key Finding | Detail |
|:---|:---|:---|
| **Shipping Mode** | #1 Lever | First Class: 100% delay; Second Class: 79.8%; Standard Class: 39.8%; Same Day: 0% |
| **Regional Spread** | Narrow (55–59%) | Central Africa leads at 58.7%, but all regions cluster between 55–59% — a company-wide systemic issue |
| **Customer Segments** | Nearly Identical (54.5–55.4%) | No segment receives preferential service; all experience the same broken delivery promise |
| **Department** | Health & Beauty (56.9%), Pet Shop (56.6%) lead | These departments warrant an inventory and carrier audit |

---

## Root Cause Analysis

Central Africa was selected for deep-dive analysis as the highest-delay region (**58.7%**). The top 10 driver factors by delay percentage were ranked within this region, revealing compounding effects across shipping mode, payment status, and product category.

---

## Time-Based Delay Patterns

Three temporal dimensions were analyzed. While delay rates are relatively stable across all dimensions (53–57%), specific peaks highlight opportunities for targeted capacity planning.

| Dimension | Peak Finding | Insight |
|:---|:---|:---|
| **Monthly** | August & September (55.4%), December (55.2%) | Mid-year promotions and Q4 holiday surge overwhelm fulfillment capacity |
| **Day of Week** | Monday (55.5%), Sunday (55.2%) | Spread across the week is < 1 percentage point — not a meaningful lever |
| **Hour of Day** | Hour 21 (57.1%), Hour 11 (56.7%), Hour 12 (56.0%) | Late-evening orders reflect processing cutoff windows; midday peaks suggest volume bottlenecks |

---

## Machine Learning Model Results

A supervised classification model was built to predict whether an individual order will be delivered late. The pipeline included:

- Frequency encoding of categorical variables
- Stratified train/test split
- SMOTE oversampling for class imbalance
- Random Forest classification

### Class Imbalance Handling (SMOTE)

| Split | Class 0 (On-time) | Class 1 (Late) |
|:---|:---:|:---:|
| Before SMOTE (train) | 59,030 | 79,182 |
| After SMOTE (train) | 79,182 | 79,182 |

### Random Forest — Test Set Performance (34,553 records)

| Metric | Class 0 (On-time) | Class 1 (Late) | Overall (Weighted) |
|:---|:---:|:---:|:---:|
| Precision | 0.68 | 0.78 | **0.74** |
| Recall | 0.72 | 0.75 | **0.74** |
| F1-Score | 0.70 | 0.77 | **0.74** |
| Accuracy | — | — | **0.74** |
| Support | 14,758 | 19,795 | 34,553 |

### Model Insights

- **74% Overall Accuracy:** Correctly classifies nearly 3 in 4 orders — a strong foundation for production deployment as an order-level late-delivery alert system.
- **78% Precision on Late Orders:** When the model predicts an order will be late, it is correct 78% of the time — sufficient to trigger targeted interventions without excessive false alarms.
- **75% Recall on Late Orders:** The model captures 75% of actual late orders. The 25% miss rate is acceptable for a first-generation alert system, with clear improvement potential.
- **Class 0 Harder to Predict (0.68 Precision):** On-time deliveries share many characteristics with late ones given the systemic nature of delays.

---

## Strategic Recommendations

| Priority | Recommendation | Details |
|:---:|:---|:---|
| 🔴 **CRITICAL** | Audit First Class & Second Class Shipping Capacity | First Class has a 100% delay rate; Second Class 79.8%. Conduct an immediate carrier SLA audit. Consider suspending First Class or repricing to reflect actual performance. |
| 🟠 **HIGH** | Deploy the Predictive Alert System | Integrate the RF model (74% accuracy, 78% precision) into the order management system to flag high-risk orders and trigger proactive customer communication. |
| 🟠 **HIGH** | Resolve Payment Processing Bottlenecks | PAYMENT_REVIEW (55.3%; 80.0% in Central Africa) and PENDING_PAYMENT (55.0%) show elevated delay rates. Introduce automated escalation for reviews exceeding 2 hours. |
| 🟡 **MEDIUM** | Develop Seasonal Surge Capacity Plans | August, October (55.4%), and December (55.2%) are peak delay months. Build pre-season capacity plans with temporary logistics partnerships and inventory pre-positioning. |
| 🟡 **MEDIUM** | Default to Standard Class for Eligible Orders | Standard Class achieves 39.8% delay rate — far superior to premium modes. Re-evaluate shipping mode assignment logic for eligible orders. |
| 🟡 **MEDIUM** | Investigate High-Delay Departments in Africa | Outdoors (61.3%) and Golf (60.8%) in Central Africa show elevated delay rates. Conduct a warehouse-level audit of stock availability and carrier assignment. |
| 🟢 **LOW** | Reduce Loss-Making Order Share (18.7%) | Review pricing and discounts. Identify whether discounted orders are disproportionately late, creating a compounded margin problem. |
| 🟢 **LOW** | Continuously Retrain the Predictive Model | Retrain quarterly. Add carrier-level data, weather events, and warehouse utilization features. Target recall > 80% on late orders within 6 months. |

---

## Conclusion & Target State

This analysis surfaced a clear and urgent picture: a global e-commerce operation where the majority of orders (**54.71%**) fail to meet their promised delivery windows, costing **$2.1M** in at-risk profit and undermining customer trust at scale.

The root causes are **identifiable and addressable**: shipping mode misconfiguration is the dominant operational failure, payment processing friction creates a secondary bottleneck, and seasonal volume spikes are not adequately planned for.

### Improvement Targets

| Priority Area | Current State | Target State |
|:---|:---:|:---:|
| Late Delivery Rate | 54.71% | **< 30%** within 12 months |
| First Class On-Time Rate | 0% | **> 80%** |
| Second Class On-Time Rate | 20.2% | **> 60%** |
| Predictive Model Accuracy | 74% | **> 82%** (enhanced model) |
| Loss-Making Orders | 18.7% | **< 12%** |
| Profit at Risk | $2.1M | **Reduce by 40%** |

> With focused execution on these eight recommendations — starting with the critical shipping mode audit and predictive alert system deployment — the business can systematically recover its delivery performance, protect its **$7.5M profit base**, and build the operational reliability that sustained e-commerce growth demands.

---



