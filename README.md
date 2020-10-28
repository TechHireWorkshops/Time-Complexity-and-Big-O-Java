# Time Complexity and Big O

![](https://pics.me.me/when-your-interviewer-asks-for-the-time-complexity-of-your-41938233.png)

### What is efficiency?
  > A measure of time and space usage. 

  When we write code, we want to measure how taxing a given program will be on a machine. The faster and lighter a program is, the less machine work needs to be done.

### Why increase efficiency?

Efficiency in algorithms are important because:
- Better-performing algorithms can enhance the user experience by decreasing wait times.
- Better-performing algorithms save money by reducing storage and processing needs.
- Algorithms and algorithm analysis are an important part of the shared language developers use to talk about programs (especially in INTERVIEWS).

## Time Complexity
The time efficiency of an algorithm refers to the time it takes for an algorithm to run, and more specifically _how the time it take for an algorithm to run increases when used to process more data._

This is to say that time complexity looks at the rate of time increase as data increases. Hope you like math.

## Big O?
_'Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity' - some nerd on wikipedia_

- Big O is a system of notation that measures the time increase in a piece of code.
- We often use it to evaluate WORST CASE SCENARIO for each algorithm.
- Big O is measured in orders of magnitude.
- Big O can also be understood as the number of operations that an algorithm runs.


### Common Big O Values

![](https://user-images.githubusercontent.com/29616227/65440287-7f5ceb00-ddf6-11e9-9409-49c5185a2c07.jpg)


Big O notation gives an upper limit for how long an algorithm could take to run. 

### Rules for Evaluating Complexity

How can you evaluate the Big O of a given algorithm? It really comes down to operations.

Some operations are constant, meaning they have a Big O of O(1).  This means that they take the same amount of time regardless of the size of the data the operation is run on.

- Arithmetic operations are constant
- Assigning variables is constant
- Accessing variables, elements in an array, or keys in an object are constant.

Some operations scale with data, namely:

- Loops
- Recursion

Usually, each loop or instance of recursion increases proportionally to the length or amount of data being iterated, meaning they are O(n).

To calculate time complexity, go through the code and assign a Big O value to each line.  We'll then combine the values appropriately, and simplify to the largest order of magnitude.

Let's look at some examples.

#### O(1) (constant time)

To say an algorithm takes constant (or `O(1)`) time means: no matter how big the input(s) are, the computer will do basically the same amount of work to perform the algorithm on them.


```javascript
const isFirstUndefined = numArray => {
  let first = numArray[0];					       //O(1)
  return first === undefined;                  //O(1)
}

```

In this examples, each time the function runs we have `O(1) + O(1), or 2*O(1)`.  We don't care about coefficients, so this simplifies to `O(1)`

#### O(n) (linear time)

To say an algorithm is has a time complexity of O(n) means the the time required to run the algorithm scales linearly with data size, n.

Algorithms that process each input at least once will take at least **O(n)** time.  Loops are a common example.  

```javascript
const addAll = numArray => {
  let sum = 1;                                // O(1)
  for (let i = 0; i < numArray.length; i++){  // O(n)
    sum += numArray[i];                       // O(1)
  }
  return sum;                                 // O(1)
}
```

Following our rules for evaluating complexity, the time complexity of `addAll` is `O(1) + O(n) * O(1) + O(1)`. You might be tempted to call this `O(n) + n*O(1) + 2*O(1)`, which we could simplify to `O(2n)`. However, as we use larger and larger values of n in this function, the 2 ceases to matter, so we would classify this function as `O(n)`.

#### O(n<sup>2</sup>) (exponential time)

Nested loops are a common example of O(n<sup>2</sup>) operations.

```javascript
const addAlltoAll = numArray => {
  let sum = 1;                                  // O(1)
  for (let i = 0; i < numArray.length; i++) {   // n times:
    sum += numArray[i];
    for (let j = 0; j < numArray.length; i++) { // n times:
      sum += numArray[j];
    }
  }
  return sum;                                   // O(1)
}
```

Here, we have `O(1) + O(n) * O(n) + O(1)`, simplifying to `O(n<sup>2</sup>) + 2*O(1)`.  We select our largest power and end up with `O(n<sup>2</sup>)`


#### O(log(n)) (logarithmic time)

Any algorithm which cuts the problem size in half each at each step is logarithmic or `O(log(n))`.

These algorithms take longer for larger inputs, but the rate of increase is very slight compared to most others.  These algorithms are famously efficient for sorting and searching, and are worth looking into.

<details><summary>Can you think of an example of an O(log(n)) algorithm?</summary>

A common example is finding an item using a binary search! Here's some pseudocode:

```javascript
const binary_search = (array, value) => {
  let low=0
  let high = array.size - 1
  if (high < low) return false;
  // if high and low overlap, nothing was found.
  let mid = low + ((high - low) / 2);
  // determine the middle element.

  if (array[mid] > value) {
    return binary_search(array, value, low, mid-1);
  } else if (array[mid] < value) {
    return binary_search(array, value, mid+1, high);
  } 
  // split the result in half and search again recursively until we succeed.
  else {
    return mid;
    // found! 
  }
}
```

</details>


#### [There are other families too!](https://en.wikipedia.org/wiki/Big_O_notation#Orders_of_common_functions)


## Exercises!
Work with your partner and find the worst case time-complexity of each of these algorithms:
#### #1

```javascript
const wordOccurrence = (word, phrase) => {
  let result = 0;
  const array  = phrase.split(' ');
  for (let i = 0; i < array.length; i++) {
    if (word.toLowerCase() === array[i].toLowerCase()) {
      result += 1;
    }
  }
  return result;
}
```

#### #2

```javascript
const bubbleSort = list => {
  for (let i = 0; i < list.length - 1; i++) {
    for (let j  = 0; j < list.length - 2; j++) {
      if (list[j+1] < list[j]) {
        const temp = list[j];
        list[j] = list[j+1];
        list[j+1] = temp;
      }
    }
  }
  return list;
}
```

#### #3
```javascript
const factorial = n => {
  if (n === 0) {
    return 1;
  } else {
    return n * factorial(n-1);
  }
}
```

#### #4

```javascript
const bobIsFirst = people => {
  return people[0] == 'bob';
}
```

#### #5

```javascript
const isPalindrome = input => {
  const stack = [];
  let output = "";
  for (let i = 0; i < input.length; i++){
    stack.push(input[i]);
  }
  while (stack.length) {
    output += stack.pop();
  }
  return output == input;
}
```

#### #6
```javascript
const sumOfDivisors = n => {
  let result = 0;
  let i = 1;
  while (i < n) {
    if (n % i == 0) {
      result += i;
    }
  }
  return result;
}
```

#### #7
```javascript
const printAllNumbersThenSumPairs = numArray => {
  numArray.forEach(num => console.log(num));
  numArray.forEach((num, index)=>{
    if (index < numArray.length - 1) {
      console.log(num + numArray[index+1]);
    }
  });
}
```

#### #8
```javascript
const isPrime = num => {
  if (num == 1 || num == 2) {
    return false;
  }
  for (let i = 2; i < num - 1; i++){
    if (num % i == 0) {
      return false;
    }
  }
  return true;
}
```


## Space complexity
Another complexity to take into consideration when writing code, though far less important.  Space complexity is the amount of temporary space needed for a function to run. All data types require space, so every variable, parameter, array, object, string, etc needs to be accounted for.

Calculating space complexity

- Most primitives (booleans, numbers, undefined, null) are constant space.
In the case of numbers, the size of the number doesn't matter, 2 and 1,000,000 take up the same amount of memory.
- Strings require O(n) space, where n is the string length
- Arrays and objects take up O(n) space, where n is the number of elements in the array or key-value pairs in the object.

Example of O(1) space complexity

``` jsx
function sum(arr) {
    let total = 0;
    for (let i = 0; i < arr.length; i++) {
        total += arr[i];
    }
    return total;
}
```

Example of O(n) space complexity

``` jsx
function double(arr) {
    let newArr = [];
    for (let i = 0; i < arr.length; i++) {
    	 let current = arr[i]
        newArray.push(2 * arr[i]);
    }
    return newArray;
}
```