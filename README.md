# gtc-ml-project1-hotel-bookings  
🏨 **GTC ML Project 1 – Data Cleaning & Preprocessing Challenge**

---

## 📌 Objective  
The goal of this project is **not** to build the final machine learning model, but to prepare the raw hotel booking data for predictive modeling.  
We aim to create a **robust data preprocessing pipeline** that handles missing values, outliers, duplicates, feature engineering, and encoding — ensuring the dataset is **ML-ready**.  

---

## 🛠 Business Problem  
The hotel’s revenue team has identified that **last-minute booking cancellations** significantly reduce profitability.  
A clean and reliable dataset will help future ML models **predict cancellations** and support better decision-making.  

---

## 📂 Dataset  
- **File:** `hotel_bookings.csv`  
- **Rows:** ~119K  
- **Columns:** 32  
- **Target:** `is_canceled` (1 = Canceled, 0 = Not Canceled)  

### 🔑 Key Columns  
- `lead_time` – Number of days before arrival the booking was made.  
- `adr` – Average Daily Rate (price per night).  
- `arrival_date_year`, `arrival_date_month` – Check-in date.  
- `adults`, `children`, `babies` – Number of guests.  
- `meal`, `market_segment`, `deposit_type`, `customer_type` – Booking characteristics.  

---

## 🚀 Project Workflow  

### **Phase 1: Exploratory Data Analysis (EDA)**  
- Loaded dataset & generated `.info()`, `.describe()`.  
- Identified missing values (`agent`, `company`, `country`, `children`).  
- Visualized missing data with **heatmap** & **missingno**.  
- Detected outliers in `adr` & `lead_time` using **boxplots + IQR**.  
- Documented data quality issues.  

### **Phase 2: Data Cleaning**  
- **Handled Missing Values:**  
  - `agent`, `company` → replaced with `0`.  
  - `country` → imputed with mode.  
  - `children` → imputed with median.  
- Removed duplicates.  
- Handled Outliers: capped `adr` at **1000**.  
- Fixed data types: converted `reservation_status_date` → datetime.  

### **Phase 3: Feature Engineering & Preprocessing**  
- **Created new features:**  
  - `total_guests = adults + children + babies`  
  - `total_nights = stays_in_weekend_nights + stays_in_week_nights`  
  - `is_family = 1 if (children + babies > 0)`  
- **Encoded categorical variables:**  
  - One-Hot Encoding → `meal`, `market_segment`, `deposit_type`, etc.  
  - Frequency/Grouping → `country`.  
- **Removed data leakage columns:**  
  - `reservation_status`  
  - `reservation_status_date`  
- **Final Train-Test Split:** 80/20 with stratification on target.  

---

## 📊 Key Insights from EDA  
- ~37% of bookings were **canceled**.  
- High `lead_time` is strongly correlated with cancellations.  
- `adr` contains extreme outliers (capped at 1000).  
- Guests from some countries cancel at higher rates.  
- Certain market segments (e.g., **Online TA**) show higher cancellations.  

---
