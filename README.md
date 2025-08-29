# OakScript

**Version 0.04** • A lightweight scripting language for RISC OS

OakScript is a simple, intuitive scripting language designed for rapid prototyping, automation, and educational purposes on the RISC OS platform. With its clear syntax and straightforward commands, OakScript enables users to quickly write scripts for a variety of tasks, from basic calculations to more complex logic and data manipulation.

## Features

- **Simple Syntax**: Clear, readable code that's accessible to both beginners and experienced programmers
- **Rich Type System**: 22 variable types including advanced data structures (dictionaries, lists, sets), optional types, union types, lambda functions, regular expressions, and exceptions
- **Advanced Variable Operations**: Compound assignment operators (+=, -=, *=, /=), increment/decrement, automatic type conversion, generic types, and comprehensive variable introspection
- **Modern Control Flow**: Pattern matching, for-in loops with ranges, enhanced if-else, switch-case, while loops, break/continue, user-defined functions, lambda expressions, and comprehensive exception handling with try-catch-finally
- **Functional Programming**: Lambda functions, higher-order functions (map, filter, reduce), function composition, partial application, currying, closures, and memoization
- **Advanced String Processing**: String interpolation with expressions, multi-line strings, regular expression support with pattern matching and replacement
- **Comprehensive Built-in Library**: 100+ built-in functions covering mathematics, strings, files, arrays, functional programming, type system, exception handling, and RISC OS system integration
- **Bytecode Compilation**: Efficient compilation to portable bytecode format
- **RISC OS Integration**: Native module with proper memory management and system integration

## Architecture

OakScript consists of three main components:

### 1. Compiler
Transforms human-readable OakScript source code into efficient bytecode using a multi-pass approach:
- **Tokenizer**: Converts source text into meaningful tokens
- **Parser**: Builds abstract syntax using recursive descent parsing
- **Code Generator**: Emits bytecode with dynamic buffer management

### 2. Virtual Machine
A stack-based virtual machine that executes compiled bytecode:
- **Execution Stack**: LIFO stack for operand storage during expression evaluation
- **Variable Storage**: Dynamic variable management with string keys
- **Built-in Functions**: Pre-defined function library for common operations
- **Memory Safety**: Module-safe memory allocation throughout

### 3. Runtime System
Complete execution environment with comprehensive error handling:
- **File Format Validation**: Verifies bytecode integrity before execution
- **Debugging Support**: Optional instruction tracing and error diagnostics
- **RISC OS Integration**: Native module interface with proper system integration

## File Types

- OakScript source files (Type &EEE)
- Compiled bytecode files (Type &EEF)

## Commands

Once the module is loaded, OakScript provides three main commands:

- **`*OakScript [filename]`** - Run an OakScript source file directly
- **`*OakScriptCompile <source> <output>`** - Compile source to bytecode
- **`*OakScriptRun <bytecode>`** - Execute compiled bytecode

## Example Usage

### Basic Script
```oakscript
print "Hello, RISC OS!"
x = 42
y = 13
result = x + y
print result

if result > 50 then
    print "Result is large"
end

counter = 0
while counter < 3 do
    print counter
    counter = counter + 1
end
```

### Compilation and Execution
```
*OakScriptCompile MyScript MyScript
*OakScriptRun MyScript
```

## Language Features

### Variable Types and Manipulation

OakScript supports a rich type system with automatic type conversion and comprehensive manipulation capabilities:

#### Basic Variable Types
```oakscript
// Integer variables
count = 42
negative = -100

// String variables  
name = "OakScript"
message = "Hello, RISC OS!"

// Boolean variables
flag = true
enabled = false

// Floating-point variables
pi = 3.14159
temperature = -2.5
```

#### Advanced Variable Types
```oakscript
// Array variables (integer arrays)
numbers = array(10)              // Create array with 10 elements
array_set(numbers, 0, 42)        // Set numbers[0] = 42
value = array_get(numbers, 0)    // Get numbers[0] → 42

// Buffer variables (mutable byte buffers)
buffer = bytes(1024)             // Create 1KB buffer
updated = update_buffer(buffer, "New content")

// Block variables (structured data for RISC OS)
icon_block = block(36, 1)        // 36-byte icon block
window_block = block(88, 1)      // 88-byte window block

// Reference variables (pointers to other variables)
ref = reference("original_var")  // Create reference

// Time variables  
current = time()                 // Current timestamp
```

