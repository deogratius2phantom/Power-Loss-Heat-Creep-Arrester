# Power Loss Heat Creep Arrester

A KiCad PCB design for a timer circuit that provides **24 V backup power to a 3D printer hotend fan** in the event of a power loss during printing. This prevents heat creep — the condition where residual heat travels up into the heatsink passage, causing filament to swell, clog, or jam.

---

## Overview

When a 3D printer loses power mid-print, the hotend heater turns off but residual heat remains in the heater block. Without the cooling fan running, this heat can creep up the cold zone, softening and swelling the filament inside the heatsink passage. The result is a jam that requires manual disassembly to clear.

This circuit detects the power loss event and uses a backup energy source (e.g. a capacitor bank or small battery) to keep the hotend fan spinning for a timed period — long enough for the heat to dissipate safely.

---

## Features

- Detects main power loss and triggers a timed backup fan drive
- Designed to supply 24 V to a standard 3D printer part-cooling or hotend fan
- Compact PCB footprint suitable for mounting inside a printer enclosure
- Fully open hardware (CC0 1.0 Universal licence)

---

## Repository Structure

```
Power-Loss-Heat-Creep-Arrester/
├── PowerLossHeatCreepArrester.kicad_pro   # KiCad project file
├── PowerLossHeatCreepArrester.kicad_sch   # Schematic
├── PowerLossHeatCreepArrester.kicad_pcb   # PCB layout
├── sym-lib-table                          # Project symbol library table
├── fp-lib-table                           # Project footprint library table
├── libraries/
│   └── PowerLossHeatCreepArrester.kicad_sym   # Custom schematic symbols
├── footprints/
│   └── PowerLossHeatCreepArrester.pretty/     # Custom PCB footprints
│       └── *.kicad_mod
├── fabrication/
│   ├── gerbers/                           # Gerber files for PCB manufacture
│   └── bom/                              # Bill of Materials exports
├── docs/                                 # Additional documentation & images
├── .gitignore
├── LICENSE
└── README.md
```

---

## Getting Started

### Prerequisites

- [KiCad 7 or later](https://www.kicad.org/download/) (the project files use the KiCad 6+ S-expression format)

### Opening the Project

1. Clone or download this repository.
2. Open KiCad and select **File → Open Project**.
3. Navigate to the repository folder and open `PowerLossHeatCreepArrester.kicad_pro`.
4. The schematic (`*.kicad_sch`) and PCB layout (`*.kicad_pcb`) will be available from the KiCad project manager.

### Generating Fabrication Files

From within PCB Editor (`pcbnew`):

1. Go to **File → Fabrication Outputs → Gerbers**.
2. Set the output directory to `fabrication/gerbers/`.
3. Generate the drill file via **File → Fabrication Outputs → Drill Files**.
4. Export the BOM via **File → Fabrication Outputs → BOM** to `fabrication/bom/`.

---

## Design Notes

| Parameter | Value |
|-----------|-------|
| Supply voltage | 24 V |
| Target load | Hotend / part-cooling fan |
| Backup duration | Configurable via RC timer |
| PCB layers | 2 |
| Board thickness | 1.6 mm |

---

## Contributing

Contributions are welcome. Please open an issue or pull request to discuss changes before submitting.

---

## Licence

This project is released into the public domain under the [CC0 1.0 Universal](LICENSE) licence. You are free to use, modify, and distribute this design without restriction.
