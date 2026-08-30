# Requirements — Four-Channel Load-Cell Instrument

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `4d5d1134eda9c434c32c91b068ed5056ff2eec77043006e39459295ed1f4e00c`.

## Fixed by the brief

### REQ-01 — The board shall measure four channels of load cell.

Brief text:

> Create a four-channel load-cell measurement board for full Wheatstone-bridge sensors.

### REQ-02 — The sensors are full Wheatstone-bridge type; the front end must interface to full bridges.

Brief text:

> load-cell measurement board for full Wheatstone-bridge sensors. Provide stable bridge excitation

### REQ-03 — The board shall provide stable bridge excitation.

Brief text:

> Provide stable bridge excitation, simultaneous or multiplexed high-resolution conversion

### REQ-04 — The board shall perform high-resolution conversion of the bridge signals; the brief permits either a simultaneous or a multiplexed channel architecture, and the design must choose its approach and justify it.

Brief text:

> simultaneous or multiplexed high-resolution conversion, calibration storage

### REQ-05 — The board shall provide calibration storage.

Brief text:

> calibration storage, and a USB or Ethernet host interface.

### REQ-06 — The board shall provide a host interface drawn from the two the brief names, USB or Ethernet. The brief asks for one and selects neither; it says nothing about carrying more than one.

Brief text:

> and a USB or Ethernet host interface. The primary challenge is preserving microvolt-level signal integrity

### REQ-07 — The design shall preserve microvolt-level signal integrity in the presence of on-board digital logic and power conversion; this is stated as the primary challenge, so the design must show how it is addressed rather than only claim it.

Brief text:

> The primary challenge is preserving microvolt-level signal integrity in the presence of digital logic and power conversion.

### REQ-08 — The design agent shall select the architecture and the parts - this selection is a deliverable of the design, not a given.

Brief text:

> Choose the architecture and parts, and document the analog grounding

### REQ-09 — The analog grounding and shielding strategy shall be documented as an explicit written deliverable.

Brief text:

> Choose the architecture and parts, and document the analog grounding and shielding strategy.

### REQ-10 — Where the brief is silent, the design agent shall make and document reasonable engineering decisions rather than invent hidden user requirements.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-11 — Stated brief requirements are authoritative and must not be diluted or overridden by design convenience.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open

### REQ-12 — This repository shall remain a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not be pushed into the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — Which host interface the board carries from the two the brief names, and what physical connector and protocol stack it uses.

The brief offers the two as alternatives ('a USB or Ethernet host interface') and selects neither; nothing in the brief or metadata favours one over the other. It asks for one interface and does not address carrying more than one, so going beyond what it asks is itself a decision that needs recording.

*Decision:* **not yet made.**

### OPEN-02 — Whether conversion is simultaneous (a converter per channel), multiplexed (shared converter with channel switching), or a hybrid of the two, and the resulting per-channel throughput.

The brief explicitly allows both named approaches - 'simultaneous or multiplexed' - and states no sample rate, settling or channel-skew requirement to force the choice.

*Decision:* **not yet made.**

### OPEN-03 — The converter itself: resolution and architecture, integrated PGA versus a discrete gain stage ahead of it, and input structure.

The brief says only 'high-resolution conversion' and names neither a part nor a converter architecture; '24-bit ADC' appears in the metadata stressor list as a difficulty driver, not as a specified component.

*Decision:* **not yet made.**

### OPEN-04 — The excitation scheme: DC versus chopped/AC excitation, one excitation source shared across bridges versus per-channel sources, current drive versus voltage drive, and whether remote sense (4-wire versus 6-wire) is supported.

The brief requires excitation to be 'stable' but fixes no level, topology, load or wiring scheme; bridge resistance and cable length are unstated.

*Decision:* **not yet made.**

### OPEN-05 — The reference strategy: ratiometric operation (excitation and converter reference derived from one source) versus an absolute reference, plus reference filtering and buffering.

'low-noise reference' is a metadata stressor naming a problem area; the brief specifies no reference part, voltage, noise figure or drift limit.

*Decision:* **not yet made.**

### OPEN-06 — What digital controller the board carries - MCU, FPGA, or a fixed-function interface bridge - and its clocking.

The brief implies digital logic by requiring a host interface and calibration storage, but never names a controller class, vendor or capability.

*Decision:* **not yet made.**

### OPEN-07 — The calibration storage medium (discrete nonvolatile memory versus controller-internal), its capacity, and the per-channel calibration data model.

The brief requires 'calibration storage' and stops there - no format, no coefficient set, no capacity, no retention or endurance target.

*Decision:* **not yet made.**

### OPEN-08 — Power input: connector, input voltage range, self-powered versus bus-powered versus Power-over-Ethernet, and the regulation chain (switching, linear, or hybrid) that feeds the analog rails.

The brief is silent on power entirely; it only flags 'power conversion' as a noise source the design must live with.

*Decision:* **not yet made.**

