# _PHP_

http://www.w3schools.com/php/default.asp

http://php.net/manual/en/

---

Comments:
PHP // this syntax

**_Syntax:_**
**\_** **\_**
**operators:**
scope resolution: to access constants
` MyClass::``$property``; `
`MyClass::myMethod();`

Variable: $variableName;
Array: $variableName = array("do", "re", "mi");

Operators: http://www.w3schools.com/php/php_operators.asp

_echo_

```
`  `echo` `"Hello!"`;`
```

_if_

```
`  `$age` = `17`;`
` `
`  `if`( `$age` > `16` ) {`
`    `echo` `"You can drive!"`;`
`  }`
```

\_ \_
_if / else_
` ```$name ` = `"Edgar"`;`` ` `` ```if`` (``$name`` == ``"Simon"``) { `
` ```print ` `"I know you!"`;` `` `}` `` ```else`` { `
` ```print ` `"Who are you?"`;` `` `}`

if/elseif/else

```
if` (`condition`) `{

}` `elseif` (`condition`) `{

}` `else` `{

}
```

switch

```
switch` (X) {`
`    `case` X:`
` `
`        `break`;`
`    `default`:`
` `
`}`

```

`// Example:`

```
$myNum` = `2`;`
` `
switch` (`$myNum`) {`
`    `case` `1`:`
`        `echo` `"1"`;`
`        `break`;`
`    `case` `2`:`
`        `echo` `"2"`;`
`        `break`;`
`    `case` `3`:`
`        `echo` `"3"`;`
`        `break`;`
`    `default`:`
`        `echo` `"None of the above"`;`
`}`
```

**_Loops:_**

for
` for`` (``$i`` = ``0``; ``$i`` < ``101``; ``$i`` = ``$i`` + ``10``) { `
` ```echo ` `$i`;``}`

foreach
` ```$numbers ` = `array`(`1`, `2`, `3`);`` ` `` ```foreach``(``$numbers`` ``as`` ``$item``) { `
` ```echo ` `$item`;` `` `}`

while
` while``(``2`` > ``1``){ `
``**`// Code`**
`}`
``
`// Example:`
` $loopCount`` = ``0``; `
` while`` (``$loopCount``<``4``){ `
` ```echo ` `"<p>Iteration number: {`\$loopCount`}</p>"`;` `` ```$loopCount`` ++; `
`}`

do/while
` do`` { `
`` `// looped statements ``go`` here` `} while (cond); ` ` ` `// Example:` `$i `` = `0`;``do`` {` `` ``echo` `$i`;``} `while` (`$i` > `0`);`

print –
print_r –
return - returns a value that we can work with, but it doesn't actually display the value
new –
unset –
extends - causes one class to inherit from another. Creates a subclass of a superclass
` class`` Immortal ``extends`` Person { `
`}`

final - control what methods can be modified by a class' subclasses

```
final` `public` `function` drive() {`
`}`
```

const - variables that don't change. Does not start with \$

```
const` alive = `true`;`
```

static - lets you use a class' property or method without having to create an instance of that class

```
public` `static` `function` greet() {`
`}`
```

**_Functions:_**
` function`` name(parameters) { `
`` `statement;`
`}`

