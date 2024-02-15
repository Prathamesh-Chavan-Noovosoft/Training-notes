# Javascript basics

JavaScript is a multi-paradigm, dynamic language with types and operators, standard built-in objects, and methods.
Its syntax is similar to Java and C languages — many structures from those languages apply to JavaScript as well.
JavaScript supports object-oriented programming with object prototypes and classes.
It also supports functional programming since functions are first-class objects
that can be easily created via expressions and passed around like any other object.

## Data Types

- Number: used for all number values (integer and floating point) except for very big integers.
  (It is an IEEE 754 64-bit double-precision floating point value)

  Number literals can also have prefixes to indicate the base (binary, octal, decimal, or hexadecimal), or an exponent suffix.
  `
console.log(0b111110111); // 503
console.log(0o767); // 503
console.log(0x1f7); // 503
console.log(5.03e2); // 503`

  The standard arithmetic operators are supported, including addition, subtraction, remainder arithmetic, etc.
  BigInts and numbers cannot be mixed in arithmetic operations.

  The Math object provides standard mathematical functions and constants.
  `
Math.sin(3.5);
const circumference = 2 * Math.PI * r;`

  There are three ways to convert a string to a number:

  parseInt(), which parses the string for an integer.
  parseFloat(), which parses the string for a floating-point number.
  The Number() function, which parses a string as if it's a number literal and supports many different number representations.
  You can also use the unary plus + as a shorthand for Number().

  Number values also include NaN (short for "Not a Number") and Infinity.
  Many "invalid math" operations will return NaN — for example, if attempting to parse a non-numeric string,
  or using Math.log() on a negative value. Division by zero produces Infinity (positive or negative).

  NaN is contagious: if you provide it as an operand to any mathematical operation, the result will also be NaN.
  NaN is the only value in JavaScript that's not equal to itself (per IEEE 754 specification).

- BigInt: used for arbitrarily large integers.
  The BigInt type is an arbitrary length integer.
  Its behavior is similar to C's integer types (e.g. division truncates to zero), eg. -3n / 2n = -1n
  except it can grow indefinitely. BigInts are specified with a number literal and an n suffix.

- String: used to store text.
  Strings in JavaScript are sequences of Unicode characters. They're UTF-16 encoded
  Note - JavaScript does not have the distinction between characters and strings.
  If you want to represent a single character, you just use a string consisting of that single character.
  `
console.log("Hello, world");
console.log("你好，世界！"); // Nearly all Unicode characters can be written literally in string literals`

- Boolean: true and false — usually used for conditional logic.

## Other types

- Symbol: used for creating unique identifiers that won't collide.
- Undefined: indicating that a variable has not been assigned a value.
- Null: indicating a deliberate non-value.

JavaScript distinguishes between null, which indicates a deliberate non-value (and is only accessible through the null keyword),
and undefined, which indicates absence of value. There are many ways to obtain undefined:

A return statement with no value (return;) implicitly returns undefined.
Accessing a nonexistent object property (obj.iDontExist) returns undefined.
A variable declaration without initialization (let x;) will implicitly initialize the variable to undefined.

JavaScript has a Boolean type, with possible values true and false — both of which are keywords. Any value can be converted to a boolean according to the following rules:

false, 0, empty strings (""), NaN, null, and undefined all become false.
All other values become true.
JavaScript will silently perform this conversion when it expects a boolean, such as in an if statement.

## Objects

Everything else is known as an Object. Common object types include:

- Function
- Array
- Date
- RegExp
- Error

Notes - Functions aren't special data structures in JavaScript — they are just a special type of object that can be called.

## Variables

Variables in JavaScript are declared using one of three keywords: let, const, or var.

let - Block Scoped
const - cannot be reassigned values, Block scoped
var - Global scope, discouraged in modern javascript. var keyword can redeclare a variable

Note about const:
const declarations only prevent reassignments — they don't prevent mutations of the variable's value, if it's an object.
e.g. ->
`const obj = {};
obj.a = 1; // no error
console.log(obj); // { a: 1 }`

Note about variables:
If you declare a variable without assigning any value to it, its value is undefined.
You can't declare a const variable without an initializer, because you can't change it later anyway.

let and const declared variables still occupy the entire scope they are defined in,
and are in a region known as the temporal dead zone before the actual line of declaration.
This has some interesting interactions with variable shadowing, which don't occur in other languages.

`function foo(x, condition) {
    if (condition) {
        console.log(x);
        const x = 2;
        console.log(x);
    }
}
foo(1, true);`

In most other languages, this would log "1" and "2", because before the const x = 2 line,
x should still refer to the parameter x in the upper scope. In JavaScript,
because each declaration occupies the entire scope, this would throw an error on the
first console.log: "Cannot access 'x' before initialization". For more information, see the reference page of let.

## Operators

JavaScript's numeric operators include +, -, \*, /, % (remainder), and \*\* (exponentiation).
Values are assigned using =. Each binary operator also has a compound assignment counterpart
such as += and -=, which extend out to x = x operator y.

If you add a string to a number (or other value) everything is converted into a string first. This might trip you up:
`"3" + 4 + 5; // "345"
3 + 4 + "5"; // "75"`
