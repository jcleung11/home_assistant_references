# Home Energy Management Reference

## Core Components
- **System View**: Dashboard tracks energy flow (source $\rightarrow$ usage).
- **Main Categories**: 
  - Electricity Grid
  - Solar Production
  - Battery Storage
  - Gas & Water Usage
- **Data Requirements**:
  - Sense of "Production", "Consumption" and "Storage".
  - Integration with sensors providing instantaneous power (W, kW) or cumulative energy (kWh).

## Configuration Details
- **State Class**: Use `state_class: measurement` for valid data tracking.
- **Unit Consistency**: Ensure correct units are used to populate the Energy dashboard automatically.
- **Utility**: Enables automation logic based on costs and availability (e.g., "run dishwasher when battery > 20%").
