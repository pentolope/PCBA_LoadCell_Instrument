# Four-Channel Load-Cell Instrument

Four-channel load-cell board for full Wheatstone-bridge sensors: stable excitation, high-resolution conversion, calibration storage, USB or Ethernet host.

This repository is the scaffold for **PCBA_LoadCell_Instrument**, a four-channel load-cell measurement board for full Wheatstone-bridge sensors. The brief fixes the function and the required blocks - stable bridge excitation, simultaneous or multiplexed high-resolution conversion, calibration storage, and a USB *or* Ethernet host interface - and names the primary challenge as preserving microvolt-level signal integrity in the presence of digital logic and power conversion. It also imposes written deliverables beyond the hardware: the analog grounding and shielding strategy must be documented, and the benchmark-intent paragraph requires that the choices the brief leaves open be made *and documented* rather than replaced by invented user requirements.

Everything else is open. At brief detail 2/5 the brief explicitly says to choose the architecture and parts, so converter topology, reference scheme, excitation method, controller, power input, connectors, protection, board outline and stackup detail are all the design agent's decisions - recorded here as open decisions, not pre-answered. No part numbers, converter architecture, voltages, sample rates, dimensions or accuracy figures appear in the brief, and none are assumed here.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 12 requirements and deliberately leaves
20 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Board function | Four-channel load-cell measurement board | brief |
| Sensor type | Full Wheatstone-bridge load cells | brief |
| Bridge excitation | Must be provided and stable; scheme, level and per-channel vs shared not fixed | brief |
| Conversion | High-resolution; simultaneous or multiplexed - the brief permits either, the agent must choose and justify its approach | brief |
| Calibration storage | Required on the board; medium, capacity and data format not fixed | brief |
| Host interface | USB or Ethernet - the brief names the two and selects neither | brief |
| Primary challenge | Microvolt-level signal integrity alongside digital logic and power conversion | brief |
| Required documentation | Analog grounding and shielding strategy must be documented | brief |
| Architecture and part selection | Explicitly delegated to the design agent by the brief | brief |
| Likely layer count | 4 | metadata |
| Category / difficulty / brief detail | precision-analog; difficulty 3; detail 2 | metadata |
| Primary stressors | 24-bit ADC, bridge excitation, low-noise reference, connector symmetry | metadata |
| Converter architecture | Not named by the brief or metadata - design agent's choice | open |
| Power input and supply rails | Not fixed by the brief - design agent's choice | open |
| Board outline, size and mounting | Not fixed by the brief - design agent's choice | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 12 of 32 |
| Category | precision-analog |
| Difficulty | 3 / 5 |
| Brief detail | 2 / 5 |
| Likely layer count | 4 |
| Primary stressors | 24-bit ADC, bridge excitation, low-noise reference, connector symmetry |

This is the precision-analog entry at difficulty 3/5 with a deliberately low-detail brief (2/5): the benchmark is testing whether an agent can build a defensible microvolt-class signal chain when the brief names the problem but not a single component. The stressor list - 24-bit ADC, bridge excitation, low-noise reference, connector symmetry - points at the four places the design can quietly fail: converter and front-end noise budgeting, how the bridges are driven and referenced, reference noise and drift, and whether four channels are actually built alike. Because the brief demands a documented grounding and shielding strategy while leaving the whole architecture open, it also tests whether the agent's reasoning is written down and traceable rather than asserted.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the claim-audit and accountability-review skills [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_LoadCell_Instrument.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `4d5d1134eda9c434c32c91b068ed5056ff2eec77043006e39459295ed1f4e00c`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
