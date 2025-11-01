# Global Loading State

A lightweight, event-driven global loading state manager for React applications. Perfect for managing loading states across multiple components without prop drilling.

## Features

- ✨ Simple and lightweight
- 🎣 React hooks API
- 🔌 Event-driven architecture
- 📦 TypeScript support
- 🚀 Zero dependencies
- ♿ Works with React 16.8+

## Installation

```bash
npm install global-loading-state
# or
yarn add global-loading-state
# or
pnpm add global-loading-state
```

## Quick Start

### Using the Hook

```jsx
import React from "react";
import { useGlobalLoading } from "global-loading-state";

const Button = () => {
  const isLoading = useGlobalLoading();

  return (
    <button disabled={isLoading}>
      {isLoading ? "Loading..." : "Click Me"}
    </button>
  );
};

export default Button;
```

### Controlling the Loading State

```jsx
import React from "react";
import { setGlobalLoading, startLoading, endLoading } from "global-loading-state";

const DataFetcher = () => {
  const fetchData = async () => {
    startLoading(); // or setGlobalLoading(true)
    try {
      await fetch("https://api.example.com/data");
    } finally {
      endLoading(); // or setGlobalLoading(false)
    }
  };

  return <button onClick={fetchData}>Fetch Data</button>;
};

export default DataFetcher;
```

## API Reference

| Function | Type | Description |
|----------|------|-------------|
| `useGlobalLoading()` | Hook | Returns the current global loading state (boolean) |
| `setGlobalLoading(state)` | Function | Set the global loading state to true or false |
| `startLoading()` | Function | Convenience function to set loading state to true |
| `endLoading()` | Function | Convenience function to set loading state to false |
| `globalLoader` | EventEmitter | Direct access to the event emitter |

## Advanced Usage

### Direct Event Emitter Access

```jsx
import { globalLoader } from "global-loading-state";

// Emit custom events
globalLoader.emit("changeLoading", true);
globalLoader.emit("changeLoading", false);

// Subscribe to events
const unsubscribe = globalLoader.subscribe("changeLoading", (isLoading) => {
  console.log("Loading state changed:", isLoading);
});

// Cleanup
unsubscribe();
```

### Multiple Loading States

```jsx
import { EventEmitter } from "global-loading-state";

const customLoader = new EventEmitter();

customLoader.emit("customEvent", "some-data");
customLoader.subscribe("customEvent", (data) => {
  console.log(data);
});
```

## License

MIT © [Mahmoud Bahaa](https://github.com/mahmoudbahaa755)
