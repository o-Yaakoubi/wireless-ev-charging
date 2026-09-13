Wireless EV Charging System

Design and simulation of a static wireless charging system for electric vehicles, with a focus on power factor correction.

Overview

Wireless charging removes the physical connector between a vehicle and the grid. It also removes the wear, weather exposure and alignment problems that come with cables. For this to be practical, the system must transfer power efficiently and draw a clean current from the grid.

This project designs and simulates a static wireless EV charging system in MATLAB/Simulink. The work covers the full power chain from the AC grid to the battery, and compares several compensation topologies and two power factor correction strategies.

Problem

Wired charging is mature, but it has real limitations. Connectors wear out. Cables are exposed to rain and dust. Users have to plug in every time. Static wireless charging solves these problems, but it introduces new ones: lower efficiency, sensitivity to coil alignment and poor power quality drawn from the grid.

The power quality problem is the focus of this project. High-frequency converters and inductive coupling generate reactive power and harmonics. Without correction, the power factor drops, line losses grow and the system violates grid standards such as IEC 61000-3-2.

System architecture

The charging system is divided into a charger side and a vehicle side.

On the charger side, the AC grid voltage is rectified by a diode bridge, filtered by a DC-link stage, then converted to high-frequency AC by an inverter. The high-frequency AC feeds the primary coil.

On the vehicle side, the secondary coil captures the magnetic field. Its output is rectified and used to charge a Li-ion battery.

A compensation network is placed on both sides. Its role is to cancel the reactive part of the impedance so the system runs near resonance, which maximises power transfer and stabilises the input current.

Two families of compensation topologies are compared in this project: basic topologies (SS, SP, PS, PP) and hybrid topologies (LCC/LCC, CCL/LC, LC/LC, LCC/LCCL). From these, three configurations were selected for detailed simulation: SS, SP and LCC/L.

Power factor correction

Two strategies were implemented and compared.

Passive PFC. A simple LC filter tuned to a low frequency (around 290 Hz). Cheap and robust, but limited. It improves the phase relationship between voltage and current without actively shaping the current waveform. Total harmonic distortion remains high.

Active PFC. A boost converter with a dual PI control loop. The outer loop regulates the DC bus voltage. The inner loop shapes the inductor current to follow a sinusoidal reference in phase with the grid voltage. This produces a near-unity power factor and low distortion, at the cost of switching losses and greater complexity.

Results

Five configurations were simulated. Each was evaluated on three metrics: efficiency, power factor and total harmonic distortion.

Configuration                      Efficiency    Power Factor    THD
SS topology, passive PFC           84 percent    0.9256          43 percent
SP topology, passive PFC           72 percent    0.9471          43 percent
LCC/L topology, passive PFC        97 percent    0.9991          46.99 percent
SP topology, active PFC            75 percent    0.9886          15.86 percent
SS topology, active PFC            78 percent    0.9998          2.99 percent

The comparison reveals a clear trade-off.

Passive PFC keeps the circuit simple and the cost low, but it leaves significant harmonic distortion. The LCC/L topology with passive PFC reaches the highest efficiency (97 percent) and a very high power factor, which shows the value of a well-chosen compensation network.

Active PFC produces the cleanest current. The SS topology with active PFC reaches a power factor of 0.9998 and reduces THD below 3 percent, which meets grid standards. Efficiency remains lower because of switching losses in the boost converter.

The final recommendation depends on the application. For low-power, cost-sensitive systems, a passive PFC with an LCC/L compensation network gives the best balance. For high-power charging where grid quality matters, active PFC with an SS topology is the better choice.

Key takeaways

Coil compensation is not optional. Without it, reactive power dominates and efficiency collapses.

The choice of compensation topology has more effect on efficiency than the choice of PFC method.

Active PFC buys power quality at the price of efficiency. Whether that trade is acceptable depends on the standards the system must meet.

Simulation is enough to compare topologies, but it cannot replace prototyping. Thermal behaviour, EMI and misalignment effects only appear on real hardware.

Tools

The simulations were built in MATLAB/Simulink with Simscape Electrical. The PFC control loops use standard PI blocks. Power factor and THD are measured with custom scopes.

Author

Oumaima Yaakoubi
Instrumentation and Intelligent Systems, INSAT, Tunisia
LinkedIn: linkedin.com/in/oumaima-yaakoubi
GitHub: github.com/o-Yaakoubi

License

MIT License. See the LICENSE file for details.