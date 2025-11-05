# British Airways Lounge Eligibility Analysis

## Project Overview

The goal of this project is to estimate passenger lounge eligibility at **British Airways Terminal 3 lounges** using historical flight data. Understanding lounge demand is critical for optimizing space and resources while maintaining the premium travel experience. This project builds a **reusable lookup table** that can be applied to current and future flight schedules.

---

## Objectives

- Analyze historical BA flight data to determine **lounge eligibility percentages** across different tiers:
  - **Tier 1:** Concorde Room  
  - **Tier 2:** First Lounge  
  - **Tier 3:** Club Lounge
- Group flights in a meaningful way to simplify future estimations (by **Arrival Region × Time of Day**).
- Apply assumptions and machine learning methods to predict eligibility percentages.
- Create a **flexible, submission-ready Excel template** for BA planners.
- Provide a justification framework for the methodology.

---

## Dataset

The dataset includes historical flight information and lounge eligibility:

| Column | Description |
|--------|-------------|
| FLIGHT_DATE | Date of flight |
| FLIGHT_TIME | Scheduled departure time |
| TIME_OF_DAY | Morning/Afternoon/Evening |
| AIRLINE_CD | Airline code |
| FLIGHT_NO | Flight number |
| DEPARTURE_STATION_CD | Departure airport code |
| ARRIVAL_STATION_CD | Arrival airport code |
| ARRIVAL_COUNTRY | Arrival country |
| ARRIVAL_REGION | Arrival region (Europe, North America, etc.) |
| HAUL | Short or Long haul |
| AIRCRAFT_TYPE | Aircraft model |
| FIRST_CLASS_SEATS | Number of first-class seats |
| BUSINESS_CLASS_SEATS | Number of business-class seats |
| ECONOMY_SEATS | Number of economy seats |
| TIER1_ELIGIBLE_PAX | Historical Tier 1 eligible passengers |
| TIER2_ELIGIBLE_PAX | Historical Tier 2 eligible passengers |
| TIER3_ELIGIBLE_PAX | Historical Tier 3 eligible passengers |

---

## Methodology

### 1. Data Preparation
- Calculated total seats per flight:  
  ```python
  total_seats = FIRST_CLASS_SEATS + BUSINESS_CLASS_SEATS + ECONOMY_SEATS
  tier1_pct = (TIER1_ELIGIBLE_PAX / total_seats * 100).round(1)
  tier2_pct = (TIER2_ELIGIBLE_PAX / total_seats * 100).round(1)
  tier3_pct = (TIER3_ELIGIBLE_PAX / total_seats * 100).round(1)


## Flight Grouping

Flights were grouped by Arrival Region × Time of Day.

Example: North America | Morning or Europe | Evening.

This captures differences in passenger composition and peak lounge usage times.

## Predicting Eligibility Percentages
Calculated mean and median percentages for each group based on historical data.

Optionally, machine learning models (like regularized linear regression or Random Forest) can be trained with features:

ARRIVAL_REGION, TIME_OF_DAY, HAUL, AIRCRAFT_TYPE, day_of_week, season

This allows predicting Tier percentages for future or unknown flight schedules.

## Clustering (Optional)
KMeans clustering was applied to discover natural flight groups based on total seats, region, and time of day.

Helps identify business-heavy clusters not captured by simple groupings.

## Business Impact

Provides predictable estimates of lounge demand per flight group.

Helps Airport Planning teams optimize lounge capacity and resource allocation.

Scales to future schedules, new routes, or aircraft changes without needing individual flight-level data.

Supports strategic decision-making for premium passenger experience.

















