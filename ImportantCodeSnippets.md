## Essential MongoDB Queries with Examples

### 1. Basic CRUD Operations:

Insert a document:
```JavaScript
db.products.insertOne({name: "iPhone 15", price: 799, category: "Electronics"});
```

Find documents:
```JavaScript
db.products.find({price: {$gt: 500}}).pretty(); // Find products with price greater than 500
```

Update a document:
```JavaScript
db.products.updateOne({name: "iPhone 15"}, {$set: {price: 849}});
```

Delete a document:
```JavaScript
db.products.deleteOne({name: "iPhone 15"});
```

2. Aggregation Pipeline:

```JavaScript
db.sales.aggregate([
    {$match: {date: {$gte: ISODate("2023-01-01"), $lte: ISODate("2023-12-31")}}},
    {$group: {_id: "$productId", totalSales: {$sum: "$quantity"}}},
    {$sort: {totalSales: -1}}
]).pretty();
```

3. Text Search:

```JavaScript
db.products.createIndex({description: "text"});
db.products.find({$text: {$search: "smartphone"}}).pretty();
```

4. Geospatial Queries:

```JavaScript
db.restaurants.createIndex({location: "2dsphere"});
db.restaurants.find({location: {$near: {$geometry: {type: "Point", coordinates: [77.5946, 12.9611]}, $maxDistance: 10000}}}).pretty();
```

5. Sorting and Limiting Results:

JavaScript
db.products.find().sort({price: 1}).limit(5).pretty(); // Sort ascending by price and limit to 5 results
```

6. Projection:

```JavaScript
db.products.find({}, {name: 1, price: 1, _id: 0}).pretty(); // Project only specific fields
```

7. Joins (Using Lookup Stage):

```JavaScript
db.orders.aggregate([
    {$lookup: {from: "customers", localField: "customerId", foreignField: "_id", as: "customer"}}
]).pretty();
```

8. Indexes:

```JavaScript
db.products.createIndex({name: 1, price: -1}); // Create a compound index
```

9. Aggregation Framework (Additional Examples):

$unwind: Unwinds an array field.
$project: Projects specific fields or calculated values.
$redact: Redacts sensitive information based on authorization rules.
$facet: Groups documents into multiple buckets based on different aggregation pipelines.
$sample: Samples a random subset of documents.


10. More queries

```javascript
db.collection.countDocuments({ department: "IT" }); // Counting
db.collection.find({}).sort({ age: -1 }); // find with sort
db.collection.find({}).skip(10).limit(5); // with pagination

db.collection.aggregate([
  { $group: { _id: "$department", total: { $sum: 1 } } }
]); // groupby

db.collection.aggregate([
  { $match: { age: { $gte: 30 } } },
  { $project: { name: 1, age: 1, _id: 0 } }
]); // aggregate with match and project

db.collection.updateOne(
  { name: "Eve" },
  { $set: { age: 29, department: "Marketing" } },
  { upsert: true }
); // upsert

db.collection.find({ department: { $in: ["HR", "IT"] } }); // in query





```
