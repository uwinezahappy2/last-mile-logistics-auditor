#The "Last Mile" Logistics Auditor


Client: Veridi Logistics


A. Executive Summary


An analysis of Veridi Logistics' delivery data reveals that inaccurate estimated delivery dates are directly causing severe customer dissatisfaction. This is not a nationwide issue; it is heavily concentrated in specific regions, with states like Alagoas (AL) and Maranhão (MA) experiencing late delivery rates nearly three times the national average (8.1%). The data proves a strong correlation between delays and sentiment: while on-time packages average 4.29 stars, "Super Late" packages (5+ days late) plummet to an average of 1.79 stars. Furthermore, the root cause extends beyond external carriers—packages that end up being delivered late spent significantly more time in our internal warehouse before handoff, pointing to a critical internal operational bottleneck.


B. Project Links


Link to Notebook: https://colab.research.google.com/drive/1zYPyN1Cv1GJsPwsTvhm9kQqY5Etbq1Nd#scrollTo=phP3IGkW5oc2

Link to Dashboard: https://datastudio.google.com/u/0/reporting/f41228c0-6d04-418b-9857-e417a4bb0f3e/page/EcNwF

Link to Presentation: https://docs.google.com/presentation/d/1NUXFaVUqkxnLxKzccw7RyIBiHsmYo6WSlpQ1_IvaBS0



C. Technical Explanation


Data Cleaning:The Olist dataset presented two major cleaning challenges. First, the order_reviews_dataset contained multiple reviews for a single order_id (customers updating their reviews). To prevent row duplication during the join—which would have ruined our aggregation metrics—I deduplicated the reviews by keeping only the last submitted review per order. Second, I excluded all orders with a status of 'canceled' or 'unavailable', as these lacked actual delivery dates and would have skewed the delay calculations. Date columns were converted to datetime objects to allow for accurate mathematical subtraction.



Candidate's Choice Addition ("The Carrier Handoff Bottleneck"):I chose to analyze the time difference between order_purchase_timestamp and order_delivered_carrier_date. While it is easy to blame third-party shipping carriers for late deliveries, this metric tells us how long WE are holding onto the package before giving it to the carrier. The analysis revealed that orders which ultimately ended up "Super Late" had a noticeably longer internal processing/handoff time than "On Time" orders. This is critical business value because it tells the CEO that throwing money at external shipping companies won't fix the problem; we must invest in our own warehouse packing and dispatch workflows first.
