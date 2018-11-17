### Set Z Offset to 0
M851 Z0

### Send to EEPROM
M500

### Read from EEPROM to Memory/Active settings
M501

### Display Current Settings
M851

### Home Z
G28 Z

### Send Z back to it's 0 After it moves up when finished homing.
G1 F60 Z0

### Turn Off Software Endstops
M211 S0

### Move printer down to touch paper used for leveling (May take a few tries to get the right value)
G1 F20 Z-1.0
G1 F20 Z-1.1
G1 F20 Z-1.15
G1 F20 Z-1.2
G1 F20 Z-1.25
G1 F20 Z-1.2

### Calculate the actual Z Offset
Note the Z Offset: -1.2
Measure thickness of your paper/business card: 0.2
Add together the Z Offset & the thickness of your card: -1.4

### Enter your result as the new Z Offset
M851 Z-1.4

### Turn on Software Endstops
M211 S1

### Send to EEPROM
M500

### Read from EEPROM to Memory/Active settings
M501

### Display Current Settings
M851
