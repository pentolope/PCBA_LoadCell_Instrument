# PCBA_LoadCell_Instrument — Four-Channel Load-Cell Instrument

**Benchmark ID:** 12  
**Difficulty:** 3/5  
**Brief detail:** 2/5  
**Category:** precision-analog  
**Likely layer count:** 4  
**Primary stressors:** 24-bit ADC, bridge excitation, low-noise reference, connector symmetry

## Design brief

Create a four-channel load-cell measurement board for full Wheatstone-bridge sensors. Provide stable bridge excitation, simultaneous or multiplexed high-resolution conversion, calibration storage, and a USB or Ethernet host interface. The primary challenge is preserving microvolt-level signal integrity in the presence of digital logic and power conversion. Choose the architecture and parts, and document the analog grounding and shielding strategy.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
