# Design of 5 Stage Pipelined MIPS32 RISC Processor  
This repository contains the details and the code for the MIPS32 ISA based RISC Processor, which is implemented in 5 stage pipelined configuration.  
## ▫️ MIPS32  
- 32 x 32 bit GPRs [R0 to R31]  
- R0 hardwired to logic0  
- 32 bit Program Counter (PC)  
- No flag registers (carry, zero, sign..etc)  
- Few Addresing Modes  
- Only Load and Store instructions can access memory  
- We assume memory word size is 32 bits (word addressable)  
## ▫️ Addressing Modes  
| Addressing Mode | Example Instruction |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Register addressing | ADD R1,R2,R3      |
| Immediate addressing | ADDI R1,R2, 100       |
| Base addressing      | LW R5, 100(R4)    |
| PC relative addressing  | BEQZ R3, Label   |
| Pseudo-direct addressing | J Label      |

## ▫️ Instruction Encoding  
![ISR](https://user-images.githubusercontent.com/68592620/231771092-0c93aeb3-6b01-478f-a363-ecadb1ec578a.png)  
- shamt : shift amount, funct : opcode extension for additional functions.
- Some instructions require two register operands rs & rt as input, while some require only rs. 
- This requirement is only identified only after the instruction is decoded. 
- While decoding is going on, we can prefetch the registers in parallel, which may or may not be used later. 
- Similarly, the 16-bit and 26-bit immediate data are retrieved and signextended to 32-bits in case they are required later.  
## ▫️ Stages of Execution  
The instruction execution cycle contains the following 5 stages in order:  
1. IF : Instruction Fetch  
2. ID : Instruction Decode / Register Fetch  
3. EX : Execution / Effective Address Calculation  
4. MEM : Memory Access / Branch Completion  
5. WB : Register Write-back  
- micro operations not shown here.
## ▫️ Non Pipelined DataPath  
![nonpipelined](https://user-images.githubusercontent.com/68592620/231771101-f7ea7e00-5c8c-4b6d-ae0c-a0419066e7ad.png)  
## ▫️ Pipelined DataPath  
![pipelined](https://user-images.githubusercontent.com/68592620/231771102-12c05fa9-6e74-4835-abc6-1bd9b20e8453.png)  
## ▫️ EDAplayground Link  
[https://edaplayground.com/x/t8Vx](https://edaplayground.com/x/t8Vx )  
## ▫️ Known problems and issues  
Following pipelining hazards are present in the given design :  
- Structural Hazards due to shared hardware.  
- Data Hazards due to instruction data dependency.  
- Control hazards due to branch instructions.  
## ▫️ References  
[NPTEL \& IIT KGP 'Hardware Modeling using Verilog'- Prof. Indranil Sengupta](https://nptel.ac.in/courses/106105165)
