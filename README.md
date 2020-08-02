# Dollar store
Store data globally in your app. Generic library, no dependencies.

## Installation

```sh
npm install dollarstore
```

```js
import { createStore } from 'dollarstore'
```

## Usage

### Creating a store
```js
const initialState = {}
createStore(initialState)
```

### Getting store values

You can get a store value either from the `get` method, or by accessing the field directly from the state object.

```js
const { state, get } = createStore({ count: 0 })
get('count') // 0
state.count // 0
```

### Setting store values

You can set a store value either from the `set` method, or by directly setting the field on the state object.

```js
const { state, set } = createStore({ count: 0 })
state.count += 1 // 1
set('count', 5) // 5
```

### Listening for state changes to fields

You can subscribe to a field execute a callback any time that field changes using the `onChange` method.

```js
const { state, onChange } = createStore({ count: 0 })
onChange('count', newValue => {
    // do some stuff
});
state.count += 1;
```

#### Unsubsribing to state changes

The method `onChange` returns a function, that when invoked, will the unsubsribe callback from those change events.

```js
const { state, onChange } = createStore({ count: 0 })
const offChange = onChange('count', newValue => {
    // do some stuff
    offChange() // effectively a 'once'
});
state.count += 1;
```

### Listening for any state events

With the `on` method, there are four events that you can subscribe to for the store: `set`, `get`, `clear`, `reset`

```js
const { state, on } = createStore({ count: 0 })
on('set', (key, value) => {})
on('get', value => {})
on('clear', () => {})
on('reset', () => {})
```

#### Unsubscribing from state events

The `on` method returns a method that, when invoked, unsubsribes the callback from that event.

```js
const { state, on } = createStore({ count: 0 })
const offSet = on('set', (key, value) => {
    offSet() // effectively a 'once'
})
```

### Setting event listeners in bulk

With the `use` method, you can set an event listener for each of the store events: `set`, `get`, `clear`, `reset`

```js
const { use } = createStore({ count: 0 })
use({
    get: () => {},
    set: () => {},
    reset: () => {},
    clear: () => {}
})
```

### Clearing the store

Clearing the store empties it of all it's values. However, the keys are kept.

```js
const { state, clear } = createStore({ count: 0 })
state.count // 0
clear()
state.count // undefined
```

### Reseting the store

Reseting the store resets the state back to what it was initially created with.

```js
const { state, reset } = createStore({ count: 0 })
state.count += 1 // 1
reset()
state.count // 0
```
