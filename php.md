
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

---


### crud

```php
<?php
// In-memory CRUD for an array of associative arrays
$database = [];

// Helper: Pretty print
function p($data) {
    echo "<pre>" . htmlspecialchars(print_r($data, true)) . "</pre>";
}

// CREATE
function createEntry(&$database, $entry) {
    $database[] = $entry;
    echo "Added: " . json_encode($entry) . PHP_EOL;
}

// CREATE: Prevent duplicate ID
function createEntryUnique(&$database, $entry) {
    foreach ($database as $row) {
        if ($row['id'] === $entry['id']) {
            echo "Duplicate ID: {$entry['id']}" . PHP_EOL;
            return;
        }
    }
    $database[] = $entry;
    echo "Added: " . json_encode($entry) . PHP_EOL;
}

// READ all
function readEntries($database) {
    foreach ($database as $idx => $entry) {
        echo "$idx: " . json_encode($entry) . PHP_EOL;
    }
}

// READ by id
function getById($database, $id) {
    foreach ($database as $entry) {
        if ($entry['id'] === $id) return $entry;
    }
    return null;
}

// READ by name (partial match)
function getByName($database, $name) {
    $results = [];
    foreach ($database as $entry) {
        if (stripos($entry['name'], $name) !== false) $results[] = $entry;
    }
    return $results;
}

// UPDATE by id
function updateEntryById(&$database, $id, $newEntry) {
    foreach ($database as &$entry) {
        if ($entry['id'] === $id) {
            foreach ($newEntry as $key => $val) {
                $entry[$key] = $val;
            }
            echo "Updated by id $id: " . json_encode($entry) . PHP_EOL;
            return;
        }
    }
    echo "Entry not found." . PHP_EOL;
}

// DELETE by id
function deleteEntryById(&$database, $id) {
    $found = false;
    foreach ($database as $k => $entry) {
        if ($entry['id'] === $id) {
            unset($database[$k]);
            $found = true;
            echo "Deleted: " . json_encode($entry) . PHP_EOL;
        }
    }
    if (!$found) echo "No entry deleted." . PHP_EOL;
    // Reindex
    $database = array_values($database);
}

// Experiment: Pagination
function paginate($database, $page = 1, $perPage = 2) {
    $offset = ($page - 1) * $perPage;
    return array_slice($database, $offset, $perPage);
}

// Experiment: Sorting
function sortByKey(&$database, $key, $desc = false) {
    usort($database, function($a, $b) use ($key, $desc) {
        if ($a[$key] == $b[$key]) return 0;
        if ($desc) return ($a[$key] < $b[$key]) ? 1 : -1;
        return ($a[$key] > $b[$key]) ? 1 : -1;
    });
}

// Example usage
for ($i = 1; $i <= 20; $i++) {
    createEntryUnique($database, [
        'id' => $i,
        'name' => 'User' . chr(64 + $i),
        'email' => "user$i@example.com",
        'active' => $i % 2 === 1,
        'roles' => ['user', $i % 3 === 0 ? 'admin' : null]
    ]);
}
readEntries($database);
p(getById($database, 2));
p(getByName($database, 'UserA'));
updateEntryById($database, 2, ['name' => 'Bobby', 'active' => false]);
deleteEntryById($database, 3);
echo "Paginated (page 2):\n";
p(paginate($database, 2, 4));
sortByKey($database, 'name', true);
echo "Sorted by name desc:\n";
p($database);

// Experiment: Nested data, deeply nested update
$database[0]['profile'] = ['bio' => 'Hello', 'contacts' => ['skype' => 'alice.skype', 'phone' => '123']];
$database[0]['profile']['contacts']['email'] = $database[0]['email'];
p($database[0]);
```
- store objects with nested arrays  
- add a batch update/delete function  
- export/import database to/from JSON file  
- implement in-memory search by any key  


### ai/ml

