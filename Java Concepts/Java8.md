Java 8 introduced several powerful functional interfaces in the `java.util.function` package to support functional programming. Here's a concise explanation and example for each:

---

### ✅ 1. **Predicate<T>**
- **Purpose**: Tests a condition and returns a boolean.
- **Method**: `boolean test(T t)`

```java
Predicate<String> isLongWord = word -> word.length() > 5;
System.out.println(isLongWord.test("HelloWorld")); // true
```

---

### 🔁 2. **Function<T, R>**
- **Purpose**: Takes one input and returns a result.
- **Method**: `R apply(T t)`

```java
Function<Integer, String> intToString = num -> "Number: " + num;
System.out.println(intToString.apply(10)); // Number: 10
```

---

### 📦 3. **Consumer<T>**
- **Purpose**: Takes one input and performs an action (no return).
- **Method**: `void accept(T t)`

```java
Consumer<String> greet = name -> System.out.println("Hello, " + name);
greet.accept("Alice"); // Hello, Alice
```

---

### 🎁 4. **Supplier<T>**
- **Purpose**: Supplies a result (no input).
- **Method**: `T get()`

```java
Supplier<Double> randomValue = () -> Math.random();
System.out.println(randomValue.get()); // e.g., 0.72345
```

---

### 🔍 5. **BiPredicate<T, U>**
- **Purpose**: Tests a condition with two inputs.
- **Method**: `boolean test(T t, U u)`

```java
BiPredicate<String, Integer> isLengthEqual = (str, len) -> str.length() == len;
System.out.println(isLengthEqual.test("Java", 4)); // true
```

---

### 🔄 6. **BiFunction<T, U, R>**
- **Purpose**: Takes two inputs and returns a result.
- **Method**: `R apply(T t, U u)`

```java
BiFunction<Integer, Integer, String> sumToString = (a, b) -> "Sum: " + (a + b);
System.out.println(sumToString.apply(5, 7)); // Sum: 12
```

---

### ➕ 7. **UnaryOperator<T>** (extends Function<T, T>)
- **Purpose**: Takes one input and returns a result of the same type.

```java
UnaryOperator<String> toUpper = str -> str.toUpperCase();
System.out.println(toUpper.apply("hello")); // HELLO
```

---

### ➗ 8. **BinaryOperator<T>** (extends BiFunction<T, T, T>)
- **Purpose**: Takes two inputs of the same type and returns a result of the same type.

```java
BinaryOperator<Integer> multiply = (a, b) -> a * b;
System.out.println(multiply.apply(3, 4)); // 12
```

---

These interfaces make Java more expressive and concise, especially when used with streams and lambda expressions. Want to dive deeper into how these are used in real-world scenarios or with collections?