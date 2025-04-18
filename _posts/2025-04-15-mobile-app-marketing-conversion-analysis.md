---
layout: post
title: "Case Study: Mobile App Marketing & Conversion Analysis"
date: 2025-04-15
---

## 📌 Overview
This case study analyzes user behavior and marketing performance for a mobile app targeting self-employed professionals in Germany, using data from 2020 to 2025. The goal is to optimize conversion rates to paid subscriptions and improve acquisition efficiency. The dataset includes 29,100 users (15.1% conversion rate) with details on sign-up dates, in-app events, professions, subscription plans, and marketing sources, all focused on the German market.

We built four interactive dashboards in Looker Studio to visualize key metrics and uncover actionable insights:

1. **Overview:** High-level performance metrics and conversion trends.
2. **User Behavior Analysis**
3. **Marketing Performance:** Effectiveness of acquisition channels.
4. **User Segmentation & Targeting:** Behavioral and demographic segmentation.

## 🔧 Tools & Methods
- **Data Cleaning & Preparation:** Python
- **Visualization:** Looker Studio (Google Data Studio)
- **Data Source:** Internal app analytics (e.g., user events, subscription dates, marketing sources).

## 🎯 Dashboard Breakdown & Insights

---

### 1. Overview Dashboard

**Purpose:**  
Offers a snapshot of app performance, focusing on user growth, conversion rates, and revenue metrics.

**Key Visualizations:**
- **KPI Cards:** Total users (29,100), conversion rate (15.1%), Monthly Recurring Revenue (MRR)
- **Funnel Chart:** Tracks user journey from sign-up to subscription, highlighting drop-off points
- **Line Graph:** Displays monthly sign-ups and conversions (2020–2025)
- **Bar Chart:** Compares session counts for converted vs. non-converted users

**Insights:**
- Conversion bottlenecks occur early, with many users dropping off before engaging with key features
- Converted users have higher session frequencies and complete onboarding steps faster

**Recommendations:**
- Simplify onboarding with clear prompts to drive early engagement
- Use push notifications to re-engage users who abandon the funnel

---

### 2. User Behavior Analysis Dashboard

**Purpose:**  
Identifies in-app actions that correlate with higher conversion rates, comparing converted and non-converted users.

**Key Visualizations:**
- **Funnel Chart:** Sign-up → high-converting actions (e.g., bank connection, AI Assistant use) → subscription
- **Bar Chart:** Feature usage (e.g., invoice creation, AI interactions) by user type
- **Heatmap:** Conversion rates by user profession
- **Time Series:** Average time to conversion for key actions

**Insights:**
- Users connecting a bank account or using the AI Assistant within 3 sessions are significantly more likely to convert
- Non-converted users engage sporadically and skip critical features, indicating UX friction

**Recommendations:**

**Onboarding Optimization:**
- Guide users to connect a bank account using tutorials/tooltips
- Introduce a skippable AI Assistant interaction to highlight its value

**Targeted Messaging:**
- Offer a 14-day free trial to users who connect a bank but don’t subscribe within 7 days

**A/B Testing:**
- AI Assistant button placement (current vs. prominent)
- AI response styles (factual vs. conversational vs. proactive)
- Feature recommendations (generic vs. high-converting vs. profession-based)

---

### 3. Marketing Performance Dashboard

**Purpose:**  
Evaluates acquisition channels to optimize Customer Acquisition Cost (CAC) and Return on Investment (ROI).

**Key Visualizations:**
- **Pie Chart:** Conversion rates by channel (e.g., social media, search engines, short-form video)
- **Bar Chart:** Revenue and conversions across channels
- **Table:** CAC, conversions, and spend per channel
- **Line Graph:** Channel performance over time

**Insights:**
- Social media (e.g., Facebook) drives high conversions and revenue
- Search engine campaigns are effective but need better targeting and landing pages
- Short-form video platforms underperform due to a mismatch between audience and app’s target users

**Recommendations:**
- Increase budget for high-performing social media campaigns
- Refine search keywords and improve landing page UX
- Run a targeted short-form video campaign (ages 25–35, business/finance interests) before reducing spend

---

### 4. User Segmentation & Targeting Dashboard

**Purpose:**  
Segments users by behavior and demographics to inform personalized marketing and onboarding strategies.

**Key Visualizations:**
- **Heatmap:** Conversion rates by profession (e.g., freelancers, consultants)
- **Geo Chart:** User activity and conversions by region
- **Bar Chart:** Conversion by VAT status, account type, in-app actions
- **Sankey Diagram:** User journeys from sign-up to conversion or churn

**Insights:**
- Certain professions and regions have higher conversion rates
- Bank-connected but non-converted users are ideal re-engagement targets
- Regional behavior differences suggest potential for localized marketing

**Recommendations:**
- Tailor campaigns by profession and region
- Re-engage non-converted users with offers (e.g., free trial for bank-connected users)
- Use user feedback to refine UX and segment more effectively by CPA, CAC, and LTV

---

## 💡 Dashboard Features

- **Interactive Filters:** Filter by date, region, profession, VAT status, platform
- **KPI Cards:** Track total conversions, MRR, and user volume
- **Funnel Visualizations:** Spot conversion bottlenecks
- **Segmentation**

## 🔗 Related Repo

➡️ [View the GitHub Repo](https://github.com/dtbkhanh/Data-Analytics-and-Reports)

## 📊 Live Dashboards

➡️ [Live Dashboards](https://lookerstudio.google.com/u/0/reporting/8959b791-5c18-4a12-8986-2f58b882b980/page/eleFF)  
