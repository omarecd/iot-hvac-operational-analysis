# IoT HVAC Operational Data Analysis

## Project Overview

This project demonstrates how IoT telemetry can be used to support real operational decisions.

Using temperature and occupancy data collected from IoT sensors deployed in an office environment, the objective was to determine whether the HVAC heating schedule could be adjusted to reduce energy usage without affecting comfort.

Instead of building dashboards for demonstration purposes, the goal of this project was to analyze real telemetry and translate it into **_actionable operational recommendations_**.

The analysis ultimately led to adjusting the HVAC shutdown schedule earlier in the evening.

## Context

Many organizations deploy IoT devices but struggle to convert the collected measurements into operational decisions. This project focuses on that gap. The goal was to answer a simple operational question:

Can the usage of the heating system be optimised without negatively affecting indoor temperature?

The office building already had IoT sensors installed, producing telemetry related to:
	•	indoor temperature
	•	office occupancy
	•	and others...
	
The challenge was to interpret the data and determine whether a change in the HVAC schedule would be feasible.

## Data Sources

The analysis used telemetry collected from sensors installed in the office.

Sensors included:
	•	temperature sensors deployed in multiple locations
	•	occupancy monitoring (people count in the office)

Telemetry was ingested into a cloud data platform and stored in a time-series event database in Microsoft Fabric Eventhouse.

The dataset covered approximately:

January 2026 – March 2026.

As is common with real IoT deployments, the dataset was not perfectly clean:
	•	some sensors started reporting later
	•	some signals were intermittent
	•	timestamps required alignment

Handling imperfect telemetry was part of the analysis.

## Operational Changes Tested

Two operational changes were implemented during the data collection period.

Originally the heating system was configured to stop at:
18:00

After reviewing the temperature trends, the following adjustments were requested.
Phase 1 — Original configuration
Heating shutdown: 18:00

Phase 2 — First adjustment
Heating shutdown moved to: 17:00
This change was implemented and clearly visible in the telemetry.

Phase 3 — Second adjustment
Heating shutdown moved to: 16:00
This adjustment was later confirmed and applied by the building management team.

These configuration changes allowed the dataset to be segmented and compared.

## Analysis Approach

The analysis focused on time-series patterns in indoor temperature.

Key steps included:
	1.	Segmenting the dataset according to the three HVAC configurations
	2.	Aggregating temperature values into time intervals
	3.	Observing the temperature decay curve after HVAC shutdown
	4.	Comparing temperature behavior across the different shutdown times

The key concept investigated was the thermal inertia of the building.

Even after heating stops, indoor temperature decreases slowly due to:
	•	building insulation
	•	internal heat retention
	•	remaining thermal energy in the system

Understanding this behavior is essential when optimizing heating schedules.

## Key Observations

The data revealed several important patterns: Indoor temperature did not drop immediately when heating stopped. Instead, the temperature remained within a comfortable range for a significant period after shutdown. This confirmed that the building retains heat effectively.

When the shutdown time moved from 18:00 to 17:00, the temperature behavior remained acceptable. This indicated that the heating system had been running longer than necessary. Later, the shutdown time was further adjusted to 16:00, continuing the optimization process.

## Outcome

Based on the analysis, the HVAC shutdown schedule was successfully adjusted.

Heating shutdown moved from:

18:00 → 17:00 → 16:00

This adjustment reduces heating runtime while maintaining indoor comfort levels. The exact energy savings were not calculated (as heating costs are handled externally by the building management company).

More importantly, this project demonstrates how IoT telemetry can support data-driven operational decisions.

## Architecture Overview

IoT Sensors (Temperature, Occupancy)
↓
LoRaWAN Gateway
↓
LoRaWAN Network Server
↓
IoT Platform / ALSO IoT Platform
↓
Using a MQTT Connector, data is sent to Event Grid in Microsoft Azure
↓
Event Hub in Microsoft Azure
↓
Event Stream in Microsoft Fabric
↓
Event House in Microsoft Fabric (KQL / Time-Series Analysis)
↓
Operational Recommendation

## Lessons Learned

Several practical lessons emerged from this project.

- IoT data is rarely clean from the beginning.
Sensors may start reporting at different times and datasets often require validation.

- Operational changes must be verified.
Configuration changes in building systems should be confirmed with telemetry rather than assumed.

- Time-series segmentation is critical.
When analyzing operational changes, clearly separating the dataset into phases is essential.

- **_IoT value comes from decisions, not dashboards_**.
Dashboards can visualize data, but operational improvements occur only when the data leads to action.

## Key Takeaway

- Many IoT deployments successfully collect data but fail to convert it into meaningful operational improvements.

- This project illustrates the role of an engineer who sits between devices, data platforms, and operations, ensuring that measurements lead to decisions people actually take.

- In this case, telemetry analysis helped identify an opportunity to reduce heating runtime while maintaining comfort.

## Technologies Used
	•	IoT sensors
	•	IoT Gateways (For this case LoRa)
	•	LoRaWAN Netxork Server
	•	IoT Platform, on this case ALSO IoT
	•	Cloud ingestion pipeline
	•	Microsoft Fabric Eventhouse
	•	KQL (Kusto Query Language)
	•	Time-series data analysis


## Annexes

### Temperature Trend

![Temperature trend](images/temperature_trend.png)

### Architecture

![Architecture](images/architecture.png)


## Author

Omar Cruz
Industrial IoT & Data-focused Engineer

