---
layout: post
title: "Case Study: Mobile App Marketing & Conversion Analysis"
date: 2025-04-15
---

# 📌 Overview

This case study explores user behavior and marketing performance for a mobile app designed for self-employed professionals in Germany. Using data from 2020 to 2025, the goal was to improve conversion rates to paid subscriptions and optimize acquisition efficiency.

The dataset covers **29.1k users** (15.1% conversion rate), capturing sign-up dates, in-app actions, profession types, subscription choices, and marketing sources.

I created **four interactive dashboards in Looker Studio** to visualize KPIs and uncover insights:

1. **Overview:** High-level performance metrics and conversion trends  
2. **User Behavior Analysis**  
3. **Marketing Performance**  
4. **User Segmentation & Targeting**


# 🔧 Tools & Methods

- **Data Cleaning & Preparation:** Python  
- **Visualization:** Looker Studio (Google Data Studio)  
- **Data Source:** Internal app analytics (user events, subscriptions, acquisition data)


# 📊 Dashboard Breakdown & Insights

## 1. Overview Dashboard  
**🎯 Goal:** Provide a high-level snapshot of user growth, conversion trends, and subscription revenue over time.

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_01.png" alt="Overview Dashboard Screenshot" width="800"/>

#### 📊 Key Visualizations
- **KPI Cards:** Total users (29.1k), Conversion Rate (15.1%), Total Monthly Recurring Revenue (MRR)
- **Pie Charts:** Conversion Status Breakdown (Free vs. Paid), Paid vs. Non-paid Conversion
- **Line Charts:** Account Creation Timeline, Monthly New subscribers

#### 🔍 Insights
- Steady user growth from 2020 to 2025 indicates increasing brand visibility and app popularity.
- Paid user breakdown: Among users who converted, this chart shows:
  - Paid: Users who subscribed without using a free trial (77.1% of Converted users).
  - Non-paid: Users who first tried the app with a free trial and then subscribed (22.9% of Converted users).
- July–September 2024 shows a noticeable spike in non-paid conversions, raising important questions:
  - Was there a large-scale marketing campaign that boosted sign-ups but didn’t convert well?
  - Could a free trial promotion have led to a surge in trial users who didn't upgrade?
  - Was the audience mismatch? (e.g., students testing features, or users from countries where payment is unsupported)

#### ✅ Recommendations
- Investigate campaign strategies and audience sources during this spike period.
- Analyze user segments to determine if trial experiences or onboarding flows contributed to lower paid conversion.
- Cross-check app store reviews or feedback during this time for additional context.
  
---

## 2. User Behavior Analysis Dashboard

**🎯 Goal:** Identify high-converting in-app actions and behavioral patterns among different user types.

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_02.png" alt="User Behavior Dashboard Screenshot" width="800"/>

#### 📊 Key Visualizations

**Engagement Metrics Table**  
- Converted users tend to have more sessions and spend more time per session, showing deeper engagement.  
- Non-converted users use the app more frequently (higher average days used) but spend less time overall, likely testing limited features such as invoice creation or bank connections that are restricted in the free plan.  

**Funnel Chart**  
- Shows which features are most and least used, as well as drop-off points.  
- Many users begin with basic actions like "Create Expense/Invoice" or inputting a tax number but stop before reaching more advanced steps like PEPPOL registration or VAT input.  
- This drop-off may suggest UX friction, unclear guidance, or users feeling overwhelmed by tax-related features.  
- Users who interact with advanced financial tools (e.g. IBAN setup, verified bank, PEPPOL registration) are significantly more likely to convert.  
- The AI Assistant's first message also has a moderate conversion rate of 71.7%.  
- Basic features (Create Expense, Other Revenue) are popular but have a low conversion rate, likely because users try them early without progressing further.

**Bar Charts: First Feature Used and Conversion Rate by First Feature**  
- Most users start with simple features like "Create Expense/Invoice" and gradually explore more complex ones.  
- Users who begin with the AI Assistant have the highest conversion rate (40%), even though they are a smaller group.  
- This suggests that early engagement with guided or advanced features is linked to higher conversion.

#### 🔍 Insights

- A significant number of users drop off before engaging with meaningful features.  
- Converted users tend to complete onboarding steps faster and engage more consistently.  
- Users who connect a bank account or use the AI Assistant within their first three sessions show higher conversion.  
- Non-converted users often skip key features entirely.

#### ✅ Recommendations

**Onboarding Optimization**  
- Add tutorials, tooltips, and contextual prompts to help users discover important features earlier.  
- Consider an optional walkthrough for the AI Assistant to improve early engagement.

**Targeted Messaging**  
- Offer a limited-time trial (e.g. 14 days) for users who connect a bank account but haven’t subscribed.  
- Use push notifications to re-engage users who drop off after basic usage.

**Improving the First-Time AI Assistant Experience**  
- Introduce a mandatory but skippable interaction with the AI Assistant during onboarding.  
- Let the Assistant guide users through logical next steps (e.g. after creating their first invoice, suggest connecting a bank or setting up VAT).

---

## 3. Marketing Performance Dashboard  
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
