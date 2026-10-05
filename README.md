# Fabrication Toolkit for All

Export manufacturing files (Gerber files, BOM files & PNP files) for PCB manufacturers worldwide. Supported by [DIYIPCB](https://www.diyipcb.com).

Fabrication Toolkit for All is a free, open-source KiCad PCB Editor plugin that generates standard PCB manufacturing files. Use the exported files with your preferred manufacturer, or import the Gerber archive, BOM and placement files directly into the DIYIPCB PCB ordering page.

**[Download the KiCad plugin](https://raw.githubusercontent.com/DIYIPCB/Fabrication-toolkit-for-all/main/fabrication-toolkit-for-all.zip)** · [Report an issue](https://github.com/DIYIPCB/Fabrication-toolkit-for-all/issues)

## Features

- Gerber X2 files for copper, solder mask, silkscreen, solder paste and board outline.
- Separate plated and non-plated drill files, where applicable.
- Procurement BOM with manufacturer, complete part number, substitution rules, datasheet, DNP and LCSC Part #.
- Pick-and-place (PNP/CPL) files with references, positions, rotation and board side.
- A production ZIP containing the current export files and reports.
- A generation dialog with archive name, output folder, zone filling, DNP exclusion, PCB snapshot and browser import options.
- Optional file import into the DIYIPCB order page, including board dimensions and copper layer count.

## Compatibility

The export engine has been tested with KiCad 10.0.5 on Windows using a HackRF One board.

The package declares KiCad 8–10 compatibility; KiCad 8/9 and other operating systems still require validation. This is a testing release using the legacy `pcbnew` SWIG API. Installation through PCM and toolbar interaction should be verified in your KiCad environment.

The plugin is currently distributed by direct download. It has not yet been accepted into the official KiCad plugin repository.

## Installation

1. Download **fabrication-toolkit-for-all.zip** using the link above. Keep the ZIP intact.
2. Open the main KiCad project manager window.
3. Open **Plugin and Content Manager**.
4. Click **Install from File…** and select the downloaded plugin ZIP.
5. Complete installation and restart the PCB Editor if needed.
6. Open the plugin from **Tools → External Plugins** or its toolbar button.

Use the packaged plugin ZIP, rather than GitHub's automatically generated repository source ZIP.

## Usage

1. Maintain the component procurement fields in your schematic, update the PCB from the schematic and save your changes.
2. Open the plugin in the PCB Editor.
3. Review the generation options. The default output folder is **Fabrication files** beside your PCB file.
4. Click **Generate**.
5. Review the generated BOM, placement files and procurement issues before manufacturing.

Generated files are written directly into **Fabrication files**, with Gerber files in its `gerber` subfolder. Re-exporting updates output files with the same names. Each production ZIP contains only that export's generated files.

Zone filling is performed on the export copy; the original PCB is not saved or modified by the plugin.

## BOM fields

| Column | Purpose |
| --- | --- |
| Reference | Component references, such as R1 or U17 |
| Quantity | Quantity per board |
| Value | Component value or model |
| Footprint | PCB footprint |
| Manufacturer | Component manufacturer |
| Part Number | Complete manufacturer ordering part number |
| Substitution | Designer-supplied substitution rules |
| Datasheet | Datasheet reference or URL |
| DNP | Do not populate status |
| LCSC Part # | LCSC component number for JLCPCB-related workflows |

Existing custom fields are retained. Different part numbers, manufacturers, substitution rules, LCSC numbers or DNP states are not combined into the same BOM group.

If **Exclude DNP components** is selected, the production BOM excludes DNP parts and **BOM-All.csv** retains the full BOM. DNP components are excluded from placement files. Missing procurement information is reported in **procurement-issues.csv**; the plugin does not invent ordering part numbers or LCSC numbers.

## Send files to DIYIPCB

Leave **Open browser and import files to DIYIPCB after generation** selected and click **Generate**.

The plugin opens the [DIYIPCB PCB ordering page](https://www.diyipcb.com/product/pcb-pcba-order-online/) and fills its Gerber, BOM and placement upload fields, along with board dimensions and copper layer count when a valid outline is available.

- Keep KiCad open until import finishes.
- If your browser requests permission to access the local device, allow access for this import.
- Review PCB options and enable assembly if required.
- Sign in and submit the order through the website's normal process.

Importing files does not automatically submit an inquiry, place an order or make a payment. Files are transferred from the plugin into your browser through a temporary local bridge. If import fails, manually upload the exported Gerber ZIP, BOM and CPL files.

Uncheck the browser option to export locally without opening the order page. You can use the exported files with another PCB manufacturer.

## Manufacturer requirements

The plugin generates standard manufacturing data, but individual manufacturers may require different names, BOM headers or placement rotation conventions. Confirm these requirements before ordering.

- Top paste uses **-F_Paste.GPS**; bottom paste uses **-B_Paste.GBS**.
- Bottom solder mask uses **.GBS** without the `B_Paste` suffix. Gerber X2 layer attributes distinguish these files.
- If your manufacturer identifies layers only by extension, rename top/bottom paste files to **.GTP/.GBP**.
- Placement coordinates use millimetres, the KiCad auxiliary origin, X right and Y up. Rotation follows KiCad's native counterclockwise convention; bottom-side coordinates are not mirrored.
- An LCSC column supports component identification, but a manufacturer-specific BOM or CPL conversion may still be necessary.

Exporting files is not a DRC, electrical design review, stock check or component lifecycle check. Complete your design checks and verify component orientation before manufacture.

## Support and license

Report problems through [GitHub Issues](https://github.com/DIYIPCB/Fabrication-toolkit-for-all/issues). Include your KiCad version, operating system, error message and reproduction steps. Share project files only if you have permission to make them public.

Released under the [MIT License](LICENSE). Supported by [DIYIPCB](https://www.diyipcb.com).
