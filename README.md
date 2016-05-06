# Examples of ES2015 features of JavaScript language

#### Where to run your ES2015 JS code?

+ http://www.es6fiddle.net/
+ http://babeljs.io/repl/

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
