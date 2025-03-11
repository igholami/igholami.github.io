---
layout: page
title: Live Traffic
description: Live Traffic Design for Balad Company
img:
importance: 1
category: work
related_publications: false
---

## Live Traffic Project at Balad Navigation  

When I first joined the Data Infrastructure team at Balad Navigation, I was assigned to work on the **Live Traffic** project. The goal was to design a system that provides real-time traffic data to users of the Balad Navigation app. This initiative aimed to enhance user experience and increase app engagement.  

The key metric for evaluating the project's success was the accuracy of the estimated time of arrival (ETA) compared to actual travel times.

### Technical Implementation  

We designed a **multi-stage streaming process**:  

1. **Data Ingestion**  
   - Location data was read from a Kafka topic, processed to determine the corresponding street and direction, and then enriched data was written to another Kafka topic.  

2. **User-Level Speed Aggregation**  
   - The enriched data, keyed by user and street, was aggregated to calculate the user's average speed on each street. This aggregated data was then written to another Kafka topic.  

3. **Street-Level Traffic Calculation**  
   - The system combined the aggregated user speeds with the current street speed and published the updated traffic data to a new Kafka topic with an expiration time.  

4. **Data Utilization**  
   - The final processed data was consumed by multiple systems:  
     - **Navigation System:** Determines the optimal route based on traffic data.  
     - **ETA System:** Computes estimated arrival times considering real-time traffic.  
     - **Map Tile System:** Colors streets on the map according to traffic congestion levels.  

### Technologies Used  

- **Kafka** for real-time streaming.  
- **Python** for data processing.  
- **Redis** for caching.  
