## Loops

### Iterating Through a List (Array)
```javascript
const fruits = ["apple", "banana", "cherry"];
for (const fruit of fruits) {
    console.log(fruit);
}
```

### For loop with range
```javascript
for (let i = 1; i < 6; i++) {
    console.log(i);
}
```
> Note: `for (let i = x; i < y; i++)` runs i from x up to (but not including) y.

### While loop
```javascript
let x = 3;
while (x > 0) {
    console.log(x);
    x -= 1;
}
```

---

## Functions

### Basic function with parameters
```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("Alex"));
```

### Default parameters
```javascript
function power(base, exponent = 2) {
    return base ** exponent;
}
console.log(power(3));     // 9
console.log(power(3, 3));  // 27
```

### Return multiple values (array)
```javascript
function getMinMax(numbers) {
    return [Math.min(...numbers), Math.max(...numbers)];
}
const [low, high] = getMinMax([4, 8, 1, 6]);
console.log(`Min: ${low}, Max: ${high}`);
```

---

## Objects

### Create and Access
```javascript
const person = {name: "Alice", age: 22};
console.log(person.name); // Alice
```


### Update and Add
```javascript
person.age = 23;
person.city = "Manila";
```


### Loop through object
```javascript
for (const [key, value] of Object.entries(person)) {
    console.log(`${key}: ${value}`);
}
```

### Object comprehension (simulate with Array.reduce)
```javascript
const squares = Array.from({length: 3}, (_, i) => i + 1)
    .reduce((obj, x) => { obj[x] = x * x; return obj; }, {});
console.log(squares); // {1: 1, 2: 4, 3: 9}
```

### Complex objects (dictionary of arrays)
```javascript
const groups = { group1: ['user1'], group2: ['user2'], group3: ['user3'] };
console.log(groups.group1);

const moreGroups = {
    group1: ['user1', 'user2', 'user3'],
    group2: ['user4', 'user5'],
    group3: ['user6', 'user7', 'user8']
};
console.log(moreGroups.group3);
```

---

## Exception Handling

### Basic try-catch
```javascript
try {
    const x = 1 / 0; // In JS, this is Infinity, not error!
    if (!isFinite(x)) throw new Error("ZeroDivisionError");
} catch (e) {
    console.log("You can't divide by zero!");
}
```

### Multiple exception types
```javascript
try {
    parseInt("hello"); // returns NaN
    if (isNaN(parseInt("hello"))) throw new Error("ValueError");
} catch (e) {
    console.log("That's not a number.");
}
```

### try-catch-finally
```javascript
try {
    // Node.js example, browser JS can't read files directly
    const fs = require('fs');
    let content = fs.readFileSync("sample.txt", "utf8");
} catch (e) {
    console.log("File not found.");
} finally {
    console.log("Operation complete.");
}
```

---

## Useful Built-in Functions

### Enumerate in loop
```javascript
const fruits = ["apple", "banana", "cherry"];
fruits.forEach((fruit, index) => {
    console.log(`${index}: ${fruit}`);
});
```

### Combine lists with zip
```javascript
const names = ["Anna", "Ben"];
const ages = [25, 30];
for (let i = 0; i < Math.min(names.length, ages.length); i++) {
    console.log(`${names[i]} is ${ages[i]} years old`);
}
```

### Vowels count
```javascript
function vowels(s) {
    return [...s.toLowerCase()].filter(c => "aeiou".includes(c)).length;
}
console.log(vowels("humanoid"));
```

### Summation of range
```javascript
let total = 0;
for (let i = 1; i < 10; i++) total += i;
console.log(total);

// or
const sum = (start, end) => {
    let t = 0;
    for (let i = start; i < end; i++) t += i;
    return t;
};
console.log(sum(1, 10));
```

### Division error (try-catch)
```javascript
let result;
try {
    let calc = 1 / 0;
    if (!isFinite(calc)) throw new Error("ZeroDivisionError");
    result = calc;
} catch (e) {
    result = "undefined";
}
console.log(result);
```

### Even numbers (loop, condition, list comprehension)
```javascript
function getEven(nums) {
    return nums.filter(x => x % 2 === 0);
}
console.log(getEven([1, 2, 3, 4, 5, 6]));
```

### Factorial (function, loop)
```javascript
function factorial(n) {
    let result = 1;
    for (let i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}
console.log(factorial(5));
```

### Count word occurrences
```javascript
function wordCount(text) {
    const counts = {};
    text.toLowerCase().split(/\s+/).forEach(word => {
        counts[word] = (counts[word] || 0) + 1;
    });
    return counts;
}
console.log(wordCount("hello world hello"));
```

### Check if number is prime
```javascript
function isPrime(n) {
    if (n < 2) return false;
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (n % i === 0) return false;
    }
    return true;
}
console.log(isPrime(13));
```

### Reverse a string
```javascript
function reverseString(s) {
    return s.split('').reverse().join('');
}
console.log(reverseString("Python"));
```

### Find the largest value (by key)
```javascript
const scores = { Alice: 88, Bob: 95, Charlie: 91 };
const topScorer = Object.keys(scores).reduce((a, b) => scores[a] > scores[b] ? a : b);
console.log(topScorer);
```

### Set (Unique Elements)
```javascript
const nums = [1, 2, 2, 3];
const unique = [...new Set(nums)];
console.log(unique); // [1, 2, 3]
```

### Map (Ordered key-value pairs)
```javascript
const map = new Map();
map.set('a', 1);
map.set('b', 2);
console.log(map.get('a')); // 1
```

### Stack (Array push/pop)
```javascript
const stack = [];
stack.push(1);
stack.push(2);
console.log(stack.pop()); // 2
```

### Queue (Array shift/push)
```javascript
const queue = [];
queue.push(1);
queue.push(2);
console.log(queue.shift()); // 1
```

### Class Syntax (OOP)
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    speak() {
        return `${this.name} makes a sound.`;
    }
}
const dog = new Animal("Rex");
console.log(dog.speak());
```

### Sorting an array of objects by a field
```javascript
const arr = [{score: 3}, {score: 1}, {score: 2}];
arr.sort((a, b) => a.score - b.score);
console.log(arr);
```

### Binary Search (Iterative)
```javascript
function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;
    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        if (arr[mid] === target) return mid;
        else if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
console.log(binarySearch([1, 2, 3, 4, 5], 3)); // 2
```

### Recursion (Fibonacci)
```javascript
function fib(n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
console.log(fib(5)); // 5
```

---

> **Tip:** In DSA interviews, JS is expected to use functional methods like `.map()`, `.filter()`, `.reduce()`, and classes for OOP.  
