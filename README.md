# MongoDB day1 

## Questions and Queries(For output ref MongoDB.docs)

### Creating Collections

```db.products.insertMany([{productJSONData]});```

### 1.	Find all the information about each products

```
db.products.find();
```

### 2.	Find the product price which are between 400 to 800

```
db.products.find(
{
   'product_price':{$gt:400,$lt:800}
});

```

### 3.Find the product price which are not between 400 to 600

```
db.products.find(
  {
    $or:[{'product_price':{$lt:400}},{'product_price':{$gt:600}}]
});

```

### 4.List the four product which are greater than 500 in price

```
db.products.find
({
  'product_price':{$gte:500}}
).limit(4);

```

### 5.Find the product name and product material of each products

```
db.products.find(
	 {},
	 {'product_name':1,'product_material':1}
	);

```

### 6.Find the product with a row id of 10

```
db.products.findOne({'id':'10'});
```

### 7.Find only the product name and product material

```
db.products.find(
 {},
 {'_id':0,'product_name':1,'product_material':1}
);
```

### 8.Find all products which contain the value of soft in product material

```
db.products.find({'product_material':'Soft'});
```

### 9. Find products which contain product color indigo  and product price 492.00

```
db.products.find({$or:[{'product_color':'indigo'},{'product_price':492}]});
```

### 10. Delete the products which product price value are same

```
let repeat =db.products_new.distinct('product_price');

  repeat.forEach((price)=>{
      let repeatPrice = db.products_new.find({product_price:price}).sort({'id':1}).skip(1);
      repeatPrice.forEach((delDoc)=>
         db.products.deleteOne({'id':delDoc.id})
  )
  });
