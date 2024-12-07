# Player Profile API

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This API endpoint retrieves the profile and statistics of a player based on their ID. The endpoint ensures that the requesting user is authorized to access the player's information.</p>
  <img src="flowchart.png" alt="Flowchart of Player Profile API"/>
</tldr>

<procedure title="To retrieve player profile and statistics:" id="procedure-id">
   <step>Send a GET request to the endpoint with the player's ID as a parameter.</step>
   <step>The server will verify the player's existence and authorization.</step>
   <step>If the player is found and authorized, the server will retrieve the player's transaction statistics.</step>
   <step>The statistics are processed and converted to USD.</step>
   <step>The server sends a JSON response containing the player's profile information and statistics.</step>
   <p>Congratulations! You have successfully retrieved the player's profile and statistics.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a> !</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the database schema and models are correctly defined to support the queries used in this endpoint.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the execution of the endpoint.

## Endpoint

`GET /:id`

## Sequence and Flow

1. **Import Dependencies**:
  - The necessary modules and utilities are imported, including `express`, `db`, `RouteError`, `toUSD`, and `ProfileSchema`.

2. **Router Initialization**:
  - An Express router is initialized using `express.Router()`.

3. **Define Route Handler**:
  - The route handler for `GET /:id` is defined. This handler performs the following steps:

4. **Parse Request Parameters**:
  - The `id` parameter from the request is parsed and validated using `ProfileSchema`.

5. **Verify Player Existence and Authorization**:
  - The database is queried to find the player with the specified `id` and ensure that the requesting user is authorized to access the player's information. The authorization check includes verifying if the player belongs to the requesting user or if the player belongs to an aggregator associated with the requesting user.

6. **Handle Player Not Found**:
  - If the player is not found, a `RouteError` with a 404 status code is thrown.

7. **Retrieve Player Statistics**:
  - The player's transaction statistics are retrieved using the `groupBy` method on the `db.transaction` model. The statistics include the count, sum, and average of the transaction amounts for "BET" and "WIN" types, grouped by currency.

8. **Process Statistics**:
  - The retrieved statistics are processed and converted to USD using the `toUSD` utility function. The statistics are then rounded to two decimal places.

9. **Send Response**:
  - A JSON response is sent back to the client, containing the player's profile information and statistics.

10. **Error Handling**:
  - Any errors that occur during the process are caught and passed to the next middleware for handling.

<img src="sequence.png" alt="Sequence Diagram of Player Profile API"/>



## Error Handling in Player Profile API

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This document explains the error handling mechanisms implemented in the Player Profile API endpoint.</p>
</tldr>

<procedure title="Error Handling Steps:" id="procedure-id_1">
   <step>Parse the request parameters using `ProfileSchema`.</step>
   <step>Verify the player's existence and authorization.</step>
   <step>If the player is not found, throw a `RouteError` with a 404 status code.</step>
   <step>Retrieve and process the player's transaction statistics.</step>
   <step>Send a JSON response containing the player's profile information and statistics.</step>
   <step>Catch any errors that occur during the process and pass them to the next middleware for handling.</step>
   <p>Congratulations! You have successfully implemented error handling in the Player Profile API.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a> !</p>
</procedure>

## Error Handling Mechanisms

1. **Parse Request Parameters**:
   - The `id` parameter from the request is parsed and validated using `ProfileSchema`.
   - If the parameter is invalid, an error is thrown and caught by the `catch` block.

2. **Verify Player Existence and Authorization**:
   - The database is queried to find the player with the specified `id` and ensure that the requesting user is authorized to access the player's information.
   - If the player is not found, a `RouteError` with a 404 status code is thrown.

3. **Retrieve and Process Statistics**:
   - The player's transaction statistics are retrieved using the `groupBy` method on the `db.transaction` model.
   - If any error occurs during this process, it is caught by the `catch` block.

4. **Send Response**:
   - A JSON response is sent back to the client, containing the player's profile information and statistics.
   - If any error occurs while sending the response, it is caught by the `catch` block.

5. **Catch and Log Errors**:
   - Any errors that occur during the process are caught by the `catch` block.
   - The error is logged using `console.error`.
   - The error is passed to the next middleware for handling using `next(error)`.

## Example Code

```typescript
import express from "express";
import db from "@/lib/db";

import { RouteError } from "@/lib/routes-loader";
import { toUSD } from "@/lib/utils/currency";
import { ProfileSchema } from "@/schemas/bo/management/players";

const router = express.Router();

router.get("/:id", async (req, res, next) => {
  try {
    const { id } = ProfileSchema.parse(req.params);

    // Verify player existence and authorization
    const player = await db.player.findFirst({
      where: {
        id,
        OR: [
          { userId: req.bo_user.sub },
          { user: { aggregatorId: req.bo_user.sub } },
        ],
      },
    });

    if (!player) throw new RouteError("not_found", 404);

    // use groupBy to get stats
    const plainStats = await db.transaction.groupBy({
      by: ["type", "currency"],
      where: {
        playerId: id,
        type: {
          in: ["BET", "WIN"],
        },
      },
      _sum: {
        amount: true,
      },
      _count: {
        id: true,
      },
      _avg: {
        amount: true,
      },
    });

    const stats = plainStats.reduce<
      Record<string, { count: number; amount: number; avg: number }>
    >(
      (acc, stat) => {
        const { type, currency, _sum, _count, _avg } = stat;

        acc[type].count += _count.id;
        acc[type].amount += toUSD(_sum.amount, currency);
        acc[type].avg += toUSD(_avg.amount, currency);

        acc[type].amount = Math.round(acc[type].amount) / 100;
        acc[type].avg = Math.round(acc[type].avg) / 100;

        return acc;
      },
      {
        BET: { count: 0, amount: 0, avg: 0 },
        WIN: { count: 0, amount: 0, avg: 0 },
      }
    );

    res.json({
      success: true,
      player: {
        ...player,
        stats,
      },
    });
  } catch (error) {
    console.error(error);
    next(error);
  }
});

export default router;