**\_String Functions:** **\_**[**http://www.w3schools.com/php/php_ref_string.asp**](http://www.w3schools.com/php/php_ref_string.asp)

**strlen()** - it returns the number of characters in that string
` $length`` = strlen(``"david"``); `
` print`` ``$length``; `

```
**// prints "5”**
```

**substr()** - allows you to return a substring (piece of) of your string

```
$myname` = `"David"`;`
$partial` = substr(`$myname`, `0`, `3`);`
print` `$partial`;`
**// prints "dav"**
```

**strtoupper()** - makes your entire string UPPERCASE

```
$myname` = `"David"`;`
$uppercase` = strtoupper(`$myname`);`
print` `$uppercase`;`
**// prints "DAVID"**
```

**strtolower()** - makes your entire string lowercase

```
$myname` = `"David"`;`
$lowercase` = strtolower(`$uppercase`);`
print` `$lowercase`;`
**// prints "david"**
```

You can also call these functions on a string directly, like so:

```
print` strtolower(`"David"`);`
**// prints "david"**
```

**strpos()** - finds the position of the first occurrence of a substring in a string

```
`strpos(`"emily"`, `"e"`);   `**// 0**
`strpos(`"emily"`, `"i"`);   `**// 2**
`strpos(`"emily"`, `"ily"`); `**// 2**
`strpos(`"emily"`, `"zxc"`); `**// false**

```

`// Example:`

```
if` (strpos(`"david"`,`"h"`) === `false`) {`
`  `print` `"Sorry, no 'h' in 'david'"`;`
`}`
** **
```

**\_Math Functions:** **\_**[**http://www.w3schools.com/php/php_ref_math.asp**](http://www.w3schools.com/php/php_ref_math.asp)

**round()** - rounds floating point numbers (numbers with decimal points in them) up or down

```
$round_decimal` = round(3.14159, `4`);`
print` `$round_decimal`; `**// prints 3.1416**
```

**rand()** - returns a random number between two numbers

```
**// prints a number between 0 and 32767**
print` rand();`
` `
**// prints a number between 1 and 10**
print` rand(`1`,`10`);`
```

---

**_Array Functions:_**http://www.w3schools.com/php/php_ref_array.asp

**array_push()** - takes two arguments: an array, and an element to add to the end of that array

```
$fav_bands` = `array`();`
`array_push(`$fav_bands`, `"Maroon 5"`);`
`array_push(`$fav_bands`, `"Bruno Mars"`);`
`array_push(`$fav_bands`, `"Nickelback"`);`
`array_push(`$fav_bands`, `"Katy Perry"`);`
`array_push(`$fav_bands`, `"Macklemore"`);`
```

**count()** - will return the number of elements in that array

```
print` count(`$fav_bands`); `**// prints 5**
```

**sort()** - sorts an array
` $array`` = ``array``(``5``, ``3``, ``7``, ``1``); `
` sort(``$array``); `
` print`` join(``", "``, ``$array``); `
**`// prints "1, 3, 5, 7"`**

**rsort()** - sorts in reverse

```
$array` = `array`(`5`, `3`, `7` ,`1`);`
`rsort(`$array`);`
print` join(`":"`, `$array`);`
**// prints "7:5:3:1"**
```

**join(glue, array)** - print out the representations of our sorted arrays
` print`` join(``", "``, ``$array``); `

**_Object/Class Methods:_**

is_a() - see if a particular object is an instance of a given class

property_exists() - see if an object has a given property
` property_exists(``$myObj``, ``"property"``); `

method_exists() - see if an object has a given method

**_Objects: _**[**http://php.net/manual/en/language.oop5.php**](http://php.net/manual/en/language.oop5.php)

Classes - object constructor, bundles our functions and data in one place
` class`` Classname { `
`property`
`}`
``
`Example:`
` class`` Fruit { `
` ```public ` `$count` = `3`;` `` ```public`` ``$type``; `
`}`

Methods - a function bound to a class
` public`` ``function`` funcname(``$optionalParameter``) { `
``**`// Do something`**
`}`
``
`Magic example:`

```
`__construct: must use “$this”`
public` `function` __construct(`$prop1`, `$prop2`) {`
`  `$this`->prop1 = `$prop1`;`
`  `$this`->prop2 = `$prop2`;`
`}`
```

Instances - objects, which have been constructed via a class

```
$obj1 = new Classname();
echo $obj1->prop1;

Magic example:
$apple` = `new` Fruit();`
$apple`->type = `"apple"`;`
print` `$apple`->count; `**// 3**
print` `$apple`->type;  `**// apple**
```

**_Arrays:_** useful way to store multiple values, like numbers, strings, and even other arrays

```
$myArray` = `array`(`0`, `1`, `2`);`
`Or:`
$myArray`[`0`] = `"value0"`;`
$myArray`[`1`] = `"value1"`;`
$myArray`[`2`] = `"value2"`;`
` `
To access:
echo` `$myArray[key];
```

**_Associative Arrays (map):_** the same as a normal array, but instead of using an integer to refer to the value, you use a defined key
` 'key'`` => value `
` $me`` = ``array``(``'hair'`` => ``'black'``, ``'skin tone'`` => ``'light'``); `
``

```
To access:
echo` `$myAssocArray`[`'key'`];`
```

**_Multidimensional Arrays:_**

```
$deck` = `array`(`array`(`'2 of Diamonds'`, `2`),`
`              `array`(`'3 of Diamonds'`, `3`),`
`              `array`(`'5 of Diamonds'`, `5`),`
`              `array`(`'7 of Diamonds'`, `7`));`
To access:
echo` `$deck`[`2`][`0`];`
```

**\_** **\_**
**\_** **\_**
**\_** **\_**
**_Mail:_**
mail ($emailTo, $subject, $body, $headers)

**_Superglobals:_**
\$\_GET: Information sent from a form with the GET method is visible to everyone (all variable names and values are displayed in the URL). Because the variables are displayed in the URL, it is possible to bookmark the page.

\$\_POST: Information sent from a form with the POST method is invisible to others (all names/values are embedded within the body of the HTTP request). Developers prefer POST for sending form data.
