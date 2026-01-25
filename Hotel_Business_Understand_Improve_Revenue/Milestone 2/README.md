Hotel Revenue Analysis - Milestone 2


Revenue and Occupancy Metrics

For the key performance indicators, I used the following DAX measure:

Occupancy %: I calculated this by dividing the total rooms sold by the total rooms available to get the true percentage of utilized capacity. 

DAX measure: DIVIDE([Total Rooms Sold], [Total Rooms Available], 0)

Average Daily Rate (ADR): I calculated it by dividing the total room revenue by the total rooms sold. 

DAX measure: DIVIDE([Total Room Revenue], [Total Rooms Sold], 0)

Revenue per Available Room (RevPAR): This tracks the revenue generated per available room, regardless of whether it was occupied. 

DAX measure: DIVIDE([Total Room Revenue], [Total Rooms Available],0)

Guest Classification and Segmentation Logic

To classify guests, I created specific logic to group them into meaningful segments based on their booking behavior.

For spending habits, I created a calculated column based on the ADR. Guests paying above 128 are classified as High Spenders, those paying between 122 and 127 are Medium Spenders and anyone paying below 122 is considered a Low Spender.

For loyalty, I compared the Total Bookings against New Bookings. This allowed me to separate First-time guests from Loyal returning guests in the visual analysis.

I also segmented guests by Booking Source to clearly compare the volume and revenue coming from Direct bookings versus Online Travel Agents (OTA).

Key Insights and Observations

From the dashboard analysis, a few key trends stood out:

The occupancy trends show clear seasonal patterns, with specific seasons driving higher demand than others. When looking at the revenue mix, 
there is a clear distinction between OTA and Direct bookings, which highlights which channel is driving the most consistent volume.

Geographically, guests from different countries show different behaviors regarding their length of stay and average spend. Some regions tend to book longer stays with a moderate spend, while others are shorter but yield a higher ADR.
