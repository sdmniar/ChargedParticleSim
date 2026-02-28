# ChargedParticleSim

Numerical simulation of electron-proton dynamics using scipy's solve_ivp, with interactive parameter exploration.

## Overview

This project investigates the orbital stability of charged particles in multi-nucleus systems, specifically exploring electron dynamics in a four-charge system (two nuclei and two electrons). The simulation models electrostatic interactions using Coulomb's law and solves the resulting differential equations numerically.

## Key Research Questions

- How does the change in initial electron velocities affect their orbital stability?
- Do electrons need to follow synchronicity for stable orbits?
- How does a two-nucleus system compare to the classical single-nucleus Bohr model?

## Physics Foundation

### Coulomb's Law
The primary force equation used in this simulation:

$$|F| = \frac{kq_pq_e}{r^2}$$

Where:
- **k** = 8.9875517923×10⁹ N·m²/C²
- **q_p** = Proton charge = 1.6×10⁻¹⁹ C
- **q_e** = Electron charge = 1.6×10⁻¹⁹ C
- **r** = Distance between charges

### Orbital Stability Criterion
Using the relationship between centripetal force and Coulomb force:

$$v = \sqrt{\frac{kq^2}{rm}}$$

For a proton-electron system at the Bohr radius (5.29×10⁻¹¹ m), the theoretical stable velocity is **2.17312×10⁶ m/s**.

## System Configuration

### Initial Parameters
- **Distance between nuclei**: 7.4×10⁻¹¹ m (scaled from H₂ configuration)
- **Distance from nuclei to electron**: 5.29×10⁻¹¹ m
- **Scaled nuclei positions**: ±3.7×10⁻¹² m from origin
- **Simulation duration**: 1×10⁻¹⁵ seconds
- **Simulation points**: 6000 time steps

### Key Assumptions
- Nuclei are stationary (do not interact with each other)
- Electrons start with zero x-velocity
- System exhibits symmetry (mirror positions)
- Electrons are captured if they approach nuclei within 1.2×10⁻¹¹ m
- Electrons escape if they exceed 10×10⁻¹⁰ m distance

## Implementation Details

### Dependencies
- **NumPy**: Numerical arrays and mathematical functions
- **SciPy**: `solve_ivp` for integrating differential equations
- **Plotly**: Interactive visualization and scatter plots
- **Pandas**: Data management and DataFrames
- **ipywidgets**: Interactive parameter control
- **Joblib**: Parallel computation for multiple simulations
- **Matplotlib**: Static trajectory visualization

### Core Components

#### Differential Equations
The system is modeled as 8 coupled ODEs representing:
- Position (x, y) of electron 1
- Velocity (vx, vy) of electron 1
- Position (x, y) of electron 2
- Velocity (vx, vy) of electron 2

Each acceleration component accounts for:
1. Attraction to nucleus 1
2. Attraction to nucleus 2
3. Electron-electron repulsion

#### Event Detection
Three types of terminal events are tracked:
- **Nucleus capture**: Electrons reaching nuclei boundaries
- **System escape**: Electrons exceeding atomic radius
- **Stable orbit**: No terminating events within simulation time

## Usage

### Running Simulations

```python
# Import packages
from sim import system, plot_electron1, plot_electron2, plot_simultaneous

# Run simultaneous electron variation
plot_simultaneous(samples=600)

# Run individual electron variations
plot_electron1(samples=600)
plot_electron2(samples=600)
