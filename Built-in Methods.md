# _Built-in Methods_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects
- code example syntax `[ ]` means optional

---

# _Array_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array

## _\_\_Properties_

## `length`

- Sets or returns the number of elements in that array
- ` myArray``.length `

## `isArray`

- Determines whether the passed value is an array
- `Array.isArray(obj)`

## `from`

- Creates a new `Array` instance from an array-like or iterable object
- `Array.from()`

## `of`

- Creates a new `Array` instance with a variable number of arguments, regardless of number or type of the arguments
- `Array.of()`

## **_\_\_Mutator_**

- Directly modifies an existing array

## `fill`

- Fills all the elements of an array from a start index to an end index with a static value
- Returns the modified array
- ``myArray`.fill(value[, start[, end]])`

```
const myArr = [1, 2, 3]

const newArr = myArr.fill(4) // [4, 4, 4]
const newArr = myArr.fill(4, 1) // [1, 4, 4]
const newArr = myArr.fill(4, 1, 2) // [1, 4, 3]
const newArr = myArr.fill(4, 1, 1) // [1, 2, 3]
const newArr = myArr.fill(4, -3, -2) // [4, 2, 3]
const newArr = Array(3).fill(4) // [4, 4, 4]
const newArr = [].fill.call({length: 3}, 4) // {0: 4, 1: 4, 2: 4, length: 3}
```

```
// Objects by reference
const newArr = Array(3).fill({})
// [{}, {}, {}]

newArr[0].hi = 'hi'
// [{hi: "hi"}, {hi: "hi"}, {hi: "hi"}]
```

## `**pop**`

- Removes the last index of an array
- Returns the removed element
- Changes the length of the array
- Must store the return value by assigning it to a variable
- `var removedFromMyArray = myArray.pop()`

```
const myArr = [1, 2, 3]

const popped = myArr.pop()

// 3
```

## `**push**`

- Adds one or more elements to the end of an array
- Returns the new length of the array
- `myArray.push(element1[, ...[, elementN]])`

```
const myArr = [1, 2, 3]

myArr.push(4)

// [1, 2, 3, 4]
```

## `**reverse**`

- Reverses the elements of an array
- Alters the array in place
- Returns the reversed array
- ``myArray`.reverse()`

```
const myArr = [1, 2, 3]

myArr.reverse()

// [3, 2, 1]
```

## `**shift**`

- Removes the first element from an array
- Returns the removed element
- Returns `undefined` if the array is empty
- Often used in the condition of a while loop, which will run until the array is empty
- Must store the return value by assigning it to a variable
- `myArray.shift()`

```
const myArr = [1, 2, 3]

const shifted = myArr.shift()

// 1
```

## `**sort**`

- Sorts the elements of an array
- Alters the array in place
- Returns the sorted array
- `myArray.sort([compareFunction])`

```
const myArr = [13, 1, 6]

myArr.sort((a, b) => {
  return a - b
})

// [1, 6, 13]
```

## `splice`

- Changes the contents of an array by removing existing elements and/or adding new elements
- Returns an array containing the deleted elements
- Start is the index at which to start changing the array
- If the start index is greater than the length of the array, the start index is set to the length of the array
- A negative index can be used, indicating an offset from the end of the sequence
- `myArray.splice(start[, deleteCount[, item1[, item2[, *...]]]]*)`

```
const myArr = [1, 2, 3]

// insert
myArr.splice(2, 0, 2.5)
// [1, 2, 2.5, 3]

// delete
myArr.splice(1, 1)
// [1, 3]

// replace
myArr.splice(1, 1, 'two')
// [1, 'two', 3]
```

## `**unshift**`

- Adds one or more elements to the beginning of an array
- Returns the new length of the array
- `myArray.unshift(element1[, ...[, elementN]])`

```
const myArr = [1, 2, 3]

myArr.unshift(0)

// [0, 1, 2, 3]
```

## _\_\_Accessor_

- Returns a new value or particular representation of an array
- Does not modify existing array

## `**concat**`

- Merges the contents of two or more arrays into one
- Takes an array as an argument
- Returns a new array
- `var newArray = oldArray.concat(value1[, value2[, ...[, valueN]]])`

```
var array1 = [1, 2, 3]
var array2 = [4, 5, 6]

var newArray = array1.concat(array2)

// [1, 2, 3, 4, 5, 6]
```

## `indexOf`

- Returns the first index at which a given element can be found in the array
- Returns `-1` if it's not present
- `myArray.indexOf(searchElement[, fromIndex])`

```
const haystack = ['hay', 'needle', 'stack']

haystack.indexOf('needle')

// 1
```

## `**join**`

