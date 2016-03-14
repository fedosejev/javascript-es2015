# Examples of ES2015 features of JavaScript language

#### Where to run your ES2015 JS code?

+ http://www.es6fiddle.net/
+ http://babeljs.io/repl/

## Block scoping

```js
var message = 'Welcome!';

{
  let message = 'Important!';
  console.log(message); // Important!
}

console.log(message); // Welcome!
```

