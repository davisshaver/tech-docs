# JavaScript style rules

- Use `'use strict';` in every Javscript file. This will help us write more secure Javascript. Declaring a variable without `var` is bad because the variable will be attached to global. [See here for more information.](http://www.yuiblog.com/blog/2010/12/14/strict-mode-is-coming-to-town/)

- Always use `var` to declare a variable otherwise that variable will be attached to global and the scope in Javascript is tricky. So always declare with `var`.

- Always end the line with `;`. It's a best practice and issues can be caused if there isn't a `;` at the end of the line. For example:

```javascript
MyClass.prototype.myMethod = function() {
  return 42;
}  // No semicolon here.

(function() {
  // Some initialization code wrapped in a function to create a scope for locals.
})();
```

- There are multiple ways to attach methods and properties to an object created via `new`, but Prototype is preferred here. If you want to know why, see [here](https://developers.google.com/v8/design), [here](http://jsperf.com/prototype-vs-closures/71), and [here](https://coderwall.com/p/jj6fwa).

- Always use `[]` to create an array because of this. 

```
new Array(2).length // returns 2
new Array(1).length // returns 1
```

Do this instead.

```
var a1 = [1];
a1.length; //returns 1

var a1 = [2];
a1.length //returns 1
```

- Always use `{}` to create an object. Do this for readability.

```
var o = {};
```

- Always use `===` or `!==` for strict comparison. [Here's why](http://stackoverflow.com/questions/523643/difference-between-and-in-javascript). 

### References
- [Google's Javascript styleguide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)