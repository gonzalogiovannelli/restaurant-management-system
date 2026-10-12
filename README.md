# Restaurant and wine shop management system

A custom management system I built and ran for a restaurant with its own wine shop in Mar
del Plata, Argentina, from November 2023 to May 2026.

## The problem

Sales lived in Maxirest, the restaurant's point-of-sale software. Purchases, supplies and several cash
boxes, in pesos and in dollars, were tracked somewhere else. Wine was sold in two places, at
the table and over the counter, out of the same stock. Nothing put it all together.

## What it does

- **`extractor/`**: a Python script that pulls invoices (items and service times) from the
  Maxirest API into Google Sheets.
- **Google Sheets** (not in this repo): purchases, supplies, cash boxes and wine stock, in
  one place.
- **`power-bi/`**: one model on top of everything. Cash and bank balances per box in pesos
  and dollars, supplier debt, sales against expenses, and wine stock calculated as bought
  minus sold in the shop minus sold in the restaurant, valued at cost.

## Notes

- It ran for two and a half years, until the business closed.
- All data is anonymised. [Live report](https://app.powerbi.com/view?r=eyJrIjoiNzRiYjA3YjktNmQzNi00OWZiLTliZDgtMDNkOWRjODkyNWIzIiwidCI6ImJhMWRhMTIzLTdhOTktNDlhNy05Yjk1LWQ2ZGUwOWJjM2RlYSIsImMiOjR9).
- The code here dates from February 2025 and was written with AI chat assistants.
- Credentials in the script are placeholders.
