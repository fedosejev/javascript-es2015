# Examples of ES2015 features of JavaScript language

#### Where to run your ES2015 JS code?

+ http://www.es6fiddle.net/
+ http://babeljs.io/repl/

## Contents

+ [(Implicit) Block scoping with `let`](#implicit-block-scoping-with-let)
+ [`const` Declarations](#const-declarations)
+ [Spread operator](#spread-operator)
+ [Functions](#functions)
+ [Arrow function](#arrow-function)
+ [Object Initializer Shorthand](#object-initializer-shorthand)
+ [Object Destructuring](#object-destructuring)
+ [Method Initializer Shorthand](#method-initializer-shorthand)
+ [Template Strings](#template-strings)
+ [`Object.assign`](#objectassign)
+ [Array Destructuring](#array-destructuring)
+ [`for ... of` statement](#for--of-statement)
+ [`Array.prototype.find`](#arrayprototypefind)
+ [Map](#map)
+ [WeakMap](#weakmap)
+ [Set](#set)
+ [WeakSet](#weakset)
+ [Classes](#classes)
+ [Modules](#modules)

## (Implicit) Block scoping with `let`

#### Example 1

```js
var message = 'Welcome!';

{
  let message = 'Important!';
  console.log(message); // Important!
}

console.log(message); // Welcome!
```

#### Example 2

```js
{
  console.log(today);
  console.log(tomorrow); // "ReferenceError: tomorrow is not defined
  
  var today;
  let tomorrow;
}
```

+ https://jsbin.com/vijudoy/edit?js,console

## `const` Declarations

```js
{
  const message = 'Tomorrow!';
  console.log(message); // Tomorrow!
  
  message = 'Today!'; // TypeError: Assignment to constant variable.
}
```

+ http://jsbin.com/hohisi/edit?js,console

## Spread operator

#### Spread array

```js
var models = ['Model S', 'Model X', 'Model 3'];

console.log(...models);
// 'Model S'
// 'Model X'
// 'Model 3'
```

+ http://jsbin.com/sexipi/edit?js,console

#### Gather arguments 

```js
function setData(soon, now, ...later) {
  console.log(later);
}

setData('Sleep', 'Work', 'Reply to all emails', 'Edit photos'); // ["Reply to all emails", "Go to meetup"]
```

+ http://jsbin.com/diheqo/edit?js,console

#### Example of using both with recursion

```js
function multiply(...list) {
	if (list.length === 1) {
		return list[0];
	}
	
	return list[0] * multiply(...list.slice(1));
}

multiply(3, 4, 5, 6); // 360
```

+ [Example](https://repl.it/CMLK)

## Functions

### Default parameters

```js
function getMessage(message = 'No message.') {
	console.log(message);
}

getMessage(); // 'No message'
getMessage(undefined); // 'No message.'
getMessage('Love the process.'); // 'Love the process.'
```

+ [Example](https://repl.it/CNW0)

### Named parameters

```js
function produceCar(modelName, options) {
	console.log(modelName);
	console.log(options.color);
	console.log(options.isAutopilotIncluded);
	console.log(options.isBioweaponDefenceModeIncluded);
}

produceCar('Telsa Model X', {
	color: 'White',
	isAutopilonIncluded: true,
	isBioweaponDefenceModeIncluded: true
});

// Or:

function produceCar(modelName, { color, isAutopilotIncluded, isBioweaponDefenceModeIncluded }) {
	console.log(modelName);
	console.log(color);
	console.log(isAutopilotIncluded);
	console.log(isBioweaponDefenceModeIncluded);
}

produceCar('Telsa Model X', {
	color: 'White',
	isAutopilotIncluded: true,
	isBioweaponDefenceModeIncluded: true
});

// Or:

function produceCar(modelName, { color, isAutopilotIncluded, isBioweaponDefenceModeIncluded } = {}) {
	console.log(modelName);
	console.log(color);
	console.log(isAutopilotIncluded);
	console.log(isBioweaponDefenceModeIncluded);
}

produceCar('Telsa Model X');
```

+ [Example](https://repl.it/CNWa)

## Arrow function

Problem:

```js
function Message(text) {
	this.text = text;
}

Message.prototype.log = function () {
	setTimeout(function () {
		console.log(this.text);
	}, 100);
}

var message = new Message('Welcome!');
message.log(); // undefined
```

Solution:

```js
function Message(text) {
	this.text = text;
}

Message.prototype.log = function () {
	setTimeout(() => {
		console.log(this.text);
	}, 100);
}

var message = new Message('Welcome!');
message.log(); // 'Welcome!'
```

+ [Example](https://repl.it/CNgW)

Arrow functions bind to the scope of where they are __defined__, not where they're __called__ - lexical binding.

## Object Initializer Shorthand

Problem:

```js
function getObject(a, b, c) {
	return {
		a: a, // - repetition!
		b: b, // - repetition!
		c: c // - repetition!
	};
}

var object = getObject(1, 2, 3);

console.log(object); // { a: 1, b: 2, c: 3 }
```

+ [Example](https://repl.it/CNv3)

Solution:

```js
function getObject(a, b, c) {
	return {a, b, c};
}

var object = getObject(1, 2, 3);

console.log(object); // { a: 1, b: 2, c: 3 }
```

+ [Example](https://repl.it/CNv4)


## Object Destructuring

Problem:

```js
let object = { a: 1, b: 2, c: 3 };
let a = object.a;
let b = object.b;
let c = object.c;

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```

+ [Example](https://repl.it/CNvr)

Solution:

```js
let { a, b, c } = { a: 1, b: 2, c: 3 };

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```

+ [Example](https://repl.it/CNvu)
 
## Method Initializer Shorthand

Problem:

```js
function getData() {
	let a = 1;
	let b = 2;
	
	return {
		a: a,
		b: b,
		getC: function () {
			return 3;	
		}
	};
}

let result = getData().getC();

console.log(result); // 3
```

+ [Example](https://repl.it/CNyT)

Solution:

```js
function getData() {
	let a = 1;
	let b = 2;
	
	return {
		a,
		b,
		getC() {
			return 3;	
		}
	};
}

let result = getData().getC();

console.log(result); // 3
``` 

+ [Example](https://repl.it/CNyQ)

## Template Strings

Problem:

```js
let firstName = 'Artemij';
let lastName = 'Fedosejev';

var message = 'Welcome, ' + firstName + ' ' + lastName + '!';

console.log(message); // 'Welcome, Artemij Fedosejev!'
```

+ [Example](https://repl.it/CNyo)

Solution:

```js
let firstName = 'Artemij';
let lastName = 'Fedosejev';

var message = `Welcome, ${firstName} ${lastName}!`;

console.log(message); // 'Welcome, Artemij Fedosejev!'
```

+ [Example](https://repl.it/CNyp)

## `Object.assign`

Without mutating `defaults`:

```js
let defaults = {
	a: 1,
	b: 2,
	c: 3
};

let settings = {
	c: 30,
	d: 40,
	e: 50
};

let results = Object.assign({}, defaults, settings);

console.log(results); // { a: 1, b: 2, c: 30, d: 40, e: 50 }
console.log(defaults); // { a: 1, b: 2, c: 3 }
```

+ [Example](https://repl.it/COB4)

Mutating `defaults`:

```js
let defaults = {
	a: 1,
	b: 2,
	c: 3
};

let settings = {
	c: 30,
	d: 40,
	e: 50
};

let results = Object.assign(defaults, settings);

console.log(results); // { a: 1, b: 2, c: 30, d: 40, e: 50 }
console.log(defaults); // { a: 1, b: 2, c: 30, d: 40, e: 50 }
```

+ [Example](https://repl.it/COB1)

## Array Destructuring

```js
let numbers = [1, 2, 3];
let [ a, b, c ] = numbers;

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```

+ [Example](https://repl.it/COBu)

```js
let numbers = [1, 2, 3];
let [ a,, c ] = numbers;

console.log(a); // 1
console.log(c); // 3
```

+ [Example](https://repl.it/COBw)

```js
let numbers = [1, 2, 3];
let [ a, ...rest ] = numbers;

console.log(a); // 1
console.log(rest); // [2, 3]
```

+ [Example](https://repl.it/COBy)

## `for ... of` statement

Problem:

```js
var numbers = [1, 2, 3];

for (let index in numbers) {
	console.log(numbers[index]); // 1 2 3
}
```

+ [Example](https://repl.it/COCM)

Solution:

```js
var numbers = [1, 2, 3];

for (let number of numbers) {
	console.log(number); // 1 2 3
}
```

+ [Example](https://repl.it/COCL)

## `Array.prototype.find`

```js
let models = [
	{
		name: 'Model S',
		price: 75000
	},
	{
		name: 'Model X',
		price: 120000
	},
	{
		name: 'Model 3',
		price: 35000
	}
];

var luxuryModel = models.find(function (model) {
	return model.price > 50000;
});

console.log(luxuryModel); // { name: 'Model S', price: 75000 }
```

+ [Example](https://repl.it/COCh)

Or:

```js
let models = [
	{
		name: 'Model S',
		price: 75000
	},
	{
		name: 'Model X',
		price: 120000
	},
	{
		name: 'Model 3',
		price: 35000
	}
];

var luxuryModel = models.find((model) => {
	return model.price > 50000;
});

console.log(luxuryModel); // { name: 'Model S', price: 75000 }
```

+ [Example](https://repl.it/COCp)

Or:

```js
let models = [
	{
		name: 'Model S',
		price: 75000
	},
	{
		name: 'Model X',
		price: 120000
	},
	{
		name: 'Model 3',
		price: 35000
	}
];

var luxuryModel = models.find(model => model.price > 50000);

console.log(luxuryModel); // { name: 'Model S', price: 75000 }
```

+ [Example](https://repl.it/COCn)

## Map

Problem:

```js
let modelS = { color: 'white' };
let modelX = { color: 'red' };

let models = {};

models[modelS] = 'Sedan';
models[modelX] = 'SUV';

console.log(models[modelS]); // 'SUV'
console.log(Object.keys(models)); // [ '[object Object]' ]
```

+ [Example](https://repl.it/COHY)

Solution:

```js
let modelS = { color: 'white' };
let modelX = { color: 'red' };

let models = new Map();
models.set(modelS, 'Sedan');
models.set(modelX, 'SUV');

console.log(models.get(modelS)); // 'Sedan'
console.log(models.get(modelX)); // 'SUV'
```

+ [Example](https://repl.it/COHl)

## WeakMap

+ Keys must be objects, not strings when using WeakMap.
+ WeakMap allows better garbage collection than Map.

```js
let models = new WeakMap();

models.set('modelS', 'Sedan'); // TypeError: Invalid value used as weak map key
```

+ [Example](https://repl.it/COHd)

## Set

```js
let set = new Set();

set.add('a');
set.add(true);
set.add(10);
set.add('a'); // ignored, because values must be unique

console.log(set.size); // 3
```

+ [Example](https://repl.it/COIJ)

## WeakSet

Unlike `Set`, only objects can be assigned to `WeakSet`.

```js
let set = new WeakSet();

set.add({ message: 'Hello' });
set.add(true); // TypeError: Invalid value used in weak set
```

+ [Example](https://repl.it/COIP)

## Classes

Problem:

```js
function Car(make, model) {
	this.make = make;
	this.model = model;
	this.isStarted = false;
}

Car.prototype.start = function () {
	this.isStarted = true;
	console.log('Started!');
};

var tesla = new Car('Tesla', 'Model S');
tesla.start();
```

+ [Example](https://repl.it/COJM)

Solution:

```js
class Car {
	constructor(make, model) {
		this.make = make;
		this.model = model;
		this.isStarted = false;	
	}
	
	start() {
		this.isStarted = true;
		console.log('Started!');
	}
}

var tesla = new Car('Tesla', 'Model S');
tesla.start();
```

+ [Example](https://repl.it/COJO)

#### Subclasses

```js
class Car {
	constructor(make, model) {
		this.make = make;
		this.model = model;
		this.isStarted = false;	
	}
	
	start() {
		this.isStarted = true;
		console.log('Started!');
	}
}

class Tesla extends Car {
	constructor(model, color) {
		super('Tesla', model);
		
		this.color = color;
	}
	
	logInfo() {
		// super.start(); - refer to a super class method
		console.log(this.make, this.model, this.color);
	}
}

var tesla = new Tesla('Model S', 'white');
tesla.logInfo(); // 'Tesla Model S white'
tesla.start(); // 'Started!'
```

+ [Example](https://repl.it/COJ8)

## Modules

#### Exporting

```js
export default function logMessage(message) {
	console.log(message);
}
```

Or:

```js
function logMessage(message) {
	console.log(message);
}

export { logMessage };
```

#### Importing

```js
import logMessage from './log-message';
```

## Promises

