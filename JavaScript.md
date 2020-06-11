# _JavaScript_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- [http://es6-features.org](http://es6-features.org/)
- https://tylermcginnis.com/javascript-visualizer/

---

# **_Comments_**

```
// will ignore the remainder of the text on the current line
```

```
Beginning with /* and
ending with */ will make a multi-line comment
```

---

# **_Data Types_**

## _**Primitives**_

- Numbers - `4, 10, 0.66`
- Strings - `"dogs go woof!”`
  - Strings go inside `' '` or `“ ”`
    - preferably single quotes for JS and double quotes for html
  - string values are immutable, which means they cannot be altered once created
- Booleans - `true`, `false`
  - Truthy - A value that is considered `true` when encountered in a Boolean context
    - `if (true)`
    - `if ({})`
    - `if ([])`
    - `if (42)`
    - `if (-42)`
    - `if (3.14)`
    - `if (-3.14)`
    - `if ("foo")`
    - `if (new Date())`
    - `if (Infinity)`
    - `if (-Infinity)`
  - Falsy - A value that is considered `false` when encountered in a Boolean context
    - `if (false)`
    - `if (null)`
    - `if (undefined)`
    - `if (NaN)`
    - `if (0)`
    - `if ('')`
    - `if ("")`
    - ` if (``) `
- Undefined - value hasn’t been assigned
- Null - nothing
- Symbol

## _**Objects**_

- Arrays
- Functions

---

# **_Operators_**

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators

## **\_**Assignment**\_**

- `=` - Sets it equal to (assigns)
  - Everything to the right of the = operator is resolved before the value is assigned to the variable to the left of the operator
- `=+` - Addition Assignment
  - Adds the value of an expression to the value of a variable and assigns the result to the variable

## _Arithmetic_

- `+` - produces the sum of numeric operands or string concatenation
- `-` - subtracts the two operands, producing their difference
- `/` - produces the quotient of its operands where the left operand is the dividend and the right operand is the divisor
- `*` - produces the product of the operands

## _Exponentiation_\*\* \*\*

- `**` - returns the result of raising first operand to the power second operand
  - `var1 ** var2`

## **_Comparison_**

- All comparison operators return a boolean true or false value

- `>` - Greater than
- `<` - Less than
- `<=` - Less than or equal to
- `>=` - Greater than or equal to
- `==` - Compares two values and returns true if they're equivalent or false if they are not
- `===` - Strict equality tests both the data type and value of the compared elements
- `!=` - Opposite of the equality operator
- `!==` - Opposite of the strict equality operator

## **_Logical_**

- The value produced by a `&&` or `||` operator is not necessarily of type Boolean. The value produced will always be the value of one of the two operand expressions.

- `&&` - And
  - Tests more than one thing at a time
  - Returns true if and only if the operands to the left and right of it are true
  - `A && B` returns the value A if A can be coerced into `false`; otherwise, it returns B
- `||` - Or
  - Returns true if either of the operands is true
  - `A || B` returns the value A if A can be coerced into `true`; otherwise, it returns B
- `!` - Not
  - Returns the opposite of a boolean

## **_Increment and decrement_**

- `i++` - post-increment
  - returns the value of `i` before incrementing
  - use the value of `i` in a statement, then increase it by 1
  - Same as `i = i + 1`
- `++i` - pre-increment
  - returns the value of `i` after it has been incremented
  - increase the value of `i` by 1, then use in a statement
  - Same as `i + 1 = i`
- `i--` - post-decrement
  - use the value of `i` in a statement, then decrease it by 1
- `--i` - pre-decrement
  - decrease the value of i by 1, then use in a statement
- `i += x` - assigns and increments up by any value (x)
  - same as `i = i + x`
- `i -= x` - assigns and decrement down by any value (x)
- `i *= x` - assigns and multiplies by any value (x)
- `i /= x` - assigns and divides by any value (x)
  - `var i` is the standard counting variable name
    - if `i` is taken, use `j`

## **_Remainder/Modulo_**

- When % is placed between two numbers, the computer will divide the first number by the second, and then return the remainder of that division
  - `17 % 5` evaluates to 2
  - `13 % 7` evaluates to 6
- A number can be checked even or odd by checking the remainder of the division of the number by 2
  - `17 % 2` = 1 (17 is Odd)
  - `48 % 2` = 0 (48 is Even)
- To check if a number is an interger
  - ` 23 % ``1`` === ``0 `

## _Grouping_

- `( )` - Controls the precedence of evaluation in expressions

## _Comma_

- `,` - Evaluates both of its operands and returns the value of the last operand

## _Concatenation_

- `+` - Combines two string values together, returning another string that is the union of the two operand strings
- `var myStr = 'My name is Alan,' + ' I concatenate.'`
  - returns My name is Chase, I concatenate

## _Spread_

