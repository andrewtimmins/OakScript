# OakScript

**Version 0.04** • A lightweight scripting language for RISC OS

OakScript is a simple, intuitive scripting language designed for rapid prototyping, automation, and educational purposes on the RISC OS platform. With its clear syntax and straightforward commands, OakScript enables users to quickly write scripts for a variety of tasks, from basic calculations to more complex logic and data manipulation.

## Features

- **Simple Syntax**: Clear, readable code that's accessible to both beginners and experienced programmers
- **Core Data Types**: Support for integers, strings, booleans, and floating-point numbers
- **Variables & Expressions**: Dynamic variable assignment with arithmetic and comparison operations
- **Control Flow**: If statements and while loops for program logic
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

- **`.oak`** - OakScript source files (Type EEE)
- **`.eef`** - Compiled bytecode files (Type EEF)

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

### Variables
```oakscript
name = "OakScript"
version = 4
pi = 3.14159
```

### Arithmetic Operations
```oakscript
sum = a + b
difference = a - b
product = a * b
quotient = a / b
```

### Comparisons
```oakscript
equal = (a == b)
not_equal = (a != b)
less_than = (a < b)
greater_equal = (a >= b)
```

### Control Flow
```oakscript
if x > 0 then
    print "Positive"
end

while count < 10
    count = count + 1
end
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
written = writefile("log.txt", "Hello") // Write to file
appended = appendfile("log.txt", "World") // Append to file
content = readfile("data.txt")        // Read file contents
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
```bash
make clean
make all
```

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
