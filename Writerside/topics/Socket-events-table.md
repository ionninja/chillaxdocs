# Socket Events Table

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This module handles socket events related to table actions, such as insuring and performing player actions.</p>
  <img src="flowchart.png" alt="Flowchart of Table Socket Events"/>
</tldr>

<procedure title="To handle table socket events:" id="procedure-id">
   <step>Listen for the `table:insure` event and handle player insurance actions.</step>
   <step>Listen for the `table:action` event and handle player actions such as hit, stand, double, and split.</step>
   <p>Congratulations! You have successfully handled table socket events.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a>!</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the table and player data are correctly validated before processing the events.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the event handling process.

## Socket Events

### `table:insure`

Handles player insurance actions.

#### Parameters

- `data`: An object containing the table ID and insurance decision.
- `cb`: A callback function to send the response back to the client.

#### Example Usage

```typescript
socket.on("table:insure", async (data, cb) => {
  try {
    const { tableId, insure } = data;
    console.log("table:insure");

    const table = tables.find((table) => table.tableId === tableId);
    if (!table) throw new SocketError("game_not_found");

    const { balance } = await table.playerInsure(session.sub, insure);

    cb({ success: true, balance });
  } catch (err) {
    console.log(err);
    next(err, socket);
  }
});