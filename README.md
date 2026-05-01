# uber-analytics
## Data Source
All data used in this Tableau portfolio is sourced from [Kaggle](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard). 

This dataset contains detailed ride-sharing data from Uber operations for the year 2024, providing insights into booking patterns, vehicle performance, revenue streams, cancellation behaviors, and customer satisfaction metrics.


## Dashboard
### Overview
<img width="750" height="600" alt="master" src="https://github.com/user-attachments/assets/a3e6c100-33e2-4539-8c18-e7531ef78e20" />

#### Analysis
The **62% Success Rate** is basically telling us that we're letting nearly 4 out of 10 of them walk away after convincing them to open the app and click 'Book'. This is a massive leakeage.

If you look at the `Booking Status` donut, the major cause of this phenomenon isn’t from the customer but the supply side. `Driver-led cancellations` (18%) are more than double `customer cancellations` (7%). It suggests that our drivers are either "cherry-picking" rides or that our current incentive structure isn't enough to keep them committed once they’ve accepted a booking.

Even more, the `Bookings over Time` chart shows that our demand is a flat line. At a steady ~12.4k rides a month, this is a mature, predictable market with zero seasonality. Yet, despite knowing exactly how many rides are coming, we still have 7% of bookings failing because `No Driver Found`. This is a structural failure to align our fleet with predictable demand. 

Adding the 25% `Cancellation Rate` and the 6% `Incomplete rides`, we are burning operational overhead on 31% of our total volume with zero payout. 

If we can just nudge the driver-side behavior by 5%, we’re looking at **$2.5M added revenue** without spending a single cent on marketing or new user acquisition. It’s the easiest growth lever we have, but right now, we’re just letting that revenue evaporate.

### Leakage
<img width="750" height="600" alt="cancellation" src="https://github.com/user-attachments/assets/02e97122-041b-4db9-849b-c02b28fac8f0" />

#### Analysis

While initial raw data suggested 100% cancellation at 16+ minutes, a volume-check revealed those were outliers with low sample sizes. I filtered the analysis to the 5–14 minute high-volume window to identify a reliable 4% surge in customer churn, pinpointing more relevantly where dispatch efficiency begins to impact the bottom line.

At 25% cancellation rate might look like a standard cost of doing business in a messy market but it's attached with a $4.5M price tag. With an average wait time of 8.5 minutes, we are right on the edge of the customer's patience.

If you look at the Cancellation Rate per Minutes Waited, the trend is relatively stable until we hit the 11-minute mark, where the probability of a cancellation spikes by nearly 50%. This is the psychological breaking point for a user in the NCR. Up until 11 minutes, they are committed. At 12 minutes, we start to lose them rapidly.

Further more, he 72% driver-led split proves this is a supply-side crisis. Drivers are actually ghosting 3 out of every 4 cancelled rides. This behavior is the primary engine behind our $4.5M leakage.

One other insight in the `Reasons for Cancelling`, nearly 18% of cancellations are tied to customers being "coughing/sick" or having "more than permitted people" in the car. This reveals an insight that customers are trying to "overload" smaller vehicle types (likely Go Mini) to save money, and drivers arem rightfully, refusing them.

#### Suggestion
- Implement an algorithm that prioritizes bookings where the VTAT is predicted to be under 11 minutes. For rides estimated at 12+ minutes, introduce incentives for drivers to accept and complete these "high-risk" trips.
- For wait times approaching the 11-minute mark, trigger in-app notifications to manage expectations and keep the user committed.
- Implement a "Driver Not Moving" automated alert. If a driver remains stationary for 2 minutes after accepting a ride, the system should auto-reassign the booking to the next nearest driver to prevent the customer from hitting the 11-minute frustration threshold.
- Replace flat cancellation fees with a tiered system. Drivers with high cancellation rates during peak demand should face temporary "dispatch cooling-off" periods or reduced priority for high-value bookings.
- Require users to select the number of passengers *before* booking a "Go Mini." If the count exceeds 4, the app should automatically gray out the Mini option and suggest a Sedan or XL to prevent the "overcrowding" cancellations at the pickup point.
- If the system detects a high volume of capacity-related cancellations in a specific neighborhood, push targeted "XL Discount" coupons to those users to move demand toward the right vehicle size.
Any vehicle receiving two such complaints in 48 hours should be blocked from the "Premier" or "Sedan" category until the driver uploads a service receipt or photo evidence of repair.
- To reduce "Coughing/Sick" cancellations, provide drivers with clear sanitization protocols and offer riders the option to add a "Sanitized Vehicle" preference for a small premium, ensuring both parties feel safe before the trip begins.
- Focus exclusively on the **15% actionable reasons**. Resolving just these specific technical and behavioral issues could immediately recover **~$680k** without the need for expensive new user acquisition campaigns.

### Vehicles
<img width="1000" height="800" alt="vehicle" src="https://github.com/user-attachments/assets/80f74313-a7d3-4c8e-9f24-496e7e7beab0" />
#### Analysis

The raw volume masks a significant operational bottleneck: `Go Sedan` and `Auto` are currently underperforming the platform’s average success rate of ~62%. This discrepancy suggests that while demand for these core four-wheel and three-wheel services is massive, we are "leaking" potential revenue due to fulfillment failures in our most popular categories.

Despite having the highest average ride distance (reaching ~25.0 km), `eBike` yields the lowest revenue per kilometer, dipping below the $35/km mark. We are essentially subsidizing long-range travel on our most hardware-intensive (electric) assets without the premium return to justify the wear and tear.

The `Uber XL` segment boasts the highest success rate on the platform (>63%), yet it contributes the least to total revenue (~$1.5M) and maintains the shortest average ride distance. We are using our highest-capacity vehicles for short-burst trips where their utility is wasted, while `Go Sedan` — the vehicle type users likely want for those mid-to-long range trips — suffers from the lowest success rate in the fleet (sub-62%).

Finally, `Bike` is the "Goldilocks" segment of the current dashboard. It successfully balances a high success rate with an average ride distance and booking value that sits comfortably above the platform average. It is currently the most stable bridge between user demand and driver reliability.

#### Suggestion
- Implement a dispatch nudge that incentivizes `Uber XL` drivers to accept bookings only when the party size is 4+ or the distance exceeds a certain threshold, preventing high-capacity supply from being tied up in low-value, short-distance "convenience" trips.
- Given they are currently traveling the furthest for the lowest per-km return, the pricing model for `eBike` needs to shift from flat-heavy to distance-sensitive to recover the current yield gap.
- Prioritize driver onboarding and incentives specifically for the `Go Sedan` category.
- Introduce a "premier status" for drivers in the `Auto` and `Go Sedan` categories who maintain a success rate above 65%, granting them priority access to the higher-value, longer-distance bookings currently being underserved.
- During high-demand periods where Go Sedan success rates plummet, offer users a discounted "XL Upgrade" to mop up excess demand using the underutilized but highly reliable XL fleet.

## Styling 
All the styling choices are made accordingly to [Uber Branding Guide](https://brandingstyleguides.com/guide/uber-2018/).
