# HWMON.md

This document outlines the HWMON nodes exposed by this driver. The nodes can be found in `/sys/devices/platform/aorus_laptop/hwmon/hwmonX`.

## Fans

All `fanX_input` nodes are read-only, and all values returned are in revolutions per minute (RPM). Channel 1 is for CPU, channel 2 is for GPU, channel 3 is for fan 3 (if equipped), and channel 4 is for fan 4 (if equipped).

## PWM

All `pwmX` and `pwmX_enable` nodes are read-only, though support for making them writable may be added in the future. Channel 1 is for CPU and channel 2 is for GPU. Fans 3 and 4 (if equipped) do not have a way of measuring their PWM whatsoever.

The `pwmX` values use the usual HWMON range of 0-255: the driver scales the embedded controller's fan duty, where 229 is 100%. `pwmX_enable` reads 1 (manual) in auto and fixed mode, which run the fans at the custom fan speed, and 2 (automatic) in the other modes, where the embedded controller sets the speed.

## Temperature

All `tempX_input` nodes are read-only, and all values are in Celsius * 1000 (so `sensors` can read it correctly). Channel 1 is for CPU, channel 2 is for GPU, and channel 3 is for the motherboard.
