# 🛒 Retail Sales Insights Dashboard | Power BI

> A multi-table Power BI dashboard built on a star schema data model — tracking retail sales performance across brands, regions, store types, and products with DAX-powered KPIs including profit margin, sales growth, and year-over-year comparison.

---

## 🛠️ Tools & Technologies

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=flat)
![Power Query](https://img.shields.io/badge/Power_Query-217346?style=flat)

---

## 🎯 Objective

To build a business-ready retail analytics dashboard that enables stakeholders to:
- Monitor **Total Sales, Total Profit, Profit Margin, and Quantity Sold** in one view
- Compare **current year sales vs. last year (Sales LY)** to track growth
- Drill down by **Region, State, Brand, Product, and Store Type**
- Identify **underperforming regions or product categories** through geographic and category breakdowns
- Enable self-service analysis using **interactive slicers**

---

## 🗂️ Data Model — Star Schema

This project uses a proper **star schema** with 1 fact table and 4 dimension tables, joined via relationships in Power BI's model view:

```
                    ┌──────────────┐
                    │  Dim_Product │
                    │  - ProductName│
                    │  - Brand     │
                    └──────┬───────┘
                           │
┌──────────────┐    ┌──────▼───────┐    ┌──────────────┐
│  Dim_Customer│────│  Fact_Sales  │────│  Dim_Store   │
│  - Customer  │    │  - Sales     │    │  - StoreType │
│  - Region    │    │  - Quantity  │    │  - State     │
│  - State     │    │  - Profit    │    │  - Region    │
└──────────────┘    └──────┬───────┘    └──────────────┘
                           │
                    ┌──────▼───────┐
                    │calender Table│
                    │  - Date      │
                    │  - Month     │
                    │  - Year      │
                    └──────────────┘
```

**All measures are centralised in an `All_Measures` table** — a clean DAX best practice that keeps the model organised.

---

## 📁 Tables & Fields

### `Fact_Sales` (Central fact table)
| Column | Description |
|--------|-------------|
| Sales key | Foreign keys linking to all dimension tables |
| Revenue & quantity data | Core transactional values |

### `Dim_Product`
| Column | Description |
|--------|-------------|
| `ProductName` | Name of the product sold |
| `Brand` | Product brand |

### `Dim_Store`
| Column | Description |
|--------|-------------|
| `StoreType` | Type of store (Online / Offline / etc.) |
| `State` | State where the store is located |
| `Region` | Geographic region (North / South / East / West) |

### `Dim_Customer`
| Column | Description |
|--------|-------------|
| Customer details | Demographics linked to transactions |
| `Region` | Customer region |
| `State` | Customer state |

### `calender Table`
| Column | Description |
|--------|-------------|
| `Date` | Full date |
| `Month` | Month number |
| `Month Name` | Month label (Jan, Feb, ...) |
| `Year` | Year |

---

## 📊 Dashboard Visuals (Page 1)

| Visual | Type | Fields Used |
|--------|------|-------------|
| Total Sales KPI | Card | `Total Sales` |
| Total Profit KPI | Card | `Total Profit` |
| Profit Margin KPI | Card | `Profit Margin` |
| Total Quantity KPI | Card | `Total Quantity` |
| Sales by Region | Clustered Bar Chart | `Region`, `Total Sales` |
| Sales by Brand | Clustered Column Chart | `Brand`, `Total Sales` |
| Sales by Product | Clustered Bar Chart | `ProductName`, `Total Sales` |
| Monthly Sales Trend | Area Chart | `Month Name`, `Total Sales`, `Sales LY` |
| Sales by Store Type | Donut Chart | `StoreType`, `Total Sales` |
| Sales by State | Map Visual | `State`, `Total Sales` |
| Performance Matrix | Pivot Table | `Brand`, `Region`, KPI measures |
| Slicers | Advanced Slicer | `Year`, `Month`, `Brand`, `StoreType`, `Region` |

---

## 🔢 DAX Measures (All_Measures Table)

```dax
-- Core KPIs
Total Sales    = SUM(Fact_Sales[Sales Amount])
Total Profit   = SUM(Fact_Sales[Profit])
Total Quantity = SUM(Fact_Sales[Quantity])
Profit Margin  = DIVIDE([Total Profit], [Total Sales], 0)

-- Year-over-Year
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('calender Table'[Date]))
```

---

## 📈 Key Insights & What the Dashboard Reveals

- **4 KPI cards** give instant visibility into sales health — Total Sales, Profit, Margin %, and Quantity
- **Sales LY (Last Year) comparison** on the monthly trend chart allows managers to spot months of growth or decline instantly — no manual Excel calculations needed
- **Map visual by State** surfaces geographic concentration — which states are driving revenue and which are underperforming
- **Donut chart by Store Type** (Online vs. Offline) shows channel preference — critical for e-commerce vs. physical expansion decisions
- **Pivot table with Brand × Region** enables drill-through to find underperforming brand-region combinations
- **Star schema model** ensures accurate many-to-one relationships and reliable cross-filtering across all visuals
- **Centralised `All_Measures` table** — a DAX best practice that keeps all calculated measures organised and reusable

---

## 📸 Dashboard Screenshots


![Main Dashboard]<img width="1920" height="978" alt="Dashboard" src="https://github.com/user-attachments/assets/a90d4e17-e698-4d19-b411-9d0c6c79ca75" />


---

## 🚀 How to Open

1. Download `Retail_Sales_Dashboard.pbix`
2. Open with **Power BI Desktop** (free — [download here](https://powerbi.microsoft.com/en-us/desktop/))
3. All data is embedded — no external database connection needed
4. Use the **slicers** (Year, Month, Brand, Region, Store Type) to filter all visuals dynamically
5. Click on any bar, slice, or map region to **cross-filter** the entire dashboard

> ⚠️ Power BI Desktop is required to open `.pbix` files. It is free to download for Windows.

---

## 📂 Project Structure

```
retail-sales-dashboard/
├── Retail_Sales_Dashboard.pbix     ← Main Power BI file (model + dashboard)
├── images/
│   └── dashboard_main.png          ← Dashboard screenshot
└── README.md
```

---

## 💡 What I Learned

- Designing a **star schema data model** with Fact and Dimension tables in Power BI
- Centralising all DAX measures in a dedicated `All_Measures` table — a professional BI best practice
- Writing **`SAMEPERIODLASTYEAR()`** for year-over-year trend comparison
- Using **`DIVIDE()`** safely in DAX to calculate Profit Margin without divide-by-zero errors
- Building **cross-filtering** across map, bar, donut, and pivot visuals for self-service analysis
- Designing a single-page dashboard that answers multiple business questions simultaneously

---

## 🙋 About Me

Made by **[Abhishek Jain](https://github.com/abhishekjain2004)**  
Aspiring Data Analyst | PG in Data Science & Analytics with Gen AI @ Imarticus Learning  
📧 abhishek2004.jain@gmail.com · [LinkedIn]www.linkedin.com/in/abhishek-jain-297014277
