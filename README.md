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

text

---

## Insert Sample Data

db.orders.insertMany([
{ orderId: 1, productId: "P001", qty: 5, price: 50, status: "completed" },
{ orderId: 2, productId: "P002", qty: 15, price: 150, status: "completed" },
{ orderId: 3, productId: "P001", qty: 12, price: 120, status: "pending" },
{ orderId: 4, productId: "P003", qty: 9, price: 90, status: "completed" },
{ orderId: 5, productId: "P002", qty: 8, price: 80, status: "completed" },
{ orderId: 6, productId: "P003", qty: 20, price: 200, status: "completed" }
]);


---

## Aggregation Query with Logical Operators

This aggregation pipeline:

- Filters orders where `status` is `"completed"` **AND** either `qty` is greater than or equal to 10 **OR** `price` is greater than or equal to 100.
- Groups the documents by `productId`.
- Calculates total quantity sold (sum of `qty`) per product.
- Sorts the results by the total sales in descending order.

db.orders.aggregate([
{
$match: {
status: "completed",
$or: [
{ qty: { $gte: 10 } },
{ price: { $gte: 100 } }
]
}
},
{
$group: {
_id: "$productId",
totalSales: { $sum: "$qty" }
}
},
{
$sort: {
totalSales: -1
}
}
]);


---

## Additional Logical Queries

- Find orders with status `"completed"` and quantity less than 15:

db.orders.find({
$and: [
{ status: "completed" },
{ qty: { $lt: 15 } }
]
});


- Find orders where status is **not** `"completed"`:

db.orders.find({
status: { $ne: "completed" }
});


- Find orders where quantity is **not** greater than 10:

db.orders.find({
qty: { $not: { $gt: 10 } }
});


---

## Projection Example in Aggregation

Show only specific fields in results:

db.orders.aggregate([
{ $match: { status: "completed" } },
{ $project: { _id: 0, orderId: 1, productId: 1, qty: 1 } }
]);


---

## Adding Computed Fields

Add a calculated `totalPrice` field in aggregation:

db.orders.aggregate([
{
$addFields: {
totalPrice: { $multiply: ["$qty", "$price"] }
}
},
{ $match: { status: "completed" } }
]);

