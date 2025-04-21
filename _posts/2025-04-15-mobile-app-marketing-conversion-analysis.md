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


## 🔧 Tools & Methods

- **Data Cleaning & Preparation:** Python ➡️ [(View here)](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)
- **Visualization:** Looker Studio (Google Data Studio)  
- **Data Source:** Internal app analytics (user events, subscriptions, acquisition data)

## 📊 Live Dashboards
➡️ [View here](https://lookerstudio.google.com/u/0/reporting/8959b791-5c18-4a12-8986-2f58b882b980/page/eleFF)

---

## 1. Overview Dashboard  
**🎯 Goal:** Provide a high-level snapshot of user growth, conversion trends, and subscription revenue over time.

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_01.png" alt="Overview Dashboard Screenshot" width="800"/>

### 📊 Key Visualizations
- **KPI Cards:** Total users (29.1k), Conversion Rate (15.1%), Total Monthly Recurring Revenue (MRR)
- **Pie Charts:** Conversion Status Breakdown (Free vs. Paid), Paid vs. Non-paid Conversion
- **Line Charts:** Account Creation Timeline, Monthly New subscribers

### 🔍 Insights
- Steady user growth from 2020 to 2025 indicates increasing brand visibility and app popularity.
- Paid user breakdown: Among users who converted, this chart shows:
  - *Paid:* Users who subscribed without using a free trial (77.1% of Converted users).
  - *Non-paid:* Users who first tried the app with a free trial and then subscribed (22.9% of Converted users).
- July–September 2024 shows a noticeable spike in non-paid conversions, raising important questions:
  - Was there a large-scale marketing campaign that boosted sign-ups but didn’t convert well?
  - Could a free trial promotion have led to a surge in trial users who didn't upgrade?
  - Was the audience mismatch? (e.g., students testing features, or users from countries where payment is unsupported)

### ✅ Recommendations
- Investigate campaign strategies and audience sources during this spike period.
- Analyze user segments to determine if trial experiences or onboarding flows contributed to lower paid conversion.
- Cross-check app store reviews or feedback during this time for additional context.
  
---

## 2. User Behavior Analysis Dashboard

**🎯 Goal:** Identify high-converting in-app actions and behavioral patterns among different user types.

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_02.png" alt="User Behavior Dashboard Screenshot" width="800"/>

### 📊 Key Visualizations

**1. Engagement Metrics Table**  
- Converted users tend to have more sessions and spend more time per session, showing deeper engagement.  
- Non-converted users use the app more frequently (higher average days used) but spend less time overall, likely testing limited features (such as invoice creation or bank connections) that are restricted in the free plan.  

**2. Feature Usage Funnel**  
- Many users begin with basic features like **Create Expense/Invoice** or **Enter Tax Number**.
- Fewer users proceed to advanced tasks such as **PEPPOL Registration**, **VAT Input**, or **IBAN Setup**.
- These drop-offs may suggest:
  - UX friction or complexity
  - Lack of onboarding or tooltips
  - Users feeling overwhelmed with tax-related setup

**3. Conversion Rate by Feature Used (100% Stacked Bar Chart)**
- Although fewer users use features like **IBAN Setup**, **Verified Bank**, and **PEPPOL Registration**, those who do are far more likely to become paid users.
  → These actions suggest serious engagement and a high intent to fully use the platform.
- **AI Assistant** has a moderate conversion rate (~71.7%).
- Frequently used basic features such as **Create Expense**, **Invoice**, or **Other Revenue** have lower conversion rates.
  → These are often used for quick testing by new or casual users without further exploration.

**4. First Feature Used Distribution**  
Shows which feature users interacted with first after installing the app.

- Most users start with simpler actions such as **Create Expense** or **Create Invoice**.
- Fewer users begin with advanced or guided features, which mirrors the behavior seen in the usage funnel.

**5. Conversion Rate by First Feature Used**  
Highlights how the first action impacts conversion likelihood.

- Users who start with **AI Assistant** have the highest conversion rate (40%), despite being a smaller group.
  → These users are more likely to explore deeply and engage meaningfully with the platform.
- Users who start with simpler features tend to explore less, leading to lower conversion.

### 🔍 Insights

- Early drop-offs in the usage funnel suggest onboarding friction.
- Users who adopt financial tools or AI early are more likely to convert.
- Conversion is influenced not only by feature use but by the **order and timing** of use.

### ✅ Recommendations

**Onboarding Improvements**  
- Add tooltips and onboarding prompts for advanced features.
- Suggest logical next steps after a user performs a basic action (e.g., after creating an invoice, prompt to connect a bank account).

**AI Assistant Optimization**  
- Introduce a required (but skippable) first interaction with the AI Assistant.
- Use the Assistant to guide users through onboarding (e.g., suggesting VAT input after tax number entry).

**Incentives and Retention**  
- Offer a 14-day trial to users who connect a bank but don’t convert.
- Send personalized in-app nudges to re-engage users who drop off early in the funnel.

---

## 3. Marketing Performance Dashboard  
**🎯 Goal:** Evaluate marketing channels by conversion, spend, and ROI to optimize acquisition strategy.

### 📊 Key Visualizations

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_03.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

**1. Conversion Speed Breakdown**  
Among converted users, 10.4% converted immediately — meaning they subscribed on the first or second day of using the app.

**2. Time to Pay Distribution**  
Most users convert within the **first 1–2 months**.

**3–5. Marketing Channel Performance**  
Evaluation by user volume, conversion rate, and maximum MRR:

- **Google**  
  - Brings in the largest volume of users  
  - Highest Max MRR  
  - Conversion rate is **moderate**

- **Facebook**  
  - Moderate user base  
  - Highest conversion rate, outperforming Google and TikTok  
  - Moderate Max MRR

- **TikTok**  
  - Lowest in user volume, conversion rate, and Max MRR  
  - Overall underperformance

**6–7. Campaign Performance**  
Analysis by conversion distribution and Max MRR.
<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_03b.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

> ⚠️ Before this analysis, I cleaned the raw data. The `campaign` column had many inconsistent names, so I grouped similar entries into clear categories:

- `sea` → Search Engine Advertising  
- `ugc` → User Generated Content  
- `vat` → VAT Campaign  

🔗 [View data cleansing here](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)

- Two campaigns (“Retargeting” and “Organic”) show **100% conversion**, but each had **only one user**, so they’re not statistically meaningful.
- Google’s **Search Engine Advertising** brings the **highest Max MRR**, despite a lower conversion rate.
- The **Static Campaign** ranks second in Max MRR and has a **high conversion rate of 52.3%**.

**8–9. Promocode Analysis**

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_03c.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

- Promocode usage significantly boosts both conversion rate and conversion speed.


### 🔍 Insights

- **Social media** campaigns deliver strong conversions and revenue.
- **Search engine** campaigns are under-optimized but promising.
- **Short-form video** campaigns underperform, possibly due to audience mismatch.


### ✅ Recommendations

**For Channels:**

- **Increase investment in Facebook**, the highest-performing channel.
- **Optimize Google**:
  - Focus on top-performing campaigns (e.g. **Search Engine Advertising**)
  - Improve **keyword targeting**
  - Refine **landing pages** and **ad messaging**

- **TikTok**:
  - Consider a budget cut.
  - Before a full cut, run a **final experiment**:
    - **Age Range**: 25–35
    - **Interest**: Business, finance, side hustles
    - **Content**: Tailor ads to address invoicing, taxes, and freelance pain points

**For Campaigns:**

- **Prioritize high-performing campaigns** with strong ROI (e.g. SEA, Static).
- Monitor high-rate but low-volume campaigns (e.g. Retargeting, Organic).
- Offer **limited-time promocodes** to speed up conversions.

---

### 4. User Segmentation & Targeting Dashboard  
**Goal:** Segment users by behavior, profession, and region to personalize marketing and onboarding.



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

## 📌 Final Takeaways

- Conversion rates differ significantly by **user behavior** and **profession**
- Top-performing channels should receive **increased budget and refinement**
- **Personalized onboarding and re-engagement** drive higher conversion and LTV

👉 These insights directly informed marketing experiments and UX adjustments to improve growth and retention.
