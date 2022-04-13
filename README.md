## Project description

This is a simple API made with Laravel 9.
It allows to create, show, update and delete products.
No user authentication is required.

The products have the following fields: name, price and quantity.


## Installation

```bash
git clone https://github.com/pawel7/product_api.git
cd product_api
composer install
cp .env.example .env
```

Edit your database name, username, password in `.env` file.
When the database connection is ready do the folowing:

```bash
php artisan migrate
php artisan serve 
```

## Do it yourself

You can create such an API yourself from scratch just by issuing the following commands and editing a few files:
```
composer create-project laravel/laravel product_api
cd product_api/
git init
git add .
git commit -m "Initial commit"
php artisan make:model Product --migration
php artisan make:controller ProductController --api
code .
```
Edit the following files:
```
.env
app/Models/Product.php
app/Http/Controllers/ProductController.php
routes/api.php
```
Run `php artisan serve`   
Run `Postman`.  
Create a new product:
```
POST http://localhost:8000/api/products
```
Supply a header `Accept: application/json`.  
Supply three keys and values in the body: name, price, quantity.   
Add another product.  

Open `http://localhost:8000/api/products` in the browser to see your products.

You can press `Ctrl-Z` to suspend the server and `fg` to resume.

## Routes

The following API routes are available:  

- List all products:
```
GET /api/products
```

- List a single product:
```
GET /api/products/{id}
```

- Search a product by name:
```
GET /products/search/{name}
```

In the real world application the following routes should be protected - available only for authorized users.  
But for simplicity of this demo all the routes are public and there is no login or logout route.  
The other API routes:  

- Create a new product.   
The body must have nonempty fields: name, price, quantity.  
```
POST /api/products
```
   
- Update a product
```
PUT /api/products/{id}
```

- Delete a product    
```
DELETE /api/products/{id}
```        

All the above public routes (except search route) are generated from a single instruction in `api.php`:
```
Route::apiResource('products', ProductController::class);
```
## Protecting routes

To protect the routes, we can write an `AuthController` with `register`, `login` and `logout` methods, and change the routes in `api.php` to the following:  

```
   // Public routes
Route::post('/register', [AuthController::class, 'register']);
Route::post('/login', [AuthController::class, 'login']);
Route::get('/products', [ProductController::class, 'index']);
Route::get('/products/{id}', [ProductController::class, 'show']);
Route::get('/products/search/{name}', [ProductController::class, 'search']);

   // Protected routes
Route::group(['middleware' => ['auth:sanctum']], function () {
    Route::post('/products', [ProductController::class, 'store']);
    Route::put('/products/{id}', [ProductController::class, 'update']);
    Route::delete('/products/{id}', [ProductController::class, 'destroy']);
    Route::post('/logout', [AuthController::class, 'logout']);
});
```

## Testing

See [Testing.md](Testing.md)