# PLC-5000 Ladder Logic & Industrial Motor Control Simulator

An interactive, single-file HTML5 Programmable Logic Controller (PLC) Ladder Logic Simulator and 3-Phase Motor Control trainer designed for industrial electricians, maintenance technicians, and automation students. Built with zero external dependencies, it runs directly in any modern desktop or mobile browser.

## Live Demo

Launch the simulator directly via GitHub Pages: `https://jeffry-lacanglacang.github.io/PLC-5000-Industrial-Ladder-Logic-Motor-Control-Simulator/`
## Architecture & Simulation Engine

The application replicates a deterministic cyclic PLC scan architecture using standard Allen-Bradley style addressing (`I:0/0`–`I:0/7`, `O:0/0`–`O:0/7`, `B3:0/0`–`B3:0/7`, and `T4:0`–`T4:3`). Each scan cycle executes an Input Image Table read, evaluates series and parallel OR-branch ladder rungs left-to-right, updates timer accumulators (`PRE`/`ACC`, `EN`, `TT`, `DN`), and writes the Output Image Table. Users can switch between continuous **RUN**, **PROGRAM**, and **SINGLE-STEP** modes with adjustable scan rates to debug logic transitions scan by scan.

## Supported Ladder Instructions

| Instruction | Mnemonic | Function Description |
| :--- | :--- | :--- |
| **Examine If Closed** | `XIC` | Evaluates true (passes power) when the referenced bit address is `1`. |
| **Examine If Open** | `XIO` | Evaluates true (passes power) when the referenced bit address is `0`. |
| **Output Energize** | `OTE` | Sets the referenced output or binary bit to `1` when rung continuity is true; resets to `0` when false. |
| **Output Latch** | `OTL` | Retentively sets the referenced bit to `1` when rung continuity becomes true. |
| **Output Unlatch** | `OTU` | Resets a latched bit to `0` when rung continuity becomes true. |
| **Timer On-Delay** | `TON` | Increments accumulated time (`ACC`) while rung-in is true and sets the Done bit (`DN`) once `ACC >= PRE`. |

## Built-In Industrial Control Presets

The simulator ships with four pre-wired industrial motor control circuits ready for testing and modification:

1. **3-Wire Start/Stop Seal-In Starter**: Standard momentary Start (`NO`), momentary Stop (`NC`), thermal overload protection, and auxiliary holding contact logic.
2. **Forward / Reverse Interlocked Starter**: Dual-contactor reversing control featuring both electrical pushbutton interlocking and software `XIO` cross-interlocking to prevent phase-to-phase short circuits.
3. **Star-Delta Reduced Voltage Starter**: Automated Wye-to-Delta motor starting sequence using a `TON` transition timer and mechanical/electrical contactor interlocking between Star (`O:0/1`) and Delta (`O:0/2`) coils.
4. **Sequential Conveyor & Latching Fault Alarm**: Two-stage material handling startup (`B3:0/0` master run, delayed main conveyor start) paired with a retentive `OTL`/`OTU` fault alarm circuit.

## Mobile & Desktop Optimization

Designed as a self-contained single HTML file (`plc_simulator.html`), the interface adapts automatically between wide multi-pane desktop workstations and Android mobile viewports. On mobile screens, pointer-captured touch controls prevent sticky momentary pushbuttons, while a persistent bottom quick-control dock lets operators actuate field inputs while observing real-time green power-flow highlighting across the ladder rungs.

## Local Usage

Clone the repository or download `plc_simulator.html` and open it directly in Chrome, Edge, Firefox, or Safari—no web server, Node.js installation, or build step required.

```bash
git clone [https://github.com/LoneWolf-create/plc-simulator.git](https://github.com/LoneWolf-create/plc-simulator.git)
cd plc-simulator
