# OakScript

**Version 0.04** • A lightweight scripting language for RISC OS

OakScript is a simple, intuitive scripting language designed for rapid prototyping, automation, and educational purposes on the RISC OS platform. With its clear syntax and straightforward commands, OakScript enables users to quickly write scripts for a variety of tasks, from basic calculations to more complex logic and data manipulation.

## Features

- **Simple Syntax**: Clear, readable code that's accessible to both beginners and experienced programmers
- **Rich Type System**: 12 variable types including integers, strings, booleans, floats, arrays, buffers, blocks, references, pointers, files, and time values
- **Advanced Variable Operations**: Compound assignment operators (+=, -=, *=, /=), increment/decrement, automatic type conversion, and variable introspection
- **Advanced Control Flow**: If-else, switch-case, while loops, for loops with ranges/steps, break/continue, user-defined functions, try-catch exception handling, and file inclusion
- **Extensive Built-in Library**: 50+ built-in functions covering mathematics, strings, files, arrays, debugging, and RISC OS system integration
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
while counter < 3
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
while counter < 10
    print counter
    counter = counter + 1
end

// For loop with range
for i = 1 to 10
    print i
end

// For loop with step
for i = 0 to 100 step 5
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
- **Memory Model**: Module-safe dynamic allocation
- **Execution Model**: Stack-based virtual machine
- **File Format**: Custom bytecode with 20-byte header
- **Instruction Set**: 40+ opcodes covering all language features

## Copyright

Copyright © 2025 Andrew Timmins. All rights reserved.

OakScript is designed specifically for the RISC OS platform and integrates seamlessly with the RISC OS module system and memory management.
