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

```js
var models = ['Model S', 'Model X', 'Model 3'];

console.log(...models);
// 'Model S'
// 'Model X'
// 'Model 3'
```

+ http://jsbin.com/sexipi/edit?js,console
