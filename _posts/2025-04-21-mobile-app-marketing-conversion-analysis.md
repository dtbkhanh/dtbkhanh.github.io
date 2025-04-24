---
layout: post
title: "Case Study: Mobile App Marketing & Conversion Analysis"
date: 2025-04-21
excerpt: "This case study explores how different marketing channels and user behaviors influence conversion rates for a mobile app targeting self-employed professionals in Germany."
---

**Table of Contents**
- [1. Overview](#1-overview)
- [2. User Behavior Analysis](#2-user-behavior-analysis)
- [3. Marketing Performance](#3-marketing-performance)
- [4. User Segmentation & Targeting](#4-user-segmentation--targeting)
- [5. Final Takeaways](#final-takeaways)

<!-- Intro -->
### 📌 Introduction

How do user behavior and marketing touchpoints shape conversions in a mobile app for self-employed professionals in Germany?

This case study explores data from **29.1k users (15.1% conversion)** between 2020 – 2025, with the goal of improving subscription rates and acquisition efficiency.

I created 4 interactive dashboards in Looker Studio to uncover actionable insights:  
1. **Overview** – Growth, revenue & conversion trends  
2. **User Behavior Analysis** – In-app actions that drive conversion  
3. **Marketing Performance** – ROI by channel & campaign  
4. **User Segmentation & Targeting** – Region & profession-based targeting

### 🔧 Tools & Methods

- **Data Preparation:** Python ➡️ **[View Code](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)**
- **Visualization:** Looker Studio (Google Data Studio)
- **Data:** Internal app analytics (events, subscriptions, acquisition)


<!------------------------------ DASHBOARDS  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>

<div style="text-align: center; font-size: 1.3em;"><h1>📊 Explore Dashboards📊 </h1></div>

<div style="border: 1px solid #ccc; padding: 15px; margin: 20px 0; border-radius: 5px; text-align: center; transition: box-shadow 0.3s ease-in-out, border-color 0.3s ease-in-out;">
  <strong><a href="https://lookerstudio.google.com/u/0/reporting/8959b791-5c18-4a12-8986-2f58b882b980/page/eleFF" target="_blank" style="text-decoration: none;">➡️ View Live Dashboards ⬅️</a></strong>
</div>

<script>
  const dashboardBox = document.querySelector('div[style*="border: 1px solid #ccc"]');
  if (dashboardBox) {
    dashboardBox.addEventListener('mouseenter', () => {
      dashboardBox.style.boxShadow = '0 4px 8px rgba(0, 0, 0, 0.2)';
      dashboardBox.style.borderColor = '#3498db'; /* Example hover border color */
    });
    dashboardBox.addEventListener('mouseleave', () => {
      dashboardBox.style.boxShadow = 'none';
      dashboardBox.style.borderColor = '#ccc';
    });
  }
</script>

<!------------------------------ PAGE 1  ----------------------------------->
<h1 id="1-overview">1. Overview</h1>

**🎯 Goal:** Provide a high-level snapshot of user growth, conversion trends, and subscription revenue over time.

<img src="/assets/images/Screenshot_Mobile App_01.png" alt="Overview Dashboard Screenshot" width="800"/>

### 📊 Key Visualizations
1. **KPI Cards:** Total users (29.1k), Conversion Rate (15.1%), Total Monthly Recurring Revenue (MRR)
2. **Pie Charts:** Conversion Status Breakdown (Subscribers vs. Non-subscibers), Paid vs. Non-paid Conversion (among Subscribers)
3. **Line Charts:** Account Creation Timeline, Monthly New Subscribers

### 🔍 Insights
- **Overall Conversion Rate opportunity**: A 15.1% overall conversion rate indicates room for improvement.  
- **Strong user acquisition trend**: The consistent growth in total users from 2020 to 2025 highlights successful brand building and increasing app popularity.  
- **Dominance of Paid Conversions**: The "Paid vs. Non-paid Conversion" pie chart reveals that:  
  - ***Paid:*** Users who subscribed without using a free trial (77.1% of Converted users).  
  - ***Non-paid:*** Users who first tried the app with a free trial and then subscribed (22.9% of Converted users).  
- **Significant Spike in trial Conversions**: The "Monthly New Subscribers" chart shows a notable increase in non-paid conversions during July – September 2024.

### ✅ Recommendations
-  Investigate the spike in non-paid conversions during the period of July – September 2024:
  -  *Marketing campaign effectiveness*: Analyze marketing campaign performance during this period. Were there specific campaigns focused on free trials? Evaluate the cost per acquisition (CPA) and conversion rate of these campaigns.  
  - *Free trial promotion analysis*: Review any free trial promotions run during this time. Was the trial duration, features offered, or onboarding process different? Examine the churn rate of users who signed up through this spike.  
  - *Potential audience mismatch*: Investigate user demographics and behavior during this period. Did the spike correlate with sign-ups from specific regions or user segments? Analyze feature usage among these trial users to see if they engaged with key value propositions.  
  - *Technical or billing issues*: Rule out any technical glitches or billing issues that might have temporarily affected direct paid sign-ups or inflated trial sign-ups.  
- Cross-check app store reviews or feedback during this time for additional context.

<!------------------------------ PAGE 2  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<h1 id="2-user-behavior-analysis">2. User Behavior Analysis</h1>

**🎯 Goal:** Identify high-converting in-app actions and behavioral patterns among different user types.

<img src="/assets/images/Screenshot_Mobile App_02.png" alt="User Behavior Dashboard Screenshot" width="800"/>

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

<!------------------------------ PAGE 3  ----------------------------------->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<h1 id="3-marketing-performance">3. Marketing Performance</h1>

**🎯 Goal:** Evaluate marketing channels by conversion, spend, and ROI to optimize acquisition strategy.

### 📊 Key Visualizations

<img src="/assets/images/Screenshot_Mobile App_03a.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

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
<img src="/assets/images/Screenshot_Mobile App_03b.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

> ⚠️ To ensure data accuracy for the campaign analysis, a data cleaning step was performed. The original `campaign` column presented inconsistencies in naming, which were resolved by grouping similar entries into these standardized categories:

- `sea` → Search Engine Advertising  
- `ugc` → User Generated Content  
- `vat` → VAT Campaign  

🔗 [View data cleansing here](https://github.com/dtbkhanh/Data-Analytics-and-Reports/blob/7da10cc3356b97b4d1f8d75133a124ccf609ac1f/Jupyter%20Notebooks/05.%20Mobile%20App%20Marketing%20%26%20Conversion%20Analysis.ipynb)

- Two campaigns (“Retargeting” and “Organic”) show 100% conversion, but each had only one user, so they’re not statistically meaningful.
- Google’s **Search Engine Advertising** brings the highest Max MRR, despite a lower conversion rate.
- The **Static Campaign** ranks second in Max MRR and has a high conversion rate of 52.3%.

**8–9. Promocode Analysis**

<img src="/assets/images/Screenshot_Mobile App_03c.png" alt="Marketing Performance Dashboard Screenshot" width="800"/>

- Promocode usage significantly boosts both conversion rate and conversion speed.


### 🔍 Insights

- **Social media (e.g., Facebook):** Demonstrates strong conversion rates and contributes significantly to revenue, suggesting a highly engaged audience. Consider further investment and scaling successful creatives.  
- **Search engine (Google):** While generating the highest user volume and MRR, search engine campaigns show a moderate conversion rate, indicating potential for optimization through improved keyword targeting and landing page relevance.  
- **Short-form video (TikTok):** Currently underperforming across key metrics (user volume, conversion, MRR), potentially due to a mismatch between the platform's demographics and our target audience. A carefully targeted experiment is recommended before further investment.


### ✅ Recommendations

**Channel Strategy:**

- **Facebook:** Increase budget to leverage its high conversion rates.
- **Google:** Optimize for better conversion by focusing on top campaigns (SEA), refining keyword targeting, and improving ad and landing page relevance.
- **TikTok:** Conduct a focused final experiment targeting people aged 25-35 who are interested in business, finance, and freelance topics, using content that addresses their pain points, before considering a budget cut.

**Campaign Tactics:**

- **Prioritize High ROI:** Allocate more budget to campaigns demonstrating strong return (e.g., SEA, Static).
- **Explore High-Potential:** Monitor and test scaling campaigns with high conversion rates but low volume (e.g., Retargeting, Organic).
- **Drive Faster Conversion:** Implement limited-time promos to encourage quicker subscriptions.

<!------------------------------ PAGE 4  ----------------------------------->

<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<h1 id="4-user-segmentation--targeting">4. User Segmentation & Targeting</h1>

**🎯 Goal:** Segment users by behavior, profession, and region to personalize marketing and onboarding.

### a. Regional Segmentation

<img src="/assets/images/Screenshot_Mobile App_04a.png" alt="Users by Region" width="800"/>

- **Berlin** stands out as the region with the largest user base, the highest conversion rate, and the highest Max MRR.   
  ➡️ Significantly increase marketing budget for Berlin to capitalize on this high-performing market.  
  ➡️ Conduct a thorough analysis of top-performing campaigns within Berlin to identify successful strategies that can be adapted and scaled to other promising regions.

- **Nordrhein-Westfalen & Bayern** demonstrate strong potential with high Max MRR and robust conversion rates.  
  ➡️ Maintain or slightly increase marketing investment in these regions.  
  ➡️ Implement A/B testing of new and innovative campaign ideas to further optimize performance and unlock additional user acquisition and revenue.
  
- **Mecklenburg-Vorpommern & Hamburg** has fewer users, but strong conversion efficiency.  
  ➡️ Explore growth potential by implementing targeted, low-budget awareness campaigns to increase user acquisition. Initial small investments could yield efficient returns.

- **Saarland** shows low user acquisition, poor conversion rates, and low revenue generation.  
  ➡️ Conduct in-depth market research within Saarland to understand the underlying reasons for the low performance and identify potential barriers to adoption.  
  ➡️ Based on the research findings, consider strategically reducing ad spend in this region or pivoting to highly targeted, experimental campaigns if a viable path to improvement is identified.


### b. Users by Self-Employment Status

<img src="/assets/images/Screenshot_Mobile App_04b.png" alt="Self-Employment Status" width="800"/>

- The majority identifies as self-employed, confirming strong alignment with the app's intended target audience.  
- A smaller segment comprises individuals who are not currently self-employed, potentially representing:
  - Users exploring the app out of general interest.
  - Individuals in the process of preparing to become self-employed.
  - A potential secondary market that could be further explored.

➡️ Continue prioritizing marketing and feature development for the core self-employed user base.  
➡️ Consider developing introductory or informational content tailored to the "pre-freelancer" segment to nurture potential future users.

### c. Profession-Based Segmentation

- **Artists & Content Creators** are the largest group and generate the highest Max MRR (due to size). However, their conversion rate is not the highest among all professions, indicating an opportunity for improvement. The high MRR is primarily driven by the sheer volume of users in this category.  
- **Disparity between Volume and Conversion**: Notably, the professions with the highest number of users are not necessarily the same as those with the highest conversion rates. This highlights the need for a nuanced approach to targeting.

### d. VAT Type Segmentation

<img src="/assets/images/Screenshot_Mobile App_04c.png" alt="VAT and Account Type" width="800"/>

- Most users fall under **franchise**, which are small businesses exempt from charging Value Added Tax (VAT).  
- Users under **subjectToVAT** show higher conversion rates, suggesting that businesses actively involved in VAT processes find greater utility and value in the app's features.

### e. Account Type Segmentation

- Most users are freelancers or solo business owners without VAT.  
- Complementary status users — those with a primary job and a freelancing side gig—have the highest conversion rates


### ✅ Recommendations

- **Region-specific Marketing:**
    - *High-performing regions* (e.g., Berlin, NRW): Develop and implement tailored campaigns to capitalize on existing strong performance.
    - *Under-tapped regions* (e.g., Hamburg): Test localized messaging and targeted campaigns to explore and unlock potential user growth.

- **Profession-based optimization:**
    - *High-converting professions*: Strategically allocate marketing budget to target these segments with tailored campaigns focused on their specific needs and pain points to maximize ROI.
    - *High-volume professions* (e.g., Artists & Content Creators): Implement a nurturing strategy involving identifying conversion blockers and running targeted A/B tests with profession-specific messaging and landing pages.

- **Targeting VAT-registered businesses:** Develop and deploy marketing messages that directly address the needs of **subjectToVAT** users, emphasizing features like streamlined VAT invoicing, comprehensive reporting, and efficient management.

- **Engaging dual-income users:** Prioritize marketing efforts towards dual-income users by highlighting how the app simplifies the complexities of managing multiple income streams.

- **Re-engagement of active but unsubscribed users:** Implement segmented re-engagement campaigns targeting users who have shown engagement (e.g., bank connections, feature usage) but haven't converted to paid plans.

- **Deepen user understanding:**
    - *Qualitative feedback*: Actively collect and analyze user feedback to inform UX improvements and refine marketing messaging.
    - *Comprehensive data analysis*: Conduct deeper segmentation analysis across profession, VAT type, region, and account status to uncover further opportunities for targeted strategies.

<!-- FINAL  -->
<div style="height: 2px; background-color: lightgray; margin: 40px 0;"></div>
<h1 id="final-takeaways">📌 Final Takeaways</h1>

This case study showed how integrating behavioral analytics and marketing performance can drive better user acquisition and retention. The combination of funnel tracking, feature analysis, and campaign ROI offers a blueprint for optimizing app growth strategies. By leveraging interactive dashboards and a structured analysis approach, we uncovered several key insights:
- **Feature engagement drives conversion**: Users who interact with advanced financial tools or the AI Assistant show significantly higher conversion rates. These features signal strong intent and deeper engagement.  
- **The onboarding experience is crucial**: Conversion likelihood is heavily influenced by the first feature users engage with. Early exposure to guided or advanced functionality leads to higher subscription rates.
- **Marketing ROI varies by Channel**: Facebook delivers the strongest conversion performance, while TikTok underperforms.
- **Regional performance varies significantly**: Berlin leads regionally with the highest conversion rate and MRR.
- **Profession & VAT status** influence conversion behavior, pointing to the value of profession-specific messaging and features for VAT-registered users.
- **Dual-income users** (e.g., freelancers with a main job) show the highest conversion rates and are an emerging high-value segment.

➡️ **Next steps:** We need to make the initial experience for new users better, focus more on the marketing that works best (like Facebook in strong regions), and try different ways to connect with users based on how they use the app and where they are. We'll keep tracking these things to make sure we keep growing effectively.
