# Supply Chain KPIs


This project calculates and visualizes Supply Chain KPIs using transactional data from orders, deliveries, and inventory.


## Included KPIs
- **OTIF** (On Time In Full)
- **Fill Rate**
- **Average Lead Time**
- **Order Cycle Time**
- **Inventory Turnover**
- **DOH (Days of Inventory on Hand)**
- **Backorder Rate**
- **Forecast Accuracy (MAPE)**
- **Service Level (proxy)**
- **Perfect Order Rate (approx.)**


## How to Use
1. Generate (or replace) the CSVs in `data/`.
2. Run `streamlit run dashboard/app.py` to browse KPIs by period, SKU, supplier, and region.


## Data Structure
- `sample_orders.csv`: order or order-line level
- `order_id, order_date, promised_date, ship_date, delivery_date, sku, supplier_id, location_id, qty_ordered, qty_shipped, qty_backordered, unit_cost, unit_price, forecast_qty, region`
- `sample_inventory.csv`: aggregated inventory per `sku` and `period`
- `period_start, period_end, sku, beginning_inventory, ending_inventory, avg_inventory_value, days_in_period`


## Metric Definitions
- **OTIF**: % of orders delivered on-time (`delivery_date <= promised_date`) and in-full (`qty_shipped >= qty_ordered`).
- **Fill Rate**: `sum(min(qty_shipped, qty_ordered)) / sum(qty_ordered)`.
- **Lead Time**: `delivery_date - order_date` (average).
- **Order Cycle Time**: order to delivery time (average).
- **Inventory Turnover**: `COGS / Avg Inventory`. COGS ~ `sum(qty_shipped * unit_cost)` per period.
- **DOH**: `Avg Inventory / Daily COGS` (or `365 / Turnover`).
- **Backorder Rate**: `sum(qty_backordered) / sum(qty_ordered)`.
- **MAPE**: `mean(|demand - forecast| / demand)` aggregated by SKU/period.
- **Service Level (proxy)**: `1 - Backorder Rate`.
- **Perfect Order Rate (approx.)**: % of orders `on_time` and `in_full`.


## License
MIT
