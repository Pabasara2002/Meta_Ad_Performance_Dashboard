# Meta Ad Performance Dashboard 📊

An interactive, insights-driven Power BI dashboard designed to analyze marketing funnel metrics, audience demographics, and geographic performance from Meta Ads (Facebook & Instagram). This report transforms raw ad tracking data into a comprehensive visual tool for optimization and executive reporting.

## 🚀 Live Visuals & Features

Based on the latest design schema, the dashboard tracks the following core components:
* **Dynamic Metric Switcher:** A dedicated control panel allowing users to instantly toggle the entire dashboard between core metrics (Impressions, Clicks, Engagements, Purchases).
* **Complete Marketing Funnel Tracking:** High-level KPI cards breaking down the user conversion journey step-by-step from awareness to purchase.
* **Audience Demographics:** Visual breakdowns of performance metrics grouped by **Gender** (Donut Chart) and **Age Group** (Clustered Column Chart).
* **Geographic Map Performance:** An interactive Map Visualization that dynamically plots and sizes performance bubbles based on user country data.
* **Advanced Root-Cause Analysis:** Integrated **Decomposition Tree** tracking how specific audience slices (Gender → Age Group → Platform) impact conversions.

---

## 🛠️ Data Model & Schema

The data engine is built on top of relational tables tracking active ad campaigns and user demographics:

### 1. `campaigns` Table
Contains structural tracking data for launched advertisements:
* `ad_id` (Unique Identifier)
* `campaign_id`
* `ad_platform` (Facebook, Instagram, etc.)
* `ad_type` (Image, Video, Carousel)
* `target_gender` / `target_age_group` / `target_interests`

### 2. `users` Table
Tracks real-time performance interaction data mapped back to target metrics:
* `user_id`
* `country` *(Data categorized as Country/Region for Bing Maps mapping)*
* `age_group` / `user_age`
* `user_gender`
* `interests` / `location`

---

## 💡 Key DAX Formulations Used

### Dynamic Measure Display
To allow the single-selection dropdown filter for metrics, a dynamic switching metric was implemented:
```dax
Select Dynamic Measure = 
SWITCH(
    SELECTEDVALUE('Select Dynamic Measure Slicer'[MetricName]),
    "Impressions", SUM(users[Impressions]),
    "Clicks", SUM(users[Clicks]),
    "Purchases", SUM(users[Purchases]),
    SUM(users[Impressions]) -- Default Fallback
)
