# Database

## Assignment

Design a database contains tables that support bellowing requirements.

**Requirements**

- As a store owner, I'd like to save customer information, so I can track age, gender and location for analysis purpose.
- As a store owner, I'd like to have a list of products, so my customers can browse and discover my collections.
  - Each product can be listed in categories.
  - Each product has different and multiple variation which can be color, size or anything.
- As a store owner, I would like my customers to be able to add items to cart, so they can process to check out.

## Database Schema

### Customers Table

| Column Name | Data Type | Description                     |
| ----------- | --------- | ------------------------------- |
| customer_id | INT       | Unique identifier for customers |
| name        | VARCHAR   | Name of the customer            |
| age         | INT       | Age of the customer             |
| gender      | VARCHAR   | Gender of the customer          |
| location    | VARCHAR   | Location of the customer        |

```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    age INT,
    gender ENUM('Male', 'Female', 'Other'),
    location VARCHAR(255)
);
```

### Products Table

| Column Name | Data Type | Description                            |
| ----------- | --------- | -------------------------------------- |
| product_id  | INT       | Unique identifier for products         |
| name        | VARCHAR   | Name of the product                    |
| category_id | INT       | Foreign key to ProductCategories table |

```sql
CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    category_id INT NOT NULL,
    FOREIGN KEY (category_id) REFERENCES ProductCategories(category_id)
);
```

### ProductCategories Table

| Column Name | Data Type | Description                      |
| ----------- | --------- | -------------------------------- |
| category_id | INT       | Unique identifier for categories |
| name        | VARCHAR   | Name of the category             |

```sql
CREATE TABLE ProductCategories (
    category_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL
);
```

### ProductVariations Table

| Column Name     | Data Type | Description                              |
| --------------- | --------- | ---------------------------------------- |
| variation_id    | INT       | Unique identifier for product variations |
| product_id      | INT       | Foreign key to Products table            |
| variation_type  | VARCHAR   | Type of the variation e.g. color, size   |
| variation_value | VARCHAR   | Value of the variation e.g. red, large   |

```sql
CREATE TABLE ProductVariations (
    variation_id INT PRIMARY KEY AUTO_INCREMENT,
    product_id INT,
    variation_type VARCHAR(50),
    variation_value VARCHAR(50),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
```

### ShoppingCart Table

| Column Name | Data Type | Description                         |
| ----------- | --------- | ----------------------------------- |
| cart_id     | INT       | Unique identifier for shopping cart |
| customer_id | INT       | Foreign key to Customers table      |
| product_id  | INT       | Foreign key to Products table       |
| quantity    | INT       | Quantity of the product in cart     |

```sql
CREATE TABLE ShoppingCart (
    cart_id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);
```
