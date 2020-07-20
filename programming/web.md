# websockets

We use websocket as an Inter program or module communication protocol. I develop a custom protocol over Websocket that implement this 2 Patterns 

* Request / Response Pattern
* Publish / Subscribe Pattern 

We can response to almost any problems in a effective way with a combination of this 2 patterns: 

* Synchronized calls
* Notifications by Events 

I start developing the protocol to communicate local Webs or \(mobile apps\) to a c\# Engine as the User Interface for Shine Product \([see more](shine.md)\).

* **nexjs - websocket** is used in frontend/Backend apps
* **nexcs - websocket** is used in local c\# application controlled by mobile, desktop or web applications.

## Nexjs - Websocket

### the idea

Separate the Function \(Operation\) from the call Protocol \(Rest API, Websocket, Pure TCP IP,  ...\). In this implementation we only use websocket but with 2 different protocols: Request/Response and Publish/Subscribe.  The implementation is in typescript with decorators. 

* Only Implements the server
* automatic client generation \(ts or c\#\)

```typescript
// ----------------------------------------------------------------------------
// Operations
class AContract {

  @Hub({ service: 'aContract', ...}) // Publish/Subscribe Protocol over websocket
  onUpdate = new HubEvent();         // Emitter custom class - only to unificate event system

  @Rest({ service: 'aContract',...}) // Request/Response Protocol over websocket
  methodA(): Promise<void>{
    // anything                      // Can return anything
  }  
}

// ----------------------------------------------------------------------------
// main.ts
const wss = new WSServer<User, Token>();  // create Websocket protocols
wss.register(new AContract ());           // register class 
wss.init(new SocketIOServer(ioServer));   // initialize with a socket.io server

// ----------------------------------------------------------------------------
// in command line (create api client)
npm install @nexjs/cli -g
nexjs ts ws up-client -s ./[server-folder] -o ./[client-folder]/[api-folder]

// ----------------------------------------------------------------------------
// in client
const wsapi = new WSApi<User, Token>(new SocketIOClient()); // create client

// [Publish/Subscribe] protocol
// 1. register event Handler
wsapi.aContract.onUpdate.on(() =>
  console.log(`onUpdate`) // 
);
// 2. Subscribe to event
await wsapi.baseContract.onUpdate.sub();

// [Request/Response]  protocol 
await wsapi.baseContract.methodA();

//That all !!! 
```

### Server

{% embed url="https://github.com/Juancoll/nexjs-ws.dev-project.server" %}

### Client

{% embed url="https://github.com/Juancoll/nexjs-ws.dev-project.client" %}

## Nexcs - Websocket \(in process\)

### Overview

### Server

### Client



