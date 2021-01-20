# use-cloned-state


[![NPM](https://img.shields.io/npm/v/use-cloned-state.svg)](https://www.npmjs.com/package/use-cloned-state) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)


## What is this?

Ever needed to sync a state between two instances of a React app? Well, you and I have something in common, not everyone has ever needed to do shit like this!

Anyway, this is a simple hook that allows you to create a state/setter that will be immediatly cloned to a local/remote source via `BroadcastChannel` (local) or `Firebase` (remote), or any sync method you like!

When creating a hook you need to provide a source: an object with `onData` and `sendData`, but worry not! a source generator for `BroadcastChannel` and `Firebase` is provided with the library, who would have thought???

You can use a hook as `receiver`, as `sender` or as `both` (default) in order to limit a component to mimic another state, or for the synchronization to work both ways.
## Install

```bash
npm install --save use-cloned-state
```

## Usage

Local source, two end sync:
```tsx
import * as React from 'react'

import { useClonedState, localSource } from 'use-cloned-state'

const source = localSource('test')
const App = () => {
  const [value, setValue] = useClonedState(altSource, 1)
  return (
    <div onClick={() => setValue(value + 1)}{value}</div>
  )
}
export default App
```

Remote source, one direction sync:
```tsx
import * as React from 'react'

import { useClonedState, firebaseSource } from 'use-cloned-state'

const firebaseConfig = {
  apiKey: 'whatanapikey',
  authDomain: 'maronn.firebaseapp.com',
  databaseURL: 'https://maronn-default-rtdb.europe-west1.firebasedatabase.app',
  projectId: 'maronn',
  storageBucket: 'maronn.appspot.com',
  messagingSenderId: '100000000',
  appId: '1:123:456',
  measurementId: 'hoooge',
}

const source = firebaseSource(firebaseConfig, 'test')
const role = window.location.hash === '#receiver' ? 'receiver' : 'sender'
const App = () => {
  const [value, setValue] = useClonedState(altSource, 1, role)
  return (
    <div onClick={() => setValue(value + 1)}{value}</div>
  )
}
export default App
```


## License

MIT © [lucamattiazzi](https://github.com/lucamattiazzi)

---

This hook is created using [create-react-hook](https://github.com/hermanya/create-react-hook).
