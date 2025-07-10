# summeranalyticsIITG

Dynamic Pricing for Urban Parking Lots
Summer Analytics 2025 — Capstone Project
By ARPIT AGARWAL

Brief Overview
Urban parking resources are limited and often inefficiently priced. Static pricing models fail to respond to real-time demand variations, leading to overutilization or underuse. This project implements a real-time dynamic pricing system for 14 parking lots over 73 days of data using demand signals such as occupancy, queue length, and special events.

We built three models of increasing complexity:

Model 1: Baseline Linear Model

Model 2: Demand-Based Dynamic Pricing

Model 3: Competitive Pricing Based on Location Intelligence

The final system runs on a simulated data stream using Pathway, and visualizes real-time pricing via Bokeh and Panel.

Tech Stack Used
Category	Tools & Libraries
Programming	Python
Stream Processing	Pathway
Data Handling	Pandas, NumPy
Visualization	Bokeh, Panel
Geolocation Logic	Geopy (Haversine/geodesic distance)
Deployment	Google Colab (Jupyter Notebook-based)

Project Architecture Diagram


Detailed Explanation of Project Architecture & Workflow
1. Data Stream Setup (Pathway)
The dataset is streamed using pw.demo.replay_csv() to simulate a real-time feed.

The data includes: Occupancy, Capacity, Latitude, Longitude, VehicleType, Traffic, SpecialDay, etc.

2. Model 1: Baseline Linear Pricing
Calculates next price as:

![image](https://github.com/user-attachments/assets/efba3252-489c-46d5-8c27-136b28de9cc6)

 
Simple, interpretable, and useful as a benchmark.

3. Model 2: Demand-Based Pricing
Uses a weighted formula of all demand factors:

![image](https://github.com/user-attachments/assets/954b38f8-fe45-4feb-ac10-1bc180fa0bd8)

4. Model 3: Competitive Pricing Model
Calculates nearby lots using geodesic(lat, long)

Compares competitor prices at the same timestamp.

Adjusts:

Price ↓ if lot is full & competitors are cheaper

Price ↑ if competitors are more expensive

5. Output and Visualization
Final prices from all models are exported to:

CSV (for reporting)

Bokeh (interactive price vs time plots per lot)

Panel (dashboard rendering for browser)

Other Documentation
Assumptions
Vehicle type and traffic levels are converted into numerical weights.

Nearby competitor lots are defined as those within a 0.5 km radius.

Demand normalization is clipped in streaming to avoid erratic price jumps.

pw.run() is used to simulate real-time stream processing.

Visualizations
Daily price trends per parking lot
![image](https://github.com/user-attachments/assets/92929189-30b2-4e52-847a-0f2ea3f12451)


Comparison between baseline and dynamic models

Interactive legend + filtering using Bokeh

Architecture Diagram Components (for All 3 Models)

1. Input Layer
Real-Time Data Stream (Pathway)

parking_stream.csv

2. Preprocessing
Timestamp Parser

Feature Extractor

Day Window Creator

3. Model 1: Baseline Linear Model
Occupancy

Capacity

Linear Pricing Logic

4. Model 2: Demand-Based Model
Occupancy

Capacity

Queue Length

Traffic Condition

Special Day

Vehicle Type

Demand Function

Normalized Demand

Demand-Based Pricing Logic

5. Model 3: Competitive Pricing Model
Latitude / Longitude

Nearby Lot Finder

Simulated Competitor Price

Competition-Based Price Adjuster

6. Output Layer
Price Output CSV

Real-Time Visualizer (Bokeh + Panel)

Report-Ready CSV for Plots

