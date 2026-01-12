

# Hotel Business: Understand and Improve Revenue

### Module 1: Data Modeling and Ingestion

**Intern:** Meenaal Joshi

**Date:** January 12, 2025

**Milestone:** 1

## Project Overview

This project focuses on building a robust Business Intelligence solution for a hotel chain to analyze booking patterns, revenue streams, and customer behavior. The goal of **Module 1** was to ingest raw CSV data, perform ETL (Extract, Transform, Load) operations using Power Query, and design a Star Schema data model in Power BI to facilitate high-performance reporting.

## Repository Structure

As per the submission guidelines, the repository is organized as follows:

```text
Hotel_Business_Understand_Improve_Revenue/
 ── Milestone 1/
     ├── Module1_PowerBI.pbix           # The main functional Power BI file
     ├── data/
     │   └── Hotel book (1).csv         # Raw dataset used for analysis
     ├── screenshots/                   
     │   ├── data_model.png             # Star Schema Diagram
     │   ├── power_query_steps.png      # ETL Transformations
     │   └── visuals.png                # Key insights visualization
     └── README.md                      # Project documentation

```

---

## Dataset Description

The source data (`Hotel book (1).csv`) contains daily aggregated booking records.

* **Timeframe:** Daily records (2024-2025).
* **Key Metrics:** Revenue, Occupancy Rate, ADR (Average Daily Rate), RevPAR, Expenses, and Profit.
* **Dimensions:** Guest Country, Guest Type (Business/Leisure), Booking Channel, and Seasonality.

---

## Methodology & Data Modeling

### 1. Data Transformation (Power Query)

The raw data was flat (denormalized). To create a scalable model, the following transformations were applied:

* **Base Query Creation:** Created a `Base_Data` staging query (load disabled) to act as the single source of truth.
* **Data Type Validation:** Ensured all currency fields were set to Fixed Decimal and dates to Date type.
* **Derived Dimensions:** Since the raw data lacked specific dimension tables, I engineered them:
* **Dim_Room:** Derived from unique price points (ADR) to categorize rooms into "Standard" and "Premium".
* **Dim_Branches:** Created a custom column to simulate a multi-branch structure (Main Hotel Branch) for future scalability.
* **Dim_Customer:** Created using unique combinations of `Guest_Type` and `Guest_Country`.



### 2. The Star Schema

A **Star Schema** was designed to optimize query performance.

* **Fact Table:** `Fact_Bookings` (Contains all quantitative metrics like Revenue, Costs, No_shows).
* **Dimension Tables:**
* `Dim_Date` (Linked via Date).
* `Dim_Customer` (Linked via Surrogate Key `Customer ID`).
* `Dim_Room` (Linked via Surrogate Key `Room_Key`).
* `Dim_Branches` (Linked via Surrogate Key `Branch_ID`).



> **Relationship Logic:** relationships were established as **1-to-Many** (from Dimension to Fact) to ensure accurate filtering and slicing.

### 3. Calculated Columns (DAX)

To meet the business requirements, the following columns were calculated in the Fact Table:

**A. Room Category** (Segmentation based on Average Daily Rate)

```dax
Room Category = IF('Fact_Bookings'[ADR] >= 125, "Premium", "Standard")

```

**B. Booking Duration** (Proxy logic based on Average Length of Stay)

```dax
Booking Duration = DIVIDE('Fact_Bookings'[Reserved_Rooms], 'Fact_Bookings'[Checkins], 1)

```

**C. Stay Type** (Categorization of stay length)

```dax
Stay Type = SWITCH(
    TRUE(),
    'Fact_Bookings'[Booking Duration] < 3, "Short",
    'Fact_Bookings'[Booking Duration] <= 7, "Medium",
    'Fact_Bookings'[Booking Duration] > 7, "Long",
    "Unknown"
)

```

---

## Key Observations

Based on the initial data modeling and visualization:

1. **Revenue Drivers:** Premium rooms contribute significantly to the total revenue despite having lower occupancy volume compared to standard rooms.
2. **Stay Duration:** The majority of bookings fall into the "Medium" (3-7 days) category, suggesting a strong leisure market.
3. **Seasonality:** Revenue peaks during specific seasons, correlating with the "Holiday" flag in the dataset.
4. **Customer Demographics:** There is a distinct split between "Business" guests (mostly short stays) and "Leisure" guests (medium/long stays).



For any queries regarding this milestone, please contact: **[Your Email]**
