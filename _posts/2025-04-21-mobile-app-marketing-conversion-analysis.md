---
layout: post
title: "Case Study: Mobile App Marketing & Conversion Analysis"
date: 2025-04-21
excerpt: "How do user behavior and marketing touchpoints shape conversions in a mobile app for self-employed professionals in Germany?"
---

### 📌 Overview

How do user behavior and marketing touchpoints shape conversions in a mobile app for self-employed professionals in Germany?

This case study explores data from **29.1k users (15.1% conversion)** between 2020 – 2025, with the goal of improving subscription rates and acquisition efficiency.  
I created **4 interactive dashboards in Looker Studio** to uncover actionable insights:

1. **Overview** – Growth, revenue & conversion trends  
2. **User Behavior Analysis** – In-app actions that drive conversion  
3. **Marketing Performance** – ROI by channel & campaign  
4. **User Segmentation & Targeting** – Region & profession-based targeting


### 🔧 Tools & Methods

- **Data Preparation:** Python ➡️ **[View Code](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)**
- **Visualization:** Looker Studio (Google Data Studio)
- **Data:** Internal app analytics (events, subscriptions, acquisition)

### 📊 Live Dashboards

➡️ **[Explore Dashboards](https://lookerstudio.google.com/u/0/reporting/8959b791-5c18-4a12-8986-2f58b882b980/page/eleFF)**

---

## 1. Overview 
**🎯 Goal:** Provide a high-level snapshot of user growth, conversion trends, and subscription revenue over time.

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_01.png" alt="Overview Dashboard Screenshot" width="800"/>

### 📊 Key Visualizations
1. **KPI Cards:** Total users (29.1k), Conversion Rate (15.1%), Total Monthly Recurring Revenue (MRR)
2. **Pie Charts:** Conversion Status Breakdown (Free vs. Paid), Paid vs. Non-paid Conversion
3. **Line Charts:** Account Creation Timeline, Monthly New Subscribers

### 🔍 Insights
- Steady user growth from 2020 to 2025 indicates increasing brand visibility and app popularity.
- Paid user breakdown: Among users who converted, this chart shows:
  - *Paid:* Users who subscribed without using a free trial (77.1% of Converted users).
  - *Non-paid:* Users who first tried the app with a free trial and then subscribed (22.9% of Converted users).
- July – September 2024 shows a noticeable spike in non-paid conversions, raising important questions:
  - Was there a large-scale marketing campaign that boosted sign-ups but didn’t convert well?
  - Could a free trial promotion have led to a surge in trial users who didn't upgrade?
  - Was the audience mismatch? (e.g., students testing features, or users from countries where payment is unsupported)

### ✅ Recommendations
- Investigate campaign strategies and audience sources during this spike period.
- Analyze user segments to determine if trial experiences or onboarding flows contributed to lower paid conversion.
- Cross-check app store reviews or feedback during this time for additional context.
  
---

## 2. User Behavior Analysis

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
- Users who start with simpler features tend to explore less, leading to lower conversion.
→ When users take the time to explore the app fully and engage with its features, they have a higher chance of becoming paying subscribers.

### 🔍 Insights

- Early drop-offs in the usage funnel suggest onboarding friction.
- Users who adopt financial tools or AI early are more likely to convert.
- Conversion is influenced not only by feature use, but by the order and timing of use.

### ✅ Recommendations

**Onboarding Improvements**  
- Add tooltips and onboarding prompts for advanced features.
- Guide users to the next helpful action after they perform a basic action. For example, if they create an invoice, suggest connecting their bank account.

**AI Assistant Optimization**  
- Introduce a required (but skippable) first interaction with the AI Assistant.
- Use the Assistant to guide users through onboarding (e.g., suggesting VAT input after tax number entry).

**Incentives and Retention**  
- Offer a 14-day trial to users who connect a bank but don’t convert.
- Send personalized in-app nudges to re-engage users who drop off early in the funnel.

---

## 3. Marketing Performance
**🎯 Goal:** Evaluate marketing channels by conversion, spend, and ROI to optimize acquisition strategy.

### 📊 Key Visualizations

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_03.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

**1. Conversion Speed Breakdown**  
Among converted users, 10.4% converted immediately — meaning they subscribed on the first or second day of using the app.

**2. Time to Pay Distribution**  
Most users convert within the **first 1–2 months**.

**3–5. Marketing Channel Performance**  
Evaluation by user volume, conversion rate, and maximum MRR:

- **Google** brings in the largest volume of users, top MRR, but moderate conversion.  
- **Facebook** achieves the highest conversion rate, surpassing Google and TikTok, despite having moderate user traffic and MRR.
- **TikTok** exhibits the lowest performance across user volume, conversion rate, and MRR, indicating overall underperformance.

**6–7. Campaign Performance**  
Analysis by conversion distribution and Max MRR.  
<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_03b.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

> ⚠️ ⚠️ To ensure data accuracy for the campaign analysis, a data cleaning step was performed. The original `campaign` column presented inconsistencies in naming, which were resolved by grouping similar entries into these standardized categories:

- `sea` → Search Engine Advertising  
- `ugc` → User Generated Content  
- `vat` → VAT Campaign  

🔗 [View data cleansing here](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)

- Two campaigns (“Retargeting” and “Organic”) show 100% conversion, but each had only one user, so they’re not statistically meaningful.
- Google’s **Search Engine Advertising** brings the highest Max MRR, despite a lower conversion rate.
- The **Static Campaign** ranks second in Max MRR and has a high conversion rate of 52.3%.

**8–9. Promocode Analysis**

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_03c.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

- Promocode usage significantly boosts both conversion rate and conversion speed.


### 🔍 Insights

- **Social media (e.g., Facebook):** Demonstrates strong conversion rates and contributes significantly to revenue, suggesting a highly engaged audience. Consider further investment and scaling successful creatives.  
- **Search engine (Google):** While generating the highest user volume and MRR, search engine campaigns show a moderate conversion rate, indicating potential for optimization through improved keyword targeting and landing page relevance.  
- **Short-form video (TikTok):** Currently underperforming across key metrics (user volume, conversion, MRR), potentially due to a mismatch between the platform's demographics and our target audience. A carefully targeted experiment is recommended before further investment.


### ✅ Recommendations

**Channel Strategy:**

- **Facebook:** Increase budget to leverage its high conversion rates.
- **Google:** Optimize for better conversion by focusing on top campaigns (SEA), refining keyword targeting, and improving ad and landing page relevance.
- **TikTok:** Conduct a focused final experiment targeting age 25-35 with interest in business, finance, and freelance topics, using content addressing their pain points, before considering a budget cut.

**Campaign Tactics:**

- **Prioritize High ROI:** Allocate more budget to campaigns demonstrating strong return (e.g., SEA, Static).
- **Explore High-Potential:** Monitor and test scaling campaigns with high conversion rates but low volume (e.g., Retargeting, Organic).
- **Drive Faster Conversion:** Implement limited-time promocodes to encourage quicker subscriptions.

---

## 4. User Segmentation & Targeting 
**🎯 Goal:** Segment users by behavior, profession, and region to personalize marketing and onboarding.

### 1. Regional Segmentation

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_04a.png" alt="Users by Region" width="800"/>

- **Berlin** has the largest user base, the highest Conversion Rate, and the highest Max MRR.  
  ➡️ **Increase marketing budget**  
  ➡️ Analyze top-performing campaigns in Berlin and scale similar strategies to other cities

- **Nordrhein-Westfalen & Bayern** shows strong performance: high MRR and high Conversion Rates.  
  ➡️ Maintain or slightly increase marketing investment  
  ➡️ Test new campaign ideas to unlock additional value

- **Mecklenburg-Vorpommern & Hamburg** has fewer users, but strong conversion efficiency.  
  ➡️ Explore potential with **low-budget awareness campaigns**

- **Saarland** has low user base, poor conversion, and revenue.  
  ➡️ Conduct **market research** to identify blockers  
  ➡️ Consider **reducing ad spend**


### 2. User Type & Self-Employment

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_04b.png" alt="Self-Employment Status" width="800"/>

**Users by Self-Employment Status**  
- The majority are self-employed, aligning with the app’s target audience  
- A small portion is not self-employed:
  - Curious explorers
  - Preparing for future freelancing
  - Representing a potential **secondary market**

➡️ Maintain focus on self-employed users  
➡️ Create light messaging for the “pre-freelancer” segment

### 3. Profession-Based Segmentation

- **Artists & Content Creators** are the largest group. They generate the highest Max MRR (due to size), though not the best conversion rate.
- Top professions by volume ≠ Top professions by conversion rate

➡️ Focus budget on **high-converting professions** to maximize ROI  
➡️ Nurture large-volume professions (like artists) by:
  - Identifying blockers to conversion  
  - Running **targeted tests** (profession-specific messaging or landing pages)

<img src="/assets/images/Screenshot_Acctbl%20Mobile%20App_04c.png" alt="VAT and Account Type" width="800"/>

### 4. VAT Type Segmentation

- Most users fall under **franchise** (small businesses exempt from charging VAT)
- Users under **subjectToVAT** show higher conversion rates—suggesting that businesses handling VAT may find more value in the app

➡️ Tailor messaging to **subjectToVAT** users' needs (highlight features like invoicing and VAT management).

### 5. Account Type Segmentation

- Most users are freelancers or solo business owners without VAT.  
- Complementary status users — those with a primary job and a freelancing side gig—have the highest conversion rates
  
➡️ Prioritize marketing toward dual-income users, as they are likely to face more complex financial management.  
➡️ Adjust messaging to emphasize how the app supports multi-income stream management.

### 🔍 Insights

- Certain **professions and regions** drive better conversion and revenue
- **Bank-connected but unsubscribed** users present an opportunity for re-engagement
- Regional differences indicate potential for **localized marketing strategies**


### ✅ Recommendations

- Tailor campaigns to high-performing regions (e.g., Berlin, NRW)
- Test localized messaging to unlock value in under-tapped regions (e.g., Hamburg)
- Re-engage unsubscribed but active users via segmented campaigns
- Invest in understanding behavior:
  - Collect qualitative feedback for improved UX  
  - Run deeper segmentation analysis by profession, VAT type, region, and account status

---
## 📌 Final Takeaways
This case study showed how a mix of behavioral analytics and marketing performance can drive better user acquisition and retention. The combination of funnel tracking, feature analysis, and campaign ROI offers a blueprint for optimizing app growth strategies. Across all four dashboards, we uncovered key insights:  
- Conversion is driven by meaningful feature use — especially financial setup and AI interaction.  
- User onboarding flow matters. Users starting with guided or advanced features convert better.
- Marketing ROI varies widely — Facebook delivers strong results; TikTok underperforms.
- Location matters. Cities like Berlin and NRW show high MRR and conversion potential.

➡️ **Next steps:** Prioritize onboarding improvements, double down on top-performing channels and regions, and test personalized nudges based on behavior.
