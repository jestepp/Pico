# RV Tank Monitor for Raspberry Pi Pico W

This example shows how to read up to eight RV tank level sensors through an
8-channel optocoupler ("octocoupler") board using MicroPython on a Raspberry
Pi Pico W.  Many RV tank probes switch 12 V, which cannot be connected to the
Pico directly.  The optocoupler isolates the high-voltage side and outputs safe
5 V logic that the Pico can read.

## Hardware overview

- Raspberry Pi Pico W running MicroPython 1.20 or newer.
- 8-channel optocoupler or isolator board (for example PC817-based boards).
- RV tank level sensors (commonly empty, 1/3, 2/3 and full probes).
- Optional: two tanks can be monitored at once (fresh and grey) with the eight
  channels.  Update the configuration in `main.py` if you need a different
  mapping.

Wire the optocoupler outputs to the GPIO pins listed in `TANK_CONFIG`.  The
script assumes the outputs go HIGH (3.3 V) when a sensor is active.  If your
board pulls the pin low instead, set `ACTIVE_HIGH = False` in the script.

## Usage

1. Copy `main.py` to the Pico's filesystem and rename it to `main.py` if you
   want it to run automatically on boot.
2. Edit the `TANK_CONFIG` dictionary to match the GPIO pins used for each tank.
3. Open a serial console (for example with Thonny) to watch the printed level
   updates.  Changes are only logged when a sensor transitions.

You can also import the `TankLevelSensor` class from another MicroPython module
if you plan to publish the readings over Wi-Fi or integrate them with Home
Assistant.
