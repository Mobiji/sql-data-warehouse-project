# Data Catalog for Gold Layer

## Overview
The Gold Layer is the business-level data representation, structured to support analytical and reporting use cases. It consists of **dimension tables** and **fact tables** for specific business metrics.

---

### 1. **gold.dim_customers**
- **Purpose:** Stores customer details enriched with demographic and geographic data.
- **Columns:**

| Column Name      | Data Type     | Description                                                                                   |
|------------------|---------------|-----------------------------------------------------------------------------------------------|
| customer_key     | bigint UN     | Surrogate key uniquely identifying each customer record in the dimension table.           |
| customer_id      | INT           | Unique numerical identifier assigned to each customer.                                        |
| customer_number  |  VARCHAR(50)  | Alphanumeric identifier representing the customer, used for tracking and referencing.         |
| customer_name    |  VARCHAR(101) | The customer's full name, as recorded in the system.                                          |
| country          |  VARCHAR(50)  | The country of residence for the customer (e.g., 'Australia').                                |
| gender           |  VARCHAR(50)  | The gender of the customer (e.g., 'Male', 'Female', 'n/a'). |   
| marital_status   |  VARCHAR(50)  | The marital status of the customer (e.g., 'Married', 'Single').                               |
| birthdate        |  DATE         | The date of birth of the customer, formatted as YYYY-MM-DD (e.g., 1971-10-06).                |
| register_date    |  DATE         | The date and time when the customer record was created in the system|

---

### 2. **gold.dim_products**
- **Purpose:** Provides information about the products and their attributes.
- **Columns:**

| Column Name         | Data Type     | Description                                                                                   |
|---------------------|---------------|-----------------------------------------------------------------------------------------------|
| product_key         | bigint UN     | Surrogate key uniquely identifying each product record in the product dimension table.         |
| product_id          | INT           | A unique identifier assigned to the product for internal tracking and referencing.            |
| category_id         |  VARCHAR(50)  | A structured alphanumeric code representing the product, often used for categorization or inventory. |
| product_number      |  VARCHAR(50)  | A unique identifier for each product. i.e. 'BK-M82B-38'                  |
| product_name        |  VARCHAR(50)  | Descriptive name of the product, including key details such as type, color, and size.         |
| category            |  VARCHAR(50)  | The broader classification of the product (e.g., Bikes, Components) to group related items.  |
| subcategory         |  VARCHAR(50)  | A more detailed classification of the product within the category, such as product type.   |
| maintenance         |  VARCHAR(50)  | Indicates whether the product requires maintenance (e.g., 'Yes', 'No').                       |
| cost                |  INT          | The cost or base price of the product, measured in monetary units.                            |
| production_line     |  VARCHAR(50)  | The specific product line or series to which the product belongs (e.g., Road, Mountain).      |
| prd_start_date      | DATE          | The date when the product became available for sale or use.|

---

### 3. **gold.fact_sales**
- **Purpose:** Stores transactional sales data for analytical purposes.
- **Columns:**

| Column Name     | Data Type     | Description                                                                                   |
|-----------------|---------------|-----------------------------------------------------------------------------------------------|
| order_number    | VARCHAR(50)   | A unique alphanumeric identifier for each sales order (e.g., 'SO54496').                      |
| product_key     | bigint UN     | Surrogate key linking the order to the product dimension table.                               |
| customer_key    | bigint UN     | Surrogate key linking the order to the customer dimension table.                              |
| order_date      | DATE          | The date when the order was placed.                                                           |
| shipping_date   | DATE          | The date when the order was shipped to the customer.                                          |
| due_date        | DATE          | The date when the order payment was due.                                                      |
| sales_amount    | INT           | The total monetary value of the sale for the line item, in whole currency units (e.g., 25).   |
| quantity        | INT           | The number of units of the product ordered for the line item (e.g., 1).                       |
| price           | INT           | The price per unit of the product for the line item, in whole currency units (e.g., 25).      |
