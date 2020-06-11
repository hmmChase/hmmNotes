# _Data Structures_

- https://github.com/Yomguithereal/mnemonist

---

# _Linked List_

- A linked list is a data structure composed of nodes
- Each node contains 2 things:
  - data
  - a pointer to the next node
- Easier to add nodes to the beginning

---

# _Binary Search Tree_

- A method of organizing data in a series of connected, sorted nodes
- Represents data in a tree of nodes
- Good at inserting, finding, and moving around data in an efficient, cheap way

## _Rules_

1. Each BST has a root node (`10` in our example above), which contains data and has no parent nodes.
2. Each node has zero to two (`two` hence the keyword `binary` in this title) child nodes.
3. Each child node linked to the left (`5`) has a data value less than or equal to the parent node.
4. Each child node linked to the right (`12`) has a data value greater than the parent node.

- less than or equal to goes to the left
- greater than goes to the right

## _Search Methods_

- Depth First Search
  - Starts at the root of our tree and moves along a single branch all the way until it reaches the bottom most node
- Breadth First Search
  - Moves laterally along tree branches checking each layer before moving deeper down a branch

---

# _Arrays_

## _Stack_

- A stack follows the Last-In First-Out (LIFO) paradigm
  - An item added last will be removed first

```
const stack = [];
stack.push(2);         // stack is now [2]
stack.push(5);         // stack is now [2, 5]
const i = stack.pop(); // stack is now [2]
console.log(i);        // 5
```

## _Queue_

- A queue follows the First-In First-Out (FIFO) paradigm
  - The first item added will be the first item removed

```
const queue = [];
queue.push(2);           // queue is now [2]
queue.push(5);           // queue is now [2, 5]
const i = queue.shift(); // queue is now [5]
console.log(i);          // 2
```

---

# _Objects_

## _Lookup table_

```
function greet(language) {
  const lookUp = {
    english: 'Welcome',
    czech: 'Vitejte',
    danish: 'Velkomst',
    dutch: 'Welkom',
    estonian: 'Tere tulemast',
    finnish: 'Tervetuloa',
    flemish: 'Welgekomen',
    french: 'Bienvenue',
    german: 'Willkommen',
    irish: 'Failte',
    italian: 'Benvenuto',
    latvian: 'Gaidits',
    lithuanian: 'Laukiamas',
    polish: 'Witamy',
    spanish: 'Bienvenido',
    swedish: 'Valkommen',
    welsh: 'Croeso'
  };
  return lookUp[language] || lookUp['english'];
}
```

```
function correct(string) {
  return [...string]
    .map(char => ({ '0': 'O', '5': 'S', '1': 'I' }[char] || char))
    .join('');
}
```

---

# _Arrays_

- Compare previous element to the next element

---

# _Sorting Algorithms_

## _Bubble Sort_

- Loop through the elements and swap them if they are greater or less than the next card
- The largest card bubbles to the top
- No need to sort cards that have already bubbled?
- Take the 1st element, compare to 2nd element, swap if needed. Take 2nd element, compare to 3rd element, swap if needed. Take 3rd element, compare to 4th element, swap if needed. Take 4th element, compare to 5th element, swap if needed. ... and so on
- After the elements have been looped through, repeat process back at new 1st element

## _Insertion Sort_

- take 1st element, compare to start of array. since it is the 1st element, it is sorted
- take next element, compare to start of array.
- If it's smaller, place in front of element, and go on to next element to be tested
- If it's bigger, test next element, unless...
- It gets to its original place, then leave it there
- repeat starting with step 2

## _Merge Sort_

1. array of size 1 is already sorted
2. continue to split arrays until only 1 element in each array
3. to combine into sorted arrays, sort by comparing the 0 index of each array and push smaller element into a sorted array
4. move remaining sorted elements to end of main array

### Code

- split array in half, then split the resulting arrays until there is only one element left in each array
- require 2 functions:
  - 1 to split the arrays
  - 1 to merge them back together

1. create a function to split the arrays, with a parameter to pass in the array
   1. `function sort(array)`
2. base case, array already sorted if it's just one element
   1. `if (array.length <= 1) {
      ``return array;
      }

      `