- Joins each element of an array into a string
- Elements are separated by whatever delimiter provided as an argument
- Returns a string with all array elements joined
- `myArray.join([separator])`

```
var elements = ['Fire', 'Wind', 'Rain']

elements.join()
// Fire,Wind,Rain

elements.join('')
// FireWindRain

elements.join(', ')
// Fire, Wind, Rain
```

## `lastIndexOf`

- Returns the index number of the last instance of an element
- Returns `-1` if it's not present
- `myArray.indexOf(searchElement[, fromIndex])`

```
const fish = [ "piranha", "barracuda", "koi", "barracuda" ];

fish.indexOf("barracuda");

// 3
```

## `slice`

- Returns a portion of an array into a new array
- `begin` is the starting index
- `end` is not included in the new array
- A negative index can be used, indicating an offset from the end of the sequence
- `myArray.slice([begin[, end]])`

```
var myArr = [1, 2, 3, 4, 5]

const newArr = myArr.slice(2)
// [3, 4, 5]

const newArr = myArr.slice(1, 4)
// [2, 3, 4]

const newArr = myArr.slice(2,-2)
// [ 3 ]
```

## _\_\_Iterater_

- Loops through the elements of an array
- May mutate values, or return some other result, based on what information you're trying to retrieve from the array
- Assign the method to a variable to capture the result (except `.forEach`)
- Requires a return keyword (except `.forEach`)
- They all take a callback function
- They all have to the optional parameters of element, index, and array

## `every`

- Tests whether all elements in the array pass the test implemented by the provided function
- Returns `true` if the callback function returns a truthy value for every array element, otherwise `false`
- `myArray.every(callback[, thisArg])`

```
const myArr = [1, 2, 3]

myArr.every(element => {
  return element < 4
})

// true
```

## `forEach`

- Executes a provided function once for each array element
- Returns `undefined`
  - Even if `return` keyword is used
- Can not use `return` keyword
- `myArray.forEach(function callback(currentValue[, index[, array]]) { // your iterator }[, thisArg])`

```
const myArr = [0, 'one', 2]

myArr.forEach(element => {
  console.log(element)
})

// logs 0
// logs one
// logs 2
```

## `filter`

- Creates a new array with all elements that pass the test implemented by the provided function
- Returns a new array with the elements that pass the test
- The expression in the callback must evaluate to `true` or `false`
- Can be used to filter out elements where a given condition is `true` or not `true`
- Elements for which the callback returns `true` will be kept
- Elements that return `false` will be filtered out
- `var newArray = myArray.filter(callback[, thisArg])`

```
const myArr = [0, 'one', 2]

const newArr = myArr.filter(element => {
  return element !== 0
})

// ['one', 2]


// only return trues
const countSheeps = arrTrueOrFalse=> {
  return arrayOfSheeps.filter(Boolean);
}
```

## `find`

- Returns the value of the first element in the array that satisfies the provided testing function
- Otherwise `undefined` is returned
- The expression in the callback must evaluate to `true` or `false`
- `myArray.find(callback[, thisArg])`

```
const myArr = [0, 'one', 2]

const newArr = myArr.find(element => {
  return element === 'one'
})

// 'one'
```

## `findIndex`

- Returns the index of the first element in the array that satisfies the provided testing function
- Otherwise `-1` is returned
- The expression in the callback must evaluate to true or false
- `arr.findIndex(callback[, thisArg])`

```
const myArr = [1, 2, 3, 4]

const newArr = myArr.findIndex(element => {
    return element > 2
})

// 2
```

## `includes`

- Determines whether an array includes a certain element
- Returns `true` or `false`
- `myArray.includes(searchElement[, fromIndex])`

```
const myArr = [1, 2, 3]

myArr.includes(2)
// true

myArr.includes(1, 2)
// false
```

## `**map**`

- Creates a new array with the results of calling a provided function on every element in the calling array
- Returns result of each iteration into a new array
- Values are modified by the callback function and added to a new array that map returns
- `var new_array = myArray.map(function callback(currentValue[, index[, array]]) { // Return element for new_array }[, thisArg])`

```
const myArr = [1, 2, 3]

const newArr = myArr.map(val => {
  return val * 4
})

// [4, 8, 12]
```

```
const kvArr = [
  { key: 1, value: 10 },
  { key: 2, value: 20 },
  { key: 3, value: 30 },
]

const newArr = kvArr.map(obj => {
  const newObj = {}
  newObj[obj.key] = obj.value
  return newObj
})

// [{1: 10}, {2: 20}, {3: 30}]
```

```
const allCase = ['Red', 'Green', 'Blue']

const lowCase = allCase.map(val => {
  if (typeof val === 'string') {
    return val.toLowerCase()
  } else {
    return val
  }
})

// ['red', 'green', 'blue']
```

