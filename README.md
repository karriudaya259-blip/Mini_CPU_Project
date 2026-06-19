# Mini_CPU_Project
# Tiny CPU - 5-Stage Pipelined RISC Core

**Brief:** A 5-stage pipelined RISC CPU (IF → ID → EX → MEM → WB) with forwarding, hazard detection, and static branch prediction. Designed in Verilog as part of my 100-day VLSI journey.

**Tools Used:** Verilog HDL, Icarus Verilog, GTKWave.

**Quick Run:**
```bash
iverilog -o cpu_sim tiny_cpu.v tb_tiny_cpu.v
vvp cpu_sim
gtkwave dump.vcd