3. find the middle of the array, using Math.floor to get a whole number, and assign to a variable
   1. `let midIndex = Math.floor(array.length / 2);`
4. slice the array in two at the middle point, and create two variable to hold each array side
   1. `let leftArray= array.slice(0, midIndex); let rightArray= array.slice(midIndex);`
5. call the merge function. and pass in the sort function twice, as two parameters, one with the leftside array as a parameter, and the other with the right side array as a parameter
   1. `return merge(sort(`leftArray`), sort(`rightArray`));`
6.
7. create the merge function, with 2 parameters, one for each side of the arrays
   1. `merge(`leftArray`,`rightArray`)`
8. create an empty array and asign to a variable to store the results
   1. `let result = [];`
9. create a while loop that checks if both the leftArray and rightArray have elements to compare, using .length property
   1. `while (`leftArray` .length && ```rightArray `.length)`
   2. create a conditional in the while loop to compare if the leftArray[0] index is <= to the rightArray[0] index
      1. `if (leftArray[0] <= rightArray[0])`
         1. if true, shift out the leftArray element and push to the result array
            1. ` result.push(l```eftArray```.shift()); `
         2. else, shift out the rightArray element and push to the result array
            1. ` result.push(```rightArray```.shift()); `
10. create 2 while loops for if either the leftArray or rightArray does not have elements to compare
    1. `while (leftArray.length)`
       1. if the leftArray has an element, shift it out and push to result array
          1. `result.push(leftArray.shift());`
    2. `while (rightArray.length)`
       1. if the rightArray has an element, shift it out and push to result array
          1. `result.push(rightArray.shift());`
11. return the result array
    1. `return result;`

## _Quick Sort_

- take last element and use as pivot
- loop through array, placing elements on each side of pivot, depending on their value
- now that pivot card is sorted
- take the pivot card on each side of the sorted pivot and repeat the process until all the cards are sorted

### Code

1. create the quickSort function with a parameter to pass in the array
   1. `function quickSort(array)`
2. create base case, array already sorted when it's just one element
   1. `if (array.length <= 1) { return array; }`
3. create variable for pivot, which .pops the last element from the array
   1. ` let pivot = array.pop()``; `
4. create variables for the lessThan and greaterThan arrays, set them to empty arrays
   1. ` let lessThanArray = []; ``let greaterThanArray = []; `
5. create a for loop to loop through array
   1. `for (let i = 0; i < array.length; i++)`
   2. create a conditional to compare elements with pivot
      1. if element is less than the pivot
      2. `if (array[i] < pivot)`
         1. push element into lessThan array
            1. `lessThan.push(array[i])`
         2. else push element into greaterThan array
            1. `greaterThan.push(array[i])`
6. return a combined array with the pivot element in the correct place
   1. recursively call quicksort on each side array, placing the pivot in it's sorted position, and combine into a new array
   2. `return [...quickSort(lessThan), pivot, ...quickSort(greaterThan)];`

## _Heap Sort_

- A binary tree with two special properties
- Rules:
  - Heap must be complete
    - All levels of the tree must be completely filled before adding a new level, except for last one
- Rule for Max Heap
  - root node must be highest number
  - child node must be less than or equal to parent node

* Parent node = `i`
* leftChild = `2 * i + 1`
* rightChild = `2 * i + 1`

---

# _Big O notation_

- http://frontend.turing.io/lessons/module-2/bigO.html
- https://repl.it/@hmmrepl/Big-O
- http://bigocheatsheet.com/
- used in Computer Science to describe the performance or complexity of an algorithm
- specifically describes the worst-case scenario
- can be used to describe the execution time required or the space used (e.g. in memory or on disk) by an algorithm
- ` | O( log n ) | O( n ) | O( n^2 ) | O( 2^n )
  ***
  100 | 2 | 100 | 10,000 | 1.27E+30
  ***
  1000 | 3 | 1,000 | 1,000,000 | 1.07E+301
  ***
  10000 | 4 | 10,000 | 1.00E+08 | 1.07E+3010
  ------------------------------------------------------------`

## _Big Ω (Omega)_

- best performance

## _Big Θ (Theta)_

- average performance

---
