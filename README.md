# VSD FPGA Internship – RTL Design and Synthesis

This repository contains the documentation and lab work performed as part of the VSD FPGA Internship Screening Program. It includes RTL design, simulation using Iverilog, waveform analysis using GTKWave, and synthesis using Yosys with Sky130 standard cell libraries.

---

## Introduction to Verilog RTL Design and Simulation

### Objective

To understand the fundamentals of Verilog design, simulation, and testbench methodology.

### Theory

#### Simulator

RTL designs are verified using simulation. The simulator checks whether the design meets the required specifications. Iverilog is used as the simulator in this workflow.

#### Design

Design refers to the Verilog code that implements the intended functionality of the system.

#### Testbench

A testbench applies input stimulus (test vectors) to the design and verifies correctness of the output.

#### Working of Simulator

The simulator monitors input changes and evaluates outputs accordingly:

* Output updates when inputs change
* Output remains constant when inputs remain unchanged

---

## Simulation Flow

* Design and Testbench are given as input to the simulator
* Simulator generates output in the form of a VCD file
* GTKWave is used to visualize waveforms

---

## Labs using Iverilog and GTKWave

### Repository Setup

Clone the required repository using:

```bash
git clone https://github.com/vsdip/vsd-rtl.git
```

This creates a directory:

```
sky130RTLDesignAndSynthesisWorkshop
```

---

### Directory Structure

* `lib/` → Contains Sky130 standard cell library
* `my_lib/` → Contains Verilog models
* `verilog_files/` → Contains design and testbench files

---

### Running Simulation

```bash
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```

If any tool is missing:

```bash
sudo apt install iverilog
sudo apt install gtkwave
```

---

### Viewing Design and Testbench

```bash
gvim good_mux.v -o tb_good_mux.v
```

---

## Introduction to Yosys and Logic Synthesis

### Objective

To understand logic synthesis and conversion of RTL to gate-level netlist.

---

### Theory

#### Synthesizer

A synthesizer converts RTL code into a gate-level netlist. Yosys is used in this flow.

#### RTL Design

RTL represents system behavior using Verilog HDL.

#### Synthesis

* Converts RTL to logic gates
* Maps design using standard cell library
* Produces a netlist file

---

### What is .lib

* A `.lib` file contains standard cells like AND, OR, NOT
* Each gate has multiple variants:

  * Slow
  * Medium
  * Fast

---

### Gate Variants and Performance

* Faster cells → lower delay, higher power and area
* Slower cells → higher delay, lower power and area
* Trade-off exists between performance, power, and area

---

### Need for Slow Cells

Slow cells are required to avoid hold time violations and ensure timing correctness.

---

### Cell Selection

The synthesizer selects cells based on constraints:

* More fast cells → better performance but higher power
* More slow cells → lower power but reduced speed

---

## Labs using Yosys and Sky130 PDK

### Launch Yosys

```bash
yosys
```

### Read Library

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

### Read Design

```bash
read_verilog good_mux.v
```

### Synthesize Design

```bash
synth -top good_mux
```

### Map to Standard Cells

```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

---

### Generate Netlist

```bash
write_verilog good_mux_netlist.v
```

---

### View Netlist

```bash
gvim good_mux_netlist.v
```

---

### Simplified Netlist

```bash
write_verilog -noattr good_mux_netlist.v
gvim good_mux_netlist.v
```

---

### Visual Representation

```bash
show
```

---

## Verification of Synthesis

* Same testbench used for RTL simulation can be reused
* Compare RTL and synthesized netlist outputs
* Outputs should match for correct synthesis

---

## Conclusion

* Understood RTL design and simulation using Iverilog
* Visualized waveforms using GTKWave
* Learned synthesis using Yosys
* Generated and analyzed gate-level netlist
* Understood trade-offs in cell selection and timing

---

![Description](images/1.png)
![Description](images/2.png)
![Description](images/3.png)

---

## Author

Amritanshu Kumar Shandilya
