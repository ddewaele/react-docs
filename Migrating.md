Migration guide - ES6


## Third party libraries

When needing to work with third party frameworks, everything should be installed via npm.

For example if jQeury is needed, you execute the following commmand:

```
npm install jquery --save
```

And then reference it in your conponents like this:

```
import React, { Component, PropTypes } from 'react';
import $ from 'jquery';

class BoardSelection extends Component {
....
}
```

## React components

```
var DetailPane = React.createClass({
```

becomes

```
class DetailPane extends Component {
```

## getInitialState

```
getInitialState: function() {
	return {selectedGpio: null};
}
```

becomes

```
constructor(props) {
	super(props);
	this.state = {selectedGpio: null};
	}
```  	

## this binding

Suppose you had this

```
     render(){
		<select id="lang" className="form-control" onChange={this.change} value={this.state.selectedBoard}>
			<option value="select">Select</option>
			...
		</select>
     }   

     change(event) {
		this.setState({selectedBoard: event.target.value});
     }

```

We need to keep in mind that ```this``` will not be bound to the React component in an ES6 class.

In order to make it work :

```
<select id="lang" className="form-control" onChange={this.change} value={this.state.selectedBoard}>
```
needs to become :

```
<select id="lang" className="form-control" onChange={this.change.bind(this)} value={this.state.selectedBoard}>
 ```


## CSS styles

Where before we would just reference a certain css style class like this :

```
 <div className="boardcontainer">
```

We can now do it like this :

```
<div className={s.boardcontainer}> 	
```

Providing we do the following on our component

```
import React, { Component, PropTypes } from 'react';
import s from './Board.scss';
import withStyles from '../../decorators/withStyles';

@withStyles(s)
class Board extends Component {
.....
}
```

## Images


When working with images, 
					 			<img src={require(this.state.board.imageUrl'./logo-small.png')}
				 			<img src={this.state.board.imageUrl}/>



## Exporting singletons

Sometimes the components you're exposing are singletons, and you can instantiate one single instance before exporting it. This way, clients don't need to intantiate your components, but they'll be able to import an object instance directly.

So instead of doing this:

```
export default RestApi;
```

You can now do this

```
export default new RestApi();
```

If you simply export the component, you'll get the ofllowing errors when executing methods on it :

```
Uncaught TypeError: _RestApi2.default.retrieveGpioDirection is not a functionretrieveGpioDirection @ Gpio.js?37ae:69proxiedMethod @ createPrototypeProxy.js?c130:44componentDidMount @ Gpio.js?37ae:48proxiedComponentDidMount @ createPrototypeProxy.js?c130:61assign.notifyAll @ CallbackQueue.js?bea8:65ON_DOM_READY_QUEUEING.close @ ReactReconcileTransaction.js?9178:81Mixin.closeAll @ Transaction.js?6dff:202Mixin.perform @ Transaction.js?6dff:149Mixin.perform @ Transaction.js?6dff:136assign.perform @ ReactUpdates.js?ce09:86flushBatchedUpdates @ ReactUpdates.js?ce09:147wrapper @ ReactPerf.js?ef93:66Mixin.closeAll @ Transaction.js?6dff:202Mixin.perform @ Transaction.js?6dff:149ReactDefaultBatchingStrategy.batchedUpdates @ ReactDefaultBatchingStrategy.js?ef70:62batchedUpdates @ ReactUpdates.js?ce09:94ReactEventListener.dispatchEvent @ ReactEventListener.js?2365:204
```

## React Bootstrap

Not really related to migrating to the react-quickstart project, but part of this migration also involved introducing [React Bootstrap] https://github.com/react-bootstrap/react-bootstrap
