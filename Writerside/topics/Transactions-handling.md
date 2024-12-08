# Transaction Handling

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This module handles transactions, including generating signatures, sending payloads to webhooks, and updating user balances.</p>
  <img src="flowchart.png" alt="Flowchart of Transaction Handling"/>
</tldr>

<procedure title="To handle a transaction:" id="procedure-id">
   <step>Generate a timestamp for the transaction.</step>
   <step>Prepare the payload with user ID and timestamp.</step>
   <step>Generate a signature for the payload using the secret key.</step>
   <step>Send the payload to the webhook URL via a POST request.</step>
   <step>If the transaction is not a balance check, update the user's balance via socket communication.</step>
   <p>Congratulations! You have successfully handled a transaction.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a>!</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the webhook URL and secret key are correctly configured.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the transaction process.

## Functions

### `genSignature`

Generates a signature for the payload using the secret key.

#### Parameters {id="parameters_1"}

- `payload`: The payload to be signed.
- `secret`: The secret key used to generate the signature.
- `timestamp`: The timestamp of the transaction.

#### Returns {id="returns_1"}

- A string representing the generated signature.

### `getTableSocket`

Retrieves the socket for a specific table and user.

#### Parameters {id="parameters_2"}

- `tableId`: The ID of the table.
- `userId`: The ID of the user.

#### Returns {id="returns_2"}

- The socket associated with the specified table and user.

### `signedFetch`

Fetches the player data from the database and sends the payload to the webhook URL.

#### Parameters

- `payload`: The payload to be sent.
- `userId`: The ID of the user.

#### Returns

- The response from the webhook.

## Example Usage

```typescript
const payload = {
  action: "bet",
  amount: 100,
  tableId: "table1",
  userId: "user:123",
};

const webhook_secret = "your_secret";
const webhook_url = "https://your-webhook-url.com";

const timestamp = Date.now().toString();
payload.timestamp = timestamp;
payload.userId = payload.userId.split(":")[1];

const signature = genSignature({
  payload: JSON.stringify(payload),
  secret: webhook_secret,
  timestamp,
});

const resp = await fetch(webhook_url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "JackBlack-Signature": signature,
  },
  body: JSON.stringify(payload),
});

if (payload.action !== "balance") {
  const tableId = payload.tableId as string;
  const userSocket = getTableSocket(tableId, payload.userId);
  const json = (await resp.json()) as { balance: number };
  userSocket.emit("balanceUpdate", json.balance);
}