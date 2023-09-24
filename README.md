# FlowingDongleCCD
DIY Multiple Connection Watchman Dongle for SteamVR
![dongle](https://github.com/ugokutennp/FlowingDongleCCD/blob/main/images/DSC04538.JPG)
FlowingDongle is a very simple dongle for SteamVR that can connect four devices simultaneously with a built-in nrf52840 module and a USB hub.
## Hardware
Includes PCB data created in kicad6 and 3D model data of the case.
The main components are made of the following.
|| components |
|--|--|
| USB 2.0 Hub Controller |FE1.1s  |
|nrf52840 module| MS88SF2 |

BOM can be viewed [here](https://htmlpreview.github.io/?https://github.com/ugokutennp/FlowingDongleCCD/blob/main/Hardware/PCB/flowing_dongle/flowing_dongle_bom.html).
The PCB design and schematic is minimal and not perfect, although stable operation has been confirmed.

[schematic](https://github.com/ugokutennp/FlowingDongleCCD/blob/main/images/flowing_dongle_schematic.pdf),
[pcb_design](https://github.com/ugokutennp/FlowingDongleCCD/blob/main/images/flowing_dongle_pcb.jpg)

## Firmware
By writing the four hex files via SWD using a device such as Jlink, it can be used immediately as a Watchman Dongle.
Firmware comes from the following locations.
|   |  name |  place |
|---|---|---|
| Bootloader  |  nrf52840_xxaa_debug.hex |  nRF5_SDK_17.1.0_ddde560\examples\dfu\open_bootloader\pca10056_usb_debug\armgcc |
|  MBR |  mbr_nrf52_2.4.1_mbr.hex | nRF5_SDK_17.1.0_ddde560\components\softdevice\mbr\hex  | 
|  SoftDevice |  s140_nrf52_6.1.1_softdevice.bin |  C:\Program Files (x86)\Steam\steamapps\common\SteamVR\drivers\indexhmd\resources\firmware\radio\gd_1558748372_dfu | 
| Application  |  temp_app_stamped.bin |  C:\Program Files (x86)\Steam\steamapps\common\SteamVR\drivers\indexhmd\resources\firmware\radio\gd_1558748372_dfu | 

## Bootloader build
Install [Make for Windows](https://gnuwin32.sourceforge.net/packages/make.htm) and Arm Embedded Toolchain ([gcc-arm-none-eabi-9-2020-q2-update-win32.exe](https://developer.arm.com/downloads/-/gnu-rm)) and build with the following command.

    cd Desktop\nRF5_SDK_17.1.0_ddde560\examples\dfu\open_bootloader\pca10056_usb_debug\armgcc
    make

## IndexHMD firmware optimization
Open temp_app_stamped.bin with a hex editor and edit the following items.
| adress  |  before |  after | effect |
|---|---|---|---|
| 0x1839D  |  1|B9 |disable index audio device |
|  0x162E0 |  Valve VR Radio | any string you like| rename USB device|

## Firmware conversion (bin to hex)
Convert firmware using [srec_cat_exe](https://sourceforge.net/projects/srecord/files/srecord-win32/).

    cd C:\Users\marim\Desktop\Dongle\gd_1558748372_dfu
    srec_cat.exe s140_nrf52_6.1.1_softdevice.bin -Binary -offset 0x1000 -o s140_nrf52_6.1.1_softdevice.hex -Intel
    srec_cat.exe temp_app_stamped.bin -Binary -offset 0x26000 -o temp_app_stamped.hex -Intel
## License
The license applies to hardware data only.