## `reduce`

- Applies a function against an accumulator and each value of the array, to reduce it to a single value
- Returns the value that results from the reduction
- Must return the accumulator
- The single value can be any data type
- The first parameter of the callback function is always an accumulator
- The accumulator accumulates the callback's return values
- The accumulator starting value goes after the callback function
- The `initialValue` sets a value to use as the first argument to the first call of the `callback`
- `myArray.reduce(callback, [initialValue])`

```
const myArr = [4, 0, -1]

const sumTotal = myArr.reduce((total, val) => {
  return total += val
}, 0)

// 3
```

```
const myArr = [[-1], [5.2], [4, 2]]

const valArr = myArr.reduce((sumArr, val) => {
  val.forEach((element) => {
    sumArr.push(element)
  })
  return sumArr
}, [])

// [-1, 5.2, 4, 2]
```

```
// shorthand
numbers.reduce((sum, num) => sum + num, 0)
```

## `some`

- Tests whether at least one element in the array passes the test implemented by the provided function
- Returns `true` if the callback function returns a truthy value for any array element, otherwise `false`
- `myArray.some(callback[, thisArg])`

```
const myArr = [1, 2, 3]

myArr.some(element => {
  // check if even
  return element % 2 === 0
})

// true
```

## _\_\_Other_

