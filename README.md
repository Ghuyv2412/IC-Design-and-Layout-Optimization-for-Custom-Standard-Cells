# IC Design and Layout Optimization for Custom Standard Cells
---
### Authors
* Gia Huy Vo @Ghuyv2412

---
## Detailed Breakdown of Project Modules (8 Chapters)

This project documents a comprehensive, hands-on digital integrated circuit design flow carried out across 8 structured laboratory modules using Synopsys EDA tools under the 90nm CMOS process node.

### Chapter 1: Design of Fundamental Logic Gates (Inverter & NAND2)
* **Objective:** Design, verify, and layout the bedrock cells of a standard-cell library: a static CMOS Inverter and a 2-input NAND gate.
* **Key Tasks:** Calculated optimal $W_P/W_N$ ratios using the specific technology library parameters to balance rise/fall delays and secure a symmetric switching threshold ($V_{th} = V_{DD}/2$).
  * Custom drafted full layouts matching geometric constraints for standard cells, followed by successful physical verification sign-off (**DRC** and **LVS** checks).
  * Extracted post-layout parasitics (**StarRC**) and simulated pre/post-layout netlists using **HSPICE** to evaluate real-world cell delays.

### Chapter 2: Transmission Gate & D Flip-Flop (DFF) Design
* **Objective:** Move from basic static gates to custom pass-transistor blocks and complex synchronous sequential circuits.
* **Key Tasks:**
  * Modeled a **Transmission Gate (TG)**, utilizing structural size balancing ($W_P = 2 \times W_N$) to keep the equivalent on-resistance ($R_{on}$) flat and stable over the full rail-to-rail dynamic input voltage range.
  * Engineered an edge-triggered Master-Slave **D Flip-Flop (DFF)** architecture utilizing cascaded chốt (latches) driven by anti-phase transmission gates.
  * Performed precise **HSPICE** transient profiling to accurately isolate and measure critical timing margins, extracting an industrial-grade **Clock-to-Q delay of ~129 ps**.

### Chapter 3: Transistor I-V Characteristic Profiling (NMOS & PMOS)
* **Objective:** Graph and mathematically document the physical transfer characteristics of active silicon devices at varying dimensional sizes.
* **Key Tasks:**
  * Configured rigorous parameter sweeping testbenches (`.dc` sweeps for $V_{DS}$ and $V_{GS}$) for $NMOS$ and $PMOS$ devices at three discrete sizes: $Width = 0.2\,\mu\text{m}$, $1.0\,\mu\text{m}$, and $2.0\,\mu\text{m}$.
  * Successfully plotted the absolute $I_D$ vs. $V_{DS}$ curves across 6 unique voltage steps to visibly define and differentiate the **Cut-off**, **Linear/Triode**, and **Saturation** operation regimes of sub-micron MOSFETs.

### Chapter 4: Pass Transistor Logic Characteristics & Noise Margin Evaluation
* **Objective:** Graphically evaluate the physical limitations of Pass Transistor Logic (PTL) configurations and define standard cell Noise Margins.
* **Key Tasks:**
  * Investigated and measured threshold voltage drops ($V_{th}$ degradation) across cascading chains of PTL structures (evaluating single NMOS, 3-series NMOS, shared-drain arrays, and independent PMOS nodes).
  * Confirmed physical source-voltage limits ($V_S = V_G - V_{tn}$ for NMOS passing high voltages).
  * Performed Voltage Transfer Characteristic (VTC) simulations to derive core static noise boundaries: **$V_{IL}, V_{IH}, V_{OL}, V_{OH}$** for optimized static CMOS Inverters.

### Chapter 5: Capacitor Charging & Discharging Dynamics
* **Objective:** Bridge the gap between classical RC circuit theory and transient physical simulation within deep-submicron semiconductors.
* **Key Tasks:**
  * Set up an active charging/discharging RC simulation environment with tiny charging pulses inside **HSPICE**.
  * Analyzed simulated signal transitions (10% to 90% threshold marks) against continuous mathematical RC equations, identifying minor numeric errors (~1.8% variance) caused by source inputs slopes and model tolerances.

### Chapter 6: Determining Real Mobility Ratios ($W_P/W_N$) & RC Delay Extraction
* **Objective:** Quantitatively pin down the physical charge-carrier mobility skew within the 90nm library node to find the perfect sizing balance.
* **Key Tasks:**
  * Extracted maximum saturation drain-source currents ($I_{DS\_max}$) under maximum bias voltage to compute the definitive physical mobility ratio: $\mu_n / \mu_p = I_{DS\_NMOS} / I_{DS\_PMOS} \approx 1.915$.
  * Successfully derived the ideal target geometric ratios: **$W_P = 1.915\,\mu\text{m}$** paired with **$W_N = 1.0\,\mu\text{m}$**.
  * Dissected internal channel resistance properties ($R_{ds}$ via transconductance functions) and calculated net parasitic capacitances ($C_{total}$) across standalone and double-cascaded inverter pairs.

### Chapter 7: Design of a Ultra-High Frequency 10GHz Ring Oscillator
* **Objective:** Generate a precise, self-sustaining periodic clock wave by leveraging cumulative hardware gate propagation delays.
* **Key Tasks:**
  * Profiled an isolated intermediate inverter inside a basic multi-stage chain to track ideal symmetric switching delays ($t_{phl} \approx 12.09\text{ ps}$ and $t_{plh} \approx 12.23\text{ ps}$), keeping delay skew tightly constrained to just **0.14 ps**.
  * Implemented and custom laid out a closed-loop **5-stage Ring Oscillator** network engineered specifically to achieve a resonant clock oscillation frequency hitting the high-speed **10 GHz** target threshold.

### Chapter 8: Full Custom Implementation of a 2-to-4 Line Decoder
* **Objective:** Execute an entire, end-to-end custom physical design and sign-off flow for a multi-stage, combinational subsystem module.
* **Key Tasks:**
  * Applied the mathematical **Logical Effort** framework beforehand to map out, estimate, and distribute path effort to achieve the absolute minimum path delay along the critical decoding chain.
  * Formulated the circuit's full physical implementation (Schematic capture and structural multi-gate cell layout assembly).
  * Achieved 100% clean verification benchmarks via extensive post-layout **DRC**, **LVS**, and **StarRC parasitic netlist extractions**.
  * Compared analytical delay models ($D \approx 8.17$) alongside post-layout HSPICE waveforms ($\tau \approx 10.75\text{ ps}$) to fully validate design accuracy against non-ideal physical parameters.