> for php, use [php-ml/php-ml](https://github.com/php-ai/php-ml) or call ai apis.

```php
<?php
// composer require php-ai/php-ml
require 'vendor/autoload.php';
use Phpml\Regression\SVR;
use Phpml\SupportVectorMachine\Kernel;

// Data: Hours studied vs. score
$X = [];
$y = [];
for ($i = 1; $i <= 100; $i++) {
    $X[] = [$i];
    $y[] = 40 + $i * 3 + rand(-5, 5); // Linear but with noise
}

$regression = new SVR(Kernel::LINEAR, 1.0, 1.0);
$regression->train($X, $y);

// Predict for 101-110 hours
$testData = [];
for ($i = 101; $i <= 110; $i++) $testData[] = [$i];
$predictions = array_map(function($x) use ($regression) { return $regression->predict($x); }, $testData);
echo "Predictions for hours 101-110: " . implode(", ", $predictions) . PHP_EOL;

// Experiment: Save and reload model
$modelFile = 'model.ser';
file_put_contents($modelFile, serialize($regression));
$loaded = unserialize(file_get_contents($modelFile));
echo "Loaded model prediction for 105: " . $loaded->predict([105]) . PHP_EOL;

// Experiment: Use a classifier
use Phpml\Classification\KNearestNeighbors;
$classifier = new KNearestNeighbors();
$Xc = [[1], [2], [3], [6], [7], [8]];
$yc = ['low', 'low', 'low', 'high', 'high', 'high'];
$classifier->train($Xc, $yc);
echo "Classify 5: " . $classifier->predict([5]) . PHP_EOL;
```
- use clustering (e.g., kmeans)  
- integrate with OpenAI API using curl  
- visualize results (generate svg/png)  
- experiment with data normalization


### data analyst

```php
<?php
$data = [];
for ($i = 1; $i <= 100; $i++) {
    $score = rand(50, 100);
    $data[] = [
        'Name' => 'Student' . $i,
        'Score' => $score,
        'Passed' => $score >= 60,
        'Class' => chr(65 + ($i % 5))
    ];
}

$scores = array_column($data, 'Score');
$avg = array_sum($scores) / count($scores);
$min = min($scores);
$max = max($scores);

echo "Average: $avg, Min: $min, Max: $max" . PHP_EOL;

// Filter, map, reduce
$passed = array_filter($data, function($row){ return $row['Passed']; });
$names = array_map(function($row){ return $row['Name']; }, $passed);
echo "Passed count: " . count($passed) . "\n";

// Group by class
$byClass = [];
foreach ($data as $row) $byClass[$row['Class']][] = $row;
foreach ($byClass as $class => $rows) {
    echo "Class $class: " . count($rows) . " students\n";
}

// Experiment: Histogram of score distribution
$hist = array_fill(0, 11, 0); // 50-59, 60-69, ..., 100
foreach ($scores as $s) $hist[intval(($s - 50)/5)]++;
foreach ($hist as $idx => $count) {
    $range = (50 + $idx*5) . '-' . (54 + $idx*5);
    echo "$range: $count\n";
}

// Read/write CSV
$fp = fopen('scores.csv', 'w');
fputcsv($fp, array_keys($data[0]));
foreach ($data as $row) fputcsv($fp, $row);
fclose($fp);

$csv = [];
if (($handle = fopen('scores.csv', 'r')) !== FALSE) {
    $header = fgetcsv($handle);
    while (($row = fgetcsv($handle)) !== FALSE) {
        $csv[] = array_combine($header, $row);
    }
    fclose($handle);
}
echo "CSV loaded: " . count($csv) . " rows\n";
?>
```
- calculate median, mode  
- visualize with google charts (output js code)  
- export to excel (use [phpoffice/phpspreadsheet](https://phpspreadsheet.readthedocs.io/))  
- aggregate by class and grade



### backend/api

```php
<?php
// Save as api.php and run: php -S localhost:8080 api.php

session_start();
if (!isset($_SESSION['messages'])) $_SESSION['messages'] = [];
if (!isset($_SESSION['users'])) $_SESSION['users'] = [
    ['id' => 1, 'name' => 'Alice'],
    ['id' => 2, 'name' => 'Bob']
];

// Routing
$uri = strtok($_SERVER['REQUEST_URI'], '?');
$method = $_SERVER['REQUEST_METHOD'];

function respond($data, $code = 200) {
    http_response_code($code);
    header('Content-Type: application/json');
    echo json_encode($data); exit;
}

// GET /hello
if ($method === 'GET' && $uri === '/hello') {
    respond(['message' => 'Hello, World!']);
}

// GET /users
if ($method === 'GET' && $uri === '/users') {
    respond(['users' => $_SESSION['users']]);
}

// GET /messages
if ($method === 'GET' && $uri === '/messages') {
    respond(['messages' => $_SESSION['messages']]);
}

// POST /messages
if ($method === 'POST' && $uri === '/messages') {
    $input = json_decode(file_get_contents('php://input'), true);
    $_SESSION['messages'][] = $input;
    respond(['received' => $input], 201);
}

// PUT /users/{id}
if ($method === 'PUT' && preg_match('#^/users/(\d+)$#', $uri, $matches)) {
    $id = (int)$matches[1];
    $input = json_decode(file_get_contents('php://input'), true);
    foreach ($_SESSION['users'] as &$user) {
        if ($user['id'] === $id) {
            $user = array_merge($user, $input);
            respond(['updated' => $user]);
        }
    }
    respond(['error' => 'User not found'], 404);
}

// DELETE /messages/{idx}
if ($method === 'DELETE' && preg_match('#^/messages/(\d+)$#', $uri, $matches)) {
    $idx = (int)$matches[1];
    if (isset($_SESSION['messages'][$idx])) {
        $removed = $_SESSION['messages'][$idx];
        unset($_SESSION['messages'][$idx]);
        $_SESSION['messages'] = array_values($_SESSION['messages']);
        respond(['deleted' => $removed]);
    } else {
        respond(['error' => 'Not found'], 404);
    }
}

respond(['error' => 'Not found'], 404);
?>
```
- add authentication (JWT)  
- validate JSON input  
- implement PATCH and OPTIONS  
- use array as database, persist to file


### database design or sql

```php
<?php
$db = new PDO('sqlite::memory:');
$db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

// Create users and posts
$db->exec("CREATE TABLE users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL
)");
$db->exec("CREATE TABLE posts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    user_id INTEGER,
    title TEXT,
    content TEXT,
    created_at TEXT,
    FOREIGN KEY (user_id) REFERENCES users(id)
)");

// Insert bulk users
$stmt = $db->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
for ($i = 1; $i <= 50; $i++) {
    $stmt->execute(["User$i", "user$i@example.com"]);
}
$userIds = [];
foreach ($db->query("SELECT id FROM users") as $row) $userIds[] = $row['id'];

// Insert posts
$stmt = $db->prepare("INSERT INTO posts (user_id, title, content, created_at) VALUES (?, ?, ?, ?)");
for ($i = 0; $i < 200; $i++) {
    $uid = $userIds[array_rand($userIds)];
    $stmt->execute([$uid, "Title $i", "Content $i", date('Y-m-d H:i:s')]);
}

// Query: join users & posts
foreach ($db->query("SELECT u.name, p.title FROM posts p JOIN users u ON u.id = p.user_id WHERE u.id=1") as $row) {
    print_r($row);
}

// Transaction
try {
    $db->beginTransaction();
    $db->exec("UPDATE users SET email='fail@example.com' WHERE id=1");
    throw new Exception("Simulated error");
    $db->commit();
} catch (Exception $e) {
    $db->rollBack();
    echo "Rolled back transaction: " . $e->getMessage() . PHP_EOL;
}

// Experiment: Prepared statement, search by keyword
$stmt = $db->prepare("SELECT * FROM posts WHERE title LIKE ?");
$stmt->execute(['%Title 1%']);
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) echo $row['title'] . "\n";
?>
```
- add indexes, triggers, views  
- use persistent DB file, backup/restore  
- add migration scripts


### devops/deployment

```php
<?php
function copyDir($src, $dest) {
    if (is_dir($dest)) {
        $files = new RecursiveIteratorIterator(new RecursiveDirectoryIterator($dest, RecursiveDirectoryIterator::SKIP_DOTS), RecursiveIteratorIterator::CHILD_FIRST);
        foreach ($files as $file) {
            $file->isDir() ? rmdir($file) : unlink($file);
        }
        rmdir($dest);
    }
    mkdir($dest, 0777, true);
    $files = new RecursiveIteratorIterator(new RecursiveDirectoryIterator($src, RecursiveDirectoryIterator::SKIP_DOTS), RecursiveIteratorIterator::SELF_FIRST);
    foreach ($files as $file) {
        $to = $dest . DIRECTORY_SEPARATOR . $files->getSubPathName();
        if ($file->isDir()) mkdir($to, 0777, true);
        else copy($file, $to);
    }
    echo "Deployed from $src to $dest\n";
}

// Versioning
function versionedDir($base, $ver) {
    $dir = $base . "_v" . $ver;
    mkdir($dir, 0777, true);
    return $dir;
}

function backupAndDeploy($src, $dest, $backupDir) {
    if (is_dir($dest)) {
        $backupPath = $backupDir . '/backup_' . time() . '_' . basename($dest);
        rename($dest, $backupPath);
    }
    copyDir($src, $dest);
    echo "Backup and deployed from $src to $dest\n";
}

// Compress files before deploy
function compressDir($src, $zipfile) {
    $zip = new ZipArchive();
    if ($zip->open($zipfile, ZipArchive::CREATE) === TRUE) {
        $files = new RecursiveIteratorIterator(new RecursiveDirectoryIterator($src), RecursiveIteratorIterator::LEAVES_ONLY);
        foreach ($files as $name => $file) {
            if (!$file->isDir()) {
                $filePath = $file->getRealPath();
                $relativePath = substr($filePath, strlen($src) + 1);
                $zip->addFile($filePath, $relativePath);
            }
        }
        $zip->close();
        echo "Compressed $src to $zipfile\n";
    } else echo "Failed to create zip\n";
}
?>
```
- use shell commands (`shell_exec`) to restart services  
- automate config file updates  
- send notifications on deploy


### security based

```php
<?php
// Hashing passwords
$hash = password_hash("mypassword", PASSWORD_DEFAULT);
echo "Hashed (bcrypt): $hash\n";

// Verify password
echo password_verify("mypassword", $hash) ? "Password matches\n" : "No match\n";

// Generate secure token
$token = bin2hex(random_bytes(32));
echo "Secure token: $token\n";

// Encrypt/Decrypt (OpenSSL)
$key = openssl_random_pseudo_bytes(32);
$iv = openssl_random_pseudo_bytes(16);
$data = "my secret data";
$enc = openssl_encrypt($data, "AES-256-CBC", $key, 0, $iv);
$dec = openssl_decrypt($enc, "AES-256-CBC", $key, 0, $iv);
echo "Encrypted: $enc\nDecrypted: $dec\n";

// JWT with firebase/php-jwt
// composer require firebase/php-jwt
use Firebase\JWT\JWT;
use Firebase\JWT\Key;
$payload = ['uid' => 123, 'exp' => time() + 3600];
$jwt = JWT::encode($payload, $key, 'HS256');
echo "JWT: $jwt\n";
$decoded = JWT::decode($jwt, new Key($key, 'HS256'));
print_r($decoded);
?>
``` 
- use hmac for message authentication  
- try timing attacks on hash comparison  
- rotate encryption keys


### system design
```php
<?php
class ServiceRegistry {
    private $services = [];
    public function register($name, $address, $ttl = 60) {
        $this->services[$name] = ['address' => $address, 'expires' => time() + $ttl];
    }
    public function get($name) {
        if (isset($this->services[$name]) && $this->services[$name]['expires'] > time()) {
            return $this->services[$name]['address'];
        }
        return null;
    }
    public function allServices() {
        return array_filter($this->services, function($svc) { return $svc['expires'] > time(); });
    }
    public function deregister($name) { unset($this->services[$name]); }
    public function cleanup() {
        foreach ($this->services as $name => $svc) {
            if ($svc['expires'] <= time()) unset($this->services[$name]);
        }
    }
}

$registry = new ServiceRegistry();
$registry->register("user-service", "localhost:5000", 2);
sleep(3);
$registry->cleanup();
print_r($registry->allServices());

// Experiment: Simulate microservices
$microservices = [];
for ($i = 0; $i < 10; $i++) {
    $name = "service$i";
    $addr = "localhost:" . (5000+$i);
    $microservices[$name] = $addr;
    $registry->register($name, $addr, rand(1,5));
}
sleep(6);
$registry->cleanup();
print_r($registry->allServices());
?>
```  
- add health checks (HTTP ping)  
- implement a round-robin load balancer  
- track service usage stats


### file and i/o manipulation

```php
<?php
// Write a large file
$fp = fopen("bigfile.txt", "w");
for ($i = 0; $i < 10000; $i++) {
    fwrite($fp, "Line " . str_pad($i, 6, '0', STR_PAD_LEFT) . " " . str_repeat("*", rand(1, 50)) . "\n");
}
fclose($fp);

// Read and count lines
$lines = 0;
foreach (file("bigfile.txt") as $line) $lines++;
echo "Lines: $lines\n";

// Read CSV (large)
$csv = [];
$fp = fopen('bigfile.csv', 'w');
fputcsv($fp, ['id', 'val']);
for ($i = 1; $i <= 10000; $i++) fputcsv($fp, [$i, rand(1,100000)]);
fclose($fp);
$fp = fopen('bigfile.csv', 'r');
while (($row = fgetcsv($fp)) !== false) $csv[] = $row;
fclose($fp);
echo "CSV rows: " . count($csv) . "\n";

// Experiment: Directory listing, file search
$files = scandir('.');
foreach ($files as $f) if (strpos($f, '.txt') !== false) echo "Found txt file: $f\n";

// Compress files
$zip = new ZipArchive();
$zip->open('archive.zip', ZipArchive::CREATE);
foreach ($files as $f) if (is_file($f)) $zip->addFile($f);
$zip->close();
?>
```
- scan and process binary files  
- monitor file changes in real time  
- generate and parse JSON logs


### testing and debugging 

```php
<?php
// Simple assertions
function add($a, $b) { return $a + $b; }
for ($i = -100; $i <= 100; $i++) {
    assert(add($i, -$i) === 0, "add($i, -$i) should be 0");
}
echo "All add assertions passed!\n";

// Debugging: var_dump, xdebug, error_log
function buggy($x) {
    var_dump($x);
    error_log("Buggy called with $x");
    if ($x === 0) throw new Exception("Zero division");
    return 10 / $x;
}
try { buggy(0); } catch (Exception $e) { echo "Caught: " . $e->getMessage() . "\n"; }

// Experiment: PHPUnit
// composer require --dev phpunit/phpunit
// phpunit test file example:
class MathTest extends PHPUnit\Framework\TestCase {
    public function testAdd() { $this->assertEquals(5, add(2, 3)); }
    public function testZero() { $this->assertEquals(0, add(0, 0)); }
}

// Experiment: property-based testing
function randomAddTests($n) {
    for ($i=0; $i<$n; $i++) {
        $a = rand(-10000,10000); $b = rand(-10000,10000);
        assert(add($a, $b) === $a + $b, "Failed for $a + $b");
    }
}
randomAddTests(5000);
echo "Random add tests passed.\n";
?>
```
- try [Pest](https://pestphp.com/) for expressive BDD  
- use mocks/stubs  
- add performance benchmarks
