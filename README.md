# vsd-internship workshop
# SKY130 RTL Design and Synthesis – VSD FPGA Internship

This repository documents the RTL design, simulation, synthesis, and verification flow using open-source EDA tools as part of the VSD FPGA Internship Screening Program.

---

## 📌 1. Introduction to RTL Design

RTL (Register Transfer Level) describes the behavior of a digital circuit.

### Example RTL Code

```verilog
module sample_code (
    input clk,
    input rst,
    output reg result,
    output reg done
);

always @(posedge clk or posedge rst) begin
    if (rst) begin
        result <= 0;
        done <= 0;
    end else begin
        result <= 1;
        done <= 1;
    end
end

endmodule
```

👉 RTL represents the **behavioral description** of hardware.

---

## 🔁 2. Iverilog Based Simulation Flow

RTL Design is verified using simulation.

### Flow

```
Design + Testbench → iverilog → VCD file → GTKWave
```

### Commands

```bash
iverilog testbench.v design.v
./a.out
gtkwave dump.vcd
```

👉 Output is a **VCD waveform file** viewed in GTKWave.

---

## 🛠️ 3. Introduction to Synthesis

Synthesis converts RTL into gate-level netlist.

### Tool Used

* **Yosys** (Open-source synthesizer)

### Flow

```
RTL Design + .lib → Yosys → Netlist
```

---

## 📚 4. What is .lib File?

* Collection of logic gates
* Contains AND, OR, NOT, etc.
* Includes different versions (flavours):

  * Slow cells
  * Medium cells
  * Fast cells

👉 Used by synthesizer to map RTL → real hardware gates

---

## ⚡ 5. Why Different Flavours of Gates?

### Timing Constraint

```
Tclk > Tcq + Tcombi + Tsetup
```

* Faster cells → reduce delay
* Slower cells → help avoid hold violations

👉 Both fast and slow cells are required for correct design.

---

## ⚖️ 6. Faster vs Slower Cells

| Type       | Advantage | Disadvantage           |
| ---------- | --------- | ---------------------- |
| Fast Cells | Low delay | High power, large area |
| Slow Cells | Low power | Higher delay           |

👉 Trade-off between:

* Speed
* Power
* Area

---

## 🎯 7. Selection of Cells

Synthesizer selects cells based on constraints:

* Too many fast cells → high power & area
* Too many slow cells → poor performance

👉 Balanced selection is important.

---

## 🔧 8. Synthesis Using Yosys

### Commands

```tcl
yosys
read_verilog design.v
read_liberty sky130.lib
synth
write_verilog netlist.v
```

👉 Output: **Gate-level Netlist**

---

## 🔍 9. Netlist Verification

The synthesized netlist is verified using the same testbench.

### Flow

```
Netlist + Testbench → iverilog → VCD → GTKWave
```

### Commands

```bash
iverilog testbench.v netlist.v
./a.out
gtkwave dump.vcd
```

---

## ✅ 10. Observation

* RTL output and Netlist output are same
* Functional correctness is verified
* Same testbench works for both

---

## 📸 11. Results

### RTL Simulation Output

(Add screenshot here)

### Netlist Simulation Output

(Add screenshot here)

---

## 📖 12. Key Learnings

* RTL design using Verilog
* Simulation using Icarus Verilog
* Waveform analysis using GTKWave
* Synthesis using Yosys
* Importance of .lib files
* Timing constraints and optimization

---

## 🚀 Conclusion

This lab demonstrates the complete RTL-to-Gate flow using open-source tools. It provides a strong foundation in digital VLSI design and synthesis techniques.

---
