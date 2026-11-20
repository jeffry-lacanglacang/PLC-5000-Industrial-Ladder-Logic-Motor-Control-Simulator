# Studio 5000 Logix Designer — Ladder Logic & Motor Control Simulator

A fully interactive, client-side **PLC (Programmable Logic Controller) simulator** built within a single-file web architecture (`index.html`). Designed for electrical technicians, automation students, and control engineers, it mimics industrial Allen-Bradley/IEC 61131-3 PLC scan cycles, supporting real-time ladder logic editing, physical digital I/O simulation, 3-phase motor control starters, and animated plant mimic displays.

**🔗 Live Demo:** [Try PLC-5000 Online](https://jeffry-lacanglacang.github.io/PLC-5000-Industrial-Ladder-Logic-Motor-Control-Simulator/)

![PLC-5000 Badge](https://img.shields.io/badge/PLC--5000-Industrial%20Simulator-059669?style=flat-square&logo=cplusplus&logoColor=white)
![HTML5 Single File](https://img.shields.io/badge/Architecture-Single%20File%20HTML5-blue?style=flat-square&logo=html5)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## Key Features

* **Deterministic Cyclic Scan Architecture**: Implements standard PLC scan cycles (1. Input Scan $\rightarrow$ 2. Program Logic Execution $\rightarrow$ 3. Output Update) with clamped 50ms scan timers.
* **Rich Instruction Set**: Supports Examine If Closed (`XIC`), Examine If Open (`XIO`), Output Energize (`OTE`), Output Latch (`OTL`), Output Unlatch (`OTU`), and Timer On-Delay (`TON`) instructions.
* **Industrial Circuit Presets**: Includes 5 built-in pre-configured templates:
  * *0. Blank Workspace* (Custom routine builder)
  * *1. 3-Wire Start/Stop Seal-In Motor Starter* (with NC Overload & Stop)
  * *2. Forward / Reverse Interlocked Motor Starter*
  * *3. Star-Delta Reduced-Voltage Starter* (with 3-second transition timer)
  * *4. Automated Conveyor + Latching Fault Alarm*
* **3-Phase Motor & Plant Mimic**: Real-time SVG visual rotor rotation (1,760 RPM CW/CCW simulation), star-delta operating states, and active pilot lamps (Green, Amber, Blue, Red fault).
* **Mobile-Optimized Touch Controls**: Fully responsive 3-column layout that adapts to tablets and smartphones with touch-safe pointer capture for physical buttons and a persistent quick-control dock.

---

## File Structure

```text
├── index.html         # Complete standalone PLC simulator (HTML, CSS, JavaScript)
└── README.md          # Project documentation
```

---

## Quick Start / Installation

Because this project is packaged as a **single-file web application**, no complex build tools, backend servers, or compiler toolchains are required.

1. **Access directly online:** Visit the live deployment at [jeffry-lacanglacang.github.io/PLC-5000-Industrial-Ladder-Logic-Motor-Control-Simulator](https://jeffry-lacanglacang.github.io/PLC-5000-Industrial-Ladder-Logic-Motor-Control-Simulator/)
2. **Clone or download locally:**
   ```bash
   git clone https://github.com/jeffry-lacanglacang/PLC-5000-Industrial-Ladder-Logic-Motor-Control-Simulator.git
   ```
3. Open `index.html` directly in any modern web browser (Google Chrome, Microsoft Edge, Mozilla Firefox, or Safari).
4. Select a pre-configured circuit from the **Preset Selector** dropdown or click **+ Add Rung** to design custom ladder logic.

---

## How to Use

### 1. CPU Control & Scan Modes
* **RUN / PROG Toggle**: Pause or resume the cyclic scan engine.
* **Step**: Execute a single scan cycle manually for debugging complex ladder loops.
* **Reset**: Clear internal memory bits (`B3`), timers (`T4`), and outputs (`O`), returning physical inputs to safe default states.

### 2. Interacting with Inputs & Outputs
* **Field Digital Inputs (`I:0/0` – `I:0/7`)**: Click or tap input tiles to toggle contact states. Each input supports configurable modes (`MOM_NO`, `MOM_NC`, and Maintained `TOGGLE`).
* **Digital Outputs (`O:0/0` – `O:0/7`)**: Monitor live output coils and LED indicators in real-time as ladder logic solves each rung.
* **Thermal Overload Trip**: Click **Trip OL Relay** to test NC thermal overload fault interruption on motor circuits.

### 3. Editing Ladder Logic
* **Tap any instruction node** (e.g., `XIC`, `OTE`, `TON`) to open the **Instruction & Tag Inspector** modal. Modify instruction types, assign memory addresses (`I`, `O`, `B3`, `T`), update timer presets (in milliseconds), or edit tag descriptions.
* **Add OR Branches**: Click **+ OR Branch** on any rung to construct parallel contact logic branches.

---

## Technical Specifications

* **Scan Engine**: Synchronous evaluation loop running at a fixed 50ms interval accumulator.
* **Timer Resolution**: Millisecond-accurate `TON` accumulators (`ACC`) comparing against preset values (`PRE`).
* **Memory Mapping**:
  * Inputs: `I:0/0` through `I:0/7`
  * Outputs: `O:0/0` through `O:0/7`
  * Binary Memory: `B3:0/0` through `B3:0/7`
  * Timers: `T4:0` through `T4:3` (supporting `.EN`, `.TT`, and `.DN` bit queries)

---

## Contributing

Contributions, bug reports, and pull requests are welcome! If you would like to add new instruction blocks (e.g., Counter `CTU`/`CTD`, Math registers, or PID loops), please feel free to fork the repository and submit a pull request.

---

## License

This project is open-source and available under the [MIT License](LICENSE).
