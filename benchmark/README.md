# Benchmark entry — board 12 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_LoadCell_Instrument` |
| Board id | `loadcell_instrument` |
| Category | precision-analog |
| Difficulty | 3 / 5 |
| Brief detail | 2 / 5 |
| Likely layer count | 4 |
| Primary stressors | 24-bit ADC, bridge excitation, low-noise reference, connector symmetry |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

This is the precision-analog entry at difficulty 3/5 with a deliberately low-detail brief (2/5): the benchmark is testing whether an agent can build a defensible microvolt-class signal chain when the brief names the problem but not a single component. The stressor list - 24-bit ADC, bridge excitation, low-noise reference, connector symmetry - points at the four places the design can quietly fail: converter and front-end noise budgeting, how the bridges are driven and referenced, reference noise and drift, and whether four channels are actually built alike. Because the brief demands a documented grounding and shielding strategy while leaving the whole architecture open, it also tests whether the agent's reasoning is written down and traceable rather than asserted.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
