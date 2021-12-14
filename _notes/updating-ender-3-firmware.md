---
---

For some time now, the Creality Ender 3 printer is being shipped with the V4.2.2 32-bit board, with a bootloader; meaning that upgrading the firmware involves just booting up the machine with a new `firmware.bin` file.

#### Step 0: Make sure the board inside is V4.2.2
Unscrew the left panel. The board inside should have its version written on top of it.

#### Step 1: Install prerequisites 
Install [VS Code](https://code.visualstudio.com) if you don't have it installed already and the [PlatformIO IDE VS Code extension](https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide). Download [the zip file with latest release of the Marlin firmware](https://marlinfw.org/meta/download/) and the corresponding [config files](https://github.com/MarlinFirmware/Configurations/releases).

#### Step 2: Download the firmware
In the downloaded folder with the config files, find the `config\examples\Creality\Ender-3\CrealityV422` subfolder. This naming may change depending on the version - look for the name of your printer and the name of the board. Copy all the files into the `Marlin` subfolder inside the other downloaded folder with the Marlin firmware - overwrite the previous config files there.

#### Step 3: Prepare the `firmware.bin` file
Launch VSCode in the folder with the Marlin firmware and open the `platformio.ini` file. Set the value of `default_envs` to `STM32F103RET6_creality` (for example `default_envs = atmega2560` to `default_envs = STM32F103RET6_creality`).

#### Step 4: Add auto-leveling
Open the `Configuration.h` file and uncomment (remove the preceding `\\`) the following definitions:
- `#define MESH_BED_LEVELING`
- `#define LCD_BED_LEVELING`
- `#define RESTORE_LEVELING_AFTER_G28`

#### Step 5: Build the `firmware.bin` file
Click the check mark in the bottom left corner (*PlatformIO: Build*) or find the *PlatformIO: Build* command in the command palette (`ctrl + shift + P`).

#### Step 6: Flash the firmware
If the build succeeded, go to the folder with the Marlin firmware and find the `.pio\build\STM32F103RET6_creality` subfolder. Copy the `firmware-[timestamp].bin` file into the empty SD card. Turn off your printer, insert the SD card, and turn it on. After a few seconds, the splash screen should appear and the firmware should be successfully updated. 

#### Troubleshooting
If you're getting an error about the eeprom version error, choose `Ignore`, and in the printer settings choose "Store settings".