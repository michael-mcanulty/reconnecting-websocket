[![Build Status](https://travis-ci.org/michael-mcanulty/reconnecting-websocket.svg?branch=master)](michael-mcanulty/reconnecting-websocket)

# Reconnecting WebSocket

WebSocket that will automatically reconnect if the connection is closed.

## Features

*   WebSocket API compatible (same interface, Level0 and Level2 event model)
*   Fully configurable
*   Multiplatform (Web, ServiceWorkers, Node.js, React Native)
*   Dependency free (does not depend on Window, DOM or any EventEmitter library)
*   Handle connection timeouts
*   Full test coverage
*   Debug mode
*   AMD build available (see dist folder)
*   Allows changing server URL between reconnections

## Use

```
Add the reconnecting-websocket.ts file directly to your project.
```

### Simple usage

```typescript
import * as Html5WebSocket from 'html5-websocket'
import {default as ReconnectingWebSocket, IReconOptions} from "./ReconnectingWebSocket/ReconnectingWebSocket";

let opts: IReconOptions = <IReconOptions>{};
opts.connectionTimeout = 4E3;
opts.debug = false;
opts.maxReconnectionDelay = 10E3;
opts.maxRetries = Infinity;
opts.minReconnectionDelay = 4E3;

let socket: ReconnectingWebSocket = new ReconnectingWebSocket('ws://my.site.com', opts);
```

### Options

#### Default values

```javascript
WebSocket: undefined,
maxReconnectionDelay: 10000,
minReconnectionDelay: 1000 + Math.random() * 4000,
minUptime: 5000,
reconnectionDelayGrowFactor: 1.3,
connectionTimeout: 4000,
maxRetries: Infinity,
debug: false,
```

## API

### Methods

```typescript
constructor(url: UrlProvider, protocols?: string | string[], options?: Options)

close(code?: number, reason?: string)
reconnect(code?: number, reason?: string)

send(data: string | ArrayBuffer | Blob | ArrayBufferView)

addEventListener(type: 'open' | 'close' | 'message' | 'error', listener: EventListener)
removeEventListener(type:  'open' | 'close' | 'message' | 'error', listener: EventListener)
```

### Attributes

[More info](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)

```typescript
binaryType: string;
bufferedAmount: number;
extensions: string;
onclose: EventListener;
onerror: EventListener;
onmessage: EventListener;
onopen: EventListener;
protocol: string;
readyState: number;
url: string;
retryCount: number;
```

### Constants

```text
CONNECTING 0 The connection is not yet open.
OPEN       1 The connection is open and ready to communicate.
CLOSING    2 The connection is in the process of closing.
CLOSED     3 The connection is closed or couldn't be opened.
```

## Contributing

[Read here](./CONTRIBUTING.md)

## License

MIT
