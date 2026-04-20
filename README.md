# uber-analytics
## Data Source
All data used in this Tableau portfolio is sourced from [Kaggle](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard). 

This dataset contains detailed ride-sharing data from Uber operations for the year 2024, providing insights into booking patterns, vehicle performance, revenue streams, cancellation behaviors, and customer satisfaction metrics.


## Dashboard
### Overview
<img width="750" height="600" alt="master" src="https://github.com/user-attachments/assets/a3e6c100-33e2-4539-8c18-e7531ef78e20" />

#### Analysis
A **$51.8M total revenue** looks like a win but the **62% Success Rate** is basically telling us that we're letting nearly 4 out of 10 of them walk away after convincing them to open the app and click 'Book'. This is a massive leakeage.

If you look at the **Booking Status** donut, the "villain" isn’t the customer but the supply side. **Driver-led cancellations (18%)** are more than double customer cancellations (7%). It suggests that our drivers are "cherry-picking" rides or that our current incentive structure isn't enough to keep them committed once they’ve accepted a booking.

The **Bookings over Time** chart shows something even more systemic: our demand is a flat line. At a steady ~12.4k rides a month, this is a mature, predictable market with zero seasonality. Yet, despite knowing exactly how many rides are coming, we still have **7% of bookings failing because "No Driver Found."** This isn't a "holiday rush" problem; it's a structural failure to align our fleet with predictable demand. 

Between the **25% Cancellation Rate** and the **6% Incomplete rides**, we are burning operational overhead on 31% of our total volume with zero payout. If we can just nudge the driver-side behavior by 5%, we’re looking at **$2.5M in "found money"** without spending a single cent on marketing or new user acquisition. It’s the easiest growth lever we have, but right now, we’re just letting that revenue evaporate.

### Leakage
<img width="750" height="600" alt="cancellation" src="https://github.com/user-attachments/assets/02e97122-041b-4db9-849b-c02b28fac8f0" />

#### Analysis

While initial raw data suggested 100% cancellation at 16+ minutes, a volume-check revealed those were outliers with low sample sizes. I filtered the analysis to the 5–14 minute high-volume window to identify a reliable 4% surge in customer churn, pinpointing exactly where dispatch efficiency begins to impact the bottom line.

At 25% cancellation rate might look like a standard cost of doing business in a messy market but it's attached with a $4.5M price tag. With an average wait time of 8.5 minutes, we are hovering right on the edge of the customer's patience.

The 72% driver-led split proves this is a supply-side crisis. Drivers are actually ghosting 3 out of every 4 cancelled rides. This behavior is the primary engine behind our $4.5M leakage.

Looking at the Reasons for Cancelling, nearly 18% of cancellations are tied to customers being "coughing/sick" or having "more than permitted people" in the car. This reveals a massive disconnect in expectations: customers are trying to "overload" smaller vehicle types (likely Go Mini) to save money, and drivers are rightfully refusing them.

If you look at the Cancellation Rate per Minutes Waited, the trend is relatively stable until we hit the 11-minute mark, where the probability of a cancellation spikes by nearly 50%. This is the psychological breaking point for a user in the NCR. Up until 11 minutes, they are committed. At 12 minutes, they start looking for an alternative.


#### Suggestion

Based on the "Friction points" identified in your analysis, here are the strategic recommendations to plug the revenue leakage and stabilize the platform:

- Implement an algorithm that prioritizes bookings where the VTAT is predicted to be under 11 minutes. For rides estimated at 12+ minutes, introduce incentives for drivers to accept and complete these "high-risk" trips.
- For wait times approaching the 11-minute mark, trigger in-app notifications to manage expectations and keep the user committed.
- Implement a "Driver Not Moving" automated alert. If a driver remains stationary for 2 minutes after accepting a ride, the system should auto-reassign the booking to the next nearest driver to prevent the customer from hitting the 11-minute frustration threshold.
- Replace flat cancellation fees with a tiered system. Drivers with high cancellation rates during peak demand should face temporary "dispatch cooling-off" periods or reduced priority for high-value bookings.
- Require users to select the number of passengers *before* booking a "Go Mini." If the count exceeds 4, the app should automatically gray out the Mini option and suggest a Sedan or XL to prevent the "overcrowding" cancellations at the pickup point.
- If the system detects a high volume of capacity-related cancellations in a specific neighborhood, push targeted "XL Discount" coupons to those users to move demand toward the right vehicle size.
Any vehicle receiving two such complaints in 48 hours should be blocked from the "Premier" or "Sedan" category until the driver uploads a service receipt or photo evidence of repair.
- To reduce "Coughing/Sick" cancellations, provide drivers with clear sanitization protocols and offer riders the option to add a "Sanitized Vehicle" preference for a small premium, ensuring both parties feel safe before the trip begins.

* **Actionable Outreach:** Direct the Operations team to focus exclusively on the **15% actionable reasons**. Resolving just these specific technical and behavioral issues could immediately recover **~$680k** without the need for expensive new user acquisition campaigns.

**Would you like to build a "Solutions Impact" slide next to estimate how much revenue each of these points would specifically recover?**
### Vehicles
<img width="1000" height="800" alt="vehicle" src="https://github.com/user-attachments/assets/80f74313-a7d3-4c8e-9f24-496e7e7beab0" />


## Styling 
All the styling choices are made accordingly to [Uber Branding Guide](https://brandingstyleguides.com/guide/uber-2018/).
