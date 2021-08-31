# Mongo-DB-Day-1

## Task - 1

**Q: Find all the information about each products**

```javascript
db.product.find().pretty();
```

**Q: Find the product price which are between 400 to 800**

```javascript
db.product.find({ product_price: { $gte: 400, $lte: 800 } }).pretty();
```

**Q: Find the product price which are not between 400 to 600**

```javascript
db.product.find({ product_price: { $not: { $gte: 400, $lte: 600 } } }).pretty();
```

**Q: List the four product which are greater than 500 in price**

```javascript
db.product
  .find({ product_price: { $gte: 500 } })
  .limit(4)
  .pretty();
```

**Q: Find the product name and product material of each products**

```javascript
db.product.find({}, { product_name: 1, product_material: 1 }).pretty();
```

**Q: Find the product with a row id of 10**

```javascript
db.product.find({ id: "10" }).pretty();
```

**Q: Find only the product name and product material**

```javascript
db.product.find({}, { product_name: 1, product_material: 1, _id: 0 }).pretty();
```

**Q: Find all products which contain the value of soft in product material**

```javascript
db.product.find({ product_material: "Soft" }).pretty();
```

**Q: Find products which contain product color indigo and product price 492.00**

```javascript
db.product
  .find({ $or: [{ product_price: 492 }, { product_color: "indigo" }] })
  .pretty();
```

**Q: Delete the products which product price value are same**

```javascript
// First get list of product_price which are repeated. Result is [36, 47]

db.product.aggregate([
  { $group: { _id: "$product_price", count: { $count: {} } } },
  { $match: { _id: { $ne: null }, count: { $gt: 1 } } },
]);

db.product.deleteMany({ product_price: { $in: [36, 47] } });
```
