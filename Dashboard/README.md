## 1. Project Objective
JCars Logistics imports, sells, and delivers vehicles to customers across regions in Kenya. The objective of this project is to transform a raw, unstandardized flat dataset into a reliable, interactive Power BI solution that moves beyond basic reporting to drive strategic management decisions.

---

## 1. Project Objective
JCars Logistics imports, sells, and delivers vehicles to customers across regions in Kenya. The objective of this project is to transform a raw, unstandardized flat dataset into a reliable, interactive Power BI solution that moves beyond basic reporting to drive strategic management decisions.

Specifically, this dashboard is designed to uncover actionable insights and support evidence-based recommendations by:
* **Optimizing Marketing ROI:** Evaluating lead source conversion (e.g., Walk-ins vs. Facebook/Instagram) to guide the reallocation of targeted marketing spend.
* **Improving Cash Flow & Liquidity:** Highlighting trapped pending revenue and tracking collection rates to support stricter, automated payment follow-up strategies.
* **Protecting Profit Margins:** Pinpointing regional logistics bottlenecks where high freight costs erode overall profitability, enabling data-driven delivery fee adjustments.
* **Enhancing Inventory Strategy:** Monitoring vehicle model profitability, fuel type demand, and transmission preferences to guide future vehicle procurement.
* **Monitoring Operational Health:** Tracking core KPIs such as gross profit margins, return rates, cancellation risks, and individual sales representative performance.

## 2. Dataset & Grain
<<<<<<< HEAD
* **Source:** A single raw flat file (`Jcars_data.csv`).
=======
<<<<<<<< HEAD:Dashboard/README.md.txt
* **Source:** A single raw flat file (`Jcars_data.csv`).
========
* **Source:** A single raw flat file Jcars_data.
>>>>>>>> c4b3e796b0949d914f85fd400b0066b0c9f00552:Dashboard/README.md
>>>>>>> c4b3e796b0949d914f85fd400b0066b0c9f00552
* **Grain:** One row represents one individual vehicle sales order transaction.
* The raw data blended transactional, vehicle, location, and customer details, which were subsequently decoupled into a relational star schema.

## 3. Data Quality Audit - Key Issues Identified
Several significant data anomalies were identified and resolved during the auditing phase:

| # | Issue | How It Was Handled |
|---|---|---|
| 1 | **Missing Entries:** Numerous critical text and numerical columns contained nulls or blanks. | Handled contextually: applied statistical imputation/conditional averages for numerical fields, and default placeholders for text columns. |
| 2 | **Currency Inconsistencies:** Client transaction data arrived in multiple different currencies. | Reconciled using Power Query; applied exchange rates to standardize all monetary outputs strictly into Kenya Shillings (KES). |
| 3 | **Invalid Data (Dates):** The dataset contained malformed, unparseable date records that violated standard calendar formats. | Invalid dates were isolated and removed to preserve the integrity of the timeline and time-intelligence functions. |
| 4 | **Ambiguous Data (Categorical Duplication):** Different text strings were used interchangeably to mean the same thing (e.g., `"False"`, `"No"`, and `"Not Returned"`). | Standardized using conditional logic in Power Query to consolidate all variations into a single unified category. |

## 4. Currency Standardization
The dataset contained transactions logged in multiple currencies. Because the exact timestamp of individual payments was not provided, current market conversion rates were applied to convert all foreign monetary values into a standardized Kenya Shilling (KES) format for accurate financial aggregation.

## 5. Data Cleaning & Preparation (Power Query)
Power Query was utilized to enforce data integrity and standard data types before loading into the DAX engine:
* **Missing Value Imputation:** Nulls replaced with appropriate baseline values depending on data type.
* **Semantic Normalization:** Consolidated boolean synonyms into strict True/False logical types.
* **Discount Normalization:** Addressed mixed formatting by treating existing decimals directly as factors, and converting unit-less whole numbers into explicit percentages.

## 6. Data Model
The flat-file structure was transitioned into a **star schema**:
* **Facts Table:** Centralized measurable transaction data (`Recorded Revenue`, `Units Sold`, `Logistics Cost`).
* **Dim_Branches & Dim_SalesReps:** Extracted repeating regional and personnel data into dedicated dimension tables, mapped back via Left Outer joins.
* **Dim_Cars:** Isolated vehicle attributes (`Car Make`, `Model`, `Fuel Type`).
* **Dim_Customers:** Although the transactional grain did not strictly require it for basic aggregations, customer entities were separated into their own table to preserve historical integrity for posterity and enable future scalability (e.g., tracking repeat buyers).

## 7. Key DAX Measures
| Measure | Purpose |
|---|---|
| `Total Revenue` / `Total Units Sold` | Core volume metrics. |
| `Total Profit` | `Total Revenue` minus (`Inventory Costs` + `Logistics Costs`). |
| `Gross Profit Margin %` | Core profitability. |
| `Average Delivery Time (Days)` | Logistics efficiency, calculated via `AVERAGEX`. |
| `Pending Revenue` | Financial risk metric summing revenue for unpaid/pending orders. |
| `Collection Rate %` | Operational health metric tracking completed payments against total valid orders. |
| `Return Rate %` / `Cancellation Rate %` | Risk/operational health. |
| `Top Performing Make` | Evaluates vehicle performance using dynamic DAX text isolation. |

## 8. Data Validation
Post-transformation validation ensured that propagating surrogate keys via Left Outer joins did not inadvertently duplicate transactional row counts, and verified that all categorical data standardized properly without dropping valid distinct values. 

## 9. Executive Dashboard (Page 1)
A single-page overview designed for C-suite monitoring, answering the question, "How is JCars Logistics performing?"
* **KPI Cards:** High-level metrics including Total Revenue, Gross Profit, and Total Units Sold.
* **Interactivity:** Dedicated slicers for Region and Sales Rep to allow leadership to dynamically filter performance without cluttering the visual layout.
* **Visual Flow:** Focuses purely on top-line trends and top performers to facilitate immediate assessment at a glance.

## 10. Assumptions & Business Rules Summary
* **Exchange Rates:** Due to missing payment dates, current market exchange rates were assumed and applied for currency conversion.
* **Discounts:** Values entered as decimals were assumed to be final discount factors, while whole numbers without symbols were assumed to represent percentages and converted accordingly.
* **Data Modeling:** Customer data was assumed valuable for future longitudinal tracking, prompting the deliberate normalization of `Dim Customers`.
<<<<<<< HEAD
=======
<<<<<<<< HEAD:Dashboard/README.md.txt
>>>>>>> c4b3e796b0949d914f85fd400b0066b0c9f00552

## 11. Repository Structure
```text
├── jcars.pbix     
├── data/
│   └── jcars.csv                   
├── screenshots/
│   ├── dashboard.png
│   └── steps.png
│   └── relationships.png
<<<<<<< HEAD
└── README.md
=======
└── README.md
========
>>>>>>>> c4b3e796b0949d914f85fd400b0066b0c9f00552:Dashboard/README.md
>>>>>>> c4b3e796b0949d914f85fd400b0066b0c9f00552
