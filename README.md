<div align="center" style="background: #5636D3; padding: 16px;">
  <img alt="GoFinances" src="https://imgur.com/QGM92ls.png" />
</div>

<p align="center">
  <a href="#rocket-about">About</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#page_facing_up-features-and-requirements">Features and requirements</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#package-used-technologies">Used technologies</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#computer-getting-started">Getting started</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
</p>

## :rocket: About

A [Node.js](https://nodejs.org) backend application for basic financial transactions management built as part of the **Rocketseat's** [Bootcamp GoStack](https://rocketseat.com.br/gostack), a 6 weeks long immersive Full Stack Javascript course.

## :page_facing_up: Features and requirements

### API Routes

- **`POST /transactions`**: This route receives `title`, `value`, `type`, and `category` inside its request body, being `type` the transaction's type (`income` for receivable transactions and `outcome` for payable transactions). When a new transaction is created, it should be stored in the database, with the `id`, `title`, `value`, `type`, `category_id`, `created_at`, `updated_at` fields. You should also store the `category` in another table and store its *id* in the `category_id` field. Make sure to check if the received category doesn't exist in the database before creating a new one.

```json
{
  "id": "uuid",
  "title": "Salário",
  "value": 3000,
  "type": "income",
  "category": "Alimentação"
}
```

- **`GET /transactions`**: This route should return a list with all transactions that are stored in the database, as well as the sum of the `income` and `outcome` values and the remaining balance. This route should return an object in the following format:

```json
{
  "transactions": [
    {
      "id": "uuid",
      "title": "Salário",
      "value": 4000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Salary",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Freela",
      "value": 2000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Pagamento da fatura",
      "value": 4000,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Cadeira Gamer",
      "value": 1200,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Recreation",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    }
  ],
  "balance": {
    "income": 6000,
    "outcome": 5200,
    "total": 800
  }
}
```

- **`DELETE /transactions/:id`**: This route should delete a transaction with the `id` within the route params;

* **`POST /transactions/import`**: This route should allow importing a `.csv` file with the necessary data to create a transaction (`id`, `title`, `value`, `type`, `category`), where each line of the file should be a new database registry, then the created `transactions` should be returned. Refer to the [example file](./assets/file.csv) to the create your own `.csv` file.

### Tests specifications

Your application should pass on all the following tests:

Para esse desafio, temos os seguintes testes:

- **`should be able to create a new transaction`**: To pass through this test, your application should make sure that a transaction is being created and then return a JSON with the created data.

* **`should create tags when inserting new transactions`**: To pass through this test, your application should make sure that when creating a transaction with a category that doesn't exist in the database it should be created and the `id` of this category should be passed to the category_id of the current transaction.

- **`should not create tags when they already exists`**: To pass through this test, your application should make sure that when creating a transaction with a category that already exists in the database, the `id` of this category should be passed to the category_id of the current transaction. Categories with the same `title` "should not pass" 🧙.

* **`should be able to list the transactions`**: To pass through the test, your application should return an object array with all the transactions as well as the sum of `income` and `outcome` transactions and the balance of them.

- **`should not be able to create outcome transaction without a valid balance`**: To pass through this test, your application shouldn't allow that transactions with the type `outcome` overcome the balance (total of the `income` - `outcome`), returning an HTTP response with the status code 400 and an error message with the following format: `{ error: string }`.

* **`should be able to delete a transaction`**: To pass through the test, your application should delete a transaction and return an empty response with the status code 204.

- **`should be able to import transactions`**: To pass through the test, your application should allow that a .csv file to be imported with the following [sample file](./assets/file.csv). With the file imported, all the transactions should be created in the database and all the transactions returned in an array of transactions.

## :package: Used technologies

This application was built with [express](https://expressjs.com) in a [Node.js](https://nodejs.org) server:

* **Express**
  * "Fast, unopinionated, minimalist web framework for Node.js".
* **Typescript**
  * A language that adds typing and other good ES5/ES6 features to JavaScript. It helps us A LOT empowering the **VS Code's Intellisense** which guides us through methods arguments and variable methods and what they expect to receive. It surely has its learning curve but it totally worths it!
* **TypeORM**
  * An ORM that can run in Node.js, Browsers, React Native and so on...
* **Multer**
  * Multer is a node.js middleware for handling multipart/form-data, which is primarily used for uploading files
* **ts-node-dev**
  * "It restarts target node process when any of required files changes (as standard node-dev) but shares Typescript compilation process between restarts. This significantly increases speed of restarting comparing to node-dev -r ts-node/register ..., nodemon -x ts-node ... variations because there is no need to instantiate ts-node compilation each time."
* **csv-parse**
  * A CSV converter with **stream.Transform API** implemented.

## :computer: Getting started

Clone this repository and then run `yarn` in the root project's folder to install all needed dependencies and get ready to use this app. You should also have a running **Postgres Server** with your database (maybe will bee containerized).

To start the server, simple run `yarn dev:server` and you're done!

---

Made with 💜 by [Pedro Fagundes](https://github.com/pedrofagundes)
