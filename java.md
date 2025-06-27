## Loops

### Iterating Through an Array/List
```java
String[] fruits = {"apple", "banana", "cherry"};
for (String fruit : fruits) {
    System.out.println(fruit);
}

// Using ArrayList
ArrayList<String> fruitsList = new ArrayList<>(Arrays.asList("apple", "banana", "cherry"));
for (String fruit : fruitsList) {
    System.out.println(fruit);
}
```

### For loop with range
```java
for (int i = 1; i < 6; i++) {
    System.out.println(i);
}
```

### While loop
```java
int x = 3;
while (x > 0) {
    System.out.println(x);
    x -= 1;
}
```

---

## Functions (Methods)

### Basic function with parameters
```java
public static String greet(String name) {
    return "Hello, " + name + "!";
}
System.out.println(greet("Alex"));
```

### Default parameters (using method overloading)
```java
public static int power(int base, int exponent) {
    return (int)Math.pow(base, exponent);
}
public static int power(int base) {
    return power(base, 2);
}
System.out.println(power(3));     // 9
System.out.println(power(3, 3));  // 27
```

### Return multiple values (using array or custom class)
```java
public static int[] getMinMax(int[] numbers) {
    int min = Arrays.stream(numbers).min().getAsInt();
    int max = Arrays.stream(numbers).max().getAsInt();
    return new int[]{min, max};
}
int[] result = getMinMax(new int[]{4, 8, 1, 6});
System.out.println("Min: " + result[0] + ", Max: " + result[1]);
```
*Or using a Pair class (not in standard library, but you can write your own).*

---

## HashMap (Associative Array / Dictionary)

### Create and Access
```java
Map<String, Object> person = new HashMap<>();
person.put("name", "Alice");
person.put("age", 22);
System.out.println(person.get("name")); // Alice
```

### Update and Add
```java
person.put("age", 23);
person.put("city", "Manila");
```

### Loop through HashMap
```java
for (Map.Entry<String, Object> entry : person.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

### Build HashMap with mapping
```java
Map<Integer, Integer> squares = new HashMap<>();
for (int x = 1; x <= 3; x++) {
    squares.put(x, x * x);
}
System.out.println(squares); // {1=1, 2=4, 3=9}
```

### Complex HashMap (dictionary of lists)
```java
Map<String, List<String>> groups = new HashMap<>();
groups.put("group1", Arrays.asList("user1"));
groups.put("group2", Arrays.asList("user2"));
groups.put("group3", Arrays.asList("user3"));
System.out.println(groups.get("group1"));

Map<String, List<String>> moreGroups = new HashMap<>();
moreGroups.put("group1", Arrays.asList("user1", "user2", "user3"));
moreGroups.put("group2", Arrays.asList("user4", "user5"));
moreGroups.put("group3", Arrays.asList("user6", "user7", "user8"));
System.out.println(moreGroups.get("group3"));
```

---

## Exception Handling

### Basic try-catch
```java
try {
    int x = 1 / 0;
} catch (ArithmeticException e) {
    System.out.println("You can't divide by zero!");
}
```

### Multiple exception types
```java
try {
    int num = Integer.parseInt("hello");
} catch (NumberFormatException e) {
    System.out.println("That's not a number.");
}
```

### try-catch-finally
```java
try {
    String content = Files.readString(Paths.get("sample.txt"));
} catch (IOException e) {
    System.out.println("File not found.");
} finally {
    System.out.println("Operation complete.");
}
```

---

## Useful Built-in Functions

### Enumerate in loop (with index)
```java
String[] fruits = {"apple", "banana", "cherry"};
for (int i = 0; i < fruits.length; i++) {
    System.out.println(i + ": " + fruits[i]);
}
```

### Combine lists with index-based loop
```java
String[] names = {"Anna", "Ben"};
int[] ages = {25, 30};
for (int i = 0; i < Math.min(names.length, ages.length); i++) {
    System.out.println(names[i] + " is " + ages[i] + " years old");
}
```

### Vowels count
```java
public static int vowels(String s) {
    int count = 0;
    for (char c : s.toLowerCase().toCharArray()) {
        if ("aeiou".indexOf(c) != -1) count++;
    }
    return count;
}
System.out.println(vowels("humanoid"));
```

### Summation of range
```java
int total = 0;
for (int i = 1; i < 10; i++) total += i;
System.out.println(total);
```

### Division error (try-catch)
```java
try {
    int result = 1 / 0;
    System.out.println(result);
} catch (ArithmeticException e) {
    System.out.println("undefined");
}
```

### Even numbers (loop, condition, streams)
```java
public static List<Integer> getEven(int[] nums) {
    return Arrays.stream(nums).filter(x -> x % 2 == 0).boxed().collect(Collectors.toList());
}
System.out.println(getEven(new int[]{1, 2, 3, 4, 5, 6}));
```

### Factorial (function, loop)
```java
public static int factorial(int n) {
    int result = 1;
    for (int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}
System.out.println(factorial(5));
```

### Count word occurrences
```java
public static Map<String, Integer> wordCount(String text) {
    Map<String, Integer> counts = new HashMap<>();
    for (String word : text.toLowerCase().split("\\s+")) {
        counts.put(word, counts.getOrDefault(word, 0) + 1);
    }
    return counts;
}
System.out.println(wordCount("hello world hello"));
```

### Check if number is prime
```java
public static boolean isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) return false;
    }
    return true;
}
System.out.println(isPrime(13)); // true
```

### Reverse a string
```java
public static String reverseString(String s) {
    return new StringBuilder(s).reverse().toString();
}
System.out.println(reverseString("Java"));
```

### Find the largest value (by key)
```java
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 88);
scores.put("Bob", 95);
scores.put("Charlie", 91);
String topScorer = Collections.max(scores.entrySet(), Map.Entry.comparingByValue()).getKey();
System.out.println(topScorer);
```

### Generics
```java
public static <T> void printArray(T[] array) {
    for (T element : array) {
        System.out.println(element);
    }
}
Integer[] nums = {1, 2, 3};
printArray(nums);
```

### Interfaces and Abstract Classes
```java
interface Animal {
    void speak();
}
class Dog implements Animal {
    public void speak() {
        System.out.println("Woof!");
    }
}
Animal dog = new Dog();
dog.speak();
```

### Enum Types
```java
enum Day { MONDAY, TUESDAY, WEDNESDAY }
Day today = Day.MONDAY;
System.out.println(today);
```

### Lambda Expressions and Functional Interfaces
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
numbers.forEach(n -> System.out.println(n * n));
```

### Stream API
```java
List<String> names = Arrays.asList("Anna", "Ben", "Carl");
names.stream().filter(n -> n.length() == 3).forEach(System.out::println);
```

### Static Initializer Blocks
```java
class Example {
    static {
        System.out.println("Static block executed!");
    }
}
```

### Inner Classes
```java
class Outer {
    class Inner {
        void display() {
            System.out.println("Inside Inner");
        }
    }
}
Outer.Inner obj = new Outer().new Inner();
obj.display();
```

### Serialization
```java
import java.io.*;
class Person implements Serializable {
    String name;
    Person(String name) { this.name = name; }
}
// Writing and reading would involve ObjectOutputStream/ObjectInputStream
```

### Annotations
```java
@interface MyAnnotation {
    String value();
}
@MyAnnotation(value = "example")
class Demo {}
```