#### Automatic Type Conversion
```oakscript
// OakScript automatically converts between compatible types
number = 42          // Integer
text = "Value: " + number    // Auto-converts to "Value: 42"
flag = (number > 0)  // Auto-converts to boolean (true)
```

#### Variable Operators and Assignment
```oakscript
// Standard assignment
x = 10

// Compound assignment operators
x += 5    // x = x + 5  (now 15)
x -= 3    // x = x - 3  (now 12)  
x *= 2    // x = x * 2  (now 24)
x /= 4    // x = x / 4  (now 6)

// Increment/decrement
x++       // x = x + 1  (now 7)
x--       // x = x - 1  (now 6)
++x       // Pre-increment
--x       // Pre-decrement
```

#### Variable Introspection
```oakscript
// Get information about variables
info = variable_print_info()     // Print all variable info
count = get_variable_count()     // Number of active variables

// Type checking (via built-in functions)
type_name = get_variable_type_name("varname")

// Constant variables
const PI = 3.14159
const MAX_SIZE = 1024
```

### Arithmetic Operations
```oakscript
sum = a + b
difference = a - b
product = a * b
quotient = a / b
```

### Comparisons and Logical Operations
```oakscript
// Comparison operators
equal = (a == b)
not_equal = (a != b)
less_than = (a < b)
less_equal = (a <= b)
greater_than = (a > b)
greater_equal = (a >= b)

// Logical operators
result = (x > 0) and (y < 10)    // Logical AND
result = (x == 0) or (y == 0)    // Logical OR
result = not (x > 0)             // Logical NOT

// Boolean literals
flag1 = true
flag2 = false
```

### Control Flow

OakScript supports comprehensive control flow statements for complex program logic:

#### Conditional Statements
```oakscript
// Basic if statement
if x > 0 then
    print "Positive"
end

// If-else statement
if temperature > 25 then
    print "Hot day"
else
    print "Cool day"
end

// Switch statement for multiple conditions
switch value
    case 1
        print "One"
    case 2
        print "Two"
    default
        print "Other"
end
```

#### Loops
```oakscript
// While loop
counter = 0
while counter < 10 do
    print counter
    counter = counter + 1
end

// For loop with range
for i = 1 to 10 do
    print i
end

// For loop with step
for i = 0 to 100 step 5 do
    print i    // Prints 0, 5, 10, 15, etc.
end

// Loop control
for i = 1 to 100
    if i == 50 then
        break      // Exit loop
    end
    if i % 2 == 0 then
        continue   // Skip to next iteration
    end
    print i
end
```

#### User-Defined Functions
```oakscript
// Function definition
function calculate_area(width, height)
    result = width * height
    return result
end

// Function call
area = calculate_area(10, 5)
print area    // Prints 50
```

#### Exception Handling
```oakscript
// Try-catch for error handling
try
    result = divide(10, 0)
catch
    print "Division by zero error!"
end
```

#### File Inclusion
```oakscript
// Include other script files
#include "utilities"
#include "constants"
```

### Built-in Functions

OakScript provides an extensive library of built-in functions across multiple categories:

#### Mathematical Functions
```oakscript
// Basic arithmetic
result = add(5, 3)         // Addition: 8
result = subtract(10, 4)   // Subtraction: 6  
result = multiply(6, 7)    // Multiplication: 42
result = divide(20, 4)     // Division: 5
result = mod(10, 3)        // Modulo: 1

// Mathematical operations
absolute = abs(-42)        // Absolute value: 42
minimum = min(10, 20)      // Minimum: 10
maximum = max(10, 20)      // Maximum: 20
squared = square(5)        // Square: 25
power = pow(2, 8)          // Power: 256
sqrt = isqrt(16)           // Integer square root: 4
clamped = clamp(15, 0, 10) // Clamp value: 10

// Random numbers
srand(42)                  // Seed random generator
random1 = rand()           // Random number
random2 = rand(1, 100)     // Random between 1-100
```

#### String Functions
```oakscript
// String operations
length = len("Hello")           // String length: 5
upper = upper("hello")          // Uppercase: "HELLO"
lower = lower("WORLD")          // Lowercase: "world"
trimmed = trim("  text  ")      // Remove whitespace: "text"

// String testing
starts = startswith("Hello", "He")    // Boolean: 1 (true)
ends = endswith("World", "ld")        // Boolean: 1 (true)
has = contains("Hello", "ell")        // Boolean: 1 (true)

// String conversion
number = parseint("123")        // Parse integer: 123
hex_val = fromhex("FF")         // From hexadecimal: 255
```

