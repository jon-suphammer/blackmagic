
# ESP32 target,

This provides a wifi based, debug probe on the esp32

# Build

. $HOME/esp/esp-idf/export.sh

./build-esp32.sh

# Based on this port
https://github.com/markrages/blackmagic/tree/a1d5386ce43189f0ac23300bea9b4d9f26869ffb/src/platforms/esp8266


So
```
GND on ESP32 connects to GND on the RAK board, opposite to the boot pins
PIN 23 on ESP32 connects to SWD_CLK
PIN 17 on ESP32 connects to SWD_TMS
```
Pins are changed in platform.h

```
I (3119) event: sta ip: 192.168.1.117, mask: 255.255.255.0, gw: 192.168.1.1
I (3119) blackmagic: Connected to AP
I (3119) gpio: GPIO[17]| InputEn: 0| OutputEn: 1| OpenDrain: 0| Pullup: 0| Pulldown: 0| Intr:0 
I (3129) gpio: GPIO[23]| InputEn: 0| OutputEn: 1| OpenDrain: 0| Pullup: 0| Pulldown: 0| Intr:0 
```


# Start the debugger,
```
arm-none-eabi-gdb .pioenvs/rak811/firmware.elf

target  extended-remote 192.168.1.136:2345

(gdb) monitor help

(gdb) monitor swdp_scan
Target voltage: not supported
Available Targets:
No. Att Driver
 1      STM32L1x

https://github.com/blacksphere/blackmagic/wiki/Frequently-Asked-Questions

(gdb) attach 1

```

Works like charm.


# Quicker download
```
arm-none-eabi-gdb .pioenvs/rak811/firmware.elf -ex 'target  extended-remote 192.168.1.136:2345'

(gdb) monitor swdp_scan
(gdb) attach 1
(gdb) load
(gdb) b main
(gdb) c


```