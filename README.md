# AnyLogic-Digital-Twin-Manufacturing
Discrete Event Simulation (DES) model for packaging line optimization. Analyzes machine replacement strategies and AMR logistics using AnyLogic &amp; Java.
#  Manufacturing Digital Twin: Machine Replacement & Logistics Optimization

[![AnyLogic](https://img.shields.io/badge/Platform-AnyLogic_Professional-blue)](https://www.anylogic.com/)
[![Language](https://img.shields.io/badge/Language-Java-orange)](https://www.java.com/)
[![Simulation](https://img.shields.io/badge/Method-Discrete_Event_Simulation-green)]()

> **Case Study:** Evaluation of mixed-asset strategies and automated logistics (AMR/AGV) for a German packaging facility.

## 📺 Project Demo
**https://youtu.be/OKZYwsZaC6s**

---

## 📖 Executive Summary
This project develops a **Discrete Event Simulation (DES)** model to assist a packaging company in decision-making regarding aging equipment replacement and internal logistics automation. 

[cite_start]Using **AnyLogic**, the model simulates a full production year (2024) with real historical order data, stochastic machine breakdowns, and variable changeover times.

**Key Business Questions Answered:**
1. Can a single high-speed New Machine replace two aging legacy machines?
2. Is the investment in Autonomous Mobile Robots (AMR) financially viable?

---

## 🛠️ Technical Implementation
The model is built using a hybrid approach (DES + Agent-based) with custom Java logic for complex control rules.

### 1. Modeling Logic & Agents
* [cite_start]**Pull-Push Logic:** Orders are prioritized and "pulled" by available machines, then "pushed" to logistics buffers.
* **Custom Agents:**
    * [cite_start]`Order Agent`: Tracks state variables like `procMinutes`, `logisticsCostEur`, and `priorityKey`.
    * [cite_start]`Machine Agent`: Represents resources with distinct attributes for "Old" vs "New" machinery reliability (MTBF/MTTR).

### 2. Stochasticity & Data-Driven Components
* **Failures:** Modeled using exponential distributions based on historical MTBF/MTTR data.
    * *New Machine:* Higher reliability, faster repair.
    * [cite_start]*Legacy Machines:* Frequent breakdowns, slower repair.
* [cite_start]**Changeovers:** Logic-dependent setup times (5-45 mins) based on SKU family sequencing.
* [cite_start]**Maintenance:** A **Data-Driven Agent Controller** reads `maintenance_calendar_2024.csv` to trigger scheduled downtime events accurately.

### 3. KPI Calculation (Java)
Custom functions were written to calculate OEE (Overall Equipment Effectiveness) and system performance in real-time:
```java
// Example: Calculating Processing Time with Scrap Rate
double qtyTotalReal = Math.ceil(targetGood / Math.max(1e-9, (1.0 - scrapRate)));
return qtyNet / rate * 60.0;
