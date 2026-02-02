# Hotel Revenue Analysis - Milestone 3

## Forecasting Approach & Logic

To predict future demand and assist in workforce planning, I implemented a forecasting model integrating historical trends with predictive analytics.

* **Forecasting Methodology:** I utilized booking data to generate predictive values (`yhat`) including upper and lower confidence intervals. These were imported into Power BI to visualize potential future occupancy.
* **Forecast Visualization:** The dashboard compares the **Actuals** against the **Forecasted Demand**, allowing for a direct comparison between realized performance and predicted targets.

---

## Cancellation & No-Show Analysis

To understand revenue leakage, I created specific visuals to track guests who cancel or fail to arrive.

* **Cancellation Rate:** I calculated this metric to track the percentage of total bookings that result in a cancellation, helping to identify retention issues.
  **DAX measure:** `DIVIDE([Total Cancellations], [Total Bookings], 0)`

* **No-Show Trends:** I created a dedicated line chart to track the volume of **No-Shows** over time. This visual helps identify specific days or seasons where guests frequently fail to check in without cancelling, indicating "wasted inventory" that could have been resold.

---

## Key Insights and Business Implications

From the forecasting and cancellation analysis, the following business implications were observed:

1.  **Future Demand Peaks:** The forecast indicates specific upcoming periods where booking volume is predicted to exceed the moving average. These periods require proactive **staffing adjustments** and **inventory management** to prevent service bottlenecks.
2.  **Cancellation Behavior:** Fluctuations in the **Cancellation Rate** correlate with specific seasonal shifts. High cancellation periods suggest a need to review **non-refundable rate policies** or implement stricter deposit rules during peak seasons.
3.  **Revenue Leakage Source:** The **No-Show** analysis highlights patterns of wasted inventory. Identifying these trends allows the management to consider overbooking strategies or pre-arrival confirmation checks during high-risk periods.
