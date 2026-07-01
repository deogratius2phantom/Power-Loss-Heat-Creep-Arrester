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
- Powered by a **Nokia BL-5C 3.7 V Li-ion battery** — widely available, compact, and plug-in replaceable
- Compact PCB footprint suitable for mounting inside a printer enclosure
- Fully open hardware (CC0 1.0 Universal licence)

---

## Board Preview

**Front (component side)**
![Board Front](docs/Screenshot%202026-06-02%20at%2018.37.28.png)

**Back — rev_1.0 silkscreen**
![Board Back rev_1.0](docs/Screenshot%202026-07-01%20at%2020.41.09.png)

The back silkscreen includes:
- **XundaTech / Heat Creep Arrester V1.0** — product branding
- **QR code** — scan to open this GitHub repository directly from the physical board
- **Connector pinout labels** (`FAN 24V`, `FAN GND`, `TO`, `GND`) — printed next to J3 for field assembly without needing a datasheet

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

Open the interactive BOM directly in your browser — no setup needed:

**🔗 [View Interactive BOM online](https://htmlpreview.github.io/?https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/blob/main/PowerLossHeatCreepArrester_v1.0/bom/manual_assembly_ibom.html)**

Or open the file locally: `PowerLossHeatCreepArrester_v1.0/bom/manual_assembly_ibom.html`

It provides an interactive board view where you can click each component to highlight its placement — ideal for hand-soldering.

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
| Fan activation | Only when hotend > 50 °C (adjustable via RV1) |
| Temperature sensing | Independent thermistor circuit (U4) — separate from printer NTC |
| PCB layers | 2 |
| Board thickness | 1.6 mm |
| Solder mask clearance | 0.005 mm |

---

## Revision History

### rev_1.0 (current branch)

Key changes from initial commit:

- **Independent temperature monitoring (U4 added):** A dedicated temperature sensing IC with its own thermistor was added after determining it is not feasible to share the printer's NTC across both the printer control board and this backup supply board without a carefully designed 3.3 V interface. U4 provides a clean, isolated temperature signal to LM393 comparator 2.
- **Comparator voltage divider recalculated:** R15 `210k → 52.3k`, R16 `40.2k → 10k` — revised to correctly set the 24 V power-loss detection threshold.
- **Hysteresis / reference network updated:** R21 `200k → 100k`, plus two comparator reference resistors adjusted (`10k → 47k` and `10k → 910k`) to match the new divider ratios.
- **GND symbol rerouted and thermistor label repositioned** on the schematic for clarity.
- **Net label typo fixed:** `indipendent_3d printer fan control input` → `independent_3d printer fan control input`.
- **PCB layout updated:** U4 placed at (138.51, 88.06), net assignments updated to match schematic changes, solder mask clearance set to 0.005 mm.
- **Back silkscreen additions:**
  - Product branding: `XundaTech / Heat Creep Arrester V1.0`
  - QR code linking to this GitHub repository (centre-back)
  - Connector pinout labels beside J3: `FAN 24V`, `FAN GND`, `TO`, `GND`

---

## Documentation

Full project documentation is in the [**GitHub Wiki**](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki):

| Wiki Page | Contents |
|-----------|----------|
| [Design Rationale](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Design-Rationale) | Why BL-5C, MT3608, TP4056, LM393 were chosen |
| [Circuit Theory](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Circuit-Theory) | How each circuit block works |
| [Bill of Materials & Sourcing](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Bill-of-Materials-and-Sourcing) | Full component list with supplier links |
| [Assembly Guide](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Assembly-Guide) | Step-by-step soldering instructions |
| [Testing & Calibration](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Testing-and-Calibration) | Verifying and tuning the circuit |
| [Troubleshooting](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Troubleshooting) | Common issues and fixes |
| [Version History](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Version-History) | Board revision log |

---

## Contributing

Contributions are welcome. See the [Contributing wiki page](https://github.com/deogratius2phantom/Power-Loss-Heat-Creep-Arrester/wiki/Contributing) for the full workflow. Please open an issue to discuss changes before submitting a pull request.

---

## Licence

This project is released into the public domain under the [CC0 1.0 Universal](LICENSE) licence. You are free to use, modify, and distribute this design without restriction.
