# Database Normalization

This file shows the normalization process of the first five database tables.

The goal was to check the tables against the First, Second and Third Normal Form (1NF, 2NF and 3NF).

During the normalization process, one additional table was created to connect bakery products with employees who work on them.

---

## 1. Stores

### 1NF

Each column contains one value.

For example, the address is divided into separate columns: `street`, `building_number`, `postal_code` and `city`.

The `id` column identifies one specific store.

**Result: The table meets 1NF.**

### 2NF

The table has a simple primary key: `id`.

Because the key is not a composite key, there is no problem with a column depending only on part of the key.

**Result: The table meets 2NF.**

### 3NF

The other columns describe the store identified by `id`.

In this model, there is no clear dependency between the non-key columns. For example, the postal code does not uniquely identify the city or the street.

**Result: The table meets 3NF.**

---

## 2. Bakery Products

### 1NF

Each column contains one value.

One bakery product can be created by more than one baker. Because of this, several bakers should not be stored in one column.

The `baker` column was removed from the `Bakery_Products` table.

A new junction table was created:

### Bakery_Product_Bakers

| Column              | Description                                  |
| ------------------- | -------------------------------------------- |
| `id_bakery_product` | ID of the bakery product                     |
| `id_employee`       | ID of the employee who worked on the product |

The primary key is a combination of both columns:

```text
(id_bakery_product, id_employee)
```

This allows one bakery product to be connected with multiple employees and one employee to be connected with multiple bakery products.

**Result: The table meets 1NF.**

### 2NF

The `Bakery_Products` table has a simple primary key: `id`.

The `Bakery_Product_Bakers` table has a composite primary key consisting of `id_bakery_product` and `id_employee`.

Both columns are required to identify a unique relationship between an employee and a bakery product.

**Result: The tables meet 2NF.**

### 3NF

The information about employees is stored in the `Employees` table and is referenced by `id_employee`.

The information about bakery products is stored in the `Bakery_Products` table and is referenced by `id_bakery_product`.

This prevents employee and product information from being repeated in the junction table.

**Result: The tables meet 3NF.**

---

## 3. Transactions

### 1NF

Each column contains one value.

Each record represents one product included in a transaction.

A single document can contain several transaction records. The `document_number` is used to identify the document to which the records belong.

**Result: The table meets 1NF.**

### 2NF

The table has a simple primary key: `id`.

Because the primary key is not composite, there are no partial dependencies.

**Result: The table meets 2NF.**

### 3NF

The information about the bakery product and the store is stored in separate tables.

The `bakery_product_id` references the `Bakery_Products` table and the `store_id` references the `Stores` table.

The transaction table therefore stores references to these entities instead of repeating their descriptive information.

**Result: The table meets 3NF.**

---

## 4. Employees

### 1NF

Each column contains one value.

The employee's address is divided into separate columns: `street`, `building_number`, `apartment_number`, `postal_code` and `city`.

**Result: The table meets 1NF.**

### 2NF

The table has a simple primary key.

Because the primary key is not composite, there are no partial dependencies.

**Result: The table meets 2NF.**

### 3NF

The employee's store is identified by `store_id`, which references the `Stores` table.

The store's address is therefore not repeated in the `Employees` table.

The remaining columns describe the employee identified by the primary key.

**Result: The table meets 3NF.**

---

## 5. Product Stock

### 1NF

Each column contains one value.

Each record represents the stock of one bakery product in one store.

The values `bakery_product_id`, `store_id` and `quantity_in_stock` are stored separately and contain single values.

**Result: The table meets 1NF.**

### 2NF

The table has a simple primary key: `id`.

Because the primary key is not composite, there are no partial dependencies.

The `bakery_product_id` and `store_id` identify the product and store related to the stock record.

**Result: The table meets 2NF.**

### 3NF

The information about bakery products and stores is stored in separate tables.

The `bakery_product_id` references the `Bakery_Products` table and the `store_id` references the `Stores` table.

The stock table therefore contains only information directly related to the stock record.

**Result: The table meets 3NF.**

---

## Summary

The initial database tables were reviewed according to 1NF, 2NF and 3NF.

The main change resulting from the normalization process was the removal of the `baker` column from `Bakery_Products` and the creation of the `Bakery_Product_Bakers` junction table.

The normalized structure reduces repeating data and separates information about different entities while keeping the relationships between them.
