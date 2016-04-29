# feathers-action

#### *work in progress*

never write another CRUD redux action!

this module helps you use [`feathers`](http://feathersjs.com), [`redux`](http://redux.js.org), and [`tcomb`](https://www.npmjs.com/package/tcomb).

## install

with [npm](https://www.npmjs.org):

```shell
npm install --save feathers-action
```

## usage

```js
// client.js
const feathers = require('feathers-client')
const fetch = require('isomorphic-fetch')

const client = feathers()
  .configure(feathers.fetch(fetch))

const t = require('tcomb')

const Thing = t.struct({
  id: t.Number,
  name: t.String,
  description: t.String
}, 'Thing')

const Things = t.List(Thing, 'Things')

const actions = require('feathers-action').createActionCreators(client, Things)
const reducer = require('feathers-action').createReducer(Things)

const redux = require('redux')
const thunk = require('redux-thunk')

const createStoreWithMiddleware = redux.applyMiddleware(thunk)(redux.createStore)

function createStore (initialState) {
  return createStoreWithMiddlware(reducer, initialState)
}
```

## ecosystem

`feathers-action` is composed of small modules for each part. if you have other opinions on how to join them together, feel free to do as you please! :)

- [feathers-client](https://www.npmjs.com/package/feathers-client)
- [feathers-action-types](https://www.npmjs.com/package/feathers-action-types)
- [feathers-action-reducer](https://www.npmjs.com/package/feathers-action-reducer)
- [feathers-action-creators](https://www.npmjs.com/package/feathers-action-creators)
- [tcomb](https://www.npmjs.com/package/tcomb)
