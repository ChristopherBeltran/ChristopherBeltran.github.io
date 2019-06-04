---
layout: post
title:      "JS Hoisting and Scope"
date:       2019-06-04 01:06:32 -0400
permalink:  js_hoisting_and_scope
---


Hoisting can be accomplished with both a variable and a function.  There are a couple of nuances with variable hoisting that can be tricky.


**Function hoisting:**

Function hoisting will hoist the function name and the definition to the top of the scope.

For example:

```
hoistedFunction();

function hoistedFunction() {
console.log("I'm getting hoisted");
}
```

The console is able to log the message from the function since the function definition is also hoisted to the top, allowing the function to not only be referenced but actually invoked.

BUT function hoisting is only possible with function *definitions* and not function *expressions*.

For example:

```
imHoisted();

notHoisted();

function imHoisted() {
console.log("Hoisting")
}

var notHoisted = () => console.log("Not hoisting");
```

This console should log the first functions message while returning `TypeError: undefined is not a function`, due to the fact that the declaration gets hoisted but not the actual function definition.



**Variable hoisting:**

Variable hoisting is only possible with the `var` variable keyword.

Only the variable declaration will get hoisted to the top of the current scope, not the variable initialization.

For example:

```
console.log(x)
var x = "not initialized"
```

This example will return `undefined` rather than `Uncaught ReferenceError: x is not defined`, due to the fact that the `var x` variable declaration was able to be hoisted, however the `= "not initialized"` initialization was not.

The following example will show a variable being hoisted.

```
x = "I'll be initialized after the declaration";
console.log(x);
var x;
```


The console is able to log the value of `x` due to the fact that the initialization takes place after the variable declaration is hoised to the top.  This variable hoisting can lead to potential issues when declaring a variable in the global scope and then redeclaring within a local block scope, which leads to the next section on Scope.


**Scope:**

Variables can be declared and assigned within the global scope and the local block scope.

Variables declared globally are accessible throughout the whole script, in and out of functions.

For example:


```
const globalVariable = "I'm global";

globalVariable;

function messageLog() {
console.log(globalVariable);
}
```


The `globalVariable` line is able to return the value of the variable and the function is also able to log the value of the variable from within the function.

Next, I'll show an example of variables declared within functions and their accessibility:

```

function globalVariable() {
var imGlobal = "Accessible";
}

function nonGlobal() {
let notGlobal = "Not accessible";
}

window.imGlobal;

window.notGlobal;
```

The call to `window.imGlobal` will return the value of the variable that was declared within the function due to `var` having a global scope, while the call to `window.notGlobal` will return `undefined` since the variable declaration is only accessible from within that block scope.  

Similarly, while working within a function there will be different capabilities of the variables.

For example:

```

let x = "first value"

function scopingTest() {
let x = "second value"
console.log(x);
}
console.log(x)

var y = "first y value"

function scopeTest() {
var y = "Second y value"
console.log(y);
}
console.log(y);
```

The first console log will display the value for `x` as it was assigned within the block of the function, whereas the second console.log will display the `x` value as it was assigned outside of the function scope.  It is the same variable being declared with `let` however, since the `let` declarations within the function only have block scope, it treats `x` as a completely new variable, so it does not affect the `x` that was assigned outside of the function.

Now, the second set of console logs will both return the same value for y `Second y value`, due to the scope of the `var` variable declaration.

There is also a difference between function declarations.

`var` and `let` can be declared without being initialized

```
var x;
let y;
```

However, `const` requires an initialization upon declaration.

Another restriction of `const` is that once it is declared it cannot be re-declared, unlike `var` and `let`.

But, one difference with `var` and `let` re-declarations is that `var` can be re-declared regardless of scope, while `let` can only be re-declared froma  different scope.  




