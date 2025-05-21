# ⚡ ElectroHub Power BI Sales Analysis Report

This project presents an interactive Power BI dashboard for **ElectroHub**, a retail company. The report analyzes sales, profit, quantity sold, discount behavior, and customer engagement through various visualizations.

---

## 📁 Data Tables Used

- `Fact` Table – Contains transactional data (unit sold, product ID, promotion ID, etc.)
- `Dim Product` – Contains product details like product name, category, price per unit
- `Dim Promotion` – Contains promotion types, price reduction types
- `Dim Customer` – Customer information including city
- Additional Date tables (for comparison features)

---

## 🛠️ Data Preparation Process

1. **Data Loading & Transformation in Power Query**
2. **Data Profiling** to assess column types and missing data
3. **Discount Percentage Column** added in `Dim Promotion`  
   - Converted formats like “20% off” to numeric (e.g., `20`)  
   - Converted “Buy 1 Get 1 Free” to `50`%
4. **Price Per Unit Column** added in Fact Table (merged from `Dim Product`)
5. **Total Sales Column** = `Unit Sold * Price Per Unit`
6. **Discount Column** added by merging with `Dim Promotion`
7. **Discount Value** = `(Total Sales * Discount%) / 100`
8. **Net Sales** = `Total Sales - Discount Value`
9. **Profit** = `Net Sales * 10%` (assumed fixed margin)
10. **Data Modeling** – Relationships defined between dimension and fact tables

---

## 📊 Report Outputs

### 1️⃣ Top/Bottom 5 Products by Sales/Profit/Quantity Sold
- **Visual**: Clustered bar charts
- **Features**: Top N filter applied for dynamic top/bottom analysis

### 2️⃣ Sales Trend Over Time
- **Visual**: Line charts
- **Granularity**: Daily, Monthly, Quarterly, Yearly
- **Purpose**: Understand seasonal trends and performance over time

### 3️⃣ Sales vs Profit Relationship
- **Visual**: Scatter plot
- **Insight**: Linear relationship (due to profit being 10% of net sales)

### 4️⃣ Period Comparison of Sales/Profit/Quantity
- **Visual**: Clustered column chart
- **Technique**:
  - Created two date tables: `Date Table 1` (active) and `Date Table 2` (inactive)
  - Used `USERELATIONSHIP()` in DAX to activate second date table in measures
  - Two slicers allow comparison between custom time periods

### 5️⃣ Average Discount by Promotion Category
- **Visual**: Bar chart
- **Insight**: Highlights which categories offer higher average discounts

### 6️⃣ Total Number of Orders
- **Visual**: Card
- **Metric**: Total count of orders from Fact table

### 7️⃣ Detailed Order Table with Visual Filtering (🔍 Highlighted)
This report page displays detailed order-level data and allows users to filter across dimensions.
#### 🎯 Visual Used:
- **Table**: Contains fields like Product, Customer, Promotion, Unit Sold, Sales, Discount, Net Sales, Profit, etc.
#### 🎛️ Filters Included:
- **Slicers**: Product Name, Order Date, Customer Name, Promotion Name
#### 🔄 Slicer Synchronization Strategy:
- Created a measure:  
  ```DAX
  Total Net Sales = SUM(Fact[Net Sales])
- Applied this measure as a visual-level filter on all slicers with condition:
    'Total Net Sales is not blank'
- Ensures slicers show only valid, contextually relevant options
- Improves user experience by filtering out non-existent combinations dynamically
✅ Result:
All slicers are synced. Changing one updates all others and the table below, creating a seamless and dynamic filtering experience.

### 8️⃣ Sales by City
- **Visual**: Map chart
- **Insight**: Displays city-wise net sales using bubble size (larger bubble = more sales)



🚀 Tools & Features Used
- Power Query Editor
- Data Modeling
- DAX (USERELATIONSHIP, SUM, Custom Measures)
- Advanced Filtering
- Slicer Synchronization
- Interactive Charts: Line, Bar, Scatter, Map, Table

