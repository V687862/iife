# IIFE 
<br/>
IIFE stands for Immediately Invoked Function Expression. It's a common pattern in JavaScript and is used for a variety of reasons, most commonly for creating a new scope. Here's a detailed breakdown of IIFE:

## Basic Structure:
The basic structure of an IIFE looks like this:

```
(function() {
// some private code that will be executed immediately
})();
```
## Breaking Down the Syntax:
The outer parentheses () around the function are what make our function an "expression". This is required because in JavaScript, only expressions can be immediately invoked.

The trailing () at the end are what immediately invoke our function expression. Hence the term, immediately invoked.

## Why use IIFE?
Avoid Global Scope Pollution: Variables defined within an IIFE are not added to the global object and are, therefore, not accessible outside of the function. This can be useful to avoid polluting the global namespace and potential variable name clashes.

```
(function() {
let privateVar = "I am private";
console.log(privateVar);  // Outputs: "I am private"
})();

console.log(typeof privateVar);  // Outputs: "undefined"
```
## Creating Private States: 
Prior to ES6 and the let and const keywords, IIFEs were a common way to create block scopes and avoid issues where a variable was unintentionally overridden in a loop.

```
for (var i = 0; i < 10; i++) {
(function(j) {
setTimeout(function() {
console.log(j);  // Outputs: 0, then 1, then 2, and so on...
}, 100);
})(i);
}
```
## Module Pattern:
IIFEs can be used to create module patterns in conjunction with objects. This allows the creation of public and private methods and properties.

```
const myModule = (function() {
let privateData = "Private data";

    function privateFunction() {
        return "This is a private function";
    }

    return {
        publicMethod: function() {
            return `Public data and ${privateFunction()}`;
        }
    };
})();

console.log(myModule.publicMethod());  // Outputs: "Public data and This is a private function"
```
## Use with Other Structures: 
IIFEs can also be used with other structures like object literals and arrays.

```
let person = ({
firstName: "John",
lastName: "Doe"
}());

let numbers = [1, 2, 3, (function() { return 4; })(), 5];
console.log(numbers);  // Outputs: [1, 2, 3, 4, 5]
```
## Things to Note:
### Parameters: 
IIFEs can accept parameters, which can be especially handy when creating isolated environments or when working with libraries:

```
(function(globalVar, library) {
// Use the parameters inside
})(window, jQuery);
```
### Returning Values: 
IIFEs can return values, which can then be assigned to variables.

```
let result = (function(a, b) {
return a + b;
})(5, 3);

console.log(result);  // Outputs: 8
```
<br/>

## In Conclusion:
IIFEs are a powerful tool in a JavaScript developer's toolbox. They provide immediate execution of functions and allow for private scopes, enabling better structured and cleaner code. However, with the introduction of ES6 block-level scoping using let and const, and with ES6 modules, some of the use-cases for IIFEs have been reduced, but they're still good to know and understand.
