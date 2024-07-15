### Fact Table: `fact_table`

| Column Name | Data Type | Description |
| --- | --- | --- |
| fact_id | Primary Key | Unique identifier for each transaction record |
| payment_key | Foreign Key | References payment_key in trans_dim |
| customer_key | Foreign Key | References customer_key in customer_dim |
| time_key | Foreign Key | References time_key in time_dim |
| item_key | Foreign Key | References item_key in item_dim |
| store_key | Foreign Key | References store_key in store_dim |
| quantity | Integer | Quantity of items purchased |
| unit | String | Unit of measurement for the item |
| unit_price | Decimal | Price per unit of the item |
| total_price | Decimal | Total price of the transaction |

### Dimension Tables:

### `customer_dim`

| Column Name | Data Type | Description |
| --- | --- | --- |
| customer_key | Primary Key | Unique identifier for each customer |
| name | String | Name of the customer |
| contact_no | String | Contact number of the customer |
| nid | String | National ID number of the customer (if applicable) |

### `item_dim`

| Column Name | Data Type | Description |
| --- | --- | --- |
| item_key | Primary Key | Unique identifier for each item |
| item_name | String | Name of the item |
| description | String | Description of the item |
| unit_price | Decimal | Price per unit of the item |
| man_country | String | Manufacturing country of the item |
| supplier | String | Supplier of the item |
| unit | String | Unit of measurement for the item |

### `store_dim`

| Column Name | Data Type | Description |
| --- | --- | --- |
| store_key | Primary Key | Unique identifier for each store |
| division | String | Division where the store is located |
| district | String | District where the store is located |
| upazila | String | Upazila (sub-district) where the store is located |

### `time_dim`

| Column Name | Data Type | Description |
| --- | --- | --- |
| time_key | Primary Key | Unique identifier for each time record |
| date | Date | Date of the transaction |
| hour | Integer | Hour of the transaction |
| day | Integer | Day of the transaction |
| week | Integer | Week number of the transaction |
| month | Integer | Month of the transaction |
| quarter | Integer | Quarter of the transaction |
| year | Integer | Year of the transaction |

### `trans_dim`

| Column Name | Data Type | Description |
| --- | --- | --- |
| payment_key | Primary Key | Unique identifier for each payment transaction |
| trans_type | String | Type of transaction (e.g., cash, credit) |
| bank_name | String | Name of the bank (if applicable) |

### Relationships:

- `fact_table` references `customer_dim` via `customer_key`.
- `fact_table` references `item_dim` via `item_key`.
- `fact_table` references `store_dim` via `store_key`.
- `fact_table` references `time_dim` via `time_key`.
- `fact_table` references `trans_dim` via `payment_key`.
