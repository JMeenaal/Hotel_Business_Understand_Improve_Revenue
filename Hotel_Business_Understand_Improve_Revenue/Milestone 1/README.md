# Milestone 1: Data Modeling and Ingestion

## Project Description
This project focuses on data modeling and ingestion to analyze hotel revenue. It involves transforming raw booking data into a Star Schema in Power BI to derive insights on booking duration, room categories, and stay types.

## Dataset Description
The dataset (`hotel_data.csv`) contains raw booking information including customer details, room types, and transaction dates.

## Methodology & Modeling Steps
1. **Data Loading:** Loaded CSV into Power BI.
2. **Data Transformation (Power Query):**
   - Cleaned headers and checked for null values.
   - Verified data types for dates and revenue columns.
3. **Data Modeling (Star Schema):**
   - **Fact Table:** `Bookings`
   - **Dimension Tables:** `Date`, `Room`, `Customer`, `Hotel Branches`
4. **Calculated Columns (DAX):**
   - **Booking Duration:** Calculated as `[Check-out Date] - [Check-in Date]`.
   - **Room Category:** Categorized based on room type codes.
   - **Stay Type:** Classified as Short, Medium, or Long based on duration.

## Repository Structure
- **Module1_PowerBI.pbix**: The functional Power BI file.
- **Data/**: Contains the source CSV file.
- **Screenshots/**: Evidence of the Data Model, Power Query steps, and Visualizations.
