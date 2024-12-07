# Transactions API

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This API endpoint handles transaction-related operations. It allows users to retrieve and manage transactions.</p>
  <img src="transactions.png" alt="Flowchart of Transactions API"/>
</tldr>

<procedure title="To manage transactions:" id="procedure-id-transactions">
   <step>Send a GET request to the endpoint to retrieve transactions.</step>
   <step>Send a POST request to the endpoint to create a new transaction.</step>
   <step>Send a PUT request to the endpoint to update an existing transaction.</step>
   <step>Send a DELETE request to the endpoint to delete a transaction.</step>
   <p>Congratulations! You have successfully managed transactions.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a> !</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the database schema and models are correctly defined to support the queries used in this endpoint.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the execution of the endpoint.

## Endpoint

`GET /transactions`
`POST /transactions`
`PUT /transactions/:id`
`DELETE /transactions/:id`

## Sequence and Flow

1. **Import Dependencies**:
- The necessary modules and utilities are imported, including `express`, `db`, `RouteError`, and `TransactionSchema`.

1. **Router Initialization**:
- An Express router is initialized using `express.Router()`.

1. **Define Route Handlers**:
- The route handlers for `GET`, `POST`, `PUT`, and `DELETE` requests are defined. These handlers perform the following steps:

### GET /transactions {id="get-transactions_1"}

1. **Retrieve Transactions**:
- The database is queried to retrieve all transactions.

1. **Send Response**:
- A JSON response is sent back to the client, containing the list of transactions.

### POST /transactions

1. **Parse Request Body**:
- The request body is parsed and validated using `TransactionSchema`.

1. **Create Transaction**:
- A new transaction is created in the database.

1. **Send Response**:
- A JSON response is sent back to the client, containing the created transaction.

### PUT /transactions/:id

1. **Parse Request Parameters and Body**:
- The `id` parameter from the request is parsed and validated using `TransactionSchema`.
- The request body is parsed and validated using `TransactionSchema`.

1. **Update Transaction**:
- The existing transaction is updated in the database.

1. **Send Response**:
- A JSON response is sent back to the client, containing the updated transaction.

### DELETE /transactions/:id

1. **Parse Request Parameters**:
- The `id` parameter from the request is parsed and validated using `TransactionSchema`.

1. **Delete Transaction**:
- The transaction is deleted from the database.

1. **Send Response**:
- A JSON response is sent back to the client, confirming the deletion.

1. **Error Handling**:
- Any errors that occur during the process are caught and passed to the next middleware for handling.

<img src="sequence.png" alt="Sequence Diagram of Transactions API"/>

## Example Requests

### GET /transactions

```http
GET /transactions