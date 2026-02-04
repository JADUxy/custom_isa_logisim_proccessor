🚀 LISA – Lightweight Instruction Set Architecture Processor

LISA is a custom-designed 16-bit multi-cycle processor architecture built completely from scratch at the hardware-logic level.
It includes a full stack of components:

Custom ISA design

Hardwired Control Unit

Multi-cycle datapath

Address Generation Unit (AGU)

Stack-based execution model

Memory-mapped I/O

Custom assembler

Custom C++-like compiler

End-to-end toolchain

This project was built to deeply understand how real CPUs work internally, from instruction fetch and decode to execution, memory access, and I/O.

Unlike emulators or high-level simulators, every component is explicitly designed at register-transfer and control-signal level, similar to how real processors are implemented.

✨ Key Highlights

✅ Designed a complete instruction set architecture
✅ Hardwired control logic (no microcode)
✅ Multi-cycle execution using one-hot ring counters
✅ Stack + heap + global base addressing
✅ Custom compiler + assembler
✅ Memory-mapped I/O peripherals
✅ Built and tested full programs end-to-end

🧠 Architecture Overview

LISA follows a multi-cycle CPU design with a shared bus datapath.

Instead of executing an instruction in a single clock cycle, each instruction is divided into multiple deterministic phases:

Fetch → Decode → Operand Read → Execute → Writeback → Commit


This design:

simplifies hardware

reduces combinational complexity

improves scalability

mirrors educational CPUs like MIPS multi-cycle designs

⚙️ Core Components
1️⃣ Control Unit (CU)

The processor uses a hardwired control unit, not microcode.

Design

6-bit opcode

6 → 64 one-hot decoder

Each instruction activates exactly one control line

Control signals generated through combinational OR networks

Timing

Execution is driven by:

Dual ring counters

Main step counter → instruction phases

Sub-cycle counter → operand phases

Benefits

deterministic timing

simple debugging

easy hardware mapping

no microprogram memory needed

2️⃣ Instruction Fetch Unit

Instruction width: 64 bits
ROM width: 32 bits

So each instruction requires two fetch cycles.

Fetch sequence

Address ROM using SP/PC

Load upper 32 bits into IR

Increment pointer

Load lower 32 bits into IR

After this, decode begins.

Why?

Reduces ROM complexity

Saves memory width

Simplifies hardware wiring

3️⃣ Instruction Format
| opcode (6) | addr1 (16) | addr2 (16) | addr3 (16) | spare (2) | mode (6) | size (2) |

Fields
Opcode

Selects instruction

addr1, addr2, addr3

Memory or register offsets

mode

Selects base addressing behavior

size

Controls:

memory width

ALU width

stack increment/decrement size

spare

Reserved for future expansion

4️⃣ Datapath

LISA uses a shared bus architecture:

single memory bus

mutually exclusive drivers

operand registers

ALU

stack pointer unit

AGU

Registers

Read Register 1 → memory data

Read Register 2 → memory OR immediate (mux controlled)

Write register → memory output

IR → 64-bit instruction

5️⃣ Address Generation Unit (AGU)

All memory accesses use:

effective_address = base + offset

Base registers

BP → stack frame

HP → heap

GN → global/static memory

Offset sources

instruction fields

stack pointer

register-indirect values

Supported modes

direct

stack-relative

heap-relative

register-indirect

dynamic addressing

Benefit

No absolute addressing → relocatable programs

6️⃣ Stack Pointer Unit

Dedicated arithmetic unit for SP updates.

Supports:

push

pop

inc/dec

direct assignment

memory-based updates

Timing

pre-update (pop)

post-update (push)

This mirrors real CPU stack behavior.

7️⃣ ALU

Handles:

arithmetic

logic

comparison

data movement

Width determined dynamically by size field.

8️⃣ Memory-Mapped I/O
Devices
Character display

7-bit ASCII output

prints to console

GPIO pins

digital outputs

external hardware control

Why memory-mapped?

Simplifies instruction set
No special I/O instructions needed

🛠 Toolchain

The processor includes a complete software stack:

Assembler

converts assembly → machine code

Custom C++-like compiler

high-level language

compiles to LISA assembly

supports structured programming

Execution flow
Source Code → Compiler → Assembly → Assembler → Machine Code → ROM → LISA CPU

📚 Learning Goals

This project was built to understand:

CPU microarchitecture

Control logic design

Instruction set design

Memory addressing modes

Stack machines

Hardware timing

Compiler backend basics

🎯 Why This Project Matters

This is not just a simulator.

It demonstrates:

real hardware thinking

control signal design

bus arbitration

cycle-level execution

architectural tradeoffs

Skills gained here directly map to:

Computer Architecture

Embedded Systems

OS internals

Compiler design

FPGA/RTL design

Systems engineering

🚧 Future Improvements

pipelining

interrupts

caching

virtual memory

branch prediction

multitasking support

debugger

FPGA implementation

📌 Project Status

✅ Architecture finalized
✅ Control unit complete
✅ Datapath working
✅ Compiler + assembler functional
✅ End-to-end programs running

