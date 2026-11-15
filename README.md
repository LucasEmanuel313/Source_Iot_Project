# Source IoT – Power Management Board (Versão de Segurança)

## Overview

This project is a printed circuit board (PCB) that manages the power supply of an IoT device. It takes power from USB and from an external 5 V input, charges a single-cell Li-Ion/Li-Polymer battery, selects the active power source, regulates the voltage for the rest of the system, and includes protection circuitry for the battery and the inputs.

The design was created in **Altium Designer** and includes a hierarchical schematic, custom libraries, the PCB layout, a bill of materials (BoM), and manufacturing outputs (Gerber, drill files, and PDF documentation).

A video demonstrating the most important features and displaying the board operation can be found in https://www.youtube.com/watch?v=zl5tvQph2-k&t=1s. Although the video is in Portuguese, automatic translated subtitles can be used directly on Youtube.

## Key Features

### Power management

- **Multiple power inputs:** USB (`+5V USB`) and external 5 V (`+5V Ext`), combined through Schottky diodes (MBR120VLSFT1G).
- **Battery charging:** MCP73831 single-cell Li-Ion/Li-Polymer charge controller, with charge status indicated by LEDs.
- **Step-down regulation:** AP63205 synchronous buck converter (32 V, 2 A) with its own sheet.
- **Power path:** a dedicated sheet (`Sheet6_Power_Path`) defines how the device switches between USB, external power and battery.

### Security and protection features

These protections are implemented in the schematic and BoM. The functions below are based on the component choices and net names; they should be checked against the schematic before production.

- **Transient voltage suppression (TVS):** unidirectional TVS diodes (SMAJ5.0A) on the 5 V input, and bidirectional TVS diodes (SMBJ28CA on the buck input and SMBJ6.0CA on the power path) to clamp voltage spikes and ESD events.
- **Overvoltage clamping:** a 15 V Zener diode (MMSZ5245B) on the buck and power-path sheets.
- **Battery protection:** a dedicated sheet (`Sheet5_Proteção_Bateria`) with a precision 1.2 V shunt reference (LM4041), a nano-power comparator (TLV7031) and a resistor divider. Together these appear to monitor the battery voltage and act on a load-disconnect switch (PJA3415 P-Channel MOSFET) when it falls outside safe limits.
- **Reverse-current blocking:** Schottky diodes on each input prevent current from flowing back from one source into another.
- **Controlled charging:** the MCP73831 charger limits charge current and terminates charging according to its fixed configuration.

## Repository Structure

| Folder / file | Contents |
| --- | --- |
| `PCB_Project_Source_IoT.PrjPcb` | Altium Designer project file. |
| `Schematics/` | Hierarchical schematic sheets (`.SchDoc`). |
| `Layouts/` | PCB layout (`PCB.PcbDoc`) and CAM files. |
| `Libraries/` | Symbol and footprint libraries, including the integrated library. |
| `BoM/` | Bill of materials exported from Altium (`.BomDoc`). |
| `GERBER/` | Gerber files, drill file (`cam.drl`) and CAM report. |
| `Jobs/` | Print output job (`Job1.OutJob`). |
| `Templates/` | A4 schematic template (VirtusCC). |
| `Project Outputs for PCB_Project_Source_IoT/` | Generated outputs: Gerber files, reports and fabrication files. |
| `*.pdf` | Diagram, assembly drawing, 3D view and project documentation. |

## Schematic Sheets

- `Sheet_Diagrama.SchDoc` – system overview
- `Sheet2_Hierarquia.SchDoc` – hierarchy and inter-sheet connections
- `Sheet3_Buck.SchDoc` – buck converter
- `Sheet4_Carregador_Bateria.SchDoc` – battery charger
- `Sheet5_Proteção_Bateria.SchDoc` – battery protection
- `Sheet6_Power_Path.SchDoc` – power path and input selection
- `Sheet7_Mechanical.SchDoc` – mechanical elements

## Main Components

- AP63205 synchronous buck converter
- MCP73831 battery charge controller
- DMP4065S and PJA3415 P-Channel MOSFETs
- MBR120VLSFT1G Schottky diodes
- SMBJ and SMAJ TVS diodes, MMSZ5245B Zener diode
- LM4041 voltage reference, TLV7031 comparator
- Chip resistors and ceramic capacitors (0805 and 1206)
- Status LEDs and screw terminal blocks

## Manufacturing Outputs

- Gerber files (`GERBER/` and `Project Outputs for PCB_Project_Source_IoT/`)
- Drill file (`cam.drl`)
- Output generation reports (e.g., `Status Report.Txt`)
- Assembly and 3D PDFs

## Tools

- Altium Designer (project, schematic and layout)
- A4 schematic template (VirtusCC)

## Skills Developed

- Hierarchical schematic design across multiple functional sheets
- Power-path and battery-management design for a single-cell Li-Ion/Li-Polymer battery
- Buck converter integration and component selection
- Circuit protection design: TVS clamping, reverse-current blocking, overvoltage clamping and battery protection
- Component selection from datasheets, including supplier and lifecycle data in the BoM
- PCB layout and design rule checks
- Preparing manufacturing outputs (Gerber, drill, BoM and assembly documentation)

## Author

**Lucas Emanuel Barbosa Vasconcelos**, electrical engineering student (UFCG) and double-degree student at ENSTA Paris, formerly embedded and hardware developer at EMBRAPII VIRTUS (VIRTUS CC).
