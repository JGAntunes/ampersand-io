ampersand-io
============

Provides a [socket.io](http://socket.io) wrapper to be used with ampersand modules. Developed mainly to be used with [ampersand-io-model](https://github.com/sinfo/ampersand-io-model) and [ampersand-io-collection](https://github.com/sinfo/ampersand-io-collection)


## Install

```
npm install ampersand-io
```

## API Reference

### extend `AmpersandIO.extend([attributes])`

Supports the normal extend behavior (through usage of [ampersand-class-extend](https://github.com/ampersandjs/ampersand-class-extend))

### socket `IO.socket`

Override this property to specify the socket that will be used when a new object reference is created. Useful for when you have a pre-existing socket connection that you would like to use.

```javascript
var io = require('socket.io-client');
var IO = AmpersandIO.extend({
    socket: io()
});
```

### events `IO.events`

Overridable property containing a key-value reference to the events to be used by the socket conection. Useful for usage with the `listeners` property and methods, as well as with the `emit` emit.

```javascript
events: {
  eventOne: 'my-awesome-event',
  eventTwo: 'my-super-awesome-event'
}
```

It also supports the usage of arrays of different events tied to a single key

```javascript
events: {
  eventArray: ['this-event', 'other-event']
}
```

### listeners `IO.listeners`

Overridable property containing a set of listeners to be used by the socket connection. The key may be an entirely unreferenced event or one of properties from the `events` property object. The `fn` property contains the callback function to be called when the event is fired. The `active` option is a Boolean that, if set to true, will set this listener to be initialized upon construction.

```javascript
events:{
  myEvent: 'thisEvent',
  arrayOfEvents: ['event1', 'event2']
}

listeners: {
	myEvent: {
		fn: function(data, cb){
			console.log('This is an event callback');
		}
	},
	arrayOfEvents: {
		fn: function(data, cb){
			console.log('This callback will be called when all the events of arrayOfEvents are fired');
		},
		active: true //will be active when the object is created
	},
	'otherEvent': {
		fn: function(data, cb){
			console.log('This event is not listed in the events property');
		}
	}
}
```
