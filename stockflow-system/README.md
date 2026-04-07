StockFlow Inventory Management System
Backend Engineering Case Study Documentation 

Part 1: Code Review & Debugging
1. No Input Validation
Issue: Input data was not validated.
Solution: Added checks for required fields, types, and values.
Implementation: Used condition checks before processing request.
2. SKU Not Unique
Issue: Duplicate SKU allowed.
Solution: Checked database before insert.
Implementation: Query used to verify uniqueness.
3. Multiple Commits
Issue: Separate commits caused inconsistency.
Solution: Used single transaction.
Implementation: try-catch with rollback.
Part 2: Database Design
1. Product in Multiple Warehouses
Solution: Created Inventory table.
2. Supplier Relationship
Solution: Created SupplierProduct table.
3. Inventory Tracking
Solution: Created InventoryTransaction table.
Part 3: API Implementation
1. Low Stock Detection
Solution: Compared stock with threshold.
2. Multiple Warehouses
Solution: Aggregated stock.
3. Supplier Info
Solution: Joined supplier data.
-------------------------------------------------------------------------------------------------------------------------------------------
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


StockFlow Inventory Management System
ER Diagram Description (Student Version)

1. Company
id (PK)
name
email
created_at

A company represents an organization using the system.
2. Warehouse
id (PK)
name
location
company_id (FK → Company.id)
created_at

One Company → Many Warehouses
3. Product
id (PK)
name
sku
price
low_stock_threshold
is_bundle
description
created_at

SKU should be unique.
4. Inventory
id (PK)
product_id (FK → Product.id)
warehouse_id (FK → Warehouse.id)
quantity
last_updated

Stores stock per warehouse.
5. Inventory Transaction
id (PK)
product_id (FK → Product.id)
warehouse_id (FK → Warehouse.id)
quantity_change
previous_quantity
new_quantity
transaction_type
notes
created_at

Tracks stock movement.
6. Sales
id (PK)
company_id (FK → Company.id)
product_id (FK → Product.id)
warehouse_id (FK → Warehouse.id)
quantity_sold
sale_date

Used for stock prediction.
7. Supplier
id (PK)
name
contact_email
contact_phone
address
created_at
8. Supplier Product
id (PK)
supplier_id (FK → Supplier.id)
product_id (FK → Product.id)
supplier_sku
lead_time_days
unit_cost
is_preferred

Many-to-Many relationship.
9. Product Bundle
id (PK)
parent_product_id (FK → Product.id)
component_product_id (FK → Product.id)
quantity

Used for bundle products.
