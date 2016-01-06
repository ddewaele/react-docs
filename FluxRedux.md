# Flux : Redux

## Getting started

### principles

- state is represented as a single javascript object
- all mutations to the state are explicit
- state is immutable. to change the state, an action needs to be dispatched
- reducer functions : pure functions, no side-effects
- reducer functions : takes existing state + action as input, and returns a new state as output


### Define your actions

What actions are going to be taking place in your application.

## Steps to write your redux app 

### Create the container component

Here's some boilerplate code to create a container component that wraps a presentation component

```js
// containers/App.js

import { bindActionCreators } from 'redux'
import { connect } from 'react-redux'
import Counter from '../components/Counter'
import * as CounterActions from '../actions/counter'

// Which part of the Redux global state does our component want to receive as props?
function mapStateToProps(state) {
  return {
    counter: state.counter
  }
}

// Which action creators does it want to receive by props?
function mapDispatchToProps(dispatch) {
  return bindActionCreators(CounterActions, dispatch)
}

export default connect(mapStateToProps, mapDispatchToProps)(Counter)
```

The connect method returns a ReactJS component that we can embed in our page.

In this case it wraps a simple counter component

```
var Counter = ({ increment, incrementIfOdd, incrementAsync, decrement, counter }) => (
  <p>
    Clicked: {counter} times
    {' '}
    <button onClick={increment}>+</button>
    {' '}
    <button onClick={decrement}>-</button>
    {' '}
    <button onClick={incrementIfOdd}>Increment if odd</button>
    {' '}
    <button onClick={() => incrementAsync()}>Increment async</button>
  </p>
)
```

The connect component does 2 things

- ensure that the counter component receives the state that it is interested in (in this case ```state.counter```)
- automatically binds ActionCreators to the component (increment, incrementIfOdd, incrementAsync, decrement, counter)


The component returned by connect is the one we'll be rendering.

```
import React from 'react'
import { render } from 'react-dom'
import { Provider } from 'react-redux'
import App from './containers/App'
import configureStore from './store/configureStore'

const store = configureStore()

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

Notice how this component is wrapped in a ```provider``` component.

