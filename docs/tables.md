# Initial Database Tables

This file contains the database tables for the bakery chain project.

The tables were created and extended during the database design process.
They will be reviewed and normalized in the next stage of the project.

## Table: Stores
| Column | Specification |
| :--- | :--- |
| id | positive integer, unique, "NOT NULL" |
| street | text field, maximum 150 characters, "NOT NULL" |
| building_number | text field, maximum 5 characters, "NOT NULL" |
| postal_code | text field, format "XX-XXX", "NOT NULL" |
| city | text field, maximum 30 characters, "NOT NULL" |

## Table: Bakery_products

| Column | Specification |
| :--- | :--- |
| id | positive integer, unique, "NOT NULL" |
| name | text field, maximum 100 characters, "NOT NULL" |
| description | text field, maximum 500 characters |
| category | text field defining the type of bakery product, "NOT NULL" |
| unit_of_measure | text field defining the basic sales unit of the product, "NOT NULL" |
| baker | text field, maximum 30 characters |
| recipe_creation_date | date when the recipe was created |
| author | text field, maximum 30 characters |
| created_at | date and time when the record was added to the database, automatically added when the record is created |

## Table: Transactions

| Column | Specification |
| :--- | :--- |
| id | positive integer, unique, "NOT NULL" |
| unit_price | decimal number with two decimal places, "NOT NULL" |
| quantity | positive integer, "NOT NULL" |
| document_type | text field, "NOT NULL" |
| document_number | text field, maximum 15 characters, "NOT NULL" |
| purchase_date | date and time ("timestamp"), "NOT NULL" |
| bakery_product_id | positive integer, "NOT NULL", references the "Bakery_Products" table |
| store_id | positive integer, "NOT NULL", references the "Stores" table |

## Table: Employees

| Column | Specification |
| :--- | :--- |
| first_name | text field, maximum 50 characters, "NOT NULL" |
| last_name | text field, maximum 50 characters, "NOT NULL" |
| PESEL | text field, 11 characters, "NOT NULL" |
| street | text field, maximum 150 characters, "NOT NULL" |
| building_number | text field, maximum 5 characters, "NOT NULL" |
| apartment_number | text field, maximum 5 characters |
| postal_code | text field, format "XX-XXX", "NOT NULL" |
| city | text field, maximum 30 characters, "NOT NULL" |
| employment_start_date | date, "NOT NULL" |
| contract_end_date | date, can be empty |
| store_id | positive integer, "NOT NULL", references the "Stores" table |

## Table: Product_Stock

| Column | Specification |
| :--- | :--- |
| id | positive integer, unique, "NOT NULL" |
| bakery_product_id | positive integer, "NOT NULL", references the "Bakery_Products" table |
| store_id | positive integer, "NOT NULL", references the "Stores" table |
| quantity_in_stock | decimal number, "NOT NULL" |
| last_updated | date and time, "NOT NULL" |