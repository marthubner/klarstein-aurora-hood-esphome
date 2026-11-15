# Bill of materials

Digestor: ESP32-C6 between the hood main board (CN2) and the glass touch panel.

## Electronics

| Ref | Qty | Part | Value / type | Notes |
|---|---|---|---|---|
| U1 | 1 | ESP32-C6-WROOM-1 board | 16 MB flash, about 52 x 28 mm, pin headers | Two USB-C ports, use the native one for flashing. Powered from CN2 5 V. |
| R1, R3 | 2 | Resistor | 100 k, 0.25 W, 1 % | Receive divider, series leg |
| R2, R4 | 2 | Resistor | 220 k, 0.25 W, 1 % | Receive divider, ground leg |
| R5, R7 | 2 | Resistor | 10 k, 0.25 W, 1 % | Transistor base |
| R6, R8 | 2 | Resistor | 100 k, 0.25 W, 1 % | Pull-down on the GPIO side of the base resistor, keeps the NPN off at boot |
| R9 | 1 | Resistor | 15 k, 0.25 W, 1 % | 5 V pull-up on the panel line |
| Q1, Q2 | 2 | NPN transistor, TO-92 | BC337 | Any small-signal NPN with Vce >= 20 V and hFE >= 50 works (BC547, 2N3904, S8050). Use the same type for both. |
| C1 | 1 | Electrolytic capacitor | 470 uF / 16 V | On the 5 V rail near the ESP |
| C2 | 1 | Ceramic capacitor | 100 nF (0805 SMD used) | On the 5 V rail near the ESP |
| J1 | 1 | JST-XH 4-pin pigtail | 20 cm leads | Plugs onto CN2 on the hood board |
| J2 | 1 | JST-XH 4-pin PCB header, right angle | 2.54 mm pitch | Receives the panel plug. Must be the right-angle type. |
| S1 | 1 | Particulate sensor | Sensirion SPS30 | I2C, 5 V, SEL tied to GND. Needs its own JST-ZH 1.5 mm 5-pin cable. |
| S2 | 1 | Temperature and humidity sensor | AHT10 module | I2C, 3.3 V |

## Boards and connectors

| Qty | Part | Notes |
|---|---|---|
| 1 | Perfboard 50 x 70 mm | Main board. The case is sized for this board. |
| 1 | Perfboard strip | Plug-in module for the interface circuit, 7 columns x 11 rows used |
| 2 | Male header strip, 6 pin | The plug-in module plugs into the main board with these |
| 2 | Female header strip, 6 pin | Main board sockets for the plug-in module |
| 2 | Female header strip, 15 pin | Sockets for the ESP32-C6 board |
| 2 | Insulated hookup wire, short | The only two wire links on the plug-in module |
| 1 | Hookup wire, about 1 m | Power, ground and I2C on the main board |

## Case and fasteners

| Qty | Part | Notes |
|---|---|---|
| 1 | Case bottom, 3D printed | case/case_bottom.stl |
| 1 | Case lid, 3D printed | case/case_lid.stl |
| 4 | M2 screws | Lid to the 5 mm bosses in the case corners. Length not recorded. |

The board standoffs, the SPS30 and AHT10 holders and the vents are part of the printed case. The case is 133 x 58 x 26 mm.

## Not in the final build

- The BSS138 4-channel level shifter module. Its 10 k pull-ups load the line too much, so the discrete interface circuit replaced it. The plug-in module for that circuit uses the sockets of the shifter.
- Jumper HV2 to HV3 and the 11 k series resistors from the pass-through test.
