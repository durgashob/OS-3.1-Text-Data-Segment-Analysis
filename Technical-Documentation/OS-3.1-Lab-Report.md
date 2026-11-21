# OS-3.1 Lab Report
## Auditing of Text and Initialized Data Segments via Hardware Disassembly

### 1. Introduction

This practical investigates the memory organization of a compiled C program. It focuses on the Text, Data, and Read-Only Data (ROData) segments.

Linux tools such as GCC, GDB, readelf, and objdump were used to compile, execute, debug, and analyze the program.

### 2. Objectives

- Understand the memory layout of a C program.
- Identify Text, Data, and Read-Only Data segments.
- Compile and execute a C program using GCC.
- Inspect memory addresses using GDB.
- Analyze ELF sections using readelf.
- Examine machine instructions using objdump.
- Understand Little Endian byte representation.

### 3. Tools and Environment

| Tool | Purpose |
|---|---|
| Ubuntu Linux | Operating environment |
| Docker | Linux environment |
| GCC | C compiler |
| GDB | Debugging and memory inspection |
| readelf | ELF section analysis |
| objdump | Disassembly and binary inspection |

### 4. Source Code

The program contains an initialized global integer, a string literal, and a function.

File: `demo2.c`

```c
#include <stdio.h>

int data_global_var = 0x12345678;

const char *text_string_literal = " Text_Segment_Verification";

void check_execution() {
    printf("Executing within the text segment instruction block.\n");
}

int main() {
    printf("Addresses:\n");

    printf("Data (Global Initialized): %p\n",
           (void*)&data_global_var);

    printf("Text String (ROData): %p\n",
           (void*)text_string_literal);

    printf("Text Code (Function): %p\n",
           (void*)&check_execution);

    check_execution();

    printf("Ready for Text/Data segment inspection!\n");

    return 0;
}
```

### 5. Compilation and Execution

The program was compiled using:

```bash
gcc -g demo2.c -o demo2
```

The `-g` option includes debugging information.

The program was executed using:

```bash
./demo2
```

The program successfully displayed the memory addresses of the initialized global variable, string literal, and function.

### 6. Debugging and Memory Inspection Using GDB

GDB was used to inspect the program during execution.

```bash
gdb ./demo2
```

A breakpoint was set:

```gdb
break 22
run
```

The following commands were used:

```gdb
info files
print &data_global_var
x/wx &data_global_var
print text_string_literal
x/s text_string_literal
print &text_string_literal
continue
```

**Observations:**

- `data_global_var` was located in the Data segment.
- The string literal was located in the Read-Only Data segment.
- The `check_execution()` function was located in the Text segment.
- GDB successfully displayed the memory addresses and variable contents.

### 7. ELF Section Analysis Using readelf

The following command was used:

```bash
readelf -S demo2
```

The important ELF sections identified were:

| Section | Address | Size |
|---|---:|---:|
| `.text` | `0x1080` | `0x194` |
| `.rodata` | `0x2000` | `0xE8` |
| `.data` | `0x4000` | `0x20` |
| `.bss` | `0x4020` | `0x08` |

**Section explanations:**

- `.text`: Contains executable machine instructions.
- `.rodata`: Contains read-only constants and string literals.
- `.data`: Contains initialized global and static variables.
- `.bss`: Contains uninitialized or zero-initialized global and static variables.

Note: These addresses are ELF section virtual addresses. Runtime addresses displayed by GDB can differ because of relocation and Address Space Layout Randomization (ASLR).

### 8. Disassembly Analysis Using objdump

The executable was disassembled using:

```bash
objdump -d demo2
```

To inspect a particular function:

```bash
objdump -d demo2 | grep -A 15 "<check_execution>"
```

This displayed the machine instructions associated with the `check_execution()` function.

Disassembly helped demonstrate how C source code is translated into machine instructions stored in the Text segment.

### 9. Raw Memory and Little Endian Analysis

The Data section was examined using:

```bash
objdump -s -j .data demo2
```

The output included:

```text
4010 78563412 00000000 08200000 00000000
```

The initialized integer was:

```text
0x12345678
```

Its bytes appeared in memory as:

```text
78 56 34 12
```

This demonstrates Little Endian byte ordering, where the least significant byte is stored first.

### 10. Post-Lab Questions and Answers

**Q1. What is the difference between Little Endian and Big Endian?**

Little Endian stores the least significant byte at the lowest memory address. Big Endian stores the most significant byte at the lowest memory address.

For example, the value `0x12345678` is represented as:

- Little Endian: `78 56 34 12`
- Big Endian: `12 34 56 78`

**Q2. Why are Text and Read-Only Data segments separated?**

The Text segment contains executable instructions, whereas the Read-Only Data segment contains constants and string literals.

Separating them allows different memory permissions to be applied. The Text segment is typically executable and read-only, while the Read-Only Data segment is non-executable and read-only. This improves memory organization and helps protect program data.

### 11. Conclusion

This practical provided an understanding of how a compiled C program is organized in memory.

Using GCC, GDB, readelf, and objdump, the Text, Data, and Read-Only Data segments were investigated. The practical also demonstrated ELF section analysis, machine-code disassembly, runtime memory inspection, and Little Endian byte ordering.

Overall, the investigation improved my understanding of Linux memory organization and executable binary analysis.
