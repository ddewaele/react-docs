## Some code snippets I use every now and then

## React Basic

### Stateless function component

```js
import React, { Component, PropTypes } from 'react'

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
export default Counter
```


Can also include logic

```js
import React, { Component, PropTypes } from 'react'

var TodoList = () => (

	<div>
	<div>TODO List</div>
	{[1,2,3,4].map(x => 
		<div>{x}</div>
	)}
	</div>
)

export default TodoList
```



### Actual React component.

```js
import React, { Component, PropTypes } from 'react'

class Counter extends Component {
  render() {
    
    const { increment, incrementIfOdd, incrementAsync, decrement, counter } = this.props
    
    return (
      <div>Hello222


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

      </div>
    )
  }
}

Counter.propTypes = {
  increment: PropTypes.func.isRequired,
  incrementIfOdd: PropTypes.func.isRequired,
  incrementAsync: PropTypes.func.isRequired,
  decrement: PropTypes.func.isRequired,
  counter: PropTypes.number.isRequired
}
```

### Text input

```js
import React, { Component, PropTypes } from 'react'

class TodoInput extends Component {

    constructor(props) {
        super(props);
        this.state = {text:"Enter something here...."};
    }

  handleSubmit(e) {
    const text = e.target.value.trim()
    if (e.which === 13) {
      console.log("Submitting " + this.state.text)
      this.setState({ text: "" })  
    }
  }

  handleChange(e) {
    this.setState({ text: e.target.value })
  }

  handleBlur(e) {
    if (!this.props.newTodo) {
      this.props.onSave(e.target.value)
    }
  }

render() {
    
    return (
    <div> 
        Add TODO : 
        <input type="text" 
            value={this.state.text} 
            onBlur={this.handleBlur.bind(this)}
            onChange={this.handleChange.bind(this)}
            onKeyDown={this.handleSubmit.bind(this)}/>
    </div>
    )
  }
}

export default TodoInput
```


## Redux

### Index

```js
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


### ConfigureStore

```js
import { createStore, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import reducer from '../reducers'

const createStoreWithMiddleware = applyMiddleware(
  thunk
)(createStore)

export default function configureStore(initialState) {
  const store = createStoreWithMiddleware(reducer, initialState)

  if (module.hot) {
    // Enable Webpack hot module replacement for reducers
    module.hot.accept('../reducers', () => {
      const nextReducer = require('../reducers')
      store.replaceReducer(nextReducer)
    })
  }

  return store
}
```


### Redux Connect

```js
import { bindActionCreators } from 'redux'
import { connect } from 'react-redux'
import Counter from '../components/Counter'
import * as CounterActions from '../actions/counter'

// Create a container component for the presentational counter component


// Which part of the Redux global state does our component want to receive as props?
function mapStateToProps(state) {

console.log("Found state " + state);

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


### Redux actions

You either return an object literal (with a type), or you include a function that does the dispatching.

```js
export const INCREMENT_COUNTER = 'INCREMENT_COUNTER'
export const DECREMENT_COUNTER = 'DECREMENT_COUNTER'

// export function increment() {
//   return {
//     type: INCREMENT_COUNTER
//   }
// }

export function increment() {
  return (dispatch) => {
    dispatch({
      type: INCREMENT_COUNTER
    });
  }
}

export function decrement() {
  return {
    type: DECREMENT_COUNTER
  }
}
```