### OPEN-09 — Whether any galvanic isolation exists - between channels, between the analog front end and the digital domain, or on the host interface - and where the isolation barrier sits.

The brief never mentions isolation, ground potential differences, or common-mode range between sensor cables.

*Decision:* **not yet made.**

### OPEN-10 — Sensor connector family, pitch, pin count and pinout, and whether cable shields land on a dedicated pin.

No connector is named. 'connector symmetry' is a metadata stressor about how the four identical channels are arranged, not a specification of a part.

*Decision:* **not yet made.**

### OPEN-11 — How channel symmetry is actually realised: mirrored versus translated placement, matched trace lengths and impedances, matched thermal environments, and matched component tolerance grades across the four channels.

The brief requires four channels but says nothing about matching, channel-to-channel offset, gain error, or crosstalk limits.

*Decision:* **not yet made.**

### OPEN-12 — Stackup detail: the actual layer count and per-layer assignment, whether analog and digital returns share one uninterrupted plane or are partitioned, copper weights, and controlled impedance if the chosen host interface needs it.

The brief's header calls 4 a 'Likely layer count' and metadata.json records layers as "4" without stating it as a constraint; the brief specifies no stackup, plane strategy or impedance target - it only demands that the resulting grounding strategy be documented.

*Decision:* **not yet made.**

### OPEN-13 — The shielding approach: cable-shield termination point and method, guard rings or driven guards around high-impedance nodes, board-level shield cans, and chassis/earth bonding.

The brief requires the shielding strategy to be documented but prescribes none of its content.

*Decision:* **not yet made.**

### OPEN-14 — Input protection strategy for sensor ports and the host port - ESD, overvoltage, miswiring/reverse-connection - and how protection components are kept from degrading the microvolt signal path.

The brief names no environment, no ESD class and no fault conditions; protection is entirely undefined.

*Decision:* **not yet made.**

### OPEN-15 — Performance targets: full-scale input range, sensitivity assumed for the bridges, output data rate, noise-free or effective resolution, the measurement bandwidth these are quoted over, and gain and offset drift over temperature.

The brief gives only the qualitative phrases 'microvolt-level signal integrity' and 'high-resolution' - no numbers of any kind are stated.

*Decision:* **not yet made.**

### OPEN-16 — Input filtering: EMI/RF filtering at the connector, anti-alias filtering ahead of the converter, and the digital filter or notch configuration for mains rejection.

The brief specifies no bandwidth, no line-frequency rejection requirement and no EMC environment.

*Decision:* **not yet made.**

### OPEN-17 — Board outline, dimensions, mounting hole pattern, connector edge placement, and whether the board targets an enclosure, DIN rail, rack or open-frame use.

The brief states no mechanical constraint at all.

*Decision:* **not yet made.**

### OPEN-18 — Test and bring-up provisions: test points, shunt-calibration or self-test injection, indicator LEDs, programming/debug access, and what the production test actually measures.

The brief describes no test, service or manufacturing-verification requirement.

*Decision:* **not yet made.**

### OPEN-19 — Host-side behaviour: command set, streaming versus polled data delivery, timestamping, and whether stored calibration is applied on-board or on the host.

The brief names an interface but defines no protocol, data format or division of processing.

*Decision:* **not yet made.**

### OPEN-20 — Fabrication and assembly constraints: fabricator and its capability limits, single- versus double-sided assembly, package/footprint restrictions, and part-availability sourcing.

The brief sets no process, cost, volume or supply-chain constraint; only the toolkit-consumer rule is stated.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Answer it under its `OPEN-nn` heading above, with the reasoning and the
   evidence that made the choice.
2. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json).
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Asserting 'microvolt-level' or 'high-resolution' performance without an input-referred noise budget built from actual datasheet noise, gain and bandwidth numbers - the single easiest unsubstantiated claim on this board.
- Writing the required grounding and shielding document as boilerplate ('star ground', 'split plane', 'keep analog away from digital') with no reference to where specific return currents flow or what the chosen converter requires.
- Fabricating specifications the brief never states - excitation voltage, full-scale range, sample rate, accuracy class, temperature range, enclosure or board size - and then presenting them as requirements.
- Resolving the brief's open USB-or-Ethernet choice silently - picking one, or carrying both - without recording it as a deliberate decision with a reason; the brief names the two and selects neither.
- Claiming simultaneous sampling while the chosen converter actually multiplexes one core, or claiming ratiometric operation without showing that excitation and reference share a single source.
- Treating 'connector symmetry' as cosmetic: declaring four matched channels without demonstrating equal routing, mirrored placement, comparable thermal environment and matched component grades.
- Naming a converter, reference or connector without confirming package, footprint and availability - plausible-sounding part numbers are hard for a reviewer to spot and easy to invent.
- Under-reading a short brief: dropping calibration storage, four-channel symmetry, or the explicit documentation deliverable because the brief mentions each only once.