#### File Operations
```oakscript
// File management
exists = exists("filename")           // Check if file exists
written = writefile("<filepath$dir>.log", "Hello") // Write to file
appended = appendfile("<filepath$dir>.log", "World") // Append to file
content = readfile("<filepath$dir>.log")        // Read file contents
```

#### System & SWI Functions
```oakscript
// RISC OS SWI calls
result = swi("OS_CLI", "Echo Hello")   // Execute SWI
error_code = swi_error()               // Get last SWI error
status = status()                      // Get execution status
```

#### Variable & Array Functions
```oakscript
// Variable management
ref = reference("varname")             // Create reference
info = variable_print_info()           // Print variable info
current_time = time()                  // Get current time

// Array operations
arr = array(10)                        // Create array with capacity 10
array_set(arr, 0, 42)                 // Set element: arr[0] = 42
value = array_get(arr, 0)              // Get element: 42

// Buffer operations
buffer = bytes(1024)                   // Create byte buffer
block = block(10, 4)                   // Create structured block
updated = update_buffer(buffer, data)  // Update buffer contents
```

#### Debug Functions
```oakscript
// Debugging support
debug_on()                     // Enable debug mode
debug_off()                    // Disable debug mode
debug_print("Debug message")   // Debug output
debug_logpath("<filepath$dir>.debug")    // Set debug log path
```

#### System Integration
```oakscript
// External command execution
exec("*Cat filename")          // Execute system command
result = exec_output("*Dir")   // Execute and capture output
```

## Advanced Language Features

OakScript now includes modern programming language features that make it suitable for complex applications:

### Advanced Data Structures

#### Dictionaries/Maps
```oakscript
// Create and manipulate dictionaries (values stored as strings)
config = dict()
dict_set(config, "host", "localhost")
dict_set(config, "port", "8080")

host = dict_get(config, "host")
has_port = dict_has(config, "port")
size = dict_size(config)
keys = dict_keys(config)

dict_remove(config, "port")
```

#### Dynamic Lists
```oakscript
// Create and manipulate lists (lists store strings)
items = list()
list_append(items, "42")
list_append(items, "hello")
list_prepend(items, "true")

first = list_get(items, 0)
list_set(items, 1, "world")
list_remove(items, 2)
length = list_size(items)
```

#### Sets (Unique Collections)
```oakscript
// Create and manipulate sets
numbers = set()
set_add(numbers, 1)
set_add(numbers, 2)
set_add(numbers, 1)  // Duplicate ignored

has_one = set_contains(numbers, 1)
set_remove(numbers, 2)
count = set_size(numbers)

// Set operations
set1 = set()
set2 = set()
union_set = set_union(set1, set2)
intersection = set_intersection(set1, set2)
```

### Advanced String Features

#### String Interpolation
```oakscript
// Template strings with variable substitution
name = "World"
age = 25
message = interpolate("Hello ${name}, you are ${age} years old!")
// Result: "Hello World, you are 25 years old!"

// Complex expressions in interpolation
total = interpolate("Total: ${price * quantity + tax}")
```

#### Multi-line Strings
```oakscript
// Multi-line strings with escape sequences
poem = multiline("""
Roses are red,
Violets are blue,
OakScript is awesome,
And so are you!
""")

// Raw strings with escape sequences
path = multiline("C:\\Users\\Name\\Documents\\file.txt")
```

#### Regular Expressions
```oakscript
// Compile and use regular expressions
email_pattern = regex("\\w+@\\w+\\.\\w+", 0)
is_valid = regex_match(email_pattern, "user@example.com")

// Find all matches
text = "Contact: john@example.com or mary@test.org"
matches = regex_find_all(email_pattern, text)

// Replace with pattern
cleaned = regex_replace(email_pattern, text, "[EMAIL]")
```

### Modern Control Flow

#### Pattern Matching
```oakscript
// Match statements with patterns
match value
    case 1 => print "One"
    case 2..10 => print "Small number"
    case _ => print "Something else"
end

// Type-based matching (typeof returns a type id; also prints the type name)
match typeof("variable")
    case 1 => print "Integer value"
    case _ => print "Other type"
end
```

#### Enhanced Loops
```oakscript
// For-in loops with ranges
for i in 1..10 do
    print i
end

// For-in with step
for i in 0..100 step 5 do
    print i
end

// For-in with collections (iterate by index)
items = list()
list_append(items, "1")
list_append(items, "2")
list_append(items, "3")
len = list_size(items)
for i in 0..len-1 do
    // use list_get(items, i) for value when supported
    print i
end

// Enhanced for loops with break/continue
for i in 1..100
    if i % 15 == 0 then
        continue
    end
    if i > 50 then
        break
    end
    print i
end
```

