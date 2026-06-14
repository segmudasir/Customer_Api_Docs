# Public ECOM API

This API has four resources: Customers, Products, Cart, and Orders.<br>

User can add Customers, Get Customers, Update Customer and Delete Customers. (CRUD) Operations.<br>

User can add Products, Get Products, Update Products and Delete Products. (CRUD) Operations.<br>

User can add items to Cart, Update items in Cart, Get all Cart items and Remove items from Cart.<br>

User can Create Orders, Get Orders, and Delete Orders.<br>

But Orders endpoint requires User Authentication. <br>

User needs to register first (Name and Email Address) to get an Access token.<br><br>

Base URL = https://ecom-api-7hkg.onrender.com
Status = https://ecom-api-7hkg.onrender.com/status

## Endpoints

- [Server Status](#server-status)
- [Customers](#customers)
- [Products](#products)
- [Cart](#cart)
- [API Authentication](#api-authentication)
- [Orders](#orders)

## Server Status

### Check server status

**`/status`**

**Method:** GET

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Server is running.                    |

Example response:

```
{
    "status": "OK",
    "message": "Server is running",
    "timestamp": "2026-06-10T10:00:00.000Z"
}
```

## Customers

### Add Customer

**`/customers/add`**

**Method:** POST  
Also called CREATE Request - In this Method something is added or posted on the Server. Therefore usually we require a body.

Example Body:
```
{
  "CustomerID": 92,
  "CustomerName": "Maria Anders",
  "Gender": "Female",
  "Age": 35,
  "Address": "Obere Str. 57",
  "City": "Berlin",
  "PostalCode": "12209",
  "Country": "Germany"
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 201 Created          | Indicates that request has been submitted successfully.                    |
| 400 Bad Request  | If a required field is missing, or if a record with this CustomerID e.g., 92 already exists. Then following message should appear "Failed - Customer with ID 92 already exists." |

Example response:

```
{
    "Message": "Customer added successfully",
    "CustomerID": 92
}
```

### Get all Customers / Get Customer(s) by filter

**`/customers`**

**Method:** GET  
Also called Retrieve Request - Returns the list of all Customers from Server.

**Parameters**

| Name        | Type    | Parameter    | Required | Description                                                                                                | 
| ----------- | ------- | ----- | -------- | -----------------------------------------------------------------------------------------------------------| 
| `CustomerID`| integer | Query | Optional      | If you specify the CustomerID it will return only that Customer Record. If not Provided it will return all Customers records.  | 
| `CustomerName`      | string  | Query | Optional      | This is optional parameter. If you want to get specific Customer by providing CustomerName.                                         | 
| `Country`      | string  | Query | Optional      | It can be one of the following: Argentina, Austria, Belgium, Brazil, Canada, Denmark, Finland, France, Germany, Ireland, Italy, Mexico, Norway, Poland, Portugal, Spain, Sweden, Switzerland, UK, USA, Venezuela.                                         | 
| `City`      | string  | Query | Optional      | It can be one of the following: Aachen, Albuquerque, Anchorage, Barcelona, Barquisimeto, Bergamo, Berlin, Bern, Boise, Brandenburg, Bruxelles, Buenos Aires, Butte, Campinas, Caracas, Charleroi, Cork, Cowes, Cunewalde, Elgin, Eugene, Frankfurt a.M., Genève, Graz, Helsinki, I. de Margarita, Kirkland, Köln, København, Lander, Leipzig, Lille, Lisboa, London, Luleå, Lyon, Madrid, Mannheim, Marseille, México D.F., Montréal, München, Münster, Nantes, Oulu, Paris, Portland, Reggio Emilia, Reims, Resende, Rio de Janeiro, Salzgurg, San Cristóbal, San Francisco, São Paulo, Seattle, Sevilla, Stavern, Strasbourg, Stuttgart, Toulouse, Torino, Tsawassen, Vancouver, Versailles, Walla, Walla Walla, Århus.                                         | 
| `Gender`      | string  | Query | Optional      | It can be Male or Female.                                         | 

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates a successful response.                    |
| 404 Not Found   | If specific CustomerID, CustomerName, Country, City or Gender filter does not match any record, you will get "Customer not found". |

Example response:

```
[
    {
        "CustomerID": 1,
        "CustomerName": "Maria Anders",
        "Gender": "Female",
        "Age": 31,
        "Address": "Obere Str. 57",
        "City": "Berlin",
        "PostalCode": "12209",
        "Country": "Germany"
    },
    {
        "CustomerID": 2,
        "CustomerName": "Ana Trujillo",
        "Gender": "Female",
        "Age": 50,
        "Address": "Avda. de la Constitución 2222",
        "City": "México D.F.",
        "PostalCode": "05021",
        "Country": "Mexico"
    }
]
```

### Update Customer

**`/customers/update`**

**Method:** PUT  
Also called Update Request - In this method something or some property is updated on the Server. Therefore we require parameters that need to be changed.

Example Body:
```
{
  "CustomerID": 92,
  "Age": 34,
  "City": "Warsaw",
  "PostalCode": "31-127",
  "Country": "Poland"
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates that request has been submitted successfully.                    |
| 400 Bad Request | If CustomerID is missing, or no update fields are provided. |
| 404 Not found  | If CustomerID does not exist. |

Example response:

```
{
    "message": "Following properties of customer updated successfully",
    "Age": 34,
    "City": "Warsaw",
    "PostalCode": "31-127",
    "Country": "Poland"
}
```
Note: Only the properties that were updated are shown in the response.

### Delete Customer

**`/customers/delete`**

**Method:** DELETE  
Also called Delete Request - In this method records are deleted from the Server. We need the CustomerID sent in the body as JSON format.

Example Body:
```
{
  "CustomerID": 92
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates that record has been deleted successfully.                    |
| 400 Bad Request | If CustomerID is not provided. |
| 404 Not found  | If CustomerID does not exist. |

Example response:

```
{
    "message": "Customer deleted successfully",
    "CustomerID": 92
}
```

## Products

### Add Product

**`/products/add`**

**Method:** POST

Example Body:
```
{
  "ProductID": 5,
  "ProductName": "Boys' Summer Short Sleeve",
  "Price": 19.99,
  "ImagePath": "images/product5.jpg"
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 201 Created          | Indicates that the product has been added successfully.                    |
| 400 Bad Request  | If ProductID, ProductName, or Price is missing, or if a Product with this ProductID already exists. Then "Failed - Product with ID 5 already exists." |

Example response:

```
{
    "Message": "Product added successfully",
    "ProductID": 5
}
```

### Get all Products / Get Product(s) by filter

**`/products`**

**Method:** GET

**Parameters**

| Name        | Type    | Parameter | Required | Description |
| ----------- | ------- | --------- | -------- | ----------- |
| `ProductID`   | integer | Query | Optional | If specified, returns only that Product record. |
| `ProductName` | string  | Query | Optional | If specified, returns the Product matching that name. |

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates a successful response.                    |
| 404 Not Found   | If the specified ProductID does not exist, "Product with ID {id} not found". |

Example response:

```
[
    {
        "ProductID": 4,
        "ProductName": "USB-C Power Bank",
        "Price": 59.99,
        "ImagePath": "images/product4.jpg"
    },
    {
        "ProductID": 5,
        "ProductName": "Boys' Summer Short Sleeve",
        "Price": 19.99,
        "ImagePath": "images/product5.jpg"
    }
]
```

### Update Product

**`/products/update`**

**Method:** PUT

Example Body:
```
{
  "ProductID": 5,
  "Price": 17.99
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates that the product was updated, or that no changes were made.                    |
| 400 Bad Request | If ProductID is missing, or no update fields are provided. |
| 404 Not found  | If ProductID does not exist. |

Example response:

```
{
    "message": "Product updated successfully and following properties were updated",
    "Price": 17.99
}
```
Note: If the submitted values are identical to the existing ones, the response will instead be:
```
{
    "message": "No changes were made",
    "ProductID": 5
}
```

### Delete Product

**`/products/delete`**

**Method:** DELETE

Example Body:
```
{
  "ProductID": 5
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates that the product was deleted successfully.                    |
| 400 Bad Request | If ProductID is not provided. |
| 404 Not found  | If ProductID does not exist. |

Example response:

```
{
    "message": "Product deleted successfully",
    "ProductID": 5
}
```

## Cart

### Add item to Cart

**`/cart/additem`**

**Method:** POST  
If the product is already in the cart, its quantity is incremented by 1. Otherwise it is added with quantity 1.

Example Body:
```
{
  "ProductID": 5
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 201 Created     | Product was newly added to the cart.                    |
| 200 OK          | Product already in cart; quantity increased by 1. |
| 400 Bad Request | If ProductID is not provided. |
| 404 Not found  | If ProductID does not exist in Products. |

Example response (new item):
```
{
    "message": "Product added to Cart",
    "ProductID": 5,
    "ProductName": "Boys' Summer Short Sleeve",
    "Quantity": 1
}
```

Example response (existing item):
```
{
    "message": "Quantity increased by 1",
    "ProductID": 5,
    "ProductName": "Boys' Summer Short Sleeve",
    "Quantity": 2
}
```

### Update item in Cart

**`/cart/updateitem`**

**Method:** PUT  
Sets the quantity of a Product in the cart. If the product isn't in the cart yet, it is inserted with the given quantity. Setting Quantity to 0 removes the item from the cart.

Example Body:
```
{
  "ProductID": 5,
  "Quantity": 3
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Quantity updated, or item removed (Quantity = 0).                    |
| 201 Created     | New item added to the cart. |
| 400 Bad Request | If ProductID or Quantity is missing, Quantity is negative, or Quantity is 0 for a non-existing item. |
| 404 Not found  | If ProductID does not exist in Products. |

Example response (updated):
```
{
    "message": "Quantity updated",
    "ProductID": 5,
    "ProductName": "Boys' Summer Short Sleeve",
    "newQuantity": 3
}
```

Example response (removed):
```
{
    "message": "Product removed from Cart",
    "ProductID": 5,
    "ProductName": "Boys' Summer Short Sleeve"
}
```

### Get all Cart items

**`/cart/getitems`**

**Method:** GET

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates a successful response.                    |

Example response:

```
[
    {
        "ProductID": 4,
        "ProductName": "USB-C Power Bank",
        "Quantity": 1
    },
    {
        "ProductID": 5,
        "ProductName": "Boys' Summer Short Sleeve",
        "Quantity": 3
    }
]
```

### Remove item from Cart

**`/cart/removeitem`**

**Method:** DELETE

Example Body:
```
{
  "ProductID": 5
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates that the item has been removed successfully.                    |
| 400 Bad Request | If ProductID is not provided. |
| 404 Not found  | If ProductID is not found in the cart. |

Example response:

```
{
    "Message": "Product with ID 5 has been deleted successfully"
}
```

## API Authentication

Some endpoints (Orders) require authentication. To create or view orders, you need to register your API client and obtain an access token.

The endpoints that require authentication expect a bearer token sent in the Authorization header.

Example:

Authorization: Bearer YOUR TOKEN

### Register a new API client

**`/users`**

**Method:** POST  

**Parameters**

The request body needs to be in JSON format.

| Name          | Type   | In   | Required | Description                            |
| ------------- | ------ | ---- | -------- | -------------------------------------- |
| `Name`  | string | body | Yes      | The name of the API client.            |
| `Email` | string | body | Yes      | The email address of the API client. * |

\* The email address DOES NOT need to be real. The email will not be stored on the server.

**Status codes**

| Status code     | Description                                                                       |
|-----------------|-----------------------------------------------------------------------------------|
| 201 Created     | Indicates that the client has been registered successfully.                       |
| 400 Bad Request | Indicates that Name and/or Email are missing.                               |
| 409 Conflict    | Indicates that an API client has already been registered with this email address. |

Example request body:

```
{
   "Name": "Postman",
   "Email": "maddy@example.com"
}
```

Example response:
```
{
    "accessToken": "123456789"
}
```

### Retrieve Access Token

**`/accesstoken`**

**Method:** POST  
If you've already registered, use this to retrieve your existing access token by Email.

Example request body:
```
{
  "Email": "maddy@example.com"
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates a successful response.                    |
| 400 Bad Request | If Email is not provided. |
| 404 Not found   | If Email is not registered. |

Example response:
```
{
    "Email": "maddy@example.com",
    "accessToken": "123456789"
}
```

### Delete Access Token (Delete API client)

**`/deletetoken`**

**Method:** DELETE

Example request body:
```
{
  "Email": "maddy@example.com"
}
```

**Status codes**

| Status code | Description |
|-----------------|-----------------------------------------------------|
| 200 OK          | Indicates that the user/token has been deleted successfully.                    |
| 400 Bad Request | If Email is not provided. |
| 404 Not found   | If Email does not exist. |

Example response:
```
{
    "message": "User has been deleted successfully"
}
```

## Orders

### Create a new order

**`/orders/add`**

**Method:** POST  

The request body needs to be in JSON format.

**Parameters**

| Name            | Type   | In     | Required | Description                          |
| --------------- | ------ | ------ | -------- | ------------------------------------ |
| `Authorization` | string | header | Yes      | The bearer token of the API client.  |
| `ProductID`  | number | body   | Yes      | ID of the product.            |
| `Quantity`       | Number | body   | Yes       | Quantity of the product. |

Note: On the basis of ProductID, it will go to Products table, search for ProductID, then insert order data with ProductName, Price, and TotalPrice (Price × Quantity). An OrderID will be generated and shown in the response.

Example request body:

```
{
  "ProductID": 5,
  "Quantity": 1
}
```

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 201 Created      | Indicates that the order has been created successfully.                                                |
| 400 Bad Request  | Invalid/missing ProductID or Quantity (Quantity must be greater than 0).                                                    |
| 401 Unauthorized | Unauthorized (missing/invalid token)  |
| 404 Not found | Product or User not found  |

Example response:

```
{
    "Message": "Order successfully created",
    "OrderID": 1770167265321
}
```

### Get all orders / Get a single order

**`/orders`**

**Method:** GET  
Returns all orders, or a single order if `OrderID` is provided as a query parameter.

**Parameters**

| Name            | Type   | In     | Required | Description                                   |
| --------------- | ------ | ------ | -------- | --------------------------------------------- |
| `Authorization` | string | header | Yes      | Specifies the bearer token of the API client. |
| `OrderID`       | Number | Query  | Optional | If specified, returns that single order as an object. |
| `CustomerName`  | string | Query  | Optional | If specified, filters orders by CustomerName. |

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 200 OK           | Indicates a successful response.                                                                       |
| 401 Unauthorized | Indicates that the request has not been authenticated. Check the response body for additional details. |
| 404 Not found    | Indicates that no order(s) match the given filters.                 |

Example response (all orders):

```
[
    {
        "OrderID": 1770167113382,
        "CustomerName": "Mudasir",
        "Email": "perdesi88@gmail.com",
        "ProductID": 5,
        "ProductName": "Boys' Summer Short Sleeve",
        "Price": 19.99,
        "Quantity": 1,
        "OrderDate": "2026-02-04",
        "TotalAmount": 19.99
    },
    {
        "OrderID": 1770167265321,
        "CustomerName": "Mudasir",
        "Email": "perdesi88@gmail.com",
        "ProductID": 4,
        "ProductName": "USB-C Power Bank",
        "Price": 59.99,
        "Quantity": 1,
        "OrderDate": "2026-02-04",
        "TotalAmount": 59.99
    }
]
```

Example response (single order, `?OrderID=1770167265321`):

```
{
    "OrderID": 1770167265321,
    "CustomerName": "Mudasir",
    "Email": "perdesi88@gmail.com",
    "ProductID": 4,
    "ProductName": "USB-C Power Bank",
    "Price": 59.99,
    "Quantity": 1,
    "OrderDate": "2026-02-04",
    "TotalAmount": 59.99
}
```

### Delete an order

**`/orders/delete`**

**Method:** DELETE

**Parameters**

| Name            | Type   | In     | Required | Description                         |
| --------------- | ------ | ------ | -------- | ----------------------------------- |
| `Authorization` | string | header | Yes      | The bearer token of the API client. |
| `OrderID`       | string | body   | Yes      | The order id.                       |

Example request body:

```
{
  "OrderID": 1770167265321
}
```

**Status codes**

| Status code      | Description                                                                                            |
| ---------------- | ------------------------------------------------------------------------------------------------------ |
| 200 OK   | Indicates that the order has been deleted successfully.                                                |
| 400 Bad Request  | Indicates that the Order ID is not provided.                                            |
| 401 Unauthorized | Indicates that the request has not been authenticated. |
| 404 Not found    | Indicates that there is no order with the specified id.                 |

Example response:

```
{
    "Message": "Order with ID 1770167265321 has been deleted successfully"
}
```
