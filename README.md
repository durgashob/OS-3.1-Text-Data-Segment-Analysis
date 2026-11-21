# OS-3.1: Auditing of Text and Initialized Data Segments via Hardware Disassembly

## Overview

This project focuses on understanding and analyzing the memory organization of a C program, particularly the Text, Data, and Read-Only Data (ROData) segments.

The practical investigation uses Linux debugging and binary analysis tools to examine how program instructions, initialized global variables, and string literals are stored in memory.

## Objectives

- Understand the memory layout of a compiled C program.
- Identify the Text, Data, and Read-Only Data segments.
- Compile and execute a C program in Linux.
- Inspect memory addresses using GDB.
- Analyze ELF sections using `readelf`.
- Examine machine instructions using `objdump`.
- Understand Little Endian byte representation.

## Tools and Technologies

- **Operating System:** Ubuntu Linux
- **Environment:** Docker
- **Programming Language:** C
- **Compiler:** GCC
- **Debugger:** GDB
- **Binary Analysis:** readelf and objdump
- **Version Control:** Git and GitHub

## Repository Structure

```text
OS-3.1-Text-Data-Segment-Analysis/
│
├── README.md
│
├── Source-Code/
│   └── demo2.c
│
├── Screenshots/
│   └── .gitkeep
│
└── Technical-Documentation/
    └── OS-3.1-Lab-Report.md
```

## Practical Tasks

1. Writing and compiling a C program.
2. Executing the compiled program.
3. Inspecting memory addresses using GDB.
4. Identifying ELF sections using readelf.
5. Disassembling executable instructions using objdump.
6. Examining raw memory contents.
7. Understanding Little Endian representation.

## Key Concepts

| Memory Segment | Purpose |
|---|---|
| `.text` | Stores executable instructions |
| `.rodata` | Stores read-only data such as string literals |
| `.data` | Stores initialized global and static variables |
| `.bss` | Stores uninitialized or zero-initialized global and static variables |

## Learning Outcomes

Through this practical investigation, I explored how compiled C programs are organized in memory and how debugging and binary analysis tools can be used to inspect executable files and their memory sections.

## Author

**Durga Shob**

BSc (Hons) Ethical Hacking and Cyber Security

## License

This project is created for educational and academic purposes.
