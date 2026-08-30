# Sources — Four-Channel Load-Cell Instrument

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Load-cell / strain-gauge bridge sensor datasheets | Bridge resistance, rated output in mV/V, permissible excitation, temperature coefficients and wiring convention set the input range, drive requirement and error budget the front end must meet. |
| High-resolution ADC datasheets for the converter architecture chosen | Input-referred noise versus gain and data rate, the characteristics of any integrated PGA, common-mode range, reference-input drive requirements and - where channels are multiplexed - settling behaviour after a channel switch are the numbers any resolution claim must be derived from. |
| Voltage reference datasheets | Low-frequency (0.1-10 Hz) noise, temperature drift, long-term stability and output drive determine whether the reference, rather than the converter, sets the noise floor. |
| Precision amplifier / instrumentation amplifier datasheets | If any gain or buffering precedes the converter, its offset, offset drift, current noise and voltage noise enter the budget directly at microvolt scale. |
| Precision analog layout and grounding application notes | The brief requires a documented grounding and shielding strategy; return-path, guarding, thermal-EMF, leakage and shield-termination guidance is the evidence base for that document. |
| Host interface specification and PHY/connector datasheets (USB specification, or IEEE 802.3 plus PHY and magnetics data) | Whichever interface or interfaces the board carries dictate impedance, routing length, isolation, connector and power rules that must be satisfied alongside the analog constraints. |
| Nonvolatile memory datasheets | Calibration storage needs stated retention, endurance and write-integrity behaviour to justify that stored coefficients survive the product's life. |
| Regulator and power-converter datasheets | Output noise spectrum, switching frequency, ripple and PSRR interact directly with the stated primary challenge of measuring microvolts next to power conversion. |
| PCB fabricator capability and stackup documentation | Minimum trace/space, available stackups, copper weights and impedance tolerances for the chosen layer count bound what the layout may claim. |
| Assembly and part-availability data (footprints, packages, sourcing) | Every named component must be shown to exist in a buildable package with a verified footprint rather than being asserted. |
| ESD / EMC immunity standards and protection-device datasheets | Any protection or immunity claim on the sensor and host ports needs a referenced level and a device whose leakage and capacitance are compatible with the signal chain. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
