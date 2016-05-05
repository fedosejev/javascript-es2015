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
getMessage('Love the process.'); // 'Love the process.'
```

+ [Example](https://repl.it/CNWX)
