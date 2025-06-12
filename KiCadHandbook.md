# KiCad Handbook

## Basics
- Workflow is project-based and involves:
  1. Drawing a schematic.
  2. Laying out a circuit board.

## Definitions
- A **board** is a physical realization of the schematic.
- A **footprint** is a copper pad that matches pins on a physical component. 

### PCB Design Workflow
1. Draw a schematic.
2. Select footprints for each componet.
3. Inspect > Design Rules Check


### Hotkeys
```
Add Component      => A
Wire Tool          => W
Assign Value       => V

Add Graphic Line   => option + D
Move Parts         => M
Rotate Parts       => R
Trace Tool         => X
Add Filled Zone    => option + Z
Fill Zones         => B


```

### Set Up
1. Create a new project directory. It will contain a `.kicad_sch` and a `.kicad_pcb` file.
2. Draw the schematic.
3. Assign footprints => Tools > Assign Footprints.
4. Import the schematic to the PCB => Tools > Update PCB from Schematic
5. Change the layer to `Edge.Cuts` and use the Add Graphic Line tool to define a board size.
6. Route traces.
7. Add a ground fill. Set Layer to `F.Cu` and set Net to `GND`. Fill the zone.
8. Run DRC => Inspect > Design Rules Checker

