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


# MongoDB `$match` Query Filters

1. **$eq** — Equals
   - Matches documents where the field is equal to the specified value.
   `{ field: { $eq: value } }`

2. **$ne** — Not Equals
   - Matches documents where the field is not equal to the specified value.
   `{ field: { $ne: value } }`

3. **$gt** — Greater Than
   - Matches documents where the field value is greater than the specified value.
   `{ field: { $gt: value } }`

4. **$gte** — Greater Than or Equal
   - Matches documents where the field value is greater than or equal to the specified value.
   `{ field: { $gte: value } }`

5. **$lt** — Less Than
   - Matches documents where the field value is less than the specified value.
   `{ field: { $lt: value } }`

6. **$lte** — Less Than or Equal
   - Matches documents where the field value is less than or equal to the specified value.
   `{ field: { $lte: value } }`

7. **$in** — In
   - Matches documents where the field’s value exists in the provided array of values.
   `{ field: { $in: [value1, value2, value3] } }`

8. **$nin** — Not In
   - Matches documents where the field’s value does not exist in the provided array of values.
   `{ field: { $nin: [value1, value2, value3] } }`

9. **$exists** — Field Existence
   - Matches documents where the field exists or does not exist based on a boolean.
   `{ field: { $exists: true } }`

10. **$type** — Type
    - Matches documents where the field is of the specified BSON type.
    `{ field: { $type: "string" } }`

11. **$regex** — Regular Expression
    - Matches documents where the field’s value matches the given regular expression.
    `{ field: { $regex: /^pattern/ } }`

12. **$all** — Array Match
    - Matches arrays that contain all elements specified in the array.
    `{ field: { $all: [element1, element2] } }`

13. **$size** — Array Size
    - Matches arrays that have the specified number of elements.
    `{ field: { $size: 3 } }`

14. **$elemMatch** — Element Match
    - Matches documents that contain an array field with at least one element that matches all the specified conditions.
    `{ field: { $elemMatch: { $gt: 5, $lt: 10 } } }`

15. **$and** — Logical AND
    - Combines multiple conditions; all must be true.
    `{ $and: [ { condition1 }, { condition2 } ] }`

16. **$or** — Logical OR
    - Matches documents if at least one of the specified conditions is true.
    `{ $or: [ { condition1 }, { condition2 } ] }`

17. **$not** — Logical NOT
    - Inverts the effect of a query expression.
    `{ field: { $not: { $gt: 5 } } }`

18. **$nor** — Logical NOR
    - Matches documents that fail all the specified conditions.
    `{ $nor: [ { condition1 }, { condition2 } ] }`

19. **$mod** — Modulus
    - Matches documents where the field value divided by the divisor has the specified remainder.
    `{ field: { $mod: [divisor, remainder] } }`

20. **$geoWithin** — Geographic Boundary
    - Matches documents with geospatial data that exist within a specified geometry.
    `{ location: { $geoWithin: { $geometry: { type: "Polygon", coordinates: [...] } } } }`

21. **$text** — Text Search
    - Matches documents that contain the specified text.
    `{ $text: { $search: "text" } }`

22. **$where** — JavaScript Expression
    - Matches documents that satisfy a JavaScript expression.
    `{ $where: "this.field > 10" }`
