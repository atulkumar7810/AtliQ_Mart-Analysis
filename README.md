# AtliQ Mart - Performance Analysis Dashboard

This repository contains the code, datasets, and configuration for the AtliQ Mart Performance Analysis Dashboard. The dashboard is designed to monitor and analyze key supply chain metrics for AtliQ Mart — a growing FMCG manufacturer based in Gujarat, India. The focus is on on-time delivery (OT%), in-full delivery (IF%), and on-time in-full (OTIF%) metrics, which help optimize supply chain operations and enhance customer retention.

## Overview

### Problem Statement
AtliQ Mart aims to enhance its service levels, optimize supply chain operations, and retain key customers. This dashboard tracks:
- **On-Time Delivery (OT%)**
- **In-Full Delivery (IF%)**
- **On-Time In-Full (OTIF%)**

### Objectives
- Track daily service levels for key customers.
- Measure operational efficiency using OT%, IF%, and OTIF% metrics.
- Identify city-wise and customer-specific performance trends.
- Provide actionable insights for strategic improvements in supply chain performance.

## Data Model Documentation

This project utilizes a Snowflake Schema with both dimension and fact tables. Metadata for these CSV files is provided within the repository.

### Dimension Tables

**dim_customers**  
Contains customer-related details. Key columns include:  
- *customer_id* – Unique ID assigned to each customer.  
- *customer_name* – Name of the customer.  
- *city* – City where the customer is located.

**dim_products**  
Contains product-related details. Key columns include:  
- *product_name* – Name of the product.  
- *product_id* – Unique ID assigned to each product.  
- *category* – Category to which the product belongs.

**dim_date**  
Contains date-related attributes at various levels. Key columns include:  
- *date* – Date at the daily level.  
- *mmm_yy* – Date at the monthly level (e.g., Jan-25).  
- *week_no* – Week number of the year.

**dim_targets_orders**  
Contains target service-level data for each customer. Key columns include:  
- *customer_id* – Unique ID for each customer.  
- *ontime_target%* – Target percentage for on-time delivery.  
- *infull_target%* – Target percentage for in-full delivery.  
- *otif_target%* – Target percentage for on-time in-full delivery.

### Fact Tables

**fact_order_lines**  
Contains detailed order-level data for each item within an order. Key columns include:  
- *order_id* – Unique ID for each order.  
- *order_placement_date* – Date when the order was placed.  
- *customer_id* – Unique ID assigned to the customer.  
- *product_id* – Unique ID assigned to the product.  
- *order_qty* – Quantity of products ordered.  
- *agreed_delivery_date* – Agreed delivery date between the customer and AtliQ Mart.  
- *actual_delivery_date* – Actual date when the product was delivered.  
- *delivery_qty* – Quantity of products delivered.  
- *In Full* – Indicator (1 or 0) if the order was delivered in full.  
- *On Time* – Indicator (1 or 0) if the order was delivered on time.  
- *On Time In Full* – Indicator (1 or 0) if the order was delivered both on time and in full.

**fact_orders_aggregate**  
Contains aggregated order performance metrics at the order level per customer. Key columns include:  
- *order_id* – Unique ID for each order.  
- *customer_id* – Unique ID assigned to the customer.  
- *order_placement_date* – Date when the order was placed.  
- *on_time* – Indicator (1 or 0) for on-time delivery.  
- *in_full* – Indicator (1 or 0) for in-full delivery.  
- *otif* – Indicator (1 or 0) for on-time in-full delivery.

## Dashboard Overview

<img src="https://github.com/user-attachments/assets/0171cd10-bf76-42e1-8cf0-4babbecae007" alt="Dashboard" width="1000" height="500" />

Our dashboard is organized into three distinct pages, each focusing on a specific aspect of performance. Below is a brief description of each page with space reserved for additional details and images.

### Page 1: Order Quantity and Fill Rate Analysis
This page provides a comprehensive overview of the core service metrics, including on-time, in-full, and OTIF percentages. It highlights deviations from targets using visual cues and conditional formatting.
<!-- Space for additional details or image for Page 1 -->
<img src="https://github.com/user-attachments/assets/2762ccb3-1a11-40d5-a575-15a8428f7bdb" alt="Order Quantity and Fill Rate Analysis" width="1000" height="500" />

