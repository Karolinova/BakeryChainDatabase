# Database Normalization

This file shows the normalization process of the database tables.

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

| Column | Description |
|---|---|
| `id_bakery_product` | ID of the bakery product |
| `id_employee` | ID of the employee who worked on the product |

The primary key is a combination of both columns:

```text
(id_bakery_product, id_employee)