# OakScript

**Version 0.04** • A lightweight scripting language for RISC OS

OakScript is a simple, intuitive scripting language designed for rapid prototyping, automation, and educational purposes on the RISC OS platform. With its clear syntax and straightforward commands, OakScript enables users to quickly write scripts for a variety of tasks, from basic calculations to more complex logic and data manipulation.

## Features

- **Simple Syntax**: Clear, readable code that's accessible to both beginners and experienced programmers
- **Core Data Types**: Support for integers, strings, booleans, and floating-point numbers
- **Variables & Expressions**: Dynamic variable assignment with arithmetic and comparison operations
- **Control Flow**: If statements and while loops for program logic
- **Built-in Functions**: Mathematical functions (`abs`, `min`, `max`) and utility functions
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
```oakscript
absolute = abs(-42)        // Returns 42
minimum = min(10, 20)      // Returns 10
maximum = max(10, 20)      // Returns 20
exists = file_exists()     // Placeholder function
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
