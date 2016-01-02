# Introduction

Some stuff written down as I'm learning ReactJS

## Getting Started

I started reading the [https://facebook.github.io/react/docs/getting-started.html](Getting started guide).

Immediately you are confronted with lot of technologies / frameworks that can b daunting.

- CommonJS
- Browserify
- Webpack
- Babel

Also the code that you see 

```
// main.js
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
```

is something that won't run in a browser. So this was also very confusing. (you'll learn later that this code needs to be compiled into javascript that the browser understands).

The following stuff is also not very relevant for a getting started guide IMHO. Beginners will be very confused with this.

```
npm install --save react react-dom babelify babel-preset-react
browserify -t [ babelify --presets [ react ] ] main.js -o bundle.js
```

You can bootstrap the generated bundle.js like this in an html page, and it will work, but it's not very clear from the getting started page :

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
  </head>
  <body>
	<div id="example"></div>
	<script src="bundle.js"></script>
  </body>
</html>
```

The bundle.js contains a compiled version of the main.js, including all of the react dependencies.

Given the original main.js that looked like this :

```
// main.js
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);

```

In the ```bundle.js``` you will see this :

```
// main.js
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(React.createElement(
  'h1',
  null,
  'Hello, world!'
), document.getElementById('example'));
```


If you try to load the main.js as a javascript in your browser it won't work, as it contains invalid javascript (The React JSX syntax)


## The application skeleton

### Empty index.html

We'll start with the following index.html

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>React Tutorial</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.6.15/browser.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/marked/0.3.2/marked.min.js"></script>
  </head>
  <body>
  </body>
</html>

```


## Problems encountered

When attempting to load my main.js in an index.html like this:


```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>React Tutorial</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.14.0/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.6.15/browser.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/marked/0.3.2/marked.min.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/babel" src="scripts/main.js"></script>
  </body>
</html>

```


I got this:

```
Uncaught SyntaxError: Unexpected token <
```

Offcourse... it's babel. But when attempting to load my main.js using a ```<script type="text/babel" src="main.js"></script>``` from a local index.html I got this:

```
XMLHttpRequest cannot load file:///Users/ddewaele/Projects/ReactJS/sample1/main.js. Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, https, chrome-extension-resource.
```

No worries, I'll just start a webserver and load my index.html. But then I get this:

```
Uncaught ReferenceError: require is not defined
```

The solution, remove the require lines :
```
// main.js
// var React = require('react');
// var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
```


## Some issues

- Difficult to debug JSX files
- In case of javascript errors (ex: missing semi column), no feedback at all.


## React components

### Creating a component

```
var CommentBox = React.createClass({
  render: function() {
    return (
      <h1>Hello</h1>
    );
  }
});
```


## Some tips

### Binding this

Instead of doing this in your component 
```
<li onClick={this.props.onClick.bind(null,this.props.id)} style={{fontWeight: this.props.selected ? "bold" : "normal"}}>
``` 

you can do this :

```
  localHandleClick: function() {
    this.props.selectItem(this.props.id)
  }
```

and
```
<li onClick={this.localHandleClick} style={{fontWeight: this.props.selected ? "bold" : "normal"}}>
```

### setState

```setState``` is asynchronous and so trying to work with state directly after a setState call won't work.
A callback argument can be passed to setState , informing you when the state is available.


## Starter pack

I started looking at [the react starter kit](https://github.com/kriasoft/react-starter-kit). 

and https://github.com/banderson/generator-flux-react


## References

- [React Complementary Tools](https://github.com/facebook/react/wiki/Complementary-Tools)
- [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)



### Components and state

- [Best Practices for Component State in React.js](http://brewhouse.io/blog/2015/03/24/best-practices-for-component-state-in-reactjs.html)
- 