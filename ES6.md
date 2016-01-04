#Introduction

This document will go over some of the patterns thart you can use when enabling ES6 support


## Sandbox

There are 2 great ways to familiarize yourself with ES6.

- Babel
- JSBin



### Babel

[Babel](https://babeljs.io/repl/) is a great way to explore the new ES6 syntax.


### JSBin

Open up [JSBin](https://jsbin.com) and insert the following HTML.

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
 <script src="https://fb.me/react-0.14.0.min.js"></script>
  <script src="https://fb.me/react-dom-0.14.0.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/3.0.4/redux.min.js"></script>
</head>
<body>
  <div id='root'></div>
</body>
</html>
```

Enter the Javascript tab and select ```ES6/Babel``` and write the simplest component possible

```
const MyApp = () => {
	return (	
	  <div>Hello World !</div> 
	)
};

ReactDOM.render(<MyApp/>,document.getElementById("root"));
```

This is called a stateless function component. We can make it even more simpler by doing the following:

- Implicit return (no rreturn statement needed)
- Destructuring the props object

We can externalize the text and pass it on as a property.

```
const MyApp = ( props ) => (
  <div>{props.text}</div> 
);
```

or even simpler:

```
const MyApp = ( { text} ) => (
  <div>{text}</div> 
);

ReactDOM.render(<MyApp text="Hello World!"/>,document.getElementById("root"));
```

The ES6 syntax will create a function called myApp, and it will render whatever is in the body of the function

```
var MyApp = function MyApp() {
  return React.createElement(
    "div",
    null,
    "Hello World !"
  );
};
```

### More complex objects

If we want to create a React Component with actual methods we can do it like this :

```

import React, { Component, PropTypes } from 'react'

class Counter extends Component {
  
  	doSomething() {
  		// do something
	}

  	render() {
    	const { increment, incrementIfOdd, incrementAsync, decrement, counter } = this.props
    
	    return (
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
```

If you're using something like JSBin just remember you can get a hold of the Component import by doing

```
const {Component} = React;
// equals the following : 
//    var _React = React;
//    var Component = _React.Component;
```
## Patterns

### Importing constants

Given the following file

```
// /constants/ActionTypes
export const ADD_TO_CART = 'ADD_TO_CART'
export const CHECKOUT_REQUEST = 'CHECKOUT_REQUEST'
export const CHECKOUT_SUCCESS = 'CHECKOUT_SUCCESS'
export const CHECKOUT_FAILURE = 'CHECKOUT_FAILURE'
export const RECEIVE_PRODUCTS = 'RECEIVE_PRODUCTS'
```

You can import all these constants as types, and then refer to them like this :

```
import * as types from '../constants/ActionTypes'

export function addTodo(text) {
  return { type: types.ADD_TODO, text }
}
```


## ReactJS components


### Props

Imagine the following code :

```
class Counter extends Component {
  render() {
    
    const { increment, incrementIfOdd, incrementAsync, decrement, counter } = this.props
    
    return (
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
  }
}
```

As you can see we're referencing a lot of this.props.XXX in the component.

Instead of writing this.props.XXX all the time, we can reference the properties directly


```
const { increment, incrementIfOdd, incrementAsync, decrement, counter } = this.props
```

becomes


```
var _props = props;
var increment = _props.increment;
var incrementIfOdd = _props.incrementIfOdd;
var incrementAsync = _props.incrementAsync;
var decrement = _props.decrement;
var counter2 = _props.counter2;
```