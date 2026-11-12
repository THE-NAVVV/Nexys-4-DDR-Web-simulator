# ⚡ Nexys 4 DDR Web Simulator — Artix-7 FPGA

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-388bfd?style=for-the-badge&logo=github)](https://the-navvv.github.io/Nexys-4-DDR-Web-simulator/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![FPGA Target](https://img.shields.io/badge/FPGA-Xilinx%20Artix--7%20xc7a100t-orange?style=for-the-badge)](https://digilent.com/reference/programmable-logic/nexys-4-ddr/start)
[![DCS Lab Ready](https://img.shields.io/badge/Lab-Digital%20Circuits%20%26%20Systems-2ea043?style=for-the-badge)]()
[![Platform](https://img.shields.io/badge/Platform-Web%20%2F%20Zero--Install-informational?style=for-the-badge)]()

> **Interactive Digilent Nexys 4 DDR FPGA Web Simulator with a Vivado-style 4-stage EDA flow, real-time board I/O, clock synthesizer, testbench runner (XSIM), and 38+ pre-loaded DCS Lab experiments.**

---

## 🎯 Motivation & Why This Was Built

In university courses like **Digital Circuits & Systems (DCS)** and **Digital Logic Design**, students spend countless hours developing Verilog HDL modules for FPGA implementation. However:
- Physical **Digilent Nexys 4 DDR boards** in university hardware labs are often limited in number.
- Students must wait in queues during designated lab hours just to test basic switch/LED behavior.
- Loose JTAG USB cables, driver issues, and hardware wear-and-tear frequently bottleneck learning.
- Installing massive multi-gigabyte EDA suites like **Xilinx Vivado** on personal laptops is not always feasible for every student.

**Nexys 4 DDR Web Simulator** was built by **Nav Vardhan Singh** to solve this exact problem: **so students don't have to keep rushing to the physical hardware lab for every verification step.** You can now write, synthesize, implement, generate bitstreams, and interactively test digital designs on a photorealistic virtual Nexys 4 DDR board directly inside your web browser.

---

## 🚀 Live Demo

Try the simulator right now without installing anything:
👉 **[https://the-navvv.github.io/Nexys-4-DDR-Web-simulator/](https://the-navvv.github.io/Nexys-4-DDR-Web-simulator/)**

---

## ✨ Key Features

### 🖥️ 1. Interactive Nexys 4 DDR Hardware Peripherals
- **16 User Slide Switches (`SW[15:0]`)**: Clickable switches with real-time toggle states and an instant "All OFF" reset button.
- **16 User LEDs (`LED[15:0]`)**: Bright green luminescent LEDs responding instantaneously to logic states.
- **2 Tri-Color RGB LEDs (`LD16`, `LD17`)**: Multi-channel PWM / RGB output simulation.
- **8-Digit 7-Segment Multiplexed Display**:
  - Full cathode (`CA` through `CG` + `DP`) and anode (`AN[7:0]`) multiplexing emulation.
  - Active-low and active-high polarity auto-detection or manual override.
- **Pushbuttons & Reset**:
  - 5 Directional Pushbuttons (`BTNU`, `BTNL`, `BTNC`, `BTNR`, `BTND`).
  - Dedicated active-low `CPU_RESETN` red button.
- **Board System Clock (`CLK100MHZ` — Pin `E3`)**:
  - Live clock synthesizer with speeds from `1 Hz`, `5 Hz`, `25 Hz`, `100 Hz`, `1 kHz`, `50 kHz` up to `Turbo 5 MHz`.
  - **Manual Single-Cycle Step**: Execute clock ticks cycle-by-cycle (`⚡ Step 1 Cycle`) to inspect state transitions and race conditions.
  - **⚡ Fast Divider**: Automatically scales internal hardware clock counters for instant visual feedback on physical human scales without waiting for 100 million physical clock ticks.

---

### ⚙️ 2. Vivado-Style 4-Stage Toolchain Flow
The simulator emulates the complete industry-standard Xilinx Vivado flow right in the browser:
```
[ 1. Synthesis ] ──▶ [ 2. Implementation ] ──▶ [ 3. Bitstream (.bit) ] ──▶ [ 4. Hardware Dump / JTAG ]
```
1. **Synthesis**: Parses Verilog AST, extracts module ports, compiles hierarchical sub-modules, and resolves combinational/sequential logic.
2. **Implementation**: Maps netlist signals to physical FPGA package pins specified in the `.xdc` constraints file and validates I/O standards (`LVCMOS33`).
3. **Bitstream Generation**: Validates design constraints and generates virtual FPGA bitstream configuration.
4. **Hardware Dump / Program FPGA**: Simulates JTAG downloading into the Artix-7 SRAM cells, transitions board status to `PROGRAMMED`, and activates live hardware I/O.

---

### 🧪 3. Built-In Behavioral Testbench Runner (XSIM)
- Switch to the **Testbench (`tb.v`)** tab to run standalone behavioral simulations without board I/O.
- Integrated event-driven simulator supporting `#delay`, clock generation loops, `initial` blocks, and `$display` console logs.
- Useful for pre-synthesis verification and regression testing.

---

### 📐 4. Ergonomic Multi-Pane Workspace
- **Dual Resizable Splitters**: Freely drag splitters horizontally (Code vs Board) and vertically (Editor vs Vivado Console Log).
- **Quick Layout Presets**:
  - `◨ 50:50`: Balanced split between code editor and board.
  - `◧ 75% Wide`: Board expansion view for testing complex I/O.
  - `⛶ Maximize`: Fullscreen board view for presentations and lab demonstrations.
- **Zoom & Pan Controls**: Zoom in/out (`−` / `+`), manual slider (65% – 180%), and `↕ Fit Height` to fit any screen resolution.

---

## 📚 Built-In DCS Lab Experiments (38+ Presets)

The simulator includes a massive built-in curriculum library of Digital Circuits & Systems (DCS) lab experiments. Select any preset from the **Load Preset** dropdown to automatically load its `top.v`, `tb.v`, and `Nexys4DDR.xdc`:

| # | Preset Name | Circuit Type | Key Concepts Demonstrated |
|---|-------------|--------------|---------------------------|
| 1 | **Traffic Light Controller FSM** | Sequential (Moore FSM) | State transitions, timing counters, RGB/LED indicators |
| 2 | **16-Bit Counter + 7-Segment** | Sequential | Clock division, 7-segment hex decoding, switch enable |
| 3 | **Johnson Counter** | Sequential (Multi-Module) | Hierarchical sub-module instantiation, D-flip-flops |
| 4 | **Hex → 7-Segment Decoder** | Combinational | 4-bit switch input mapped to 7-segment cathodes |
| 5 | **4-Bit ALU** | Combinational | ADD, SUB, AND, OR, XOR, NOT operations via opcodes |
| 6 | **16-Bit Shift Register** | Sequential | Serial-in / Parallel-out (SIPO) shifting, reset control |
| 7 | **Sequence Detector '101'** | Sequential (FSM) | Overlapping state machine with detection flag |
| 8 | **Majority Function** | Combinational | Boolean logic: $F = AB + BC + CA$ |
| 9 | **4-Bit Odd Parity Generator** | Combinational | Bitwise XOR reduction logic |
| 10 | **4-Bit Ripple Carry Adder** | Combinational (Hierarchical) | Full adders cascade with carry-in and carry-out |
| 11 | **4-Bit Carry Lookahead Adder** | Combinational | Fast addition using Generate ($G$) & Propagate ($P$) |
| 12 | **4-Bit Subtractor (2's Comp)** | Combinational | Subtraction via XOR 2's complement inversion |
| 13 | **4-to-1 Multiplexer (MUX)** | Combinational | 2-bit select lines routing 4 data inputs |
| 14 | **1-to-4 Demultiplexer (DEMUX)** | Combinational | Single input distributed to 4 outputs via select lines |
| 15 | **3-to-8 Decoder with Enable** | Combinational | Binary address decoding to active-high output lines |
| 16 | **8-to-3 Priority Encoder** | Combinational | Highest-priority active bit encoded into 3-bit binary |
| 17 | **4-Bit Magnitude Comparator** | Combinational | Arithmetic comparison: $A > B$, $A = B$, $A < B$ |
| 18 | **Binary to Gray Code Converter** | Combinational | Shifted XOR code conversion |
| 19 | **Gray Code to Binary Converter** | Combinational | Cascaded XOR feedback conversion |
| 20 | **BCD to 7-Segment Decoder** | Combinational | Decimal 0–9 decoding on active-low 7-segment |
| 21 | **BCD to Excess-3 Converter** | Combinational | Decimal arithmetic offset code conversion |
| 22 | **4-Bit Barrel Shifter** | Combinational | Logical right/left rotators |
| 23 | **4-Bit Up/Down Counter** | Sequential | Bidirectional synchronous counting |
| 24 | **Mod-10 (BCD) Decade Counter** | Sequential | Synchronous modulo-10 counter with asynchronous reset |
| 25 | **Mod-N Arbitrary Counter** | Sequential | Parameterized counter resetting at arbitrary modulus |
| 26 | **4-Bit Ring Counter** | Sequential | Circulating one-hot shift pattern |
| 27 | **4-Bit Universal Shift Register** | Sequential | Hold, Shift Left, Shift Right, and Parallel Load modes |
| 28 | **Sequence Detector '1101'** | Sequential (FSM) | Overlapping Moore/Mealy sequence detector |
| 29 | **Sequence Detector '11010'** | Sequential (FSM) | Non-overlapping sequence detector |
| 30 | **Sequence Detector with Start/Stop** | Sequential (FSM) | Controlled state detector with enable gating |
| 31 | **Digital Clock with 7-Seg Multiplex** | Sequential | Multi-digit time display with refresh clock |
| 32 | **PWM LED Brightness Controller** | Sequential | Duty-cycle modulated LED dimming |
| 33 | **4-Bit Linear Feedback Shift Reg (LFSR)**| Sequential | Pseudo-random binary sequence (PRBS) generator |
| 34 | **Binary to ASCII Converter** | Combinational | Maps 5-bit numbers to printable ASCII alphanumeric characters |
| 35 | **4-Bit Up/Down Counter (JK-FF)** | Sequential | Implemented using toggle logic with JK Flip-Flops |
| ...| *And more!* | | |

---

## 📌 Nexys 4 DDR Master Pin Mapping

All pins correspond directly to Digilent's official **Nexys 4 DDR Artix-7 FPGA (xc7a100tcsg324-1)** master constraint file:

```tcl
## Clock Signal (100 MHz)
set_property -dict { PACKAGE_PIN E3    IOSTANDARD LVCMOS33 } [get_ports { clk }]

## Slide Switches (SW0 - SW15)
set_property -dict { PACKAGE_PIN J15   IOSTANDARD LVCMOS33 } [get_ports { sw[0] }]
set_property -dict { PACKAGE_PIN L16   IOSTANDARD LVCMOS33 } [get_ports { sw[1] }]
set_property -dict { PACKAGE_PIN M13   IOSTANDARD LVCMOS33 } [get_ports { sw[2] }]
set_property -dict { PACKAGE_PIN R15   IOSTANDARD LVCMOS33 } [get_ports { sw[3] }]
set_property -dict { PACKAGE_PIN R17   IOSTANDARD LVCMOS33 } [get_ports { sw[4] }]
set_property -dict { PACKAGE_PIN T18   IOSTANDARD LVCMOS33 } [get_ports { sw[5] }]
set_property -dict { PACKAGE_PIN U18   IOSTANDARD LVCMOS33 } [get_ports { sw[6] }]
set_property -dict { PACKAGE_PIN R13   IOSTANDARD LVCMOS33 } [get_ports { sw[7] }]
set_property -dict { PACKAGE_PIN T8    IOSTANDARD LVCMOS33 } [get_ports { sw[8] }]
set_property -dict { PACKAGE_PIN U8    IOSTANDARD LVCMOS33 } [get_ports { sw[9] }]
set_property -dict { PACKAGE_PIN R16   IOSTANDARD LVCMOS33 } [get_ports { sw[10] }]
set_property -dict { PACKAGE_PIN T13   IOSTANDARD LVCMOS33 } [get_ports { sw[11] }]
set_property -dict { PACKAGE_PIN H6    IOSTANDARD LVCMOS33 } [get_ports { sw[12] }]
set_property -dict { PACKAGE_PIN U12   IOSTANDARD LVCMOS33 } [get_ports { sw[13] }]
set_property -dict { PACKAGE_PIN U11   IOSTANDARD LVCMOS33 } [get_ports { sw[14] }]
set_property -dict { PACKAGE_PIN V10   IOSTANDARD LVCMOS33 } [get_ports { sw[15] }]

## LEDs (LED0 - LED15)
set_property -dict { PACKAGE_PIN H17   IOSTANDARD LVCMOS33 } [get_ports { led[0] }]
set_property -dict { PACKAGE_PIN K15   IOSTANDARD LVCMOS33 } [get_ports { led[1] }]
set_property -dict { PACKAGE_PIN J13   IOSTANDARD LVCMOS33 } [get_ports { led[2] }]
set_property -dict { PACKAGE_PIN N14   IOSTANDARD LVCMOS33 } [get_ports { led[3] }]
set_property -dict { PACKAGE_PIN R18   IOSTANDARD LVCMOS33 } [get_ports { led[4] }]
set_property -dict { PACKAGE_PIN V17   IOSTANDARD LVCMOS33 } [get_ports { led[5] }]
set_property -dict { PACKAGE_PIN U17   IOSTANDARD LVCMOS33 } [get_ports { led[6] }]
set_property -dict { PACKAGE_PIN U16   IOSTANDARD LVCMOS33 } [get_ports { led[7] }]
set_property -dict { PACKAGE_PIN V16   IOSTANDARD LVCMOS33 } [get_ports { led[8] }]
set_property -dict { PACKAGE_PIN T15   IOSTANDARD LVCMOS33 } [get_ports { led[9] }]
set_property -dict { PACKAGE_PIN U14   IOSTANDARD LVCMOS33 } [get_ports { led[10] }]
set_property -dict { PACKAGE_PIN T16   IOSTANDARD LVCMOS33 } [get_ports { led[11] }]
set_property -dict { PACKAGE_PIN V15   IOSTANDARD LVCMOS33 } [get_ports { led[12] }]
set_property -dict { PACKAGE_PIN V14   IOSTANDARD LVCMOS33 } [get_ports { led[13] }]
set_property -dict { PACKAGE_PIN V12   IOSTANDARD LVCMOS33 } [get_ports { led[14] }]
set_property -dict { PACKAGE_PIN V11   IOSTANDARD LVCMOS33 } [get_ports { led[15] }]

## 7-Segment Cathodes (CA - CG, DP)
set_property -dict { PACKAGE_PIN T10   IOSTANDARD LVCMOS33 } [get_ports { seg[0] }] ;# CA
set_property -dict { PACKAGE_PIN R10   IOSTANDARD LVCMOS33 } [get_ports { seg[1] }] ;# CB
set_property -dict { PACKAGE_PIN K16   IOSTANDARD LVCMOS33 } [get_ports { seg[2] }] ;# CC
set_property -dict { PACKAGE_PIN K13   IOSTANDARD LVCMOS33 } [get_ports { seg[3] }] ;# CD
set_property -dict { PACKAGE_PIN P15   IOSTANDARD LVCMOS33 } [get_ports { seg[4] }] ;# CE
set_property -dict { PACKAGE_PIN T11   IOSTANDARD LVCMOS33 } [get_ports { seg[5] }] ;# CF
set_property -dict { PACKAGE_PIN L18   IOSTANDARD LVCMOS33 } [get_ports { seg[6] }] ;# CG
set_property -dict { PACKAGE_PIN H15   IOSTANDARD LVCMOS33 } [get_ports { seg[7] }] ;# DP

## 7-Segment Anodes (AN0 - AN7, Active-Low)
set_property -dict { PACKAGE_PIN J17   IOSTANDARD LVCMOS33 } [get_ports { an[0] }]
set_property -dict { PACKAGE_PIN J18   IOSTANDARD LVCMOS33 } [get_ports { an[1] }]
set_property -dict { PACKAGE_PIN T9    IOSTANDARD LVCMOS33 } [get_ports { an[2] }]
set_property -dict { PACKAGE_PIN J14   IOSTANDARD LVCMOS33 } [get_ports { an[3] }]
set_property -dict { PACKAGE_PIN P14   IOSTANDARD LVCMOS33 } [get_ports { an[4] }]
set_property -dict { PACKAGE_PIN T14   IOSTANDARD LVCMOS33 } [get_ports { an[5] }]
set_property -dict { PACKAGE_PIN K2    IOSTANDARD LVCMOS33 } [get_ports { an[6] }]
set_property -dict { PACKAGE_PIN U13   IOSTANDARD LVCMOS33 } [get_ports { an[7] }]

## Pushbuttons & Reset
set_property -dict { PACKAGE_PIN C12   IOSTANDARD LVCMOS33 } [get_ports { reset_n }] ;# CPU_RESETN (Active Low)
set_property -dict { PACKAGE_PIN N17   IOSTANDARD LVCMOS33 } [get_ports { btnc }]
set_property -dict { PACKAGE_PIN M18   IOSTANDARD LVCMOS33 } [get_ports { btnu }]
set_property -dict { PACKAGE_PIN P17   IOSTANDARD LVCMOS33 } [get_ports { btnl }]
set_property -dict { PACKAGE_PIN M17   IOSTANDARD LVCMOS33 } [get_ports { btnr }]
set_property -dict { PACKAGE_PIN P18   IOSTANDARD LVCMOS33 } [get_ports { btnd }]
```

---

## 📖 Quickstart Guide for Students

1. Open the [Nexys 4 DDR Web Simulator](https://the-navvv.github.io/Nexys-4-DDR-Web-simulator/).
2. Select your experiment from the **Load Preset** dropdown (or write your own custom module in `Design (top.v)`).
3. Verify your module ports match the pins defined in the `Constraints (.xdc)` tab.
4. Run through the Vivado flow buttons in order:
   - Click **`1. Synthesis`**
   - Click **`2. Implementation`**
   - Click **`3. Bitstream`**
   - Click **`4. Hardware Dump Code`**
5. Once programmed, the board status badge will flip to <span style="color:#39d353">**PROGRAMMED**</span>!
6. Click **`▶ Run Clock`** (or step manually using `⚡ Step 1 Cycle`).
7. Toggle switches, press pushbuttons, and watch the LEDs and 7-segment display update live!

---

## 💻 Local Development & Offline Usage

No web server or build toolchain (like Node.js or Webpack) is required. Everything runs in vanilla HTML5, CSS3, and JavaScript!

1. Clone the repository:
   ```bash
   git clone https://github.com/THE-NAVVV/Nexys-4-DDR-Web-simulator.git
   cd Nexys-4-DDR-Web-simulator
   ```
2. Open `index.html` directly in any web browser:
   ```bash
   # On Windows
   start index.html

   # On macOS
   open index.html

   # On Linux
   xdg-open index.html
   ```
   Or use VS Code's **Live Server** extension on port `5501`.

---

## 📂 Project Repository Structure

```
Nexys-4-DDR-Web-simulator/
│
├── index.html              # Complete self-contained Nexys 4 DDR Web Simulator
├── Nexys4DDR_Master.xdc    # Official Master Digilent XDC constraint file
├── dcs.xdc                 # Quick constraint template for DCS Lab assignments
├── LICENSE                 # MIT License
└── README.md               # Documentation and user guide
```

---

## 👨‍💻 Developer & Credits

Designed and developed with ❤️ for DCS students by:

**Nav Vardhan Singh**
- 🐙 GitHub: [@THE-NAVVV](https://github.com/THE-NAVVV)
- 💼 LinkedIn: [Nav Vardhan Singh](https://www.linkedin.com/in/nav-vardhan-singh-ranawat-923255364/)
- 🏫 Institution: **The LNM Institute of Information Technology (LNMIIT)**

If this simulator helped you in your DCS lab, please drop a ⭐ on GitHub!
