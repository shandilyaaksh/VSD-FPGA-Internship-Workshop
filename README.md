# VSD FPGA Internship – RTL Design, Simulation and Synthesis

<p align="center">
  <b>End-to-End Digital Design Flow</b><br>
  RTL → Simulation → Synthesis → Netlist Verification
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HDL-Verilog-blue">
  <img src="https://img.shields.io/badge/Simulator-Iverilog-green">
  <img src="https://img.shields.io/badge/Waveform-GTKWave-orange">
  <img src="https://img.shields.io/badge/Synthesis-Yosys-red">
  <img src="https://img.shields.io/badge/Library-Sky130-lightgrey">
</p>

---

## Overview

This repository presents the complete implementation of RTL design and synthesis flow as part of the **VSD FPGA Internship Screening Program**.

It demonstrates how a behavioral Verilog design is:

* Simulated and verified
* Converted into gate-level representation
* Optimized using standard cell libraries
* Validated post-synthesis

---

## Complete Design Flow

```
RTL Design + Testbench
        │
        ▼
     Iverilog (Simulation)
        │
        ▼
     VCD Output File
        │
        ▼
     GTKWave (Waveform)
        │
        ▼
     Verified RTL Design
        │
        ▼
     Yosys (Synthesis)
        │
        ▼
  Gate-Level Netlist
        │
        ▼
  Netlist Verification
```

---

## Toolchain

| Stage              | Tool          |
| ------------------ | ------------- |
| Design             | Verilog       |
| Simulation         | Iverilog      |
| Debugging          | GTKWave       |
| Synthesis          | Yosys         |
| Technology Mapping | Sky130 (.lib) |

---

# Module 1: RTL Design and Simulation

## Objective

To design digital logic using Verilog and verify functionality using simulation.

---

## Simulation Flow

```
Design + Testbench → Iverilog → VCD → GTKWave
```

---

## Setup and Execution

```bash
git clone https://github.com/vsdip/vsd-rtl.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files

iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```

---

## Key Observations

* Output follows input stimulus
* Stable signals when no input change
* Waveforms confirm expected behavior

---

# Module 1: Logic Synthesis using Yosys

## Objective

Convert RTL into optimized gate-level netlist using standard cells.

---

## Synthesis Flow

```
RTL + Standard Cell Library → Yosys → Netlist
```

---

## Commands

```bash
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog good_mux_netlist.v
```

---

## Verification Strategy

* Same testbench reused
* Compare RTL vs synthesized output
* Matching waveforms confirm correctness

---

# Module 2: Timing Libraries, Synthesis Styles and Optimization

---

## Timing Library (.lib)

### Purpose

The `.lib` file defines how logic cells behave in real hardware.

---

### Open Library

```bash
gvim sky130_fd_sc_hd__tt_025C_1v80.lib
```

---

## PVT Variations

| Parameter   | Description                            |
| ----------- | -------------------------------------- |
| Process     | Manufacturing variation (tt = typical) |
| Voltage     | Supply voltage                         |
| Temperature | Operating temperature                  |

Example:

```
sky130_fd_sc_hd__tt_025C_1v80.lib
```

---

## Library Contents

* Logic gates (AND, OR, NOT)
* Timing characteristics
* Power consumption
* Area information

---

## Cell Variants and Trade-offs

| Cell Type | Delay    | Power    | Area     |
| --------- | -------- | -------- | -------- |
| Fast      | Low      | High     | High     |
| Slow      | High     | Low      | Low      |
| Medium    | Balanced | Balanced | Balanced |

---

## Timing Constraints

### Setup Constraint

```
Tclk > Tcq + Tcomb + Tsetup
```

### Hold Constraint

```
Thold < Tcq + Tcomb
```

---

## Importance

* Fast cells → Improve performance
* Slow cells → Prevent hold violations
* Balanced selection → Optimal design

---

# Hierarchical vs Flat Synthesis

## Hierarchical Synthesis

* Module-wise processing
* Faster compilation
* Easier debugging
* Limited optimization

---

## Flat Synthesis

* Entire design flattened
* Better optimization
* Higher runtime

---

## Comparison

| Feature      | Hierarchical | Flat    |
| ------------ | ------------ | ------- |
| Speed        | Fast         | Slow    |
| Optimization | Limited      | High    |
| Debugging    | Easy         | Complex |

---

# Efficient Flop Coding Styles

## Correct Implementation

```verilog
module dff (input clk, input rst, input d, output reg q);
always @(posedge clk or posedge rst)
begin
    if (rst)
        q <= 0;
    else
        q <= d;
end
endmodule
```

---

## Incorrect Implementation

```verilog
always @(clk)
begin
    if(clk)
        q = d;
end
```

---

## Best Practices

* Use edge-triggered logic
* Use non-blocking assignments
* Always include reset logic

---

# Optimization Techniques

* Constant propagation
* Dead code removal
* Logic simplification
* Resource sharing

---

## Example

```verilog
assign y = sel ? a : a;
```

Optimized to:

```verilog
assign y = a;
```

---

# Shapshots


![1](images/1.png)

![2](images/2.png)

![3](images/3.png)

![4](images/4.png)

![5](images/5.png)

![6](images/6.png)

![7](images/7.png)

---

# Repository Structure

```
.
├── verilog_files/
├── lib/
├── my_lib/
├── images/
└── README.md
```

---

# Key Learnings

* RTL to Gate-level transformation
* Importance of timing libraries
* Trade-offs in speed, power, and area
* Correct coding practices for synthesis
* Differences between synthesis strategies

---

# Author

Amritanshu Kumar Shandilya
