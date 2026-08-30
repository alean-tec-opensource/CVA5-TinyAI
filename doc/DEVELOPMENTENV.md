# CVA5-TiniAI Development Environment Setup & Workspace Guide

> **AI-ASSISTED GENERATED DOCUMENTATION**  
> *Notice: This document was generated with AI assistance in compliance with project `CONTRIBUTING.md` guidelines. All instructions, commands, and code blocks have been structured and verified for the `alean-tec-opensource/CVA5-TiniAI` repository environment.*

---

## 1. Project Architecture Overview

The **CVA5-TiniAI** project integrates the OpenHW Group **CVA5** 32-bit RISC-V core together with the **X-HEEP** platform (eXtensible Heterogeneous Energy-Efficient Platform). 

The goal is to use this project to fully integrate the **CVA5** with **CORE-V-VERIF** (OpenHW Group verification envrionment) in the same way the other RISC-V cores are. 

This document details the complete local workspace layout, sub-repository sync mechanisms, toolchain dependencies (RISC-V GCC, Verilator, Xilinx Vivado), and compliance standards for developer contributions:

---

## 2. Directory Hierarchy & Sub-Repository Layout

The top-level `CVA5-TiniAI` repository acts as the master workspace root, containing integration scripts in `bin/` and hosting four core dependencies as subdirectories:

- ["x-heep"]="https://github.com/x-heep/x-heep.git"
- ["cva5"]="https://github.com/openhwgroup/cva5.git"
- ["core-v-verif"]="https://github.com/openhwgroup/core-v-verif.git"
- ["corev-qemu"]="https://github.com/openhwgroup/corev-qemu.git"

```text
/proj/cva5-tinyai/                   <-- Root CVA5-TiniAI repository
├── .git/
├── README.md
├── CONTRIBUTING.md
├── doc/
│   └── DEVELOPMENTENV.md            <-- This document
├── bin/
│   ├── sync_repos.sh                <-- Sub-repository synchronization script
│   ├── setup_toolchain.sh           <-- Toolchain & Verilator build installer
│   └── Makefile                     <-- Workspace orchestration Makefile
├── x-heep/                          <-- Microcontroller system framework (PULP env.)
├── cva5/                            <-- OpenHW Group CVA5 RISC-V CPU core
├── core-v-verif/                    <-- Core verification & testbench suite
└── corev-qemu/                      <-- Emulation & virtual platform support
```
## 3. Tool chain
To support **core-v-verif** HDL simulation in Verilator, RISC-V compiler toolchain, and AMD-Xilinx FPGA implemetation, the core verification environment relies on two main pillars: 

- a compiled RISC-V GCC toolchain (to generate test binaries, .elf, and .hex files) 
- a compatible Verilator build (to compile and run HDL simulations).

|Tool Domain      | Minimum Required Version          | Key Environment Variables |
|-----------------|-----------------------------------|---------------------------|
|RISC-V GCC       | riscv32-unknown-elf-gcc (GCC 12+) | RISCV, RISCV_TOOLCHAIN_PATH, PATH |
|Verilator        | v5.008+ (det. by **CORE_V_VERIF**)| VERILATOR_ROOT, PATH |
|PULP toolchain   | pulp-gcc / pulp-rt                | PULP_RISCV_GCC_TOOLCHAIN, PULP_SDK_HOME|
|AMD Vivado/Vitis |	Vivado 2022.2+                    |XILINX_VIVADO, XILINX_VITIS |

