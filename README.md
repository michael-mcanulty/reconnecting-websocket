# Reconnecting WebSocket

[![Build Status](https://travis-ci.org/pladaria/reconnecting-websocket.svg?branch=master)](https://travis-ci.org/michael-mcanulty/reconnecting-websocket.svg?branch=master)

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
import {default as ReconnectingWebSocket, IReconOptions} from "./ReconnectingWebSocket/ReconnectingWebSocket";

let socket: ReconnectingWebSocket = new ReconnectingWebSocket('ws://my.site.com', this._reconOptions);

rws.addEventListener('open', () => {
    rws.send('hello!');
});
```

### Options

#### Available options

```typescript
type Options = {
    WebSocket?: any; // WebSocket constructor, if none provided, defaults to global WebSocket
    maxReconnectionDelay?: number; // max delay in ms between reconnections
    minReconnectionDelay?: number; // min delay in ms between reconnections
    reconnectionDelayGrowFactor?: number; // how fast the reconnection delay grows
    minUptime?: number; // min time in ms do consider connection as stable
    connectionTimeout?: number; // retry connect if not connected after this time, in ms
    maxRetries?: number; // maximum number of retries
    debug?: boolean; // enables debug output
};
```

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