### Page 2: City Performance Analysis
This page breaks down performance metrics by city, showcasing regional differences in delivery efficiency and fulfillment. It helps identify which cities require targeted improvements.
<!-- Space for additional details or image for Page 2 -->
<img src="https://github.com/user-attachments/assets/f4708da2-52bc-499c-8ea7-7e18d47e98c3" alt="City Performance Analysis" width="1000" height="500" />

### Page 3: Cumulative OTIF % and Trend Analysis
This page offers insights into individual customer performance, presenting a matrix of OT%, IF%, and OTIF% metrics. It helps pinpoint high-risk customers and highlights opportunities for enhanced service.
<!-- Space for additional details or image for Page 3 -->
<img src="https://github.com/user-attachments/assets/146d577e-817c-4713-b6fc-070e58482cb7" alt="Cumulative OTIF % and Trend Analysis" width="1000" height="500" />

## Key Insights

- **Critically Low OTIF Performance:**  
  The overall OTIF (On Time In Full) percentage is **29.02%**, which is far below optimal levels. This points to major inefficiencies in supply chain execution and fulfillment operations.

- **On-Time Delivery Challenges:**  
  The on-time delivery rate stands at **59.03%**, meaning over 40% of orders are delivered late. A late delivery percentage of **28.88%** further emphasizes that nearly one-third of orders do not meet the promised delivery schedule.

- **Suboptimal In-Full Fulfillment:**  
  The in-full delivery rate is **52.78%**, indicating that almost half of the orders are not completely fulfilled. This may be due to issues such as inventory mismanagement or supply disruptions.

- **High Backorder Rate:**  
  With a backorder rate of **61.25%**, a significant portion of orders cannot be fulfilled immediately, affecting customer satisfaction and loyalty.

- **Fill Rate Discrepancies:**  
  While the volume fill rate is high at **96.59%** (suggesting overall quantity fulfillment is strong), the line fill rate is only **65.96%**, meaning that many individual items within orders are not being delivered as required.

- **Customer Base and Delivery Timing:**  
  The dataset indicates a total of **35 customers**, and early deliveries account for **6.32%**. Although early deliveries are positive, there is room to better align scheduling with customer expectations.

- **Inconsistent Performance Trends:**  
  On-time performance fluctuates between **54% and 62%**, with a noted low of **53.9%** and a high of **62.8%**. This inconsistency suggests operational variability that needs to be addressed.

## Recommendations

- **Enhance Supply Chain and Order Fulfillment:**  
  - Optimize supplier lead times and increase safety stock levels to reduce inventory shortages.  
  - Implement real-time tracking and AI-driven forecasting to identify and mitigate potential delays.

- **Improve Logistics and Last-Mile Delivery:**  
  - Collaborate with logistics partners to improve routing and scheduling, aiming to raise on-time delivery rates above 70%.  
  - Introduce performance-based incentives and penalties to encourage timely deliveries.

- **Reduce Backorders with Better Demand Planning:**  
  - Revise forecasting models to better predict demand and avoid stockouts.  
  - Establish buffer stocks for high-demand items to ensure orders are delivered in full.

- **Implement City-Specific Strategies:**  
  - Prioritize improvements in cities with lower performance. For instance, while Surat shows slightly better metrics, Ahmedabad and Vadodara require focused interventions.  
  - Consider expanding warehouse capacity or establishing distribution hubs in underperforming regions.

- **Increase Fill Rates:**  
  - Address the low line fill rate (65.96%) by optimizing warehouse processes and ensuring consistent product availability.  
  - Enhance supplier agreements and logistics coordination to improve order line completion.

- **Set and Monitor Clear Targets:**  
  - Establish short-term improvement goals, such as increasing OTIF to 40-50% within the next quarter and on-time delivery to at least 70%.  
  - Use real-time dashboards with alerts to monitor daily and weekly performance, enabling swift corrective actions.
