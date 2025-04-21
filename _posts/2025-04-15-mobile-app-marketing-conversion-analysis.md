---
layout: post
title: "Case Study: Mobile App Marketing & Conversion Analysis"
date: 2025-04-15
---

## 📌 Overview

This case study explores user behavior and marketing performance for a mobile app designed for self-employed professionals in Germany. Using data from 2020 to 2025, the goal was to improve conversion rates to paid subscriptions and optimize acquisition efficiency.

The dataset covers **29.1k users** (15.1% conversion rate), capturing sign-up dates, in-app actions, profession types, subscription choices, and marketing sources.

I created **four interactive dashboards in Looker Studio** to visualize KPIs and uncover insights:

1. **Overview:** High-level performance metrics and conversion trends  
2. **User Behavior Analysis**  
3. **Marketing Performance**  
4. **User Segmentation & Targeting**

---

## 🔧 Tools & Methods

- **Data Cleaning & Preparation:** Python  
- **Visualization:** Looker Studio (Google Data Studio)  
- **Data Source:** Internal app analytics (user events, subscriptions, acquisition data)

---

## 📊 Dashboard Breakdown & Insights

---

### 1. Overview Dashboard  
**Goal:** Provide a high-level snapshot of user growth, conversion trends, and subscription revenue over time.

![Overview Dashboard Screenshot](/assets/images/Screenshot_Acctbl Mobile App_01.png)

**Key Visualizations:**
- **KPI Cards:** Total users (29.1k), Conversion Rate (15.1%), Total Monthly Recurring Revenue (MRR)
- **Pie Charts:** Conversion Status Breakdown (Free vs. Paid), Paid vs. Non-paid Conversion
- **Line Charts:** Account Creation Timeline, Monthly New subscribers

**Insights:**
- Steady user growth from 2020 to 2025 indicates increasing brand visibility and app popularity.
- Paid User Breakdown: Among users who converted, this chart shows:
  - Paid: Users who subscribed without using a free trial (77.1% of Converted users).
  - Non-paid: Users who first tried the app with a free trial and then subscribed (22.9% of Converted users).
- July–September 2024 shows a noticeable spike in non-paid conversions, raising important questions:
  - Was there a large-scale marketing campaign that boosted sign-ups but didn’t convert well?
  - Could a free trial promotion have led to a surge in trial users who didn't upgrade?
  - Was the audience mismatch? (e.g., students testing features, or users from countries where payment is unsupported)

**Recommendations:**
- Investigate campaign strategies and audience sources during this spike period.
- Analyze user segments to determine if trial experiences or onboarding flows contributed to lower paid conversion.
- Cross-check app store reviews or feedback during this time for additional context.
  
---

### 2. User Behavior Analysis Dashboard  
**Goal:** Identify high-converting in-app actions and patterns among different user types.

![User Behavior Dashboard Screenshot](/assets/images/Screenshot_Acctbl Mobile App_02.png)


**Key Visualizations:**
- **Funnel Chart:** Sign-up → key actions (e.g., bank connection, AI Assistant use) → subscription
- **Bar Chart:** Feature usage (invoice, AI) by user type
- **Heatmap:** Conversion rates by profession
- **Time Series:** Time to conversion by action
- - **Funnel Chart:** Tracks user journey from sign-up to subscription
- **Line Graph:** Monthly sign-ups and conversions (2020–2025)
- **Bar Chart:** Sessions by converted vs. non-converted users

**Insights:**
- Early funnel drop-offs are significant before users engage with features
- Converted users show higher session frequency and faster onboarding

**Recommendations:**
- Simplify onboarding with tooltips and prompts
- Send push notifications to re-engage users who drop off early

**Insights:**
- Users who connect a **bank account** or use the **AI Assistant within 3 sessions** convert more
- Non-converted users often skip essential features

**Recommendations:**

**Onboarding Optimization:**
- Use tutorials/tooltips to encourage early feature use  
- Add an optional AI Assistant walkthrough to increase awareness

**Targeted Messaging:**
- Offer a **14-day trial** to bank-connected users who don’t convert

**A/B Testing Ideas:**
- AI button placement (current vs. prominent)  
- AI tone (factual vs. conversational)  
- Feature recommendations (generic vs. tailored by profession)

---

### 3. Marketing Performance Dashboard  
**Goal:** Evaluate marketing channels by conversion, spend, and ROI to optimize acquisition strategy.

![Marketing Dashboard Screenshot](/assets/images/Screenshot_Acctbl Mobile App_03.png)

**Key Visualizations:**
- **Pie Chart:** Conversion rate by channel (social, search, video)
- **Bar Chart:** Revenue/conversions by channel
- **Table:** CAC, conversions, and spend
- **Line Graph:** Channel trends over time

**Insights:**
- **Social media** campaigns deliver strong conversions and revenue
- **Search engine** campaigns are under-optimized
- **Short-form video** underperforms due to a misaligned audience

**Recommendations:**
- Increase budget on social channels
- Improve keyword targeting and landing page UX for search
- A/B test content on video platforms (ages 25–35, finance interests)

---

### 4. User Segmentation & Targeting Dashboard  
**Goal:** Segment users by behavior, profession, and region to personalize marketing and onboarding.

![Segmentation Dashboard Screenshot](insert-segmentation-dashboard-screenshot-url-here)

**Key Visualizations:**
- **Heatmap:** Conversion rates by profession (freelancers, consultants)
- **Geo Chart:** Regional activity and conversion
- **Bar Chart:** VAT status, account type vs. conversion
- **Sankey Diagram:** Paths from sign-up to conversion or churn

**Insights:**
- Certain **professions and regions** convert better
- **Bank-connected but unsubscribed** users are prime re-engagement targets
- Regional behavior suggests potential for localized campaigns

**Recommendations:**
- Run campaigns tailored by profession/region
- Offer trials or incentives to re-engage active non-subscribers
- Use CPA, CAC, and LTV to refine targeting and segmentation

---

## 🛠️ Dashboard Features

- **Interactive Filters:** Date, region, profession, VAT status, platform  
- **KPI Cards:** Track total conversions, MRR, and user volume  
- **Funnel Visualizations:** Identify where users drop off  
- **Segmentation Views:** Behavioral and demographic filters

---

## 🧹 Data Preparation

The dataset was cleaned and analyzed in Python.  
➡️ [View Jupyter Notebook](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)

---

## 📊 Live Dashboards

Explore the interactive dashboards here:  
➡️ [Live Looker Dashboards](https://lookerstudio.google.com/u/0/reporting/8959b791-5c18-4a12-8986-2f58b882b980/page/eleFF)

---

## 📌 Final Takeaways

- Conversion rates differ significantly by **user behavior** and **profession**
- Top-performing channels should receive **increased budget and refinement**
- **Personalized onboarding and re-engagement** drive higher conversion and LTV

👉 These insights directly informed marketing experiments and UX adjustments to improve growth and retention.
