# FlowingDongleCCD
DIY Multiple Connection Watchman Dongle for SteamVR
FlowingDongle is a very simple dongle for SteamVR that can connect four devices simultaneously with a built-in nrf52840 module and a USB hub.
## Hardware
Includes PCB data created in kicad6 and 3D model data of the case.
The main components are made of the following.
|| components |
|--|--|
| USB 2.0 Hub Controller |FE1.1s  |
|nrf52840 module| MS88SF2 |

The PCB design and schematic is minimal and not perfect, although stable operation has been confirmed.

## Firmware
By writing the four hex files via SWD using a device such as Jlink, it can be used immediately as a Watchman Dongle.
Firmware comes from the following locations.
|   |  name |  place |
|---|---|---|
| Bootloader  |  nrf52840_xxaa_debug.hex |  nRF5_SDK_17.1.0_ddde560\examples\dfu\open_bootloader\pca10056_usb_debug\armgcc |
|  MBR |  mbr_nrf52_2.4.1_mbr.hex | nRF5_SDK_17.1.0_ddde560\components\softdevice\mbr\hex  | 
|  SoftDevice |  s140_nrf52_6.1.1_softdevice.bin |  C:\Program Files (x86)\Steam\steamapps\common\SteamVR\drivers\indexhmd\resources\firmware\radio\gd_1558748372_dfu | 
| Application  |  temp_app_stamped.bin |  C:\Program Files (x86)\Steam\steamapps\common\SteamVR\drivers\indexhmd\resources\firmware\radio\gd_1558748372_dfu | 

## Bootloader Build
