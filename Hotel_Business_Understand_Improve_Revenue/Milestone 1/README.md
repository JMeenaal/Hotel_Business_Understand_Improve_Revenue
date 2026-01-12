# Hotel Business: Understand and Improve Revenue

## Project Description
This project focuses on data modeling and ingestion to analyze hotel revenue performance. The goal was to transform raw booking data (spanning 2018-2020) into a structured **Star Schema** in Power BI. This involved extensive cleaning, feature engineering in Power Query, and creating a robust data model to derive insights on booking duration, room categories, and revenue trends.

## Dataset Description
The source data consists of three separate datasets (`2018`, `2019`, `2020`) containing hotel booking records. Key attributes include:
* **Booking Details:** Arrival dates, status (check-out, canceled), and meal plans.
* **Customer Demographics:** Adults, children, babies, and country of origin.
* **Room & Revenue:** Reserved room types, market segments, and pricing.

## Methodology & Modeling Steps

### 1. Data Ingestion & Cleaning (Power Query)
* **Data Loading:** Imported datasets for years 2018, 2019, and 2020.
* **Error Handling:** Identified error values in the `children` column and replaced them with `0`.
* **Data Consolidation:** Appended all three tables into a single master table named **`Raw_fact`**.

### 2. Feature Engineering & Key Creation
To facilitate a Star Schema, several custom keys and columns were created within Power Query:
* **Booking_ID:** Generated a unique primary key using an Index Column (starting from 1).
* **Date_Key:** Created a custom surrogate key using M-code: `Date.Year([arrival_date])*10000 + Date.Month([arrival_date])*100 + Date.Day([arrival_date])`.
* **Cost & Discount Columns:** Created conditional columns based on `meal` and `market_segment` mappings.
* **ID Mapping:** Generated `hotel_id` and `room_id` by duplicating and mapping descriptive columns.

### 3. Dimension Modeling
Dimension tables were created by duplicating the `Raw_fact` table, selecting relevant columns, and removing duplicates to ensure unique keys:
* **`Dim_Hotel`:** Derived from `hotel` and `hotel_id`.
* **`Dim_Room`:** Derived from `reserved_room_type` and `room_id`.
* **`Dim_Date`:** Derived from `arrival_date` and `Date_Key`.
* **`Dim_Customer`:** Created by grouping unique combinations of `adult`, `children`, `babies`, and `country`, then adding a custom `customer_id` index.
    * *Transformation:* Merged `Dim_Customer` back into `Raw_fact` to bring the `customer_id` foreign key into the fact table.

### 4. Data Modeling (Star Schema)
The final model follows a Star Schema architecture with **One-to-Many** relationships:
* **Fact Table:** `Raw_fact`
* **Dimension Tables:** `Dim_Hotel`, `Dim_Room`, `Dim_Date`, `Dim_Customer`

### 5. Calculated Columns (DAX)
New metrics were added using DAX for analysis:
* **Booking Duration (Total Nights):** `DATEDIFF('Raw_fact'[Check-in Date], 'Raw_fact'[Check-out Date], DAY)`
* **Stay Type:** Categorized duration into:
    * *Short* (0-3 days)
    * *Medium* (4-7 days)
    * *Long* (8+ days)
* **Room Category:** Grouped room codes (A, B, C...) into business categories (Standard, Luxury, etc.) using `SWITCH`.

## Key Observations
* **Occupancy Drivers:** The "Standard" room category (Type A) accounts for the highest volume of bookings.
* **Revenue Sources:** Short-term stays contribute the majority of revenue, indicating a high turnover of transient guests.
* **Demographics:** A significant portion of guests are adults traveling without children, correlating with the high volume of "Business" market segment bookings.

## Repository Structure
```text
Hotel_Business_Understand_Improve_Revenue/
 ── Milestone 1/
    ├── Module1_PowerBI.pbix      # Functional Power BI file with Star Schema
    ├── data/
    │   └── hotel_data.csv        # (Attached dataset)
    ├── screenshots/              
    │   ├── data_model.png        # Evidence of Star Schema
    │   ├── power_query_steps.png # Evidence of Appending & Cleaning
    │   └── visuals.png           # Key insights
    └── README.md                 # Project documentation
