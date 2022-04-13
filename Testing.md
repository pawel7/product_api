## Testing

You can test the API routes for products with Postman.  

To create a new product:
```
POST http://localhost:8000/api/products
```
The body must have nonempty fields: name, price, quantity.   
We get the following response:
```
{
    "name": "shoes",
    "price": "200",
    "quantity": "20",
    "updated_at": "2022-04-13T08:25:37.000000Z",
    "created_at": "2022-04-13T08:25:37.000000Z",
    "id": 1
}
```

To edit a product:
```
PUT http://localhost:8000/api/products/1 
```
In the body we put the fields to change, e.g. name and quantity.   
We get a response:
```
{
    "id": 1,
    "name": "jogging shoes",
    "price": "200",
    "quantity": 5,
    "created_at": "2022-04-13T08:58:22.000000Z",
    "updated_at": "2022-04-13T09:14:18.000000Z"
}
```

To get products as a *JSON resource*:
```
GET http://localhost:8000/api/products
```
The response:
```
[
    {
        "id": 1,
        "name": "jogging shoes",
        "price": 200,
        "quantity": 5,
        "created_at": "2022-04-13T08:58:22.000000Z",
        "updated_at": "2022-04-13T09:14:18.000000Z"
    },
    {
        "id": 2,
        "name": "trousers",
        "price": 100,
        "quantity": 10,
        "created_at": "2022-04-13T08:59:07.000000Z",
        "updated_at": "2022-04-13T08:59:07.000000Z"
    },
     {
        "id": 3,
        "name": "shoes for climbing",
        "price": 180,
        "quantity": 20,
        "created_at": "2022-04-13T11:25:37.000000Z",
        "updated_at": "2022-04-13T11:25:37.000000Z"
    }
]
```

To search for a product - we supply its name or part of the name:
```
GET http://localhost:8000/api/search/sho
```
Response:
```
[
    {
        "id": 1,
        "name": "jogging shoes",
        "price": 200,
        "quantity": 5,
        "created_at": "2022-04-13T08:58:22.000000Z",
        "updated_at": "2022-04-13T09:14:18.000000Z"
    },
    {
        "id": 3,
        "name": "shoes for climbing",
        "price": 180,
        "quantity": 20,
        "created_at": "2022-04-13T11:25:37.000000Z",
        "updated_at": "2022-04-13T11:25:37.000000Z"
    }
]
```