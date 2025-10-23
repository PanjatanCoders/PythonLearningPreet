# Python Functions - Complete Teaching Guide

## 📚 Table of Contents
- [Introduction to Functions](#introduction-to-functions)
- [Basic Function Concepts](#basic-function-concepts)
- [Advanced Function Techniques](#advanced-function-techniques)
- [Practical Examples & Best Practices](#practical-examples--best-practices)

---

## Introduction to Functions

Functions are one of the most fundamental building blocks in Python programming. They allow you to:
- **Organize code** into reusable, logical blocks
- **Reduce repetition** by writing code once and calling it multiple times
- **Improve readability** by giving meaningful names to operations
- **Simplify debugging** by isolating functionality
- **Enable modularity** in your programs

Think of functions as recipes: once you write down the steps (define the function), you can follow them anytime you need (call the function) without rewriting everything.

---

## Basic Function Concepts

### 1. Defining Your First Function

A function is defined using the `def` keyword, followed by the function name, parentheses, and a colon. The function body is indented.

**Syntax:**
```python
def function_name(parameters):
    """Docstring: describes what the function does"""
    # Function body
    return result
```

**Example:**
```python
def greet(name):
    """Greet a person with their name."""
    return f"Hello, {name}!"

# Calling the function
print(greet("Alice"))
```

**Output:**
```
Hello, Alice!
```

**Key Points:**
- Use descriptive function names (verbs are good: `calculate`, `process`, `fetch`)
- Docstrings (triple quotes) explain what the function does
- The `return` statement sends a value back to the caller

---

### 2. Function Parameters

Parameters allow functions to accept input and work with different data.

#### Default Parameters

Default parameters provide fallback values when arguments aren't provided.

```python
def introduce(name, age=25, city="Unknown"):
    """Introduce a person with optional parameters."""
    return f"Hi, I'm {name}, {age} years old, from {city}"

# Different ways to call the function
print(introduce("Bob"))                      # Uses all defaults
print(introduce("Charlie", 30))               # Overrides age
print(introduce("Diana", city="Paris"))       # Named argument
print(introduce("Eve", 28, "London"))         # All arguments
```

**Output:**
```
Hi, I'm Bob, 25 years old, from Unknown
Hi, I'm Charlie, 30 years old, from Unknown
Hi, I'm Diana, 25 years old, from Paris
Hi, I'm Eve, 28 years old, from London
```

**Best Practices:**
- Required parameters come first, then optional parameters
- Use default values for commonly used options
- Avoid mutable defaults (like lists or dictionaries)

---

### 3. Multiple Return Values

Python functions can return multiple values as a tuple, which can be unpacked.

```python
def calculate_circle(radius):
    """Calculate area and circumference of a circle."""
    import math
    area = math.pi * radius ** 2
    circumference = 2 * math.pi * radius
    return area, circumference

# Unpacking return values
area, circumference = calculate_circle(5)
print(f"Circle (radius=5):")
print(f"  Area = {area:.2f}")
print(f"  Circumference = {circumference:.2f}")

# Can also capture as tuple
result = calculate_circle(3)
print(f"\nAs tuple: {result}")
```

**Output:**
```
Circle (radius=5):
  Area = 78.54
  Circumference = 31.42

As tuple: (28.274333882308138, 18.84955592153876)
```

---

## Advanced Function Techniques

### 4. Variable-Length Arguments (*args and **kwargs)

When you don't know in advance how many arguments a function will receive, use `*args` for positional arguments and `**kwargs` for keyword arguments.

```python
def flexible_function(*args, **kwargs):
    """Function that accepts any number of arguments."""
    print(f"Positional arguments (*args): {args}")
    print(f"Keyword arguments (**kwargs): {kwargs}")
    
    # Process positional arguments
    if args:
        total = sum(args)
        print(f"Sum of numbers: {total}")
    
    # Process keyword arguments
    if kwargs:
        print("Processing keyword arguments:")
        for key, value in kwargs.items():
            print(f"  {key} = {value}")

# Examples
flexible_function(1, 2, 3)
print()
flexible_function(name="Alice", age=25, city="NYC")
print()
flexible_function(10, 20, 30, operation="sum", unit="meters")
```

**Output:**
```
Positional arguments (*args): (1, 2, 3)
Keyword arguments (**kwargs): {}
Sum of numbers: 6

Positional arguments (*args): ()
Keyword arguments (**kwargs): {'name': 'Alice', 'age': 25, 'city': 'NYC'}
Processing keyword arguments:
  name = Alice
  age = 25
  city = NYC

Positional arguments (*args): (10, 20, 30)
Keyword arguments (**kwargs): {'operation': 'sum', 'unit': 'meters'}
Sum of numbers: 60
Processing keyword arguments:
  operation = sum
  unit = meters
```

**Use Cases:**
- Creating wrapper functions
- Building flexible APIs
- Forwarding arguments to other functions

---

### 5. Lambda Functions (Anonymous Functions)

Lambda functions are small, unnamed functions defined using the `lambda` keyword. They're perfect for simple operations.

**Syntax:** `lambda arguments: expression`

```python
# Regular function vs Lambda
def square_regular(x):
    return x ** 2

square_lambda = lambda x: x ** 2

print(f"Regular: {square_regular(5)}")
print(f"Lambda: {square_lambda(5)}")

# Lambda with multiple arguments
add = lambda x, y: x + y
print(f"Add: {add(3, 7)}")

# Using lambda with map()
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(f"Original: {numbers}")
print(f"Squared: {squared}")

# Using lambda with filter()
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(f"Even numbers: {even_numbers}")

# Using lambda with sorted()
people = [("Alice", 25), ("Bob", 30), ("Charlie", 20)]
sorted_by_age = sorted(people, key=lambda person: person[1])
print(f"Sorted by age: {sorted_by_age}")
```

**Output:**
```
Regular: 25
Lambda: 25
Add: 10
Original: [1, 2, 3, 4, 5]
Squared: [1, 4, 9, 16, 25]
Even numbers: [2, 4]
Sorted by age: [('Charlie', 20), ('Alice', 25), ('Bob', 30)]
```

**When to Use Lambda:**
- ✅ Simple, one-line operations
- ✅ As arguments to higher-order functions (`map`, `filter`, `sorted`)
- ❌ Complex logic (use regular functions with names)
- ❌ When you need docstrings or multiple statements

---

### 6. Higher-Order Functions

Functions that take other functions as arguments or return functions are called higher-order functions.

```python
def apply_operation(numbers, operation):
    """Apply an operation to each number in a list."""
    return [operation(num) for num in numbers]

# Define some operations
def cube(x):
    return x ** 3

def double(x):
    return x * 2

# Apply different operations
numbers = [1, 2, 3, 4]
cubed = apply_operation(numbers, cube)
doubled = apply_operation(numbers, double)

print(f"Original: {numbers}")
print(f"Cubed: {cubed}")
print(f"Doubled: {doubled}")

# Using with lambda
squared = apply_operation(numbers, lambda x: x ** 2)
print(f"Squared: {squared}")
```

**Output:**
```
Original: [1, 2, 3, 4]
Cubed: [1, 8, 27, 64]
Doubled: [2, 4, 6, 8]
Squared: [1, 4, 9, 16]
```

---

### 7. Decorators

Decorators are a powerful way to modify or enhance functions without changing their code. They "wrap" a function with additional functionality.

**Basic Decorator Pattern:**

```python
def timing_decorator(func):
    """Decorator to measure function execution time."""
    import time
    
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"⏱️  {func.__name__} took {end_time - start_time:.4f} seconds")
        return result
    
    return wrapper

# Apply decorator using @syntax
@timing_decorator
def slow_calculation():
    """Simulate a slow calculation."""
    import time
    total = 0
    for i in range(1000000):
        total += i
    time.sleep(0.1)
    return total

@timing_decorator
def fast_calculation():
    """A faster calculation."""
    return sum(range(1000))

# Call decorated functions
result1 = slow_calculation()
print(f"Result: {result1}\n")

result2 = fast_calculation()
print(f"Result: {result2}")
```

**Output:**
```
⏱️  slow_calculation took 0.1156 seconds
Result: 499999500000

⏱️  fast_calculation took 0.0001 seconds
Result: 499500
```

**Another Practical Decorator - Logging:**

```python
def log_decorator(func):
    """Decorator to log function calls."""
    def wrapper(*args, **kwargs):
        print(f"📝 Calling {func.__name__} with args={args}, kwargs={kwargs}")
        result = func(*args, **kwargs)
        print(f"✅ {func.__name__} returned: {result}")
        return result
    return wrapper

@log_decorator
def add(a, b):
    return a + b

@log_decorator
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

# Test the decorated functions
add(5, 3)
print()
greet("Alice")
print()
greet("Bob", greeting="Hi")
```

**Output:**
```
📝 Calling add with args=(5, 3), kwargs={}
✅ add returned: 8

📝 Calling greet with args=('Alice',), kwargs={}
✅ greet returned: Hello, Alice!

📝 Calling greet with args=('Bob',), kwargs={'greeting': 'Hi'}
✅ greet returned: Hi, Bob!
```

**Common Use Cases for Decorators:**
- ⏱️ Performance timing and profiling
- 📝 Logging and debugging
- 🔒 Authentication and authorization
- 💾 Caching results (memoization)
- ✅ Input validation
- 🔄 Retry logic for network calls

---

## Practical Examples & Best Practices

### 8. Function Documentation

Always document your functions with clear docstrings.

```python
def calculate_statistics(numbers):
    """
    Calculate basic statistics for a list of numbers.
    
    Args:
        numbers (list): A list of numeric values
        
    Returns:
        dict: A dictionary containing mean, median, min, and max
        
    Raises:
        ValueError: If the numbers list is empty
        
    Example:
        >>> calculate_statistics([1, 2, 3, 4, 5])
        {'mean': 3.0, 'median': 3, 'min': 1, 'max': 5}
    """
    if not numbers:
        raise ValueError("Cannot calculate statistics for empty list")
    
    sorted_nums = sorted(numbers)
    n = len(numbers)
    
    return {
        'mean': sum(numbers) / n,
        'median': sorted_nums[n // 2],
        'min': sorted_nums[0],
        'max': sorted_nums[-1]
    }

# Test the function
data = [10, 20, 15, 30, 25]
stats = calculate_statistics(data)
print("Statistics:")
for key, value in stats.items():
    print(f"  {key}: {value}")
```

**Output:**
```
Statistics:
  mean: 20.0
  median: 20
  min: 10
  max: 30
```

---

### 9. Pure Functions vs Side Effects

**Pure Function:** Returns the same output for the same input, no side effects.

```python
# Pure function - Good!
def add_numbers(a, b):
    return a + b

# Impure function - Has side effects
counter = 0

def increment_counter():
    global counter
    counter += 1  # Modifies external state
    return counter

# Demonstration
print("Pure function:")
print(add_numbers(2, 3))  # Always returns 5
print(add_numbers(2, 3))  # Always returns 5

print("\nImpure function:")
print(increment_counter())  # Returns 1
print(increment_counter())  # Returns 2 (different result!)
```

**Output:**
```
Pure function:
5
5

Impure function:
1
2
```

**Best Practice:** Prefer pure functions when possible for easier testing and debugging.

---

### 10. Function Composition

Combining simple functions to create complex behavior.

```python
# Simple, focused functions
def remove_whitespace(text):
    return text.strip()

def convert_to_lowercase(text):
    return text.lower()

def replace_spaces(text):
    return text.replace(" ", "_")

# Compose functions
def slugify(text):
    """Convert text to a URL-friendly slug."""
    text = remove_whitespace(text)
    text = convert_to_lowercase(text)
    text = replace_spaces(text)
    return text

# Test
titles = ["  Hello World  ", "Python Programming", "  Data Science 101  "]
print("Original titles → Slugs:")
for title in titles:
    print(f"'{title}' → '{slugify(title)}'")
```

**Output:**
```
Original titles → Slugs:
'  Hello World  ' → 'hello_world'
'Python Programming' → 'python_programming'
'  Data Science 101  ' → 'data_science_101'
```

---

## 🎯 Key Takeaways

1. **Functions promote code reuse** - Write once, use many times
2. **Use descriptive names** - `calculate_total()` is better than `calc()`
3. **Keep functions focused** - Each function should do one thing well
4. **Document with docstrings** - Future you will thank present you
5. **Default parameters** add flexibility without complexity
6. **Lambda functions** are great for simple, one-time operations
7. **Decorators** enhance functions without modifying their code
8. **Prefer pure functions** for predictable, testable code

---

## 🚀 Practice Exercises

Try creating these functions to reinforce your learning:

1. **Temperature Converter**: Function that converts between Celsius, Fahrenheit, and Kelvin
2. **Password Validator**: Function that checks password strength (length, special chars, numbers)
3. **List Processor**: Function using `*args` to find common elements across multiple lists
4. **Caching Decorator**: Create a decorator that caches function results to avoid recalculation
5. **Data Pipeline**: Compose multiple functions to clean and transform text data

---

**Next Steps:** Practice writing functions daily, explore Python's built-in functions (`map`, `filter`, `reduce`), and study function decorators in popular libraries like Flask and Django to see real-world applications!
