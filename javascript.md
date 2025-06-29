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


---

### crud
- prevent duplicate IDs  
- implement searching by name  
- store more complex data (lists, nested objects) per entry  
- add pagination or sorting

**ES5:**
```javascript
// In-memory CRUD for an array of objects
var database = [];

// CREATE
function createEntry(entry) {
    database.push(entry);
    console.log("Added:", entry);
}

// READ
function readEntries() {
    for (var i = 0; i < database.length; i++) {
        console.log(i + ":", database[i]);
    }
}

// READ by id
function getById(entryId) {
    for (var i = 0; i < database.length; i++) {
        if (database[i].id === entryId) return database[i];
    }
    return null;
}

// UPDATE by id
function updateEntryById(entryId, newEntry) {
    for (var i = 0; i < database.length; i++) {
        if (database[i].id === entryId) {
            for (var key in newEntry) {
                database[i][key] = newEntry[key];
            }
            console.log("Updated:", database[i]);
            return;
        }
    }
    console.log("Entry not found.");
}

// DELETE by id
function deleteEntryById(entryId) {
    for (var i = 0; i < database.length; i++) {
        if (database[i].id === entryId) {
            var removed = database.splice(i, 1);
            console.log("Deleted:", removed[0]);
            return;
        }
    }
    console.log("Entry not found.");
}

// Example usage
createEntry({id: 1, name: "Alice"});
createEntry({id: 2, name: "Bob"});
readEntries();
console.log("Get by id:", getById(2));
updateEntryById(2, {name: "Bobby"});
deleteEntryById(1);
readEntries();
createEntry({id: 3, name: "Charlie"});
readEntries();
```

**ES6+:**
```javascript
let database = [];

// CREATE
const createEntry = entry => {
    database.push(entry);
    console.log(`Added:`, entry);
};

// READ
const readEntries = () => {
    database.forEach((entry, idx) => console.log(`${idx}:`, entry));
};

// READ by id
const getById = entryId => database.find(entry => entry.id === entryId) || null;

// UPDATE by id
const updateEntryById = (entryId, newEntry) => {
    let entry = database.find(e => e.id === entryId);
    if (entry) {
        Object.assign(entry, newEntry);
        console.log(`Updated:`, entry);
    } else {
        console.log("Entry not found.");
    }
};

// DELETE by id
const deleteEntryById = entryId => {
    const idx = database.findIndex(e => e.id === entryId);
    if (idx !== -1) {
        const removed = database.splice(idx, 1);
        console.log(`Deleted:`, removed[0]);
    } else {
        console.log("Entry not found.");
    }
};

// Example usage
createEntry({id: 1, name: "Alice"});
createEntry({id: 2, name: "Bob"});
readEntries();
console.log("Get by id:", getById(2));
updateEntryById(2, {name: "Bobby"});
deleteEntryById(1);
readEntries();
createEntry({id: 3, name: "Charlie"});
readEntries();
```

---

### ai, machine learning

