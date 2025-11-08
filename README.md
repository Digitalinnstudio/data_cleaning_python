# Data Cleaning-Sales Dataset

## Overview
Comprehensive data cleaning process performed on a messy sales dataset.  
The goal was to ensure data integrity, consistency, and readiness for analysis by handling missing values, outliers, and inconsistent data types.

---

## Steps

### 1. Initial Inspection
- df.info(), df.head() to inspect data types, non-null counts, and structure.

### 2. Data Type Conversion and Cleaning
- **Price & Quantity:** Removed non numeric characters, converted to numeric and errors to NaN.  
- **Negative Values:** Converted negative Quantity values to absolute corrected negative Total Price values linked to them.  
- **Date Columns:** Converted Order Date and Ship Date to datetime, errors to NaT.

### 3. Handling Missing Values
- **Price:** added where possible using Total Price / Quantity.  
  - Remaining unresolved rows were isolated to unresolvable_price_df and exported to unresolvable_prices.csv.  
- **Quantity:** added where possible using Total Price / Price.  
- **Customer Name & Region:** Filled missing values with 'Unknown'.

### 4. Derived and Corrected Columns
- **instore_purchase:** Y if Order Date was NaT or equal to Ship Date,  N otherwise.  
- **Order & Ship Dates (In-store):** For in-store purchases, set Order Date to Ship Date and cleared Ship Date to NaT.  
- **ship_time:** Calculated as Ship Date - Order Date in days.  
- **Total Price:** Recalculated as Price * Quantity for consistency.

---

## ✅ Final State of DataFrames

### Main DataFrame (`df`)
| Aspect | Description |
|--------|--------------|
| **Missing Values** | None in key columns (Order ID, Customer Name, Order Date, Product, Quantity, Price, Total Price, Region, instore_purchase) |
| **Data Types** | Correct (datetime, int64, float64, object) |
| **Outliers** | Negative quantities and prices corrected |
| **Derived Columns** | instore_purchase, ship_time added successfully |
| **Expected NaT Values** | 258 entries in Ship Date and ship time (for instore_purchase = Y) |

### Unresolvable Prices (`unresolvable_price_df`)
- Contains **38 rows** with unresolvable Price values.  
- Exported as unresolvable_prices.csv for client review.

---

## 📊 Data Validation Highlights
- All 52 missing Total Price values successfully recalculated.  
- No missing data in critical columns.  
- Numerical ranges validated:
  - Quantity: 1–5  
  - Price: £19.67 – £4990  
  - Total Price: £50 £4990  

