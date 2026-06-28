# Mini CPU — 8-bit CPU in Verilog (Fetch-Decode-Execute)

A simple 8-bit CPU designed and simulated in Verilog — implementing the classic fetch-decode-execute cycle with a custom instruction set, program counter, ALU, register file, and instruction memory.

**Tools:** Icarus Verilog · GTKWave  
**Language:** Verilog HDL  
**Architecture:** 8-bit · Custom ISA · Single-cycle

---

## 🧠 Architecture Overview

```
        ┌─────────────┐
        │  Instruction │
        │  Memory (ROM)│
        └──────┬───────┘
               │ instr[7:0]
        ┌──────▼───────┐
        │    Decoder    │
        │  (opcode +   │
        │   operands)  │
        └──────┬───────┘
          ┌────┴─────┐
          ▼          ▼
   ┌─────────┐  ┌──────────┐
   │ Register│  │   ALU    │
   │  File   │  │(ADD/SUB/ │
   │ (8 regs)│  │AND/OR/   │
   └────┬────┘  │NOT/MOV)  │
        │       └────┬─────┘
        └────────────▼
              ┌────────────┐
              │  Program   │
              │  Counter   │
              │  (PC + 1)  │
              └────────────┘
```

---

## 📋 Instruction Set (Custom ISA)

| Opcode | Instruction | Operation |
|---|---|---|
| `000` | `ADD Rd, Rs` | Rd = Rd + Rs |
| `001` | `SUB Rd, Rs` | Rd = Rd - Rs |
| `010` | `AND Rd, Rs` | Rd = Rd & Rs |
| `011` | `OR Rd, Rs` | Rd = Rd \| Rs |
| `100` | `NOT Rd` | Rd = ~Rd |
| `101` | `MOV Rd, imm` | Rd = immediate value |
| `110` | `LOAD Rd, addr` | Rd = Memory[addr] |
| `111` | `HLT` | Halt execution |

**Instruction format (8-bit):**
```
[7:5] opcode | [4:3] Rd | [2:0] Rs / immediate
```

---

## 🏗️ Modules

| Module | Description |
|---|---|
| `program_counter.v` | Increments PC each cycle, resets to 0 |
| `instruction_memory.v` | ROM — stores the program instructions |
| `decoder.v` | Decodes 8-bit instruction into control signals |
| `register_file.v` | 8 general-purpose 8-bit registers |
| `alu.v` | Performs ADD, SUB, AND, OR, NOT operations |
| `mini_cpu.v` | Top-level integration of all blocks |
| `mini_cpu_tb.v` | Testbench — runs a test program and checks outputs |

---

## 📊 Test Program

The testbench loads this program into instruction memory:

```
MOV R0, 5      // R0 = 5
MOV R1, 3      // R1 = 3
ADD R0, R1     // R0 = 8
SUB R0, R1     // R0 = 5
HLT            // Stop
```

Expected waveform output: R0 = 8 after ADD, R0 = 5 after SUB.

---

## 🛠️ How to Simulate

```bash
iverilog -o mini_cpu.vvp program_counter.v instruction_memory.v decoder.v register_file.v alu.v mini_cpu.v mini_cpu_tb.v
vvp mini_cpu.vvp
gtkwave mini_cpu.vcd


## 🔗 Links

- 📂 [100 Days VLSI Journey](https://github.com/jyoshnakarri/100-days-vlsi)
- 📂 [Full Verilog Portfolio](https://jyoshnakarri.github.io/Verilog_Codes/)
- 💼 [LinkedIn](https://www.linkedin.com/in/jyoshna-k-5b1626401/)