> javascript can use [ml.js](https://github.com/mljs), [TensorFlow.js](https://www.tensorflow.org/js).
- try polynomial regression with `ml-regression-polynomial`  
- change the dataset (e.g., house prices)  
- save/load model coefficients  
- use TensorFlow.js for neural networks


**ES6+ (with ml-regression):**
```javascript
// npm install ml-regression
const SimpleLinearRegression = require('ml-regression').SimpleLinearRegression;

const X = [1, 2, 3, 4, 5];
const y = [50, 55, 65, 70, 75];

const regression = new SimpleLinearRegression(X, y);

// Predict for 6 hours
console.log("Predicted score for 6 hours:", regression.predict(6));

// Predict for multiple hours
console.log("Predictions for [1,2,3,7,10]:", [1,2,3,7,10].map(x => regression.predict(x)));
```

---

### data analyst
- use [danfo.js](https://danfo.jsdata.org/) for dataframe-like features  
- read from CSV/JSON files  
- visualize with [Plotly.js](https://plotly.com/javascript/) or [Chart.js](https://www.chartjs.org/)


**ES6+:**
```javascript
const data = [
    {Name: "A", Score: 90, Passed: true},
    {Name: "B", Score: 85, Passed: true},
    {Name: "C", Score: 78, Passed: false},
    {Name: "D", Score: 92, Passed: true}
];

const scores = data.map(row => row.Score);
const avg = scores.reduce((a, b) => a + b) / scores.length;
const min = Math.min(...scores);
const max = Math.max(...scores);
console.log({avg, min, max});

console.log("Passed Students:", data.filter(row => row.Passed));

// Experiment: Add Grade, group by grade
const addGrades = rows => rows.map(row => ({
    ...row,
    Grade: row.Score >= 90 ? "A" : row.Score >= 80 ? "B" : "C"
}));
const withGrades = addGrades(data);
console.log(withGrades);

const groupBy = (arr, key) => arr.reduce((acc, obj) => {
    (acc[obj[key]] = acc[obj[key]] || []).push(obj);
    return acc;
}, {});
console.log("Grouped by Grade:", groupBy(withGrades, "Grade"));
```

---

### backend/api
- add a PUT method for updating messages  
- use Express.js for easier routing  
- write a client using `fetch` or `axios`  
- add validation and error handling

**ES6+:**
```javascript
const http = require('http');

let messages = [];

const server = http.createServer((req, res) => {
    if (req.method === 'GET' && req.url === '/hello') {
        res.writeHead(200, {'Content-Type': 'application/json'});
        res.end(JSON.stringify({message: 'Hello, World!'}));
    } else if (req.method === 'GET' && req.url === '/messages') {
        res.writeHead(200, {'Content-Type': 'application/json'});
        res.end(JSON.stringify({messages}));
    } else if (req.method === 'POST' && req.url === '/messages') {
        let body = '';
        req.on('data', chunk => body += chunk);
        req.on('end', () => {
            const data = JSON.parse(body);
            messages.push(data);
            res.writeHead(201, {'Content-Type': 'application/json'});
            res.end(JSON.stringify({received: data}));
        });
    } else {
        res.writeHead(404);
        res.end();
    }
});

server.listen(8080, () => console.log('Server running at http://localhost:8080'));
```
---

### database design and SQL 
- add transaction handling  
- use SQL joins  
- try using a persistent database file  
- use [knex.js](http://knexjs.org/) for query building
  
**ES6+:**
```javascript
// npm install sqlite3
const sqlite3 = require('sqlite3').verbose();

let db = new sqlite3.Database(':memory:');

// Create table
db.serialize(() => {
    db.run(`CREATE TABLE users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        email TEXT UNIQUE NOT NULL
    )`);

    db.run("INSERT INTO users (name, email) VALUES (?, ?)", ["Alice", "alice@example.com"]);
    db.run("INSERT INTO users (name, email) VALUES (?, ?)", ["Bob", "bob@example.com"]);

    db.all("SELECT * FROM users", (err, rows) => {
        console.log("All users:", rows);
    });

    db.run("UPDATE users SET email = ? WHERE name = ?", ["alice@new.com", "Alice"]);
    db.run("DELETE FROM users WHERE name = ?", ["Bob"]);

    db.all("SELECT * FROM users", (err, rows) => {
        console.log("After delete:", rows);
    });

    db.run(`CREATE TABLE posts (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        user_id INTEGER,
        title TEXT,
        FOREIGN KEY(user_id) REFERENCES users(id)
    )`);

    db.run("INSERT INTO posts (user_id, title) VALUES (?, ?)", [1, "First post"]);
    db.all("SELECT * FROM posts", (err, rows) => {
        console.log("Posts:", rows);
    });
});
```

---

### devops/deployment
- add a function to restart a service  
- compress files before deployment (use [archiver](https://www.npmjs.com/package/archiver))  
- automate with npm scripts
  
**ES6+:**
```javascript
const fs = require('fs');
const path = require('path');

function copyDir(src, dest) {
    if (fs.existsSync(dest)) fs.rmSync(dest, {recursive: true});
    fs.mkdirSync(dest, {recursive: true});
    for (const file of fs.readdirSync(src)) {
        const from = path.join(src, file);
        const to = path.join(dest, file);
        if (fs.lstatSync(from).isDirectory()) copyDir(from, to);
        else fs.copyFileSync(from, to);
    }
    console.log(`Deployed from ${src} to ${dest}`);
}

// Experiment: Add backup/versioning
function backupAndDeploy(src, dest, backupDir) {
    if (fs.existsSync(dest)) {
        fs.renameSync(dest, path.join(backupDir, `backup_${Date.now()}_${path.basename(dest)}`));
    }
    copyDir(src, dest);
    console.log(`Deployed with backup from ${src} to ${dest}`);
}

// Example usage
// copyDir('my_app', '/tmp/deployed_app');
// backupAndDeploy('my_app', '/tmp/deployed_app', '/tmp/backup_dir');
```

---

### security-based tasks
- try different hash algorithms (MD5, SHA512)  
- use HMAC for message authentication  
- use [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) for JWTs
  
**ES6+:**
```javascript
const crypto = require('crypto');

// Hashing passwords
function hashPassword(password) {
    return crypto.createHash('sha256').update(password).digest('hex');
}
console.log(hashPassword("mypassword"));

// Generate a token
const token = crypto.randomBytes(16).toString('hex');
console.log("Secure token:", token);

// Encrypt/Decrypt (AES)
function encrypt(text, key) {
    const cipher = crypto.createCipheriv('aes-256-cbc', key, key.slice(0,16));
    let enc = cipher.update(text, 'utf8', 'hex');
    enc += cipher.final('hex');
    return enc;
}
function decrypt(enc, key) {
    const decipher = crypto.createDecipheriv('aes-256-cbc', key, key.slice(0,16));
    let dec = decipher.update(enc, 'hex', 'utf8');
    dec += decipher.final('utf8');
    return dec;
}
const key = crypto.randomBytes(32);
const enc = encrypt("my secret data", key);
console.log("Encrypted:", enc);
console.log("Decrypted:", decrypt(enc, key));

// Experiment: Use bcryptjs for password hashing
// npm install bcryptjs
const bcrypt = require('bcryptjs');
bcrypt.hash("mypassword", 10, (err, hash) => {
    console.log("Bcrypt:", hash);
    bcrypt.compare("mypassword", hash, (err, res) => console.log("Match?", res));
});
```

---

### system design or architecture questions 
- add TTL/expiration for registered services  
- implement health checks  
- simulate microservices with multiple registries
  
**ES6+:**
```javascript
class ServiceRegistry {
    constructor() {
        this.services = {};
    }
    register(name, address) {
        this.services[name] = address;
    }
    get(name) {
        return this.services[name];
    }
    allServices() {
        return {...this.services};
    }
}

const registry = new ServiceRegistry();
registry.register("user-service", "localhost:5000");
registry.register("order-service", "localhost:5001");
console.log("All services:", registry.allServices());

// Deregister
const deregister = (registry, name) => {
    delete registry.services[name];
    console.log(`Deregistered ${name}`);
};
deregister(registry, "order-service");
console.log("After deregister:", registry.allServices());
```

---

### file and i/o manipulation
- read/write binary files with `Buffer`  
- use `fs.readdirSync` to list directory contents
  
**ES6+:**
```javascript
const fs = require('fs');

// Write to a file
fs.writeFileSync("example.txt", "Hello, file!\nSecond line.");

// Read from a file
const content = fs.readFileSync("example.txt", "utf8");
console.log("File content:\n", content);

// Append to a file
fs.appendFileSync("example.txt", "\nAppended line.");

// Read lines
fs.readFileSync("example.txt", "utf8")
  .split("\n").forEach(line => console.log("Line:", line.trim()));

// Experiment: Read CSV, write JSON
const csv = require('csv-parse/sync');
const data = [
    ["name", "score"],
    ["Alice", 90],
    ["Bob", 85]
];
fs.writeFileSync("data.csv", data.map(r => r.join(",")).join("\n"));

const csvData = csv.parse(fs.readFileSync("data.csv"), {columns: true});
console.log("CSV as array of objects:", csvData);

fs.writeFileSync("data.json", JSON.stringify(csvData, null, 2));
```

---

### testing and debugging
- try [jest](https://jestjs.io/) for more advanced testing  
- mock api's with [sinon.js](https://sinonjs.org/)  
- intentionally add bugs and debug with `node inspect`
**ES6+:**
```javascript
// Simple test function (manual)
function add(a, b) { return a + b; }
function testAdd() {
    console.assert(add(2, 3) === 5, "2+3 should be 5");
    console.assert(add(-1, 1) === 0, "-1+1 should be 0");
    console.log("All tests passed.");
}
testAdd();

// Debugging with console.log and Node.js debugger
function buggyFunction(x) {
    console.log("Debug: x =", x);
    // debugger; // Uncomment for Node.js debugging
    return 10 / x;
}
try {
    console.log(buggyFunction(0));
} catch (e) {
    console.log("Caught exception:", e);
}

// Experiment: Use Mocha for unit tests
// npm install mocha --save-dev
// In test.js:
// const assert = require('assert');
// describe('add', function() {
//   it('should add numbers', function() {
//     assert.equal(add(2,3), 5);
//   });
// });
```
