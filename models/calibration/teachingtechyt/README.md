# Calibration models

These models are generated from <https://teachingtechyt.github.io/calibration.html>
for calibration of Creality Ender 3 v3 SE.

## Common settings

The following settings are used for all calibration prints:

| Parameter              | Value                                   |
| ---------------------- | --------------------------------------- |
| Nozzle                 | 0.40 mm                                 |
| Layer height           | 0.20 mm                                 |
| Auto Bed leveling      | Restore Saved ABL/manual mesh - M420 S1 |
| **Bed Dimensions**     |                                         |
| 0,0 at centre of bed   | Off                                     |
| X dim                  | 220 mm                                  |
| Y dim                  | 220 mm                                  |
| X offset               | 0 mm                                    |
| Y offset               | 0 mm                                    |
| Extra margin from Edge | 0 mm                                    |
| **Temperatures**       |                                         |
| Hot end                | 205°C                                   |
| Bed                    | 60°C                                    |
| **Part cooling fan**   |                                         |
| Part cooling fan speed | 100%                                    |
| starting on            | Layer 2                                 |
| **Retraction**         |                                         |
| Retraction distance    | 2 mm                                    |
| Retraction speed       | 45 mm/s                                 |
| Extra restart distance | 0 mm                                    |
| Z hop                  | 0 mm                                    |

### Additional Start gcode

All generated gcode has the following added in the `Additional start gcode`
section of the gcode generator. It will ensure that the test-lines that are
usually printed when using Creality Print is also printed before the calibration
prints. This should ensure that the nozzle and filament is ready for action.

```gcode
G28 ;Home

G92 E0 ;Reset Extruder
G1 Z2.0 F3000 ;Move Z Axis up
G1 X10.1 Y20 Z0.28 F5000.0 ;Move to start position
M109 S205.000000
G1 X10.1 Y145.0 Z0.28 F1500.0 E15 ;Draw the first line
G1 X10.4 Y145.0 Z0.28 F5000.0 ;Move to side a little
G1 X10.4 Y20 Z0.28 F1500.0 E30 ;Draw the second line
G92 E0  ;Reset Extruder
G1 E-1.0000 F1800 ;Retract a bit
G1 Z2.0 F3000 ;Move Z Axis up
G1 E0.0000 F1800 
```

## Frame check

All screws and fittings in the printer have been checked as described in the guide.
I have not removed the bed and thus haven't been able to check the screws underneath it.

## PID autotune

Not performed yet.

## Extruder e-steps calibration

Performed as described, but without Octoprint. Instead, I manually set the extruder
to extrude 100mm filament.

## First layer

Performed regular Auto Bed Levelling using the built-in functions on the printer.
This produced fairly even map. No warpint, but a slight slant to the left and back.

Additional settings:

| Parameter      | Value    |
| -------------- | -------- |
| **Feedrate**   |          |
| Base feedrate  | 100 mm/s |
| - Perimeters   | 36 mm/s  |
| - Solid infill | 48 mm/s  |
| - Travel moves | 100 mm/s |
| - First layer  | 30 mm/s  |

## Baseline

Prints a cube that can be measured for dimensional accuracy.

Additional settings:

| Parameter      | Value    |
| -------------- | -------- |
| **Feedrate**   |          |
| Base feedrate  | 100 mm/s |
| - Perimeters   | 60 mm/s  |
| - Solid infill | 80 mm/s  |
| - Travel moves | 167 mm/s |
| - First layer  | 50 mm/s  |

Initial print looked great. Very very slight elephants foot on top/bottom, but
probably nothing to worry about.

Target dimentions is 20 mm on all sides.

Measured dimensions:

- X: 19.93
- Y: 19.86
- Z: 20.14

## Slicer Flow Calibration

### Crality Print

Used the Cura settings described in the guide. They are located a bit differently
in Creality Print:

- Turn off infill:
  - Infill > Infill Density: 0 %
- Turn off top layers:
  - Shell > Top layers: 0
- Wall thickness:
  - Shell > Wall line count: 1
  - Extruder > Line width > Outer/Inner/Top/Bottom: 0.40
- Flow rate:
  - Material > Wall flow > Outer/Inner wall flow: 100%

Print takes a while.

Measurements after first print average to: 0.47

This leads to an adjusted wall flow of: 85.11

## Temperature tuning

- Hot end temperatures:
  - Segment E: 215
  - Segment D: 210
  - Segment C: 205
  - Segment B: 200
  - Segment A: 195
  - First layer: 205

Best layer: Segment D, 210°C.
