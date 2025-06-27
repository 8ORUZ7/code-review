
## Loops

### Iterating Through an Array
```php
$fruits = ["apple", "banana", "cherry"];
foreach ($fruits as $fruit) {
    echo $fruit . "\n";
}
```

### For loop with range
```php
for ($i = 1; $i < 6; $i++) {
    echo $i . "\n";
}
```

### While loop
```php
$x = 3;
while ($x > 0) {
    echo $x . "\n";
    $x -= 1;
}
```

---

## Functions

### Basic function with parameters
```php
function greet($name) {
    return "Hello, $name!";
}
echo greet("Alex");
```

### Default parameters
```php
function power($base, $exponent = 2) {
    return pow($base, $exponent);
}
echo power(3) . "\n";     // 9
echo power(3, 3) . "\n";  // 27
```

### Return multiple values (using array)
```php
function getMinMax($numbers) {
    return [min($numbers), max($numbers)];
}
list($low, $high) = getMinMax([4, 8, 1, 6]);
echo "Min: $low, Max: $high\n";
```

---

## Associative Arrays

### Create and Access
```php
$person = ["name" => "Alice", "age" => 22];
echo $person["name"]; // Alice
```

### Update and Add
```php
$person["age"] = 23;
$person["city"] = "Manila";
```

### Loop through associative array
```php
foreach ($person as $key => $value) {
    echo "$key: $value\n";
}
```

### Array comprehension-like (build associative array with mapping)
```php
$squares = [];
foreach (range(1, 3) as $x) {
    $squares[$x] = $x * $x;
}
print_r($squares); // [1 => 1, 2 => 4, 3 => 9]
```

### Complex associative arrays (dictionary of arrays)
```php
$groups = [
    "group1" => ["user1"],
    "group2" => ["user2"],
    "group3" => ["user3"]
];
print_r($groups["group1"]);

$moreGroups = [
    "group1" => ["user1", "user2", "user3"],
    "group2" => ["user4", "user5"],
    "group3" => ["user6", "user7", "user8"]
];
print_r($moreGroups["group3"]);
```

---

## Exception Handling

### Basic try-catch
```php
try {
    $x = 1 / 0; // Generates a warning in PHP, not an exception!
    if (!is_finite($x)) {
        throw new Exception("Division by zero");
    }
} catch (Exception $e) {
    echo "You can't divide by zero!\n";
}
```

### Multiple exception types
```php
try {
    $num = intval("hello");
    if ($num === 0 && "hello" !== "0") {
        throw new InvalidArgumentException("That's not a number.");
    }
} catch (InvalidArgumentException $e) {
    echo $e->getMessage() . "\n";
}
```

### try-catch-finally
```php
try {
    $content = file_get_contents("sample.txt");
    if ($content === false) throw new Exception("File not found.");
} catch (Exception $e) {
    echo "File not found.\n";
} finally {
    echo "Operation complete.\n";
}
```

---

## Useful Built-in Functions

### Enumerate in loop (with index)
```php
$fruits = ["apple", "banana", "cherry"];
foreach ($fruits as $index => $fruit) {
    echo "$index: $fruit\n";
}
```

### Combine lists with array_map
```php
$names = ["Anna", "Ben"];
$ages = [25, 30];
foreach ($names as $i => $name) {
    if (isset($ages[$i])) {
        echo "$name is {$ages[$i]} years old\n";
    }
}
```

### Vowels count
```php
function vowels($s) {
    return preg_match_all('/[aeiou]/i', $s);
}
echo vowels("humanoid") . "\n";
```

### Summation of range
```php
$total = array_sum(range(1, 9));
echo $total . "\n";
```

### Division error (try-catch)
```php
try {
    $result = 1 / 0;
    if (!is_finite($result)) {
        throw new Exception("Division by zero");
    }
} catch (Exception $e) {
    $result = "undefined";
}
echo $result . "\n";
```

### Even numbers (loop, condition, array_filter)
```php
function getEven($nums) {
    return array_values(array_filter($nums, function($x) { return $x % 2 === 0; }));
}
print_r(getEven([1, 2, 3, 4, 5, 6]));
```

### Factorial (function, loop)
```php
function factorial($n) {
    $result = 1;
    for ($i = 2; $i <= $n; $i++) {
        $result *= $i;
    }
    return $result;
}
echo factorial(5) . "\n";
```

### Count word occurrences
```php
function wordCount($text) {
    $counts = [];
    $words = str_word_count(strtolower($text), 1);
    foreach ($words as $word) {
        if (!isset($counts[$word])) $counts[$word] = 0;
        $counts[$word]++;
    }
    return $counts;
}
print_r(wordCount("hello world hello"));
```

### Check if number is prime
```php
function isPrime($n) {
    if ($n < 2) return false;
    for ($i = 2; $i <= sqrt($n); $i++) {
        if ($n % $i == 0) return false;
    }
    return true;
}
echo isPrime(13) ? 'true' : 'false';
echo "\n";
```

### Reverse a string
```php
function reverseString($s) {
    return strrev($s);
}
echo reverseString("PHP") . "\n";
```

### Find the largest value (by key)
```php
$scores = ['Alice' => 88, 'Bob' => 95, 'Charlie' => 91];
$topScorer = array_keys($scores, max($scores))[0];
echo $topScorer . "\n";
```

### Variable variables (dynamic variable names)
```php
$foo = "bar";
$$foo = "baz"; // creates $bar = "baz"
echo $bar . "\n"; // Output: baz
```

### Heredoc and Nowdoc syntax (multi-line strings)
```php
$text = <<<EOT
This is a
multi-line string
in PHP.
EOT;
echo $text . "\n";
```

### Superglobals usage
```php
// $_GET, $_POST, $_SERVER, etc.
echo $_SERVER['HTTP_USER_AGENT'] . "\n";
```

### Include and require (file inclusion)
```php
// include 'file.php';
// require 'file.php';
```

### Anonymous functions and closures
```php
$square = function($x) { return $x * $x; };
echo $square(4) . "\n";
```

### Traits (code reuse in classes)
```php
trait Logger {
    public function log($msg) {
        echo "Log: $msg\n";
    }
}
class App {
    use Logger;
}
$app = new App();
$app->log("Trait working!");
```

### Namespaces
```php
namespace MyProject;
function hello() {
    echo "Hello from MyProject\n";
}
\MyProject\hello();
```

### Type declarations (scalar type hints, return types)
```php
function add(int $a, int $b): int {
    return $a + $b;
}
echo add(2, 3) . "\n";
```

### Null coalescing operator (??)
```php
$name = $_GET['name'] ?? 'Guest';
echo $name . "\n";
```

### Spaceship operator (<=>) for sorting
```php
$nums = [3, 1, 2];
usort($nums, function($a, $b) { return $a <=> $b; });
print_r($nums);
```
