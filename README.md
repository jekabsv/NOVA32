# NOVA32

NOVA32 is a custom 32-bit RISC CPU core implemented in Verilog for FPGA targets. It uses a 6-stage pipeline, supports user and kernel modes, system calls, and is intended to later support MMU, external DRAM with cache, branch prediction, and multi-threading.

# Core Specifications
- 32-bit data width
- 6 pipeline stages: IF, ID, Issue, EX, MEM, WB
- 30 general purpose registers (R0-R29)
- R0 is constant zero (writes ignored)
- R31 is LINK register
- SP (stack pointer), PC (program counter)
- FLAGS register with N, E, V, C bits
- MODE register for user/kernel mode
- Dedicated kernel SP and kernel PC for interrupts and traps

# Pipeline Stages
IF   Instruction Fetch  
ID   Instruction Decode  
Issue Operand selection and hazard resolution  
EX   ALU and branch evaluation  
MEM  Data memory access  
WB   Write results to register file

# Privilege Model
- User mode for applications
- Kernel mode for OS and system control
- SysCall transitions to kernel mode
- IRET returns to user mode
- WFI for interrupt waiting
- Kernel has separate SP and PC for interrupt handling

# Memory
Current: 1-cycle BRAM  
Planned: External DRAM via memory controller  
BRAM will become CPU cache  
Planned prefetch and branch prediction

# Register Set
R0   constant zero  
R1-R29 general purpose  
R31  LINK  
SP   user stack pointer  
PC   program counter  
FLAGS condition flags  
MODE privilege mode  
SP_K kernel stack pointer  
PC_K kernel program counter

# ALU and Logical Instructions
ADD SUB ADC SBC  
AND OR XOR NOT  
BIC BSET BTG BCL  
MOV  
VLSL VLSR VASR  
VROL VROR VROLC VRORC  
XNOR NAND NOR  
INC DEC  
MUL  
CLZ MIN MAX ABS NEG

# General Instructions
NOP  
HLT (kernel only)  
LDI  
LDW LDB LDH  
STW STB STH  
PUSH POP  
ADDI SUBI ANDI ORI XORI CMPI  
BRANCH (relative, conditional, optional link)  
JMP (absolute)  
RET (jump to LINK)  
MRF (reg to FLAGS, kernel only)  
MFR (FLAGS to reg)  
WFI  
SysCall (trap to kernel, sets LINK)  
MovPC  
PCMov (kernel only)  
SysCfg (kernel only)  
IRET  
SPMOV (SP to reg, kernel only)  
MOVSP (reg to SP, kernel only)

# Future Development
- MMU with paging
- External DRAM + cache hierarchy
- Branch prediction
- Instruction prefetch
- Hardware multithreading
- Multi-core scaling
