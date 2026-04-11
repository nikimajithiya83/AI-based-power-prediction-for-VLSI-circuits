**⚡AI-Based Power Dissipation Prediction and Optimization in VLSI Design**

An AI-powered system for predicting power dissipation in digital circuits at an early design phase — eliminating the need for full EDA tool simulation.

**Overview**
Power dissipation is one of the most critical challenges in modern VLSI design. Traditional power estimation relies on EDA tools like Synopsys or Cadence — a process that is slow, expensive, and can only be applied late in the design cycle. This project builds a machine learning system that predicts power dissipation from circuit design parameters at an early stage, without running any physical simulation.

**Dataset**
**Source:** CircuitNet-N28 (28nm technology node) — an open benchmark dataset for ML in EDA, published by Peking University.

- 10,242 samples generated from real open-source RISC-V CPU designs (RISCY, RISCY-FPU, zero-riscy)
- Each sample represents a unique chip layout configuration varied across clock frequency, utilization, macro count, power mesh, and macro placement
- Each sample is a 298×297 spatial IR drop map — IR drop is used as a proxy for power dissipation since high IR drop directly corresponds to high current demand and switching power


**What the System Does**
1. Feature Extraction
Design parameters are extracted from each circuit configuration — clock period, utilization, macro count, power mesh density, macro placement, and filler insertion. Statistical features like mean, max, standard deviation, and 90th/99th percentile IR drop are derived from the spatial maps.
2. Power Prediction Model
Two ML models were trained and compared on 3,860 processed samples:
ModelR² ScoreMAERandom Forest Regressor0.700.0335Gradient Boosting Regressor0.680.0356
Random Forest is used as the primary model. An R² of 0.70 means the model explains 70% of power variation using just 8 design parameters — no simulation needed.
3. Testing with Different Circuit Configurations
The system was tested across multiple circuit types and input parameter combinations — varying clock frequency, utilization levels, macro counts, and power mesh settings — to validate prediction consistency and generalization across diverse design scenarios.
4. Power-Hungry Module Identification with Graph Visualization
After prediction, the system identifies the top power-consuming modules from the IR drop maps. These hotspot modules are converted into an interactive graph visualization, making it easier to understand the spatial distribution of power across the chip and pinpoint which regions require optimization.
5. Redesigned Optimization Recommendations
The optimization recommendation engine has been redesigned to give targeted suggestions based specifically on the identified power-hungry modules rather than generic thresholds. Each flagged module receives recommendations relevant to its characteristics — such as applying clock gating to high-toggle regions, operand isolation for inactive datapaths, or strengthening the local power mesh.
6. User Interface
A UI is designed to allow users to interact with the system in two ways:

- Manual Input — Fill in circuit design parameters through structured input fields (design type, clock frequency, utilization, macro count, etc.)
- CSV Upload — Upload a CSV file containing multiple circuit configurations for batch prediction and analysis

The UI displays predicted power levels, module-level hotspot graphs, and tailored optimization recommendations for each input.

**Key Findings**

Clock frequency is the strongest predictor of power dissipation (~52% feature importance), consistent with the fundamental relationship P = αCV²f
Designs running at 500 MHz consume on average 8.5× more power than those at 50 MHz
193 out of 3,860 designs were flagged as high-power (top 5%), each with module-specific optimization recommendations
Early-stage prediction with no simulation achieves R² = 0.70 — sufficient to guide design decisions before EDA tools are involved


**Limitations & Future Work**

Actual switching power files from the dataset were corrupted at source; IR drop is used as a proxy — integrating real power data would improve accuracy
Only 3,860 of 10,242 samples were processed due to filename parsing edge cases in RISCY-FPU designs
Extending the system to CircuitNet-N14 (14nm) would improve cross-technology generalization
A CNN-based spatial model operating directly on IR drop maps could enable finer-grained, tile-level power prediction


**References**

CircuitNet Dataset — https://github.com/circuitnet/CircuitNet
