# Bill Queues and Workers

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This module sets up and manages Bill queues and workers for billing and currency operations.</p>
  <img src="flowchart.png" alt="Flowchart of Bill Queues and Workers"/>
</tldr>

<procedure title="To set up and manage Bill queues and workers:" id="procedure-id">
   <step>Initialize the Bill queues for billing and currency operations.</step>
   <step>Define the processing logic for each worker.</step>
   <step>Handle the completion and failure events for each worker.</step>
   <p>Congratulations! You have successfully set up and managed Bill queues and workers.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a>!</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the Redis server is correctly configured and running.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the execution of the workers.

## Queues

### `BillingQueue`

This queue handles billing-related tasks.

### `CurrencyQueue`

This queue handles currency-related tasks.

## Workers

### `BillingWorker`

This worker processes tasks from the `BillingQueue`.

### `CurrencyWorker`

This worker processes tasks from the `CurrencyQueue`.

## Interfaces

### `OERResponse`

Represents the response from the Open Exchange Rates API.

#### Properties

- `disclaimer`: A disclaimer message.
- `license`: The license information.
- `timestamp`: The timestamp of the rates.
- `base`: The base currency (always "USD").
- `rates`: The exchange rates.

## Example Usage

```typescript
import { BillingQueue, CurrencyQueue, BillingWorker, CurrencyWorker } from './bull';

// Add a job to the BillingQueue
BillingQueue.add({ userId: '123', amount: 100 });

// Add a job to the CurrencyQueue
CurrencyQueue.add({ base: 'USD', target: 'EUR' });