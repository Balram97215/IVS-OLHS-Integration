# Post-Acquisition Supply Chain Analytics & Network Optimization

**Company:** Indian Vellness Solutions (IVS) – Manufacturing Division (Oriental Lotus)
**Context:** B2B E-Commerce & Manufacturing
**Tech Stack:** `Python` (`Pandas`, `NumPy`), `SQL`, `Excel`, `Geospatial Analysis`

---

## 📜 The Context
IVS, a B2B enterprise, expanded its portfolio by acquiring *Oriental Lotus*, a hospitality product manufacturer. While the strategic intent was growth, the operational reality was chaotic. The newly acquired unit operated on fragmented Excel files and legacy systems, creating a data silo that isolated it from HQ.

**The Problem:** We needed to integrate this new node into our supply chain and determine the optimal location for a new West Coast warehouse. However, we lacked the data infrastructure to make these decisions. There was no centralized Data Team, and manual reporting processes created a **3-day latency** in inventory visibility.

## 🛠️ The Solution: Agile Data Architecture
Originally hired to drive Business Development, I identified that our growth strategy was blocked by a lack of measurement and data infrastructure. I pivoted to bridge the gap between business strategy and execution, effectively acting as the **Data Operations Lead**.

I architected a data workflow to centralize a "Single Source of Truth" and collaborated with engineering to build a custom Network Optimizer.

### 1. Geospatial Network Optimizer (Python)
*Focus: Collaborative Development & Logic Design*

To support the strategic expansion, we needed to identify the mathematically optimal distribution node to minimize shipping costs. We moved beyond intuition-based planning to build a **Weighted Center of Gravity (CoG)** model.

* **Filtering the Scope:** I wrote scripts to isolate the "Problem Region" (Shipping Zones 7 & 8), focusing purely on high-cost West Coast demand rather than skewing the data with local East Coast orders.
* **The Physics of "Weighted Average":**
    * *Logic:* `Coordinate * Shipment Weight`
    * *Why:* A 50lb shipment exerts 50x more "cost pressure" on the warehouse location than a 1lb shipment. This ensured the model prioritized heavy, expensive-to-ship orders.
* **Reverse Geocoding (The Translator):**
    * *The Problem:* The CoG formula output raw coordinates (e.g., `39.5, -118.2`) which were meaningless to business stakeholders.
    * *The Solution:* I engineered a custom function, `estimate_closest_state`, utilizing **Pandas broadcasting** to instantly calculate the distance between the target point and 20 candidate states.
    * *Manhattan Distance Heuristic:* Implemented a Manhattan Distance calculation (`|Lat1-Lat2| + |Lon1-Lon2|`) rather than Haversine. This was chosen for computational efficiency while providing sufficient accuracy for state-level selection.

### 2. Establishing a "Single Source of Truth"
*Focus: Independent Ownership*

The data required to feed the optimizer was scattered across B2B Sales Orders, 15+ external Vendor Invoices, and legacy Warehouse Management Systems (WMS).

* **ETL & Standardization:** Developed Python scripts to ingest diverse CSV/Excel formats, normalizing inconsistent SKU naming conventions and cleaning data artifacts.
* **Redundancy Elimination:** Merged siloed datasets into a local SQL instance, resolving conflicting inventory counts between the WMS and Sales Logs.
* **Dashboarding:** Designed the division's first Sales Performance Dashboard, translating the cleaned data into real-time visibility for "Manufacturing vs. Sold" metrics.

## 📋 Project Governance & Vendor Management
Beyond the technical data work, I supported the broader operational integration by managing critical project workflows:

* **Strategic Vendor Sourcing ("Make vs. Buy"):** Conducted comprehensive capacity analysis and led negotiations with potential vendors to outsource the manufacturing of niche hospitality products that the internal Oriental Lotus factory could not produce.
* **Project Tracking:** Maintained the master schedule and Minutes of Meeting (MoM), tracking critical path action items to ensure the technical data integration aligned with business timelines.

## 🚀 Impact & Results

| Metric | Outcome |
| :--- | :--- |
| **90% Latency Reduction** | Automating the data consolidation process reduced the time to generate sales & inventory reports from **3 days to <30 minutes**. |
| **Cost Optimization** | The CoG model identified a strategic warehouse zone that projected a **15-20% reduction** in long-haul shipping costs for West Coast fulfillment. |
| **100% Data Integrity** | Successfully mapped and standardized 100% of active SKUs across the new division, eliminating inventory discrepancies caused by manual data entry. |
