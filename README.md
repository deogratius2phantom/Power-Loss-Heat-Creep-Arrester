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

## Board Preview

**Front (component side)**
![Board Front](docs/Screenshot%202026-06-02%20at%2018.37.28.png)

**Back**
![Board Back](docs/Screenshot%202026-06-02%20at%2018.37.43.png)

📄 Full schematic & layout documentation: [PowerLossHeatCreepArrester.pdf](docs/PowerLossHeatCreepArrester.pdf)

---

## Repository Structure

```
Power-Loss-Heat-Creep-Arrester/
├── PowerLossHeatCreepArrester_v1.0/                      # KiCad v1.0 project (main design)
│   ├── PowerLossHeatCreepArrester_v1.0.kicad_pro         # KiCad project file
│   ├── PowerLossHeatCreepArrester_v1.0.kicad_sch         # Schematic
│   ├── PowerLossHeatCreepArrester_v1.0.kicad_pcb         # PCB layout
│   ├── board_v1.step                                     # 3D board export (v1)
│   ├── board_v11.step                                    # 3D board export (v11)
│   ├── .step                                             # Additional 3D export
│   ├── fabrication-toolkit-options.json                  # KiCad fabrication toolkit config
│   ├── bom/                                              # Bill of Materials & assembly aids
│   │   └── manual_assembly_ibom.html                    # Interactive BOM for manual assembly
│   └── production/                                       # Ready-to-order production files
│       ├── PowerLossHeatCreepArrester_v1.0.zip           # Gerber bundle for PCB fab
│       ├── bom.csv                                       # Bill of Materials
│       ├── designators.csv                               # Component designators
│       ├── netlist.ipc                                   # IPC netlist
│       └── positions.csv                                 # Pick-and-place positions
├── libraries/
│   └── PowerLossHeatCreepArrester.kicad_sym              # Custom schematic symbols
├── footprints/
│   └── PowerLossHeatCreepArrester.pretty/                # Custom PCB footprints
├── fabrication/
│   ├── gerbers/                                          # Gerber files for PCB manufacture
│   └── bom/                                             # Bill of Materials exports
├── docs/                                                 # Documentation & board images
│   ├── PowerLossHeatCreepArrester.pdf                   # Full schematic & layout PDF
│   ├── Screenshot 2026-06-02 at 18.37.28.png            # Board front view
│   └── Screenshot 2026-06-02 at 18.37.43.png            # Board back view
├── Heat Creep Arrester.pdf                               # Project overview document
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
3. Navigate to `PowerLossHeatCreepArrester_v1.0/` and open `PowerLossHeatCreepArrester_v1.0.kicad_pro`.
4. The schematic (`*.kicad_sch`) and PCB layout (`*.kicad_pcb`) will be available from the KiCad project manager.

### Generating Fabrication Files

### Interactive BOM (Manual Assembly)

Open `PowerLossHeatCreepArrester_v1.0/bom/manual_assembly_ibom.html` in any browser. It provides an interactive board view where you can click each component to highlight its placement — ideal for hand-soldering.

### Production Files

Ready-to-order files are in `PowerLossHeatCreepArrester_v1.0/production/`:

| File | Description |
|------|-------------|
| `PowerLossHeatCreepArrester_v1.0.zip` | Gerber bundle — upload directly to your PCB fab |
| `bom.csv` | Bill of Materials |
| `designators.csv` | Component designator mapping |
| `netlist.ipc` | IPC-D-356 netlist |
| `positions.csv` | Pick-and-place positions for SMT assembly |

To regenerate from source in KiCad PCB Editor (`pcbnew`):

1. Go to **File → Fabrication Outputs → Gerbers** → output to `fabrication/gerbers/`.
2. Generate the drill file via **File → Fabrication Outputs → Drill Files**.
3. Export the BOM via **File → Fabrication Outputs → BOM** → output to `fabrication/bom/`.

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