#### Range Expressions
```oakscript
// Create and use ranges
numbers = range(1, 10, 1)       // Start, end, step
even_numbers = range(0, 20, 2)
reverse = range(10, 1, -1)
```

### Functional Programming

#### Lambda Functions
```oakscript
// Define lambda functions
square = lambda(x) => x * x
add = lambda(a, b) => a + b
greet = lambda(name) => "Hello, ${name}!"

// Use lambdas
result = square(5)              // Returns 25
sum = add(10, 15)              // Returns 25
message = greet("Alice")        // Returns "Hello, Alice!"
```

#### Higher-Order Functions
```oakscript
// Map operation
numbers = [1, 2, 3, 4, 5]
squared = map(numbers, lambda(x) => x * x)
// Result: [1, 4, 9, 16, 25]

// Filter operation
evens = filter(numbers, lambda(x) => x % 2 == 0)
// Result: [2, 4]

// Reduce operation
sum = reduce(numbers, lambda(acc, x) => acc + x, 0)
// Result: 15

// Function composition
double = lambda(x) => x * 2
increment = lambda(x) => x + 1
double_then_increment = compose(increment, double)
result = double_then_increment(5)  // (5 * 2) + 1 = 11
```

#### Partial Application and Currying
```oakscript
// Partial application
multiply = lambda(a, b) => a * b
double = partial(multiply, 2)
result = double(5)  // 2 * 5 = 10

// Currying
add_curry = curry(lambda(a, b, c) => a + b + c)
add_five = add_curry(5)
add_five_ten = add_five(10)
result = add_five_ten(3)  // 5 + 10 + 3 = 18

// Function memoization for performance
fibonacci = memoize(lambda(n) => 
    if n <= 1 then n else fibonacci(n-1) + fibonacci(n-2)
)
```

### Enhanced Error Handling

#### Specific Exception Types
```oakscript
// Built-in exception types
try
    result = divide(10, 0)
catch DivisionByZero as e
    print "Cannot divide by zero: ${exception_message(e)}"
catch RuntimeError as e
    print "Runtime error occurred: ${exception_message(e)}"
catch Exception as e
    print "General error: ${exception_type(e)}"
finally
    print "Cleanup operations"
end
```

#### Custom Exception Types
```oakscript
// Define custom exception types
define_exception("ValidationError", "ValueError", "Input validation failed")
define_exception("NetworkTimeout", "NetworkError", "Network operation timed out")

// Throw custom exceptions
if age < 0 then
    throw("ValidationError", "Age cannot be negative")
end

// Create and throw exceptions programmatically
error = create_exception("CustomError", "Something went wrong")
throw_exception(error)
```

#### Exception Hierarchy
```oakscript
// Exception inheritance and type checking
try
    risky_operation()
catch ValueError as e
    // Catches ValueError and all its subtypes
    print "Value error: ${exception_message(e)}"
catch Exception as e
    // Catches any other exception
    print "Unexpected error: ${exception_type(e)}"
end
```

### Advanced Type Features

#### Optional Types
```oakscript
// Optional values that can be null (functions take variable names as strings)
name_var = "Alice"
user_name = optional_create("name_var")
empty_value = optional_create()

if optional_has_value(user_name) then
    value = optional_get(user_name)
    print "User: ${value}"
else
    print "No user name provided"
end

// Safe optional chaining
result = user_name?.upper()?.length()
```

#### Union Types
```oakscript
// Variables that can hold multiple types
id = union_create("int", "string")
union_set(id, 12345, "int")        // Store as integer
union_set(id, "USER001", "string") // Store as string

current_type = union_get_type(id)
if current_type == "string" then
    print "ID is a string: ${union_get(id)}"
end
```

#### Type Checking and Conversion
```oakscript
// Runtime type checking (pass variable names as strings)
value = 42
type_id = typeof("value")
is_number = is_type("value", "int")
is_empty = is_null("value")

// Type conversion (pass variable names as strings)
text_number = "123"
number = cast("text_number", "int")
back_to_text = cast("number", "string")

// Type compatibility checking
can_convert = is_compatible_type("int", "float")  // true
```

#### Generic Types (Simplified)
```oakscript
// Generic function definitions (conceptual)
function identity<T>(value: T): T
    return value
end

// Type-safe collections
int_list = list<int>()
string_dict = dict<string, string>()
```

