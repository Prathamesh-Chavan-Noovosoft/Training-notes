# Javascript basics

JavaScript is a multi-paradigm, dynamic language with types and operators, standard built-in objects, and methods.
Its syntax is similar to Java and C languages — many structures from those languages apply to JavaScript as well.
JavaScript supports object-oriented programming with object prototypes and classes.
It also supports functional programming since functions are first-class objects
that can be easily created via expressions and passed around like any other object.

## Data Types

- ### Number: used for all number values (integer and floating point) except for very big integers.

  (It is an IEEE 754 64-bit double-precision floating point value)

  - Number literals can also have prefixes to indicate the base (binary, octal, decimal, or hexadecimal), or an exponent suffix.

  ```javascript
  console.log(0b111110111); // 503
  console.log(0o767); // 503
  console.log(0x1f7); // 503
  console.log(5.03e2); // 503
  ```

  - The standard arithmetic operators are supported, including addition, subtraction, remainder arithmetic, etc.
    BigInts and numbers cannot be mixed in arithmetic operations.

  - The Math object provides standard mathematical functions and constants.

    ```javascript
    Math.sin(3.5);
    const circumference = 2 * Math.PI * r;
    ```

  - There are three ways to convert a string to a number:
    parseInt(), which parses the string for an integer.
    parseFloat(), which parses the string for a floating-point number.
    The Number() function, which parses a string as if it's a number literal and supports many different number representations.
    You can also use the unary plus + as a shorthand for Number().

  - Number values also include NaN (short for "Not a Number") and Infinity.
    Many "invalid math" operations will return NaN — for example, if attempting to parse a non-numeric string,
    or using Math.log() on a negative value. Division by zero produces Infinity (positive or negative).
    NaN is contagious: if you provide it as an operand to any mathematical operation, the result will also be NaN.
    NaN is the only value in JavaScript that's not equal to itself (per IEEE 754 specification).

- ### BigInt: used for arbitrarily large integers.

  The BigInt type is an arbitrary length integer.
  Its behavior is similar to C's integer types (e.g. division truncates to zero), eg. -3n / 2n = -1n
  except it can grow indefinitely. BigInts are specified with a number literal and an n suffix.

- ### String: used to store text.

  Strings in JavaScript are sequences of Unicode characters. They're UTF-16 encoded
  Note - JavaScript does not have the distinction between characters and strings.
  If you want to represent a single character, you just use a string consisting of that single character.

  ```javascript
  console.log("Hello, world");
  console.log("你好，世界！"); // Nearly all Unicode characters can be written literally in string literals
  ```

- ### Boolean: true and false — usually used for conditional logic.

## Other types

- ### Symbol: used for creating unique identifiers that won't collide.
- ### Undefined: indicating that a variable has not been assigned a value.
- ### Null: indicating a deliberate non-value.

  JavaScript distinguishes between null, which indicates a deliberate non-value (and is only accessible through the null keyword),
  and undefined, which indicates absence of value. There are many ways to obtain undefined:

  A return statement with no value (return;) implicitly returns undefined.
  Accessing a nonexistent object property (obj.iDontExist) returns undefined.
  A variable declaration without initialization (let x;) will implicitly initialize the variable to undefined.

  - ### Notes about other types
    JavaScript has a Boolean type, with possible values true and false — both of which are keywords. Any value can be converted to a boolean according to the following rules:
    false, 0, empty strings (""), NaN, null, and undefined all become false.
    All other values become true.
    JavaScript will silently perform this conversion when it expects a boolean, such as in an if statement.

## Objects

Everything else is known as an Object. Common object types include:

- ### Function
- ### Array
- ### Date
- ### RegExp
- ### Error

Notes - Functions aren't special data structures in JavaScript — they are just a special type of object that can be called.

## Variables

Variables in JavaScript are declared using one of three keywords: let, const, or var.

### let - Block Scoped

### const - cannot be reassigned values, Block scoped

### var - Global scope, discouraged in modern javascript. var keyword can redeclare a variable