- [`entries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/entries)
- [`keys()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)
- [`values()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/values)
- [`copyWithin()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin)
- [`lastIndexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf)
- [`reduceRight()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/ReduceRight)
- [`toLocaleString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toLocaleString)
- [`toSource()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toSource)
- [`toString()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toString)

---

# _Object_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object

## _\_\_Methods_

## `assign`

- Copies the values of all enumerable own properties from one or more source objects to a target object
- `Object.assign(target, ...sources)`
- The latter source Object values take precedence

## `keys`

- Returns an array of a given object's own property names
- `Object.keys(obj)`

## `**values**`

- Returns an array of a given object's own enumerable property values
- `Object.values(obj)`

## `**entries**`

- Returns an array of a given object's own enumerable property `[key, value]` pairs
- `Object.entries(obj)`

## `fromEntries`

- Transforms a list of key-value pairs into an object
- `Object.fromEntries(iterable)`

---

# **_String_**

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String

## **_\_\_Properties_**

## `**length**`

- Returns the number of characters in a string
- `str.length`
- You can get the value of the last letter of the string by using `firstName[firstName.length - 1]`

## _\_\_Methods_

## `**charAt**`

- Returns the specified character from a string
- `character = str.charAt(index)`

## `includes`

- Determines whether one string may be found within another string
- Returns `true` or `false`
- `str.includes(searchString[, position])`

## `indexOf`

- Returns the index within the calling `String` object of the first occurrence of the specified value
- Returns `-1` if the value is not found
- `str.indexOf(searchValue[, fromIndex])`

## `lastIndexOf`

- Returns the index within the calling `String` object of the last occurrence of the specified value
- Returns `-1` if the value is not found
- `str.lastIndexOf(searchValue[, fromIndex])`

## `match`

- Retrieves the matches when matching a string against a regular expression
- `str.match(regexp)`

## `padStart`

- Pads the start of the current string with another string (multiple times, if needed) until the resulting string reaches the given length
- `str.padStart(targetLength [, padString])`

## `padEnd`

- Pads the end of the current string with a given string (repeated, if needed) so that the resulting string reaches a given length
- `str.padEnd(targetLength [, padString])`

## `repeat`

- Constructs and returns a new string which contains the specified number of copies of the string
- `str.repeat(count)`

## `**replace**`

- Returns a new string with some or all matches of a pattern replaced by a replacement
- `str.replace(regexp|substr, newSubstr|function)`

## **`search`**

- Executes a search for a match between a regular expression and this `String` object
- `str.search(regexp)`

## `**slice**`

- Extracts a section of a string and returns a new string
- A negative index can be used, indicating an offset from the end of the sequence
- `str.slice(beginIndex[, endIndex])`

## `**split**`

- Splits a string into an array of strings
- Uses a specified separator string to determine where to make each split
- `str.split([separator[, limit]])`

## `startsWith`

- Determines whether a string begins with the characters of a specified string
- Returns `true` or `false`
- `str.startsWith(searchString[, position])`

## `endsWith`

- Determines whether a string ends with the characters of a specified string
- Returns `true` or `false`
- `str.endsWith(searchString[, length])`

## `**substring**`

- Returns the part of the `string` between the start and end indexes, or to the end of the string
- `str.substring(indexStart[, indexEnd])`

## `toLowerCase`

- Returns the calling string value converted to lower case
- `str.toLowerCase()`

## `toUpperCase`

- Returns the calling string value converted to uppercase
- `str.toUpperCase()`

## `trim`

- Removes whitespace from both ends of a string
- `str.trim()`

## `trimStart`

- Removes whitespace from the beginning of a string
- `str.trimStart()`

## `trimEnd`

- Removes whitespace from the end of a string
- `str.trimEnd()`

---

# _Number_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number

## _\_\_Methods_

## `isInteger`

- Determines whether the passed value is an integer
- `Number.isInteger(value)`

## `isNaN`

- Determines whether the passed value is `NaN` and its type is `Number`
- `isNaN()`
- `Number.isNaN(value)`

## `parseFloat`

- Parses a string argument and returns a floating point number
- `parseFloat()`
- `Number.parseFloat(string)`

## `parseInt`

- Parses a string argument and returns an integer of the specified radix or base
- `parseInt()`
- `Number.parseInt(string,[ radix ])`

## `toFixed`

- Formats a number using fixed-point notation
- `numObj.toFixed([digits])`

## `toPrecision`

- Returns a string representing the `Number` object to the specified precision
- `numObj.toPrecision([precision])`

## `toString`

- Returns a string representing the specified `Number` object
- `numObj.toString([radix])`

## `toLocaleString`

- Returns a string with a language-sensitive representation of this number
- `numObj.toLocaleString([locales [, options]])`

```
const formatPrice = (cents) => {
  return (cents / 100).toLocaleString('en-US', {
    style: 'currency',
    currency: 'USD'
  });
}
```

---

# _Math_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math

## _\_\_Methods_

## `abs`

- Returns the absolute value of a number
- `Math.abs(x)`

```
Math.abs('-1');     // 1
Math.abs(-2);       // 2
Math.abs(null);     // 0
Math.abs('');       // 0
Math.abs([]);       // 0
Math.abs([2]);      // 2
Math.abs([1,2]);    // NaN
Math.abs({});       // NaN
Math.abs('string'); // NaN
Math.abs();         // NaN
```

## `floor`

- Rounds any value down to its nearest whole number
- `Math.floor(x)`

## `ceil`

- Rounds any value up to its nearest whole number
- `Math.ceil(x)`

## `round`

- Rounds any value to its nearest whole number
- `Math.round(x)`

## `random`

- Generates a random decimal number between 0 (inclusive) and not quite up to 1 (exclusive)
- `Math.random()`
- Multiply by your maximum desired result to get the random number
- To produce a random number:
  - `Math.floor(Math.random() * 100);`

## `min`

- Returns the number with the lowest value
- `Math.min([value1[, value2[, ...]]])`

## `max`

- Returns the number with the highest value
- `Math.max([value1[, value2[, ...]]])`

---

# _Date_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date

## _\_\_Methods_

## `now`

- Returns the number of milliseconds elapsed since January 1, 1970 00:00:00 UTC
- `var timeInMs = Date.now()`

## `getDate`

- Returns the day of the month
- `dateObj.getDate()`

## `getDay`

- Returns the day of the week
- `dateObj.getDay()`

## `getMonth`

- Returns the month
- `dateObj.getMonth()`

## `getFullYear`

- Returns the year
- `dateObj.getFullYear()`

## `getTime`

- Returns the number of milliseconds since midnight Jan 1 1970, and a specified date
- `dateObj.getTime()`

## `toDateString`

- Converts the date of a Date object into a readable string
- `dateObj.toDateString()`
- Turn a string into a date:
  - `const dateDisplay = dateString => new Date(dateString).toDateString();`

---

# _JSON_

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON
- JavaScript Object Notation
- Language agnostic data format
- Chrome won’t allow JSON to run locally unless through http-server
- Syntax:

```
`{`
`  `"jsonObject"`: {`
`    `"param1"`: `"value1"`,`
`    `"param2"`: true,`
`    `"param3"`: 3`
`}`
```

## _\_\_Methods_

## `parse`

- Parses a JSON string and returns a JavaScript object
- Takes a string containing a JSON-serialized object and breaks it up, creating an object with properties corresponding to the `"parameter":"value"` pairs found in the string
- `JSON.parse(JSONobject[, reviver])`

## `stringify`

- Converts a JavaScript object to a JSON object
- `JSON.stringify(value[, replacer[, space]])`

```
`{`
    “Family”: [{
        "name" : "Jason",
        "age" : "24",
        "gender" : "male"
    },
    {
        "name" : "Kyle",
        "age" : "21",
        "gender" : "male"
    }];
`}`
```

---

#
