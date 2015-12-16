## Introduction

Some stuff written down as I'm learning ReactJS

### Sample app

In the [https://facebook.github.io/react/docs/getting-started.html](Getting started guide), after creating your bundle.js like so:

```
npm install --save react react-dom babelify babel-preset-react
browserify -t [ babelify --presets [ react ] ] main.js -o bundle.js
```

You can bootstrap it like this:

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


The bundle.js contains a compiled version of the main.js

The original main.js :

```
// main.js
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);

```

In bundle.js :

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

Now, if you try to load the main.js it won't work, as it contains invalid javascript


Or, when not using a bundle, you can do this:


## Problems encountered

When attempting to load my main.js using a ```<script type="text/javascript" src="main.js"></script>``` from a local index.html I got this:

```
Uncaught SyntaxError: Unexpected token <
```

Offcourse... it's babel. But when attempting to load my main.js using a ```<script type="text/babel" src="main.js"></script>``` from a local index.html I got this:

```
XMLHttpRequest cannot load file:///Users/ddewaele/Projects/ReactJS/sample1/main.js. Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, https, chrome-extension-resource.
```

No worries, I'll just start a webserver and load my index.html


```
Uncaught ReferenceError: require is not defined
```