- `…` - Spreads the contents of what it's being used on, into wherever it's being used
  - Allows an iterable such as an array or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected
  - Or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected
- Spreading an array will spread the elements
- Spreading an object will spread the key/value pairs

```
var arr = [4, 5, 6];
// es5
var completeArr = [1, 2, 3].concat(arr2); // [1, 2, 3, 4, 5, 6]

// es6
var completeArr = [1, 2, 3, ...arr]; // [1, 2, 3, 4, 5, 6]
```

## _Unary_

- An operation with only one operand
- `-`
  - Unary negation operator
  - Precedes its operand and negates it

```
`const x = 3;
const y = -x;
// y = -3
console.log(-y)
// 3`
```

- `+`
  - Unary plus operator
  - Precedes its operand and evaluates to its operand but attempts to convert it into a number, if it isn't already
  - It can convert string representations of integers and floats, as well as the non-string values `true`, `false`, and `null`

```
+3     // 3
+'3'   // 3
+true  // 1
+false // 0
+null  // 0
+function(val){  return val } // NaN
```

- `!`

  - Logical NOT operator

- `delete`
  - Deletes an object, an object's property, or an element at a specified index in an array
- `typeof`
  - Returns a string indicating the type of the unevaluated operand
  - `typeof {a: 1} === 'object';`
  - Return types:
    - `"string"`
    - `"number"`
    - `"boolean"`
    - `"undefined"`
    - `"object"`
    - `"function"`
    - `"symbol"`
- `void`
  - Specifies an expression to be evaluated without returning a value

## _Relational_

- compares its operands and returns a `boolean` value based on whether the comparison is true

- `in`
  - Returns `true` if the specified property is in the specified object
  - 'property' `in` object

```
var mycar = {make: 'Honda', model: 'Accord', year: 1998};
'make' in mycar  // returns true
```

- `instanceof`
  - Returns `true` if the specified object is of the specified object type

---

# **_Syntax_**

- `[ ]` - array initializer
- `{ }` - object initializer
- `( )` - grouping operator, controls order of operations

- Some JavaScript statements must be terminated with semicolons

  - Empty statement
  - `let`, `const`, variable statement
  - `import`, `export`, module declaration
  - Expression statement
  - `debugger`
  - `continue`, `break`, `throw`
  - `return`

- Escape sequences in strings ( `\` ):
  - `var sampleStr = "Alan said, \"Peter is learning JavaScript\".";`
    - returns `Alan said, "Peter is learning JavaScript".`
    - Or you can use single and double quotes together without escaping
  - Others:
  - _Code_ _Output_
  - `\'` single quote
  - `\"` double quote
  - `\\` backslash
  - `\n` newline
  - `\r` carriage return
  - `\t` tab
  - `\b` backspace
  - `\f` form feed

```
var arr = [4, 5, 6];
// es5
var completeArr = [1, 2, 3].concat(arr2); // [1, 2, 3, 4, 5, 6]

// es6
var completeArr = [1, 2, 3, ...arr]; // [1, 2, 3, 4, 5, 6]
```

---

# _Keywords_

- Cannot use certain reserved words as variables, labels, or function names
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords

---

# **_Variables_**

- They're a simple name to represent the data we want to refer to
- `var myVariable = “somedata”;`
- A variable is a label for a location in memory
- Give them a label and tell them what data to hold onto
- Labels can be made up of numbers, letters, and \$ or \_ , but can’t start with a number or contain spaces
- If we want to use a variable outside of a function we need to make sure to return that element out of the function
- We also need to make a new variable where we can store our returned value so we can reference it later.
- A variable can be a function:

```
var` sayHello = `function(name) {
`    console.log(`'Hello '` + name);`
`};`
```

## var

- ES5
- global, function scoped
- The name gets hoisted to the top of its scope, but not the value

## let

- ES6
- global, function, block scoped
- Can be reassigned

## const

- ES6
- global, function, block scoped
- Cannot be reassigned

---

# **\_**Expressions**\_**

- Evaluates to (results in) a single value
- They rely on operators to create this single value

## _**Primary Expressions**_

- **this**
  - Refers to the function's execution context
  - A keyword that changes respective to what scope it is called in
  - Four rules that define the context of `this`
  - Default context is always global (i.e. the window)
  - Traditional function called as a method of an object
  - The `new` keyword uses your object “blueprint” to give `this` meaning
  - Passing an object into `.call`, `.apply`, or `.bind` makes `this` refer to that object
- **function**
  - Defines a function expression
- **class**
  - Defines a class expression

## _**Left-hand-side expressions**_

- **property accessors**
  - Provides access to a property or method of an object
- **new**
  - Creates an instance of a constructor

## _**Regular Expressions (Regex)**_

- http://play.inginf.units.it/#/
- https://regexr.com/

