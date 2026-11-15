# Home Assistant entities

What the firmware in `esphome/range-hood.yaml` exposes. Entity ids depend on the device name and your language,
so the table uses the ESPHome entity names. The example values were read from a running unit.

Two snapshots: **idle** (hood off, standby) and **running** (fan level 2, downlight on, turquoise backlight,
read about 6 s after the command, while the fan was still spinning up).

## Control

| Entity | Type | Idle | Running | Notes |
|---|---|---|---|---|
| Fan | fan | off | on, 66 % | 3 speeds: 33 / 66 / 100 % |
| Downlight | light | off | on | on/off only |
| Backlight | light | off | on | on/off only. Turning it on restores the last colour. |
| Backlight Select | select | off | turquoise | off, white, red, green, blue, pink, yellow, turquoise, yellow-green |
| Follow Panel | button | | | Drops the Home Assistant override, the hood follows the touch panel again |
| Dust Sensor | switch | off | | Starts and stops the SPS30. The first reading comes about 30 s after a start. |
| SPS30 Fan Clean | button | | | Runs the sensor's fan cleaning |
| Stop Pulse | number | 3500 us | | Length of the stop pulse the relay re-creates. Range 500 to 40000 us. |

## State and measurements

| Entity | Type | Idle | Running | Notes |
|---|---|---|---|---|
| Power | sensor, W | 1.6 | 20.9 | Estimated total including 1.6 W standby |
| Fan Power | sensor, W | 0.0 | 12.9 | Fan only, no standby |
| Downlight Power | sensor, W | 0.0 | 2.1 | |
| Backlight Power | sensor, W | 0.0 | 4.25 | Turquoise, reduced by 15 % because the downlight is on |
| Energy Today | sensor, kWh | | | Daily total of Power |
| Energy Total | sensor, kWh | 0.049 | | Integral of Power, kept across reboots |
| Fan Energy | sensor, kWh | 0.017 | | Integral of Fan Power |
| Fan Level | sensor | 0 | 2 | 0 to 3, as decoded from the hood's own frames |
| Motor Feedback | sensor | 0 | 73, then 88 | Settles at about 70 / 88 / 106 at levels 1 / 2 / 3 |
| Light Mode | sensor | off | both | off, downlight, backlight or both |
| Backlight Color | sensor | | turquoise | Decoded colour name |
| Backlight Color Index | sensor | | 8 | Raw colour code |
| Panel Lit | binary sensor | off | | The touch panel's own state is active |
| Override Active | binary sensor | | on | Home Assistant is currently overriding the panel |
| Frame A | sensor | 00 00 00 01 | 1D 18 08 01 | Last decoded frame, hex: fan code, flags, colour, counter |

## Air quality (SPS30 and AHT10)

| Entity | Type | Example |
|---|---|---|
| PM 1.0, PM 2.5, PM 4.0, PM 10 | sensor, ug/m3 | unknown while the Dust Sensor switch is off |
| PM 0.5 to PM 10 Count, Typical Particle Size | sensor, diagnostic | |
| Temperature | sensor | 22.7 C |
| Humidity | sensor | 48.6 % |

## Diagnostics

| Entity | Example | Notes |
|---|---|---|
| Relayed Panel Frames | counter | Frames A forwarded to the hood |
| Relayed Hood Frames | counter | Frames B received from the hood |
| Answered Panel Frames | counter | Frames B the ESP answered to the panel itself. It should track the panel frames closely. |
| Wi-Fi Signal | -79 dBm | |
| Status | on | Connection state |
