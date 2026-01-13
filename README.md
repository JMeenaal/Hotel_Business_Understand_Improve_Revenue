

# Hotel Business: Understand and Improve Revenue

### Module 1: Data Modeling and Ingestion

## Dataset Description

The source data (`Hotel book (1).csv`) contains daily aggregated booking records.

* **Timeframe:** Daily records (2024-2025).
* **Key Metrics:** Revenue, Occupancy Rate, ADR (Average Daily Rate), RevPAR, Expenses and Profit.
* **Dimensions:** Guest Country, Guest Type, Booking Channel and Seasonality.


## Data Modeling Steps

### 1. Data Transformation (In Power Query)

* **Base Query Creation:** Created a `fact table` query to act as the single source of truth.
* **Data Type Validation:** Ensured all currency fields were set to Fixed Decimal and dates to Date type.
* **Derived Dimensions:** Since the raw data lacked specific dimension tables, made the following:
    **Dim_Room:** Derived from unique price points (ADR) to categorize rooms into "Standard" and "Premium".
    **Dim_Branches:** Created a custom column to simulate a multi-branch structure (Main Hotel Branch) for future scalability.
    **Dim_Customer:** Created using unique combinations of `Guest_Type` and `Guest_Country`.

### 2. The Star Schema

* **Fact Table:** `Fact_Bookings`
* **Dimension Tables:**
* `Dim_Date` (Linked via Date).
* `Dim_Customer` (Linked via Surrogate Key `Customer ID`).
* `Dim_Room` (Linked via Surrogate Key `Room_Key`).
* `Dim_Branches` (Linked via Surrogate Key `Branch_ID`).

## Key Observations

Based on the initial data modeling and visualization:

1. **Revenue Drivers:** Premium rooms contribute significantly to the total revenue despite having lower occupancy volume compared to standard rooms.
2. **Stay Duration:** The majority of bookings fall into the "Medium" (3-7 days) category, suggesting a strong leisure market.
3. **Seasonality:** Revenue peaks during specific seasons, correlating with the "Holiday" flag in the dataset.
4. **Customer Demographics:** There is a distinct split between "Business" guests (mostly short stays) and "Leisure" guests (medium/long stays).


