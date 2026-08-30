# Architecture — Four-Channel Load-Cell Instrument

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- 24-bit ADC
- bridge excitation
- low-noise reference
- connector symmetry

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Bridge excitation and sensor interface

- Is excitation DC or chopped/AC, and what evidence supports that choice against thermal-EMF and 1/f error at microvolt level?
- Is one excitation source shared by all four bridges, or is each bridge driven separately - and what does that imply for crosstalk and for a fault on one channel?
- What bridge resistance range and cable length is the excitation drive sized for, and is that an assumption or a derived requirement?
- Does the design support remote sense (6-wire) so cable and connector IR drop does not appear as gain error, or is 4-wire accepted with a stated consequence?
- How is excitation current budgeted against self-heating of the load cell and against the board's own power dissipation?
- What happens electrically if a sensor is hot-plugged, mis-wired, or left disconnected on one of the four channels?

## Analog front end and conversion architecture

- Is conversion simultaneous, multiplexed, or a hybrid, and what concrete requirement (channel skew, throughput, settling time) drives that decision?
- What conversion architecture is chosen, and what does the microvolt-level accuracy requirement demand of it - noise, linearity, drift, input structure?
- If any channel is multiplexed, how long must the front end settle after a channel switch to reach the claimed resolution, and where does that number come from?
- Is there gain ahead of the converter at all, and if so where does it live - a converter-integrated PGA, a discrete instrumentation stage, or both - and what is the noise and offset contribution of each?
- What is the referred-to-input noise budget from sensor to output code, and how much of it does each stage own?
- What common-mode voltage does the bridge output sit at, and is that inside the chosen front end's usable common-mode range on all four channels?
- How are offset and drift handled - chopping, autozero, periodic zeroing, or calibration - and is that mechanism verifiable on the bench?

## Reference and ratiometric strategy

- Do the excitation source and the converter reference share a common origin so excitation drift cancels ratiometrically, and if so, is that path shown on the schematic?
- If the reference is absolute rather than ratiometric, what drift and noise does the system then inherit, and is that budgeted?
- What reference noise in the measurement bandwidth is tolerable given the target resolution, and how is that bandwidth defined?
- How is the reference filtered and buffered without violating the converter's reference-input drive requirement?
- Is one reference shared by four channels, and does that create a common error, a common-mode-rejected error, or a crosstalk path?

## Grounding, partitioning and shielding (required deliverable)

- Where does every return current physically flow - excitation return, sense return, digital return, power-converter return - and are those paths drawn, not just described?
- Is the ground a single uninterrupted plane with disciplined placement, or partitioned, and what specific failure is the chosen approach preventing?
- If the analog and digital domains are partitioned, where do they meet and what makes that meeting point better than the alternatives considered; if they share one plane, what keeps digital return current out of the analog area?
- How are cable shields terminated - at the connector, to chassis, to analog ground, through an impedance - and what assumption about the installation does that encode?
- Are guard structures used around high-impedance or high-sensitivity nodes, and what leakage or coupling mechanism justifies them?
- How will this strategy be validated after fabrication rather than asserted before it?

## Power architecture and conversion noise

- What is the input power source and range, and does the chosen host interface (USB or Ethernet) change that answer?
- Which rails feed the analog front end, and is any switching converter in that path - if so, what is its switching frequency relative to the measurement bandwidth and the converter's sampling?
- How much rail noise can the front end tolerate given its PSRR at the frequencies of concern, and does the regulation chain meet that with margin?
- Where are switching nodes and their current loops placed relative to the four analog channels and their connectors?
- What is the sequencing and settling behaviour at power-up, and can a partially powered state stress the sensor inputs?

## Digital controller, calibration storage and host interface

- What class of digital controller is required by the chosen conversion architecture and interface, and what is the minimum capability it must have?
- Is calibration stored in dedicated nonvolatile memory or inside the controller, and what retention, endurance and corruption-detection behaviour does that give?
- What exactly is stored per channel, and who applies it - the board or the host?
- How is digital activity (clocks, interface traffic, memory writes) kept out of the conversion window and off the analog rails and grounds?
- For each interface the board actually carries: if Ethernet, where do the PHY, magnetics and any isolation barrier sit relative to the analog section; if USB, where does bus power and its noise go?
- How is the board updated or re-calibrated in the field, and does that path exist on the schematic?

## Four-channel symmetry

- Are the four channels laid out as exact translations, mirrored pairs, or ad hoc - and what does the chosen arrangement do to matching?
- Are per-channel trace lengths, via counts and coupling to neighbouring returns equal, and how is that verified?
- Do all four channels see comparable thermal environments, or does one sit next to the regulator or the interface PHY?
- What channel-to-channel crosstalk is acceptable, and by what mechanism (shared excitation, shared reference, mux charge injection, ground coupling) would it occur?
- Are the sensor connectors arranged so cable dress does not privilege one channel over another?
- Does sourcing introduce any per-channel component tolerance or grade difference that would show up as inter-channel mismatch?

## Protection and fault behaviour

- What ESD, overvoltage and miswire events are the sensor ports expected to survive, and on what basis was that set?
- How is protection implemented without adding leakage, capacitance or nonlinearity that degrades microvolt-level measurement?
- Is the host port protected separately, and does its protection reference the same ground as the analog section?
- What happens to the other three channels when one channel is faulted or shorted?
- Are there fault conditions the design explicitly does not protect against, and are they written down?

## Mechanical, stackup and manufacturability

- What board outline, mounting and connector placement does the intended use imply, and is that an assumption being recorded as such?
- What layer count and layer assignment does the analog partitioning plus the chosen host interface actually require?
- Does the chosen host interface need controlled impedance, and does the stackup deliver it within the fabricator's capability?
- Which fabricator and assembler capability limits (minimum trace/space, drill, stackup options) constrain this design, and are they cited?
- Is the assembly single- or double-sided, and does connector and shield placement force the answer?

## Verification, calibration and test

- What measurement proves the microvolt-level claim - shorted-input noise, effective resolution at a stated rate - and is that test defined before layout?
- How is a channel calibrated at manufacture, and what equipment does that require?
- Are there test points or an injection path that let each stage be characterised without cutting traces?
- What self-test can the board run with no load cell attached?
- What acceptance criteria distinguish a passing board from a failing one on each of the four channels?

## Repository scope and toolkit boundary

- Which parts of this design belong in board-local configuration, and which, if any, are a genuine gap in the shared toolkit?
- How are board-specific rules expressed as configuration rather than as forked toolkit logic?
- What generated search, routing or simulation output is disposable, and what would have to be explicitly promoted to be kept?
- Where are the assumptions this design makes recorded, so a reviewer can separate brief requirements from design decisions?

## Answers still owed

All of them. See [status.md](status.md).
