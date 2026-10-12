# Power BI model

This Power BI dashboard provides a comprehensive **financial and inventory analysis** for a wine business.  
It includes key insights on **account balances, supplier debt, wine stock levels, and monthly results**.


## 📊 Project Overview

This Power BI dashboard is designed to provide **financial insights and inventory tracking** for a wine business.  
It helps stakeholders make data-driven decisions by visualizing **monthly results, supplier debts, and stock levels**.

### 🔹 Key Features:
- **Financial Overview**: Tracks **account balances**, **net assets**, and financial performance.
- **Sales Analysis**: Visualizes **monthly revenue trends** from different sources.
- **Supplier Debt Tracking**: Monitors outstanding payments to suppliers.
- **Wine Inventory Management**: Displays **stock levels** and their valuation by winery.
- **Database Snowflake Model**: Optimized relational model for seamless reporting.

### 🛠 Tools Used:
- **Power BI** for interactive data visualization.
- **DAX (Data Analysis Expressions)** for calculations and measures.
- **Relational Database (Snowflake Schema)** for structured data modeling.

## 🗂 Database Structure & Tables

This Power BI dashboard is built using a **Snowflake Schema**, ensuring efficient data relationships and performance.

### 🔹 Main Tables:

- **Ventas (Sales)**: Stores **transaction data, revenue sources, and amounts** for analysis.
- **Saldos (Account Balances)**: Tracks **bank balances and financial statements**.
- **Proveedores (Suppliers)**: Lists **supplier names and outstanding debts**.
- **Inventario (Inventory)**: Manages **wine stock levels, valuations, and winery details**.
- **Calendario (Calendar Table)**: A **date reference table** for time-based analysis.
- **Pagos (Payments & Expenses)**: Stores **business expenses, invoices, and financial movements**.

📌 This relational model allows **efficient filtering, aggregation, and financial analysis** across all reports.

## 📊 Key DAX Measures  
This section includes the most relevant **DAX calculations** used in this Power BI dashboard.  

### 🔹 Bank Account Balances  
Calculates the total balance for different bank accounts.  
```DAX
VAR CAJAACTUAL = "Bank Account 1"
RETURN
    CALCULATE(SUM(Cobros[Importe AR$]), Cobros[Caja] = CAJAACTUAL) +
    CALCULATE(SUM(Vinoteca[Total]), Vinoteca[Caja] = CAJAACTUAL) -
    CALCULATE(SUM(Pagos[Importe AR$]), Pagos[Caja] = CAJAACTUAL) +
    CALCULATE(SUM('Arqueo de Cajas'[Importe AR$]), 'Arqueo de Cajas'[Destino] = CAJAACTUAL) -
    CALCULATE(SUM('Arqueo de Cajas'[Importe AR$]), 'Arqueo de Cajas'[Origen] = CAJAACTUAL)
```

### 🔹 ASSETS USD  
Calculates the total assets in USD, converting AR$ balances at the exchange rate.  
```DAX
ASSETS USD = 
    ([Bank Account 1 AR$] + 
     [Bank Account 2 AR$] + 
     [Bank Account 3 AR$] + 
     [Checks AR$] + 
     [AR$ Wine Stock]) / [Exchange Rate] + 
     [Bank Account 1 USD] + 
     [Bank Account 2 USD]
```

### 🔹 Total Supplier Debt  
Computes the outstanding payments to suppliers.  
```DAX
Total Supplier Debt = SUM(Proveedores[Debt])
```

### 🔹 Net Profit Calculation  
Calculates the **profit after deducting expenses**.  
```DAX
Net Profit = [Total Sales] - SUM(Pagos[Total Expenses])
```

### 🔹 Exchange Rate Conversion  
Converts local currency into USD using the latest exchange rate.  
```DAX
Sales in USD = SUM(Ventas[Revenue]) / SELECTEDVALUE(Tipo_Cambio[ExchangeRate])
```

### 🔹 Units Sold Winery  
Calculates the total number of wine bottles sold in the winery.  
```DAX
Units Sold Winery = CALCULATE(SUM(Vinoteca[Cantidad]), Vinoteca[Categoria] = "Wines")
```

### 🔹 Units Purchased Wines  
Calculates the total number of wine bottles purchased.  
```DAX
Units Purchased Wines = CALCULATE(SUM('Wine Records'[Net Quantity]), 'Wine List'[Category] = "Wines")
```

### 🔹 Units Stock Wines  
Calculates the total stock of wine bottles available.  
```DAX
Units Stock Wines = [Units Purchased Wines] - [Units Sold Winery] - [Units Sold Restaurant]
```

### 🔹 AR$ Wine Stock  
Calculates the total valuation of wine stock in AR$.  
```DAX
AR$ Wine Stock = SUMX('Wine List', 'Wine List'[Final Cost] * [Units Stock Wines])
```

📌 These **DAX calculations enhance financial analysis and enable advanced reporting** in Power BI.  
