# Routes Loader

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This module dynamically loads and sets up routes for the application based on the directory structure and file names.</p>
  <img src="flowchart.png" alt="Flowchart of Routes Loader"/>
</tldr>

<procedure title="To dynamically load and set up routes:" id="procedure-id">
   <step>Scan the directory for route files.</step>
   <step>Determine the authentication type for each route.</step>
   <step>Load the route modules and apply the appropriate middleware.</step>
   <step>Register the routes with the Express router.</step>
   <p>Congratulations! You have successfully set up dynamic route loading.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a>!</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the directory structure and file naming conventions are consistent.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the route loading process.

## Functions

### `loadRoutes`

This function recursively loads routes from the specified directory and registers them with the Express router.

#### Parameters

- `dir`: The directory to scan for route files.
- `basePath`: The base path for the routes.
- `authType`: The default authentication type for the routes.

#### Example Usage

```typescript
await loadRoutes(__dirname + "/routes", "", "api");