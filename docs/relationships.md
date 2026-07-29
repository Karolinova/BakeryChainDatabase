# Table Relationships

This file describes the relationships between the tables in the database.

## Direct Relationships

| Table A | Table B | Cardinality | Type | Degree | Description |
|---|---|---|---|---|---|
| Stores | Employees | One-to-many (1:N) | Binary | 2 | One store can have many employees. One employee works in one store. |
| Stores | Product_Stock | One-to-many (1:N) | Binary | 2 | One store can have many stock records. |
| Bakery_Products | Product_Stock | One-to-many (1:N) | Binary | 2 | One bakery product can have stock records in many stores. |
| Bakery_Products | Transactions | One-to-many (1:N) | Binary | 2 | One bakery product can appear in many transaction items. |

## Junction Tables

| Junction Table | Table A | Table B | Cardinality | Type | Degree | Description |
|---|---|---|---|---|---|---|
| Bakery_Product_Bakers | Bakery_Products | Employees | Many-to-many (M:N) | Binary | 2 | One bakery product can be created by many employees, and one employee can work on many bakery products. The junction table contains two foreign keys: `id_bakery_product` and `id_employee`. Together, they form a composite primary key. |