- Used to find certain words or patterns inside of `strings`

* If we wanted to find the word “the” in the string “The dog chased the cat”, we could use the following regular expression: `/the/gi`
  - `/` is the start of the regular expression.
  - `the` is the pattern we want to match.
  - `/` is the end of the regular expression.
  - `g` means global, which causes the pattern to return all matches in the string, not just the first one.
  - `i` means that we want to ignore the case (uppercase or lowercase) when searching for the pattern.

- can use special selectors in Regular Expressions to select a particular type of value:
  - `\d` - digit selector - used to retrieve one digit (e.g. numbers 0 to 9) in a string
  - Appending a plus sign `+` after the selector, e.g. `/\d+/g`, allows this regular expression to match one or more digits
  - `\s` to find whitespace in a string
  - `\r` (carriage return)
  - `\n` (newline)
  - `\t` (tab)
  - `\f` (the form feed).

* you can invert any match by using the uppercase version of the regular expression selector
  - for example, `\s` will match any whitespace, and `\S` will match anything that isn't whitespace

---

# **_Objects_**

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects
- Representation of real world things in computer programming
- key/value storage, similar to arrays, except that instead of using indexes, data is stored as properties
  - Keys are also called properties
  - When you need to depend on the order of the elements in the collection, use arrays
  - When order is not important, use objects
- Objects have their own attributes, called properties, and their own functions, called methods
- We can also create private properties and private methods, which aren't accessible from outside the object

```
var school = {  // object
  name: "International School of Denver",  //property
  capacity: 250,
  languageImmersion: true,
  currentStudents: 75,
  checkOpenSpots: function() {  // method
    console.log(this);
    return this.capacity - this.currentStudents;
  }
}
```

## _Creating Objects_

- There are three ways to create an object:

### _Object literal_

- Creates a new object
- `var obj = {};`
- shorthand for `var obj = new Object();`

### _ConSTRUCTOR Function_

- https://repl.it/@hmmrepl/constructor-functions-and-prototype
- A function used to create objects
- It’s given a capitalized name to make it clear that it's a constructor

```
function ObjectMaker() {
  this.prop = 123;
  this.meth = function() {
    console.log('im a method');
  };
}
```

- In a constructor, the “`this`” variable refers to the new object being created by the constructor
- In the example, “`this`” refers to the Car function
- To use a constructor function, we call it with the “`new`” keyword in front of it

```
`const newObject = new ObjectMaker();`
`console.log(newObject); // ObjectMaker { prop: 123, meth: [Function] }`
```

- To change a property on the object

```
`newObject.prop = 456;`
`console.log(newObject); // ObjectMaker { prop: 456, meth: [Function] }`
```

- To execute a method on the object

```
console.log(newObject.meth()); // 'im a method'
```

### _Object.create_

- Old

## _Accessing properties_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors
- https://repl.it/@hmmrepl/Accessing-and-updating-Object
- There are two ways to access the properties of an object:

### **dot Notation**

- `object.property`
- The dot operator is what you use when you know the name of the property you're trying to access ahead of time

```
`var myObj = {``
``    `prop1: "val1",`
``    `prop2: "val2"`
`};`
`var prop1val = myObj.prop1; // val1`
`var prop2val = myObj.prop2; // val2``
```

### **bracket notation**

- `object['property']`
- Use when you have a variable with a property name that changes dynamically
- Use if the property has a space, dash, or starts with a number
- Expects an expression which evaluates to a string (or can be coerced into one)

