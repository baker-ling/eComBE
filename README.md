# eComBE [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Description

A simple backend for an e-commerce website.

## Contents

- [Installation](#installation)
- [Usage](#usage)
- [Questions](#questions)
- [License](#license)

## Installation

You must have Node and MySQL installed to use this program.

At the command line terminal of your choice type the following:

```
git clone https://github.com/baker-ling/eComBE
cd eComBE
npm install
```

Next, you need to create a file named '.env' in that directory with the following information to create connections to MySQL.

```
DB_NAME=ecommerce_db
DB_USER=[your mysql username]
DB_PW=[your mysql password]
```

Next, you need to create the database that this program uses. You can do that by logging into the MySQL CLI from the project directury and running `source db/schema.sql`.

Finally, seed the database by running the command `npm run seed` at the shell prompt.

## Usage

Start up the server by running the command `node server`. The server will start up and log the port that it is listening on. You can then begin interacting with the backend via HTTP requests.

## HTTP API

### Categories

#### GET /api/categories

Provides a list of all categories and their products. Successful response is a JSON-serialization of an *array* of objects of following structure:

```json
{
  "id": 1,
  "category_name": "Shirts",
  "products": [
    {
      "id": 1,
      "product_name": "Plain T-Shirt",
      "price": 14.99,
      "stock": 14,
      "category_id": 1
    }
  ]
}
```

#### GET /api/categories/[id]

Provides the category specified by `[id]` in the request URL. Successful response is a JSON-serialization of an object of following structure:

```json
{
  "id": 5,
  "category_name": "Shoes",
  "products": [
    {
      "id": 2,
      "product_name": "Running Sneakers",
      "price": 90,
      "stock": 25,
      "category_id": 5
    }
  ]
}
```

#### POST /api/categories

Creates a category. Request body should contain JSON data with the following structure:

```json
{
  "category_name": "NAME OF NEW CATEGORY"
}
```

The response for a successful request will contain the `category_name` as well as the `id` assigned to the new category.

#### PUT /api/categories/[id]

Updates a category. Request body should have the same form as the POST request for creating a new category.

#### DELETE /api/categories/[id]

Deletes a category.

### Products

#### GET /api/products

Provides a list of all products. Successful response is a JSON-serialization of an *array* of objects of following structure:

```json
{
    "id": 1,
    "product_name": "Plain T-Shirt",
    "price": 14.99,
    "stock": 14,
    "category_id": 1,
    "category": {
      "id": 1,
      "category_name": "Shirts"
    },
    "tags": [
      {
        "id": 6,
        "tag_name": "white",
        "product_tag": {
          "id": 1,
          "product_id": 1,
          "tag_id": 6
        }
      },
      {
        "id": 7,
        "tag_name": "gold",
        "product_tag": {
          "id": 2,
          "product_id": 1,
          "tag_id": 7
        }
      },
      {
        "id": 8,
        "tag_name": "pop culture",
        "product_tag": {
          "id": 3,
          "product_id": 1,
          "tag_id": 8
        }
      }
    ]
  }
```

#### GET /api/products/[id]

Provides the product specified by `[id]` in the request URL. Successful response is a JSON-serialization of an object of following structure:

```json
{
  "id": 2,
  "product_name": "Running Sneakers",
  "price": 90,
  "stock": 25,
  "category_id": 5,
  "category": {
    "id": 5,
    "category_name": "Shoes"
  },
  "tags": [
    {
      "id": 6,
      "tag_name": "white",
      "product_tag": {
        "id": 4,
        "product_id": 2,
        "tag_id": 6
      }
    }
  ]
}
```

#### POST /api/product

Creates a new product. Request body should contain JSON data with the following structure:

```json
{
	"product_name": "Single-Breasted Suit",
	"price": 649.99,
	"stock": 5,
	"category_id": 6,
	"tagIds": [3]
}
```

Note: The `tagIds` property may be omitted. Leave it out and specify the tags for the new product via PUT request if you want to get the id assigned to the new product back in the response.

#### PUT /api/product/[id]

Updates a product. Request body should have the same form as the POST request for creating a new product, except that the `tagIds` property is required.

#### DELETE /api/product/[id]

Deletes a product.

### Tags

#### GET /api/tags

Provides a list of all tags. Successful response is a JSON-serialization of an *array* of objects of following structure:

```json
  {
    "id": 7,
    "tag_name": "gold",
    "products": [
      {
        "id": 1,
        "product_name": "Plain T-Shirt",
        "price": 14.99,
        "stock": 14,
        "category_id": 1,
        "product_tag": {
          "id": 2,
          "product_id": 1,
          "tag_id": 7
        }
      }
    ]
  }
```

#### GET /api/tags/[id]

Provides the tag specified by `[id]` in the request URL. Successful response is a JSON-serialization of an object of following structure:

```json
{
  "id": 7,
  "tag_name": "gold",
  "products": [
    {
      "id": 1,
      "product_name": "Plain T-Shirt",
      "price": 14.99,
      "stock": 14,
      "category_id": 1,
      "product_tag": {
        "id": 2,
        "product_id": 1,
        "tag_id": 7
      }
    }
  ]
}
```

#### POST /api/tag

Creates a new tag. Request body should contain JSON data with the following structure:

```json
{
  "tag_name": "outerwear",
  "productIds": [
    7
  ]
}
```

Note: The productIds` property may be omitted. Leave it out and specify the products for the new tag via PUT request if you want to get the id assigned to the new tag back in the response.

#### PUT /api/tag/[id]

Updates a tag. Request body should have the same form as the POST request for creating a new tag, except that the `productIds` property is required.

#### DELETE /api/tag/[id]

Deletes a tag.

## Video Walkthrough

A video walkthrough is available [here](https://1drv.ms/v/s!Amp9wAf74eY0myN69eZuwa5cb5ap?e=exdHqw).



## Questions

If you have any questions, feel free to reach out via one of the following:

- Email: [brian.baker.bdb@gmail.com](mailto:brian.baker.bdb@gmail.com)
- Github: @baker-ling

## License

This application is distributed under the terms of [MIT License](./LICENSE).
