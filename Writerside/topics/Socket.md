# WebSocket Implementation

<primary-label ref="stable"/>
<secondary-label ref="beta"/>

<tldr>
  <p>This module handles WebSocket connections, including authentication, event handling, and error management for table-related actions.</p>
  <img src="flowchart.png" alt="Flowchart of WebSocket Implementation"/>
</tldr>

<procedure title="To handle WebSocket connections and events:" id="procedure-id">
   <step>Initialize the WebSocket server and configure connection settings.</step>
   <step>Authenticate incoming WebSocket connections using JWT tokens.</step>
   <step>Listen for various table-related events and handle them accordingly.</step>
   <step>Manage errors and ensure they are safely communicated to the client.</step>
   <p>Congratulations! You have successfully handled WebSocket connections and events.</p>
   <p>Need more help? Checkout the <a href="Installation-guide.md">Installation-guide</a>!</p>
</procedure>

While not strictly necessary, the following things are highly recommended:

* Ensure that the JWT tokens are correctly validated before allowing WebSocket connections.
* Implement proper error handling and logging mechanisms to capture and address any issues that may arise during the WebSocket communication process.

## WebSocket Initialization

The WebSocket server is initialized and configured with the necessary settings, including CORS and connection state recovery.

```typescript
import { Server } from "socket.io";
import { WebServer } from "@/index";
import { CorsConfig } from "@/config";

const io = new Server(WebServer, {
  cors: CorsConfig,
  path: "/api/JackBlack.socket",
  connectionStateRecovery: {
    skipMiddlewares: false,
  },
});

export { io };