```
`var myObj = {``
``    `"Space Name": "Kirk",`
``    `"More Space": "Spock"`
`};`
`myObj["Space Name"]; // Kirk`
`myObj['More Space']; // Spock``
```

- Another use of bracket notation is to use a variable or expression to access a property
  - Useful for iterating through lists of the object properties, or for doing the lookup

```
`var someProp = "propName";``
`var myObj = {`
``    `propName: "Some Value"`
`}`
`myObj[someProp]; // "Some Value"``
```

- Accessing indexes
  - Use to get a character at a specific index within a string or array
- JavaScript starts counting at 0
  - This is referred to as Zero-based indexing

```
var firstName = "Charles";
firstName[0] // C
```

- To target the last index:

```
var firstName = "Charles";
firstName[firstName.length -1] // s
```

- Use Dot notation whenever possible

## _Iterating properties_

- There are three native ways to list/traverse object properties:
- `for / in loops`
  - Traverses all enumerable properties of an object and its prototype chain
- `Object.keys(objectName)`
  - Returns an array with all the own (not in the prototype chain) enumerable properties' names ("keys") of an object `objectName`.
- `Object.getOwnPropertyNames(objectName)`
  - Returns an array containing all own properties' names (enumerable or not) of an object `objectName`.

## _Adding properties_

- `objectName.newProperty = propertyValue;`
- `objectName['newProperty'] = propertyValue;`

* Add a property to a previously defined object type by using the `prototype` property
  - Defines a property that is shared by all objects of the specified type, rather than by just one instance of the object

## _Updating properties_

- https://repl.it/@hmmrepl/Changing-keys-of-Object-using-dot-and-bracket-notation
- `objectName.property = { … };`

```
`people.person = {
  name: {
    first: '',
    last: ''
}`
```

```
`people.person.name.first = "John"
`people`.person.name.last = "Doe"`
```

- Updating multiple properties

```
``objectName`.person.name = {first : "John", last : "Doe"}`
```

## _Removing properties_

- Remove a non-inherited property by using the `delete` operator
  - ` delete ``objectName``.propertyName; `

## _Methods_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions
- A method is a function associated with an object, or, simply put, a method is a property of an object that is a function

```
var myObj = {
    myMethod: function(params) {
        // ...do something
    }

    // OR THIS WORKS TOO

    myOtherMethod(params) {
        // ...do something else
    }
};
```

- To call the method:
  - `myObj.myMethod(params);`

## _Inheritance_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
- All objects in JavaScript inherit from at least one other object
- The object being inherited from is known as the prototype
- The inherited properties can be found in the `prototype` object of the constructor
  - `__proto__`

---

# **_Classes_**

```
class Dog {
    constructor(name) {
        this.name = name;
        this.behavior = 0;
    }
}
```

- Templates for objects
- Use to quickly produce similar objects
- Primarily syntactical sugar over JavaScript's existing prototype-based inheritance
- Semantic sugar for constructor functions
- Create in a separate file and capitalize the file name

## constructor

- `Constructor()`
- The constructor method is called every time a new instance of a class is created
- Inheritance
  - Creates a parent class (superclass) with properties and methods that child classes (subclasses) share

```
class Cat extends Animal {
    constructor(name, usesLitter) {
        super(name);
        this._usesLitter = usesLitter;
    }
}
```

## super

- The `super` keyword calls the constructor of the parent class
- You must always call the `super` method before you can use the `this` keyword

## extends

- The `extends` keyword makes all of the parent properties and methods available to the child class
  - The class extended from is called the Parent or Super class
  - The extended class is call the Sub class
- Child classes can contain their own properties, getters, setters, and methods

## new

- The `new` keyword creates a new instance of the class
- Necessary in order to access methods on the class
- The new keyword uses your object “blueprint” to give `this` meaning

## static

- Use the `static` keyword to create a static method
- Methods that aren't available in individual instances, but that you can call directly from the class

---

# **_Arrays_**

- Arrays are objects whose keys are numbers that start their count at 0
- Arrays have special methods which make it easier to add and remove properties, as well as interact with all of their properties
- Stores lists of data
- Can store different data types at the same time
- Are ordered so the position of each piece of data is fixed
- Each item is counted starting from 0, not 1
- Arrays are mutable and can be changed freely

## _Array literal_

- `var arrayName = [item1, item2, ...];`

```
var` names = [`"Mao"`,`"Gandhi"`,`"Mandela"`];`
var` sizes = [`4`, `6`, `3`, `2`, `1`, `9`];`
var` mixed = [`34`, `"candy"`, `"blue"`, `11`];`
```

## _Multi-dimensional Array_

- An array nested in an array
- `[["Bulls", 23], ["White Sox", 45]]`

---

# **_Functions_**

```
function functionName(parameter) {
    statement;
}
```

- Does something useful
- Returns (produces) a value
  - Functions that don’t return anything, return undefined
- The parameter is a placeholder word that we give a specific value when we call the function
  - Arguments are the real data passed to the parameters
- The statement is the reusable code that is between the curly brackets
- Functions should handle a single responsibility
- Each line of code inside `{ }` must end with a semi-colon

## **_Arrow functions_**

- Shorthand for ECMAScript 5 function syntax
- Best suited for non-method functions
- Cannot be used as constructors

```
// Es5
function() {}
```

```
// Es6
() => {}
```

- Named functions have to be stored in variables
  - `const namedFunction = () => {}`
- Rules for `()`:

  1. If using a single parameter, can omit
  2. If using no parameters, or more than 1 parameters, must use parenthesis

- Rules for `{}` or `return`:

  1. If returning a single expression, can omit
  2. Implicit return only when a single expression is written and no curly brackets are used
  3. Return an object (can also use syntax from ES5 instead of parentheses if more semantic/readable)
  4. Passing in multiple parameters (requires parentheses)
  5. Implicit return only with one parameter
  6. When your function requires more than one line or expression, you must use curly brackets, and if the function returns anything, the return must be written

* Implicit return
  - Only for ES6 arrow functions
  - You can omit the `return` statement when using parens instead of curly brackets
  - Can't use `console.log()`'s because it will try to return it

## _Extended parameter handling_

- Sets default parameter values

```
function f (x, y = 7, z = 42) {
 return x + y + z
 }

f(1) === 50
```

## _Rest parameter_

```
function f (x, y, ...a) {
 return (x + y) * a.length
 }

f(1, 2, "hello", true, 7) === 9
```

## _Generators_

- Generators are functions that can be exited, and then re-entered, and save context (variable bindings) across re-entrances
- Instead of running to completion, they may be paused in the middle, one or many times, and resumed later, allowing other code to run during these paused periods
- Returns an object called the generator iterator
- Must use vanilla function syntax
- Simply calling a generator function (ie: just calling `doSomething()`) doesn’t actually execute its contents, instead it returns a Generator Object
- To command the generator to execute the function and read the next line of code you must use the method `.next()`

```
function* doSomething() {
  yield 'hello world'
  yield 'HAHAHAH'
}

const words = doSomething()

console.log(words.next())
```

## _IIFE_

- Immediately invoked function expressions
- Function is invoked as soon as it is created
- he function itself is enclosed in function scope and unavailable to the global scope

```
(function () {
    statements
})();
```

## _Prototypes_

```
myFunction.prototype.sing = function() {
  console.log('Im singing')
}
```

- Function `sing()` will only be loaded into memory once, instead of being copied for every new instance
- Prototype chain
- Put all methods inside prototype
- `__proto__` is called a dunder proto

---

# _Global functions_

- Built-in functions
- [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval)
  - Evaluates JavaScript code represented as a string
  - `eval('2 + 2') // 4`
  - Do not ever use
- [`uneval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/uneval)
- [`isFinite()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isFinite)
- [`isNaN()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN)
- [`parseFloat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)
- [`parseInt()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

---

# **\_**Statements**\_**

- A unit of code representing one or more instruction
- Usually starts with a language reserved keyword and ends, _explicitly_ or _implicitly_, with a statement terminator semicolon

## _**return**_

- When the return statement is reached, the function will immediately stop, return the value that comes out of the function to that point, and control returns to the calling location
- If you don’t `return` a value at the end of a function, it will return undefined

---

# **\_**Conditionals**\_**

- Controls behavior in JavaScript and determines whether or not pieces of code can run

## _**if statement**_

- Runs the `if` statement when the condition is true

````
`if`` (condition) ``{
```    ``**`// if condition is true
`**``    ``**`// do this code
`**`}`
````

Ex.

````
`if``( ``"myName"``.``length`` >= ``7`` ) {
```    `console.``log``(``"You have a long name!"``);
``}`
````

- Shorthand for single line statments
  - `if (condition) do something;`

## _**if...else**_

- Runs the `if` statement when the condition is true
- Runs the `else` statement when the condition is true

````
`if`` (condition) ``{
```    ``**`// if condition is true
`**``    ``**`// do this code
`**`} ``else`` { `**`// "otherwise"
`****`    // do this code instead
`**`}`
````

- Ex.:

```
if`( `"myName"`.`length` >= `7` ) {`
`    console.`log`(`"You have a long name!"`);`
`} `else` {`
`    console.`log`(`"You have a short name!"`);  `
`}`
```

## _**if...else if...else**_

- Same as `if/else`, but for more than 2 outcomes

```
if` (condition1) {`
`    code code code;`
`} `else` `if` (condition2) {`
`    code code code;`
`} `else` {`
`    code code code;`
`}`
```

## _**for loop**_

- It runs "for" a specific number of times.
- Doing something multiple times and looping through the results
- Every for loop makes use of a counting variable (i) with an initial value, and increments until the condition is no longer true

- `for ([initialization]; [condition]; [final-expression])`
  - **Initialization** is executed once before the loop (statement) starts. The starting point.
    - typically used to define and setup your loop variable.
  - **Condition** defines the condition for running the loop. The stopping point.
    - is evaluated at the beginning of every loop iteration and will continue as long as it evaluates to true.
  - **Final-expression** is executed each time after the loop has been executed. The increment length.
    - will always run the statement first before starting to increment

```
for (let i = 1; i < arr.length; i += 1) {
  /* your code here */
}
```

## _**for...in**_

- Loops through the keys of an object
- A different property name is assigned to `variable` on each iteration

```
for (variable in object) {
  ...
}
```

```
const obj = {a: 1, b: 2, c: 3};

for (const prop in obj) {
  console.log(`obj.${prop} = ${obj[prop]}`);
}
// "obj.a = 1"
// "obj.b = 2"
// "obj.c = 3"
```

## _for...of_

- Loop over the values in an iterable
  - Not objects
- Similar to `.forEach` but works for any iterable
- On each iteration a value of a different property is assigned to `variable`

```
for (variable of iterable) {
  statement
}
```

```
const iterable = [10, 20, 30];

for (let value of iterable) {
  return value += 1;
}
// 11
// 21
// 31
```

```
const arr = ['a', 'b'];

for (const [index, element] of arr.entries()) {
  console.log(`${index}. ${element}`);
}
// 0. a
// 1. b
```

## _**while loop**_

- Creates a loop that executes a specified statement as long as the test condition evaluates to true
- Loops function “as long as” the condition is true
- The condition is evaluated before executing the statement
- Used when you don’t know how long the loop is going to be

```
while (condition) {
  statement
}
```

```
var n = 0;

while (n < 3) {
  n++;
}
```

## _**do...while**_

- Creates a loop that executes a specified statement until the test condition evaluates to false
- Loops through a block of code while a specified condition is true
- The condition is evaluated after executing the statement

```
do
   statement
while (condition);
```

```
var result = "";
var i = 0;

do {
  i = i + 1;
  result = result + i;
} while (i < 5);
```

## _**Switch statement**_

- Tests a value and can have many case statements which defines various possible values
- Statements are executed from the first matched case value until a break is encountered
- Case values are tested with strict equality (`===`)
- The break tells JavaScript to stop executing statements
  - If the break is omitted, the next statement will be executed

```
`switch (num) {
`  `case value1:
`    `statement1;
`    `break;
`  `case value2:
`    `statement2;
`    `break;
 ...
`  `default:
`    `defaultStatement;
 }`
```

## **_Ternary operator_**

- A shortcut for the `if` statement
- Takes three operands
- `condition ? exprTrue : exprFalse`
- Right-associative, which means it can be chained

```
function example(…) {
  return condition1 ? value1
    : condition2 ? value2
      : condition3 ? value3
        : value4;
}

// Equivalent to:
function example(…) {
  if (condition1) { return value1; }
  else if (condition2) { return value2; }
  else if (condition3) { return value3; }
  else { return value4; }
}
```

---

# **_Hoisting_**

- Function declarations are hoisted to the beginning of the document so you can call them at the beginning of your code
- Variable names are hoisted, not the value or function
- Function expressions are not hoisted

---

# **_Scope_**

- Refers to where variables and functions are accessible, and in what context it is being executed
- [_https://repl.it/@hmmrepl/variable-scope_](https://repl.it/@hmmrepl/variable-scope)

- Execution scope:

## _global_

- Default, everyone has access
- Variables defined outside of a function are accessible anywhere once they have been declared
  - Stored in memory for as long as the web page is loaded
  - Bad practice

## _local_

- Variables defined inside a function cannot be accessed outside of that function
  - If the variable is locally scoped, then two different functions can use the same variable name without a naming conflict
  - They are created when the function is run, and removed when it is done

## _function_

- variables which are created in the function only exist in that function

## _block_

- Only exists in the block they are defined in
- if & for statements (const & let)

---

# _This_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this
- The only time the value of `this` can change is when an ES5 keyword function or ES6 class function is executed
- By default `this` refers to the global object (i.e. window)

- Rules when `this` changes:

  - when calling a keyword function as a property/method of an object
  - new keyword => new object instance
  - Methods call, apply, bind

- `.call`, `.apply`, `.bind` set the context of _this_
  - .`call`, `.apply` are invoked immediately
  - `.bind` can saved to a variable
- Regular functions - `this` is set when the function is called or executed

  - because of this fact we can change what the value of `this` will be inside of ES5 functions

- Arrow functions - `this` is set at the time the function is created
  - `this` is set to whatever the current value of `this` is in its current scope
  - because of this fact `this` will always be the same inside of this function and we can never change the value of it after it is created.
- React
  - the `this` object from the component will be automatically transferred to the method
  - so it won't create it's own this object

## bind

- Creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called
- `fun.bind(thisArg[, arg1[, arg2[, ...]]])`

```
this.x = 9;    // this refers to global "window" object here in the browser
var module = {
  x: 81,
  getX: function() { return this.x; }
};

module.getX(); // 81

var retrieveX = module.getX;
retrieveX();
// returns 9 - The function gets invoked at the global scope

// Create a new function with 'this' bound to module
// New programmers might confuse the
// global var x with module's property x
var boundGetX = retrieveX.bind(module);
boundGetX(); // 81
```

---

# **_Get_**

- Binds an object property to a function that will be called when that property is looked up
  - `{ get prop() { ... } }`
  - `{ get [expression]() { ... } }`

---

# **_Set_**

- Binds an object property to a function to be called when there is an attempt to set that property
  - `{ set prop(val) { . . . } }`
  - `{ set [expression](val) { . . . } }`

---

# **_Template literal_**

- Strings that allow embedded expressions
- `const tempLit = ``My name is \$(varName).```
- Same as `'My name is' + varName + '.'`

## Tagged Template Literals

- One feature that comes along with template literals is the ability to tag them
- Run a template string through a function, and rather than have the browser immediately assign that value to a variable, we can have control over how this actual string is made
- Simply make a function, and you take the name of the function that you want to run against the string, and you just put the name right in front of the template

```
function highlight() {
  // do something
}

const name = 'Snickers';
const age = '100';
const sentence = highlight`My dog's name is ${name} and he is ${age} years old`;
console.log(sentence)
```

- Whatever we return from `highlight()` is what `sentence` actually is going to be

---

# **_Destructuring_**

- An expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables
- Helps define variables pulled out of objects, as in the following code:
  - Array destructuring

```
var foo = ['one', 'two', 'three'];
var [one, two, three] = foo;
console.log(one); // "one"
console.log(two); // "two"
console.log(three); // "three"
```

    * Object destructuring

```
var o = {p: 42, q: true};
var {p, q} = o;
console.log(p); // 42
console.log(q); // true
```

- Reassigning values

```

```

- Reorder values in arrays

```
var list = [ 1, 2, 3 ]
[ list[0], list[2] ] = [ list[2], list[0] ]
```

---

# _Callbacks_

- A function that is passed to another function as a parameter, and called by that other function

- "`doSomething`" below is a callback function:

```
function doSomething() {
  console.log("doing something!");
}

setTimeout(doSomething, 5000);
```

- Problems with async callbacks:
  - callback hell
    - needing async callbacks to happen in order
  - race
    - give me the first one
  - all
    - give me all of them
  - Inversion of control
  - A solution is Promises

---

# _Chaining_

- A technique that can be used to simplify code in scenarios that involve calling multiple functions on the same object consecutively

```
class Calculator {
    constructor() {
        this.total = 0;
    }

    add(num) {
        this.total += num;
        return this;
    }

    minus(num) {
        this.total -= num;
        return this;
    }

    divide(num) {
        this.total = this.total / num;
        return this;
    }

    result() {
        return this.total;
    }
}

var cal = new Calculator();
cal.add(10).add(20).minus(2).divide(2);
console.log(cal.result()); // 14
```

---

# _Recursion_

- https://repl.it/@hmmrepl/Recursive-Functions

- A technique for iterating over an operation by having a function call itself repeatedly until it arrives at a result
- Best applied when you need to call the same function repeatedly with different parameters from within a loop
- Most effective for solving problems involving iterative branching, such as fractal math, sorting, or traversing the nodes of complex or non-linear data structures
- Allows for the construction of code that doesn’t require setting and maintaining state with local variables

- Every recursive function (again, just a function that calls itself) must have these two pieces:

1. A simple base case (or cases)
   1. A terminating scenario that does not use recursion to produce an answer
2. A set of rules that reduce all other cases toward the base case

- One of the most basic patterns of recursion is when you can reduce a problem to a smaller one and then keep reducing until you can't do it anymore
  - This is also known as natural recursion

---

# _Import/Export_

- Import
  - default imports
    - `import defaultExport from "module-name/path";`
  - named imports
    - `import { export } from "module-name`/path`";`
  - import all the exported functions of a file
    - `import * as name from "module-name`/path`";`
  - `import { export as alias } from "module-name`/path`";`
  - `import { export1 , export2 } from "module-name`/path`";`
  - `import { export1 , export2 as alias2 , [...] } from "module-name`/path`";`
  - `import defaultExport, { export [ , [...] ] } from "module-name`/path`";`
  - `import defaultExport, * as name from "module-name`/path`";`
  - `import "module-name`/path`";`
  - Imported modules are in [`strict mode`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) whether you declare them as such or not

* Export
  - default
    - `export default myClass`
    - `export default { myFun1,`myFun1 `}`
  - named exports
    - `export function myFunction() {}`

---

# _Call Stack_

- Data structure that records where in the code execution we are
- First in, last out

---

# _Stack Trace_

- State of the stack when an error happens
- Heap
  - Where memory is allocated

---

# _Hooks & Iteration_

---

# _Events_

- Event-driven responses on page elements, such as when text is entered into a form element or the mouse pointer is moved
- In some cases, such as the page load and unload events, the browser itself will trigger the event

## Propagation

- Phases:

  1. Capture
  2. Target
  3. Bubbling

## Delegation

- A method for managing event listeners
- Allows us to attach a single event listener, to a parent element, that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future
- `event.target.tagname`

* event handler
* event listener

---

# _Asynchronous_

- JavaScript is single-threaded, meaning code is read and executed line-by-line

## Synchronous

- Happens one after another
- I order my food, everyone in the restaurant has to wait until I get my food before the next person can order
  - `|<----A---->||<-----B--------->||<----C-------------->|`
- Blocking
  - Code that slow and prevents other code from running
    - Image loading
    - Requesting and sending data
    - Event handlers

## Asynchronous

- Happens concurrently, out of order
- Like, a normal restaurant experience where you’d tip the server at least 20%
  - `|<-----------------A---------------------------->| |<------------B---------------------------------->| |<----C-------------->|`
- Callbacks
  - Fundamental async units
  - Unreliable

## AJAX

- [Asynchronous JavaScript And XML](https://developer.mozilla.org/en-US/docs/AJAX)
- The method of exchanging data with a server, and updating parts of a web page – without reloading the entire page

---

# _Promises_

- An object representing the eventual completion or failure of an asynchronous operation, and its resulting value
- Allows us to start an asynchronous process in the background and respond to its result when it becomes available
- Solves the issue of callbacks blocking the callstack

* If you wanted to chain two or three actions together:
  - After the first action is completed
  - The second action uses the result and runs
  - Then the third action runs based on the result of the second action
  - You would end up with a bunch of nested callbacks
    - Which is commonly known as "callback hell”
* Promises are a good solution to improve readability and usability

- 3 states:
  - Pending
    - returns undefined
  - Fulllfilled
    - resolved
    - returns value from async operation
  - Rejected
    - returns error message

## _Methods_

- `.then()`
  - Allows you to react to the promise
  - Executed when the promise is resolved
  - Takes a callback
  - The argument resolves the previous promise
  - Returns a new promise
  - Chaining another `.then()` will be called on a new unresolved promise
  - Each `then` receives the result of the previous `then`'s return value
- `.catch()`
  - Executed when the promise is rejected
  - For error handling
  - Returns a new promise
  - The error will be the argument of the callback
- `.finally()`
  - Takes a callback
  - When you want something to happen regardless of result

* `Promise.race()`
  - Returns the first promise that either resolves or rejects
  - Triggers as soon as any promise in the array is resolved or rejected
  - Can use for fetching the same data from multiple resources
* `Promise.all()`
  - When you trigger multiple async interactions but only want to respond when all of them are completed
  - Takes an array of unresolved promises
  - Returns a single `Promise` that resolves when all of the promises in the `iterable` argument have resolved
    - or when the iterable argument contains no promises
    - in the same order of the promises in the iterable
  - If any promise is rejected, the `catch` fires with the reason for the first rejection

- `Promise.resolve()`
  - Creates a promise with a resolved state
  - Resolves to a value
  - Returns promise object with status of fullfilled
- `Promise.reject()`
  - Creates a promise with a rejected state
  - Returns the reason for the rejection
  - Error is accessed with a `catch`

* `new Promise()`
  - The `new Promise()` constructor should only be used for legacy async tasks, like usage of `setTimeout` or `XMLHttpRequest`
  - Provides `resolve` and `reject` functions to the provided callback

```
// Resolves
new Promise(function(resolve, reject) {
  // A mock async action using setTimeout
  setTimeout(function() {
    resolve(10);
  }, 3000);
})

  // The then method callback receives the
  // result given to it by the resolve() call
  .then(function(result) {
    console.log(result);
  });

// From the console:
// 10
```

```
// Rejects
new Promise(function(resolve, reject) {
  // A mock async action using setTimeout
  setTimeout(function() {
    reject(Error('Done!'));
  }, 3000);
})
.then(function(e) { console.log('done', e); })
.catch(function(e) { console.log('catch: ', e); });

// From the console:
// 'catch: Done!'
```

```
// Resolves or Rejects
const p = new Promise(function(resolve, reject) {

  // Do an async task, async task, and then...

  // Call resolve or reject within the body of the
  // callback based on the result of their given task
  if(/* good condition */) {
    resolve('Success!');
  }
  else {
    reject('Failure!');
  }
});

p.then(function() {
  /* do something with the result */
}).catch(function() {
  /* error :( */
})
```

---

# _Async/Await_

- Used to wait for a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise). It can only be used inside an [`async function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- Inside a function marked as async, you are allowed to place the await keyword in front of an expression that returns a promise. When you do, the execution of the async function is paused until the promise is resolved
- async functions will always return a promise
- By using async on a function, the function gets wrapped in a promise

```
const url = `https://api.github.com/users/${handle}`

// ES5
async function makeFetch(url) {
  const response = await fetch(url);
  return await response.json();
}

// ES6
const makeFetch = async (url) => {
  const response = await fetch(url);
  return await response.json();
}
```

---

# _Event loop_

- If the stack is empty, pushes callback from task queue into the stack
- First in, first out
- Steps:

1. a function runs
2. it gets put on the callstack as a stackframe
3. async functions get moved to heap
4. heap items move to task queue when complete
5. when call stack is complete
6. the event loop will move items from queue to the callstack

---

# **_Misc_**

- To link to a JavaScript file:
  - `<script type="text/javascript" src="main.min.js"></script>`
  - place at the bottom of the `<body>` tag

---