### Advanced Built-in Functions

The enhanced OakScript now includes over **100 built-in functions**:

#### Data Structure Functions
- **Dictionary**: `dict()`, `dict_set()`, `dict_get()`, `dict_has()`, `dict_remove()`, `dict_size()`, `dict_keys()`
- **List**: `list()`, `list_append()`, `list_get()`, `list_set()`, `list_remove()`, `list_size()`
- **Set**: `set()`, `set_add()`, `set_contains()`, `set_remove()`, `set_size()`, `set_union()`, `set_intersection()`

#### Functional Programming
- **Lambda**: `lambda()`, `map()`, `filter()`, `reduce()`, `compose()`, `partial()`, `curry()`, `memoize()`

#### String Processing
- **Interpolation**: `interpolate()`, `multiline()`
- **Regex**: `regex()`, `regex_match()`, `regex_find_all()`, `regex_replace()`

#### Type System
- **Type Checking**: `typeof()`, `is_type()`, `is_null()`, `cast()`
- **Optional**: `optional_create()`, `optional_has_value()`, `optional_get()`
- **Union**: `union_create()`, `union_set()`, `union_get()`, `union_get_type()`

#### Exception Handling
- **Exceptions**: `throw()`, `create_exception()`, `define_exception()`, `exception_type()`, `exception_message()`

#### Control Flow
- **Pattern Matching**: `match()`, `range()`
- **Collections**: `foreach()`, `range_create()`

## Bytecode Format

OakScript uses a custom bytecode format optimised for the virtual machine:

- **Header**: 20-byte header with magic number "OAKSCODE", version, and section sizes
- **Code Section**: Sequence of opcodes and operands for execution
- **Data Section**: String constants referenced by the code

The bytecode format is platform-independent, allowing for cross-platform development tools whilst maintaining RISC OS-specific runtime features.

## Implementation Details

### Memory Management
- Module-safe memory allocation using `mod_malloc`/`mod_free`
- Automatic cleanup on program termination
- No memory leaks or unsafe pointer operations

### Stack-Based Execution
- Similar to JVM or .NET CLR execution model
- LIFO stack for expression evaluation
- Type safety with runtime checking

### Error Handling
- Comprehensive error reporting with context information
- Graceful handling of runtime errors
- Memory cleanup on error conditions

## Project Structure

```
OakScript/
├── Source/          # C source code
│   ├── c/          # Implementation files
│   ├── h/          # Header files
│   ├── cmhg/       # CMHG module definition
│   └── Makefile    # Build configuration
├── Docs/           # Technical documentation
│   ├── Bytecode    # Bytecode format specification
│   ├── Compiler    # Compiler design documentation
│   ├── OpCodes     # Virtual machine instruction reference
│   └── Runtime     # Runtime architecture documentation
├── Examples/       # Example scripts and test cases
└── !OakScript/     # RISC OS application directory
    ├── !Boot       # Application bootstrap
    ├── !Run        # Application launcher
    └── !Help       # User documentation
```

## Development

### Building

OakScript is built using the Acorn C/C++ compiler and AMU (Acorn Make Utility) on RISC OS:

```
*AMU clean
*AMU all
```

**Requirements:**
- Acorn C/C++ Development Suite
- AMU (Acorn Make Utility)  
- CMHG (C Module Header Generator)
- RISC OS development environment

**Build Process:**
1. The Makefile uses AMU-specific syntax and RISC OS path conventions
2. CMHG generates the module header from `cmhg.header`
3. Acorn C compiler builds all source files with RISC OS-specific flags
4. Final output is a RISC OS module (`OakScript`) ready for loading

### Testing
The `Examples/` directory contains comprehensive test scripts that exercise all language features and opcodes.

## Technical Specifications

- **Target Platform**: RISC OS (ARM 32-bit)
- **Memory Model**: Module-safe dynamic allocation with garbage collection for advanced types
- **Execution Model**: Stack-based virtual machine with closure support
- **File Format**: Custom bytecode with 20-byte header supporting advanced features
- **Instruction Set**: 60+ opcodes covering all language features including advanced constructs
- **Type System**: 22 distinct types with optional/union type support and runtime type checking
- **Function Model**: First-class functions with lambda support, closures, and higher-order functions
- **Exception Model**: Hierarchical exception system with custom types and stack traces

## Copyright

Copyright © 2025 Andrew Timmins. All rights reserved.

OakScript is designed specifically for the RISC OS platform and integrates seamlessly with the RISC OS module system and memory management.
