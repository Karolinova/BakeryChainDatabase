# Database Tables

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
| status          | text field defining the current store status, "NOT NULL" |
| opening_date    | date when the store was opened                           |
| suspension_date | date when the store was suspended                        |
| closure_date    | date when the store was closed                           |
| phone_number    | text field containing the store phone number             |

## Table: Store_Opening_Hours

| Column       | Specification                                               |
| :----------- | :---------------------------------------------------------- |
| id           | positive integer, unique, "NOT NULL"                        |
| store_id     | positive integer, "NOT NULL", references the "Stores" table |
| day_of_week  | value defining the day of the week, "NOT NULL"              |
| opening_time | time when the store opens, "NOT NULL"                       |
| closing_time | time when the store closes, "NOT NULL"                      |

Each store has seven records in this table, one for each day of the week.

## Table: Bakery_products

| Column | Specification |
| :--- | :--- |
| id | positive integer, unique, "NOT NULL" |
| name | text field, maximum 100 characters, "NOT NULL" |
| description | text field, maximum 500 characters |
| category | text field defining the type of bakery product, "NOT NULL" |
| unit_of_measure | text field defining the basic sales unit of the product, "NOT NULL" |
| recipe_creation_date | date when the recipe was created |
| status| text field defining the current product status, "NOT NULL"|

## Table: Product_Authors

| Column            | Specification                                                        |
| :---------------- | :------------------------------------------------------------------- |
| employee_id       | positive integer, "NOT NULL", references the "Employees" table       |
| bakery_product_id | positive integer, "NOT NULL", references the "Bakery_Products" table |

The table links bakery products with their authors.

A bakery product can have multiple authors, and an employee can be the author of multiple bakery products.

The combination of `employee_id` and `bakery_product_id` is unique and forms a composite primary key.

## Table: Product_Prices

| Column            | Specification                                                        |
| :---------------- | :------------------------------------------------------------------- |
| id                | positive integer, unique, "NOT NULL"                                 |
| bakery_product_id | positive integer, "NOT NULL", references the "Bakery_Products" table |
| price             | decimal number with two decimal places, "NOT NULL"                   |
| valid_from        | date when the price becomes valid, "NOT NULL"                        |
| valid_to          | date when the price stops being valid                                |

The table stores current and historical prices of bakery products.

## Table: Transactions

| Column | Specification |
| :--- | :--- |
| id | positive integer, unique, "NOT NULL" |
| unit_price | decimal number with two decimal places, "NOT NULL" |
| quantity | positive integer, "NOT NULL" |
| document_type | text field, "NOT NULL" |
| document_number | text field, maximum 15 characters, "NOT NULL" |
| purchase_timestamp | date and time ("timestamp"), "NOT NULL" |
| bakery_product_id | positive integer, "NOT NULL", references the "Bakery_Products" table |
| store_id | positive integer, "NOT NULL", references the "Stores" table |
| employee_id | positive integer, "NOT NULL", references the "Employees" table |

## Table: Transaction_Cancellations

| Column                 | Specification                                                     |
| :--------------------- | :---------------------------------------------------------------- |
| id                     | positive integer, unique, "NOT NULL"                              |
| transaction_id         | positive integer, "NOT NULL", references the "Transactions" table |
| quantity               | positive number, "NOT NULL"                                       |
| amount                 | decimal number with two decimal places, "NOT NULL"                |
| cancellation_timestamp | date and time ("timestamp"), "NOT NULL"                           |

The table stores information about cancelled transaction items.

A cancellation can apply to selected items or to the whole document.

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