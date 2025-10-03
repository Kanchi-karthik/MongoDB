# MongoDB
FSD_ExperimentNo_12

# MongoDB Aggregation and Logical Operations

## Project Aim
To implement and demonstrate MongoDB aggregation pipeline commands combined with logical query operators for effective data querying and analysis.

---

## Setup

### Create Database and Collection

use salesDB;
db.createCollection("orders");

---

## Insert Sample Data

![Sample Data Insert](./images/Insert%20sample%20data.png)


---
![Sample Data Insert](./images/insertMany_output.png)
---

## Aggregation Query with Logical Operators

This aggregation pipeline:

- Filters orders where `status` is `"completed"` **AND** either `qty` is greater than or equal to 10 **OR** `price` is greater than or equal to 100.
- Groups the documents by `productId`.
- Calculates total quantity sold (sum of `qty`) per product.
- Sorts the results by the total sales in descending order.

![Aggregation Pipeline Output](./images/Aggregation%20pipeline.png)

---
![Aggregation Pipeline Output](./images/aggregationpipeline_output.png)
---

## Additional Logical Queries

- Find orders with status `"completed"` and quantity less than 15:

![Logical queries $and](./images/Logical%20queries%20_$and.png)

---
![Logical queries $and](./images/$and_1.png)
![Logical queries $and](./images/$and_2.png)
---

- Find orders where status is **not** `"completed"`:

![Logical queries $ne](./images/Logical%20queries%20_$ne.png)

---
![Logical queries $ne](./images/$ne_output.png)
---

- Find orders where quantity is **not** greater than 10:

![Logical queries $not](./images/Logical%20queries%20_$not.png)

---
![Logical queries $not](./images/$not_output_1.png)
![Logical queries $not](./images/$not_output_2.png)
---

## Projection Example in Aggregation

Show only specific fields in results:

![Projection Aggregation Output](./images/Projection%20example%20in%20aggregation.png)

---
![Projection Aggregation Output](./images/projection_aggregation_output.png)
---

## Adding Computed Fields

Add a calculated `totalPrice` field in aggregation:

![Computed Field Example](./images/$addFields.png)

---
![Computed Field Example](./images/$addFields_output_1.png)
![Computed Field Example](./images/$addFields_output_2.png)
![Computed Field Example](./images/$addFields_output_3.png)
---