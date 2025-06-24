# Airbnb Occupancy and Revenue Analytics Using Spark - Los Angeles County

## Project Overview
This project aims to analyze **Airbnb occupancy rates and revenue trends** in **Los Angeles County** using **Apache Spark**. It integrates **Airbnb listings data**, **crime statistics**, and **public transportation availability** to uncover insights that can help optimize pricing strategies, improve listing appeal, and assist hosts in making informed investment decisions.

By incorporating external factors like **crime rates and public transportation accessibility**, this study provides a **holistic perspective** on the Airbnb market, going beyond conventional pricing models that rely solely on historical trends.

## Objectives
- **Prediction:** Develop models to estimate **Airbnb listing prices** and **occupancy rates**.
- **Inference:** Identify **key factors** influencing pricing and occupancy.
- **Recommendations:** Offer actionable insights for **optimizing amenities, locations, and pricing**.
- **Revenue Forecasting:** Enable hosts to **estimate potential earnings** based on demand trends.

## Data Sources
The project aggregates and processes **four datasets**:
1. **Airbnb Listings Data** - Retrieved from [InsideAirbnb](https://insideairbnb.com/los-angeles/), containing **45,533 listings** with **82 features** (e.g., price, reviews, host details, availability).
2. **Crime Data** - Obtained from [LAPD](https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8/about_data), containing **130,000 crime records**, mapped to zip codes.
3. **Public Transportation Data** - Includes **bus stops** and **metro stations** from the [Los Angeles Public Transportation dataset](https://geohub.lacity.org/).
4. **Aggregations & Merging:** Crime and transportation data were processed using **GeoPandas** to map their locations to zip codes and integrated with Airbnb listings.

## Data Processing
- **Missing Value Treatment:**
  - Numeric columns (e.g., `bathroom_count`) filled with **zero**.
  - `days_since_last_review` replaced with **-1** when missing.
  - Mean imputation by **zip code** to account for location variations.
- **Outlier Treatment:**
  - Removed **4,800 extreme values** in pricing.
  - Applied **log transformation** to reduce skewness.
- **Feature Engineering:**
  - **Categorical Encoding:** Grouped property types and amenities.
  - **Zip Code Encoding:** Used ordinal encoding.
  - **Temporal Features:** Converted dates into numerical attributes.

## Machine Learning Models
We leveraged **PySpark** for scalable ML modeling:

| Model                 | Price Prediction (R²) | Occupancy Prediction (R²) |
|----------------------|----------------------|--------------------------|
| **Linear Regression**  | 52.97% | 89.99% |
| **Random Forest**      | 63.66% | 91.61% |
| **Gradient Boosted Trees (GBT)** | **76.80%** | **94.6%** |

🔹 **Gradient Boosted Trees (GBT) outperformed all models** for price prediction.
🔹 **Random Forest provided the best occupancy prediction** results.

## Key Findings
### 🔹 **Top Factors Affecting Pricing**
- **Weapons-related crime rates**
- **Superhost status**
- **Free Wi-Fi and Internet**
- **Number of reviews**
- **Safety features (e.g., smoke detectors)**
- **Swimming pools and kitchen essentials**
- **Number of bathrooms**

### 🔹 **Top Factors Affecting Occupancy**
- **Years as host** and **host response rate**
- **Total listings owned by the host**
- **Average minimum nights required**
- **Total amenities offered**
- **Private room listings**

### 🔹 **Surprising Insights**
1. **Low Seasonality:** Only **~3,000 listings** showed seasonal trends in bookings.
2. **Crime Impact:** Only **weapon-related crimes** influenced occupancy/pricing.
3. **Location Preferences:** Outskirts of Los Angeles had **higher occupancy rates** than downtown.
4. **Pricing Strategy:** High-end unique stays had **low occupancy** but **higher prices**, targeting niche travelers.


## Revenue Prediction
- Forecasted revenue for **next 90 days** by multiplying **predicted price × occupancy**.
- Analysis by **zip code, property type, and room type** to help hosts maximize earnings.

## Tech Stack
- **Data Processing:** Apache Spark, PySpark, Pandas, GeoPandas
- **Machine Learning:** Scikit-learn, PySpark MLlib
- **Visualization:** Matplotlib, Seaborn, Tableau
- **Data Storage:** CSV, JSON