### Note about const:

const declarations only prevent reassignments — they don't prevent mutations of the variable's value, if it's an object.
e.g. ->

```javascript
const obj = {};
obj.a = 1; // no error
console.log(obj); // { a: 1 }
```

### Note about variables:

If you declare a variable without assigning any value to it, its value is undefined.
You can't declare a const variable without an initializer, because you can't change it later anyway.

let and const declared variables still occupy the entire scope they are defined in,
and are in a region known as the temporal dead zone before the actual line of declaration.
This has some interesting interactions with variable shadowing, which don't occur in other languages.

```javascript
function foo(x, condition) {
  if (condition) {
    console.log(x);
    const x = 2;
    console.log(x);
  }
}
foo(1, true);
```

In most other languages, this would log "1" and "2", because before the const x = 2 line,
x should still refer to the parameter x in the upper scope. In JavaScript,
because each declaration occupies the entire scope, this would throw an error on the
first console.log: "Cannot access 'x' before initialization". For more information, see the reference page of let.

## Operators

JavaScript's numeric operators include +, -, \*, /, % (remainder), and \*\* (exponentiation).
Values are assigned using =. Each binary operator also has a compound assignment counterpart
such as += and -=, which extend out to x = x operator y.

If you add a string to a number (or other value) everything is converted into a string first. This might trip you up:

```javascript
"3" + 4 + 5; // "345"
3 + 4 + "5"; // "75"
```

### Comparisons

Comparisons in JavaScript can be made using <, >, <= and >=, which work for both strings and numbers.
For equality, the double-equals operator performs type coercion if you give it different types, with sometimes interesting results.
On the other hand, the triple-equals operator does not attempt type coercion, and is usually preferred.

```javascript
123 == "123"; // true
1 == true; // true

123 === "123"; // false
1 === true; // false
```

The double-equals and triple-equals also have their inequality counterparts: != and !==.

JavaScript also has bitwise operators and logical operators.
Notably, logical operators don't work with boolean values only — they work by the "truthiness" of the value.

```javascript
const a = 0 && "Hello"; // 0 because 0 is "falsy"
const b = "Hello" || "world"; // "Hello" because both "Hello" and "world" are "truthy"
```

The && and || operators use short-circuit logic, which means whether they will execute their second operand is dependent on the first.
This is useful for checking for null objects before accessing their attributes:

```javascript
const name = o && o.getName();
```

## Grammar

JavaScript grammar is very similar to the C family. There are a few points worth mentioning:

Identifiers can have Unicode characters, but they cannot be one of the reserved words.
Comments are commonly // or /\* \*/, while many other scripting languages like Perl, Python, and Bash use #.
Semicolons are optional in JavaScript — the language automatically inserts them when needed.
However, there are certain caveats to watch out for, since unlike Python, semicolons are still part of the syntax.

// Javascript Array Methods
```javascript
[3, 4, 5, 6].at(1); // 4
[3, 4, 5, 6].pop(); // [3, 4, 5]
[3, 4, 5, 6].push(7); // [3, 4, 5, 6, 7]
[3, 4, 5, 6].fill(1); // [1, 1, 1, 1]
[3, 4, 5, 6].join("-"); // 3-4-5-6
[3, 4, 5, 6].shift(); // [4, 5, 6]
[3, 4, 5, 6].reverse(); // [6, 5, 4, 3]
[3, 4, 5, 6].unshift(1); // [1, 3, 4, 5, 6]
[3, 4, 5, 6].includes(5); // true
[3, 4, 5, 6].map((num) => num + 6); // [9, 10, 11, 12]
[3, 4, 5, 6].find((num) => num > 4); // 5
[3, 4, 5, 6].filter((num) => num > 4); // [5, 6]
[3, 4, 5, 6].every((num) => num > 5); // false
[3, 4, 5, 6].findeIndex((num) => num > 4); // 2
[3, 4, 5, 6].reduce((acc, num) => acc + num, 0); // 18
```
