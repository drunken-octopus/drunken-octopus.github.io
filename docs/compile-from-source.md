## Compile from source

**Windows 10:** If you are using Windows 10, one of the easiest ways to build the firmware is using *Windows Subsystem for Linux (WSL)*. Simply follow [this guide] to set up WSL and get yourself an Ubuntu shell, then proceed with the steps for Linux.

**Linux:** Open a shell and execute the following commands one at a time:

```bash
sudo apt-get update
sudo apt-get install python git make rename
sudo apt-get install gcc-avr avr-libc
sudo apt-get install gcc-arm-none-eabi
sudo ln -s "/mnt/c/Users/YOUR_WINDOWS_USER_DIR/Documents" Documents
cd Documents
git clone https://github.com/marciot/drunken-octopus-marlin.git marlin
cd marlin
./build-configs.sh
./build-firmware.sh
```

Once this process is complete (it may take several hours), the firmware files will be in the `build` directory of your Documents folder.

**Arduino IDE:** In order to use the Arduino IDE, you will need download and extract the zip file from the [GitHub repo].

The, go into the unpacked folder and replace the "Configuration.h" and "Configuration_adv.h" files in the "Marlin" subdirectory with one of the example configuration files from "config/examples/AlephObjects". *Drunken Octopus* will only include the configuration files for the standard printers and toolheads.

Open the "Marlin.ino" file from the "Marlin" subdirectory in the Arduino IDE.

Choose "Preferences" from the "File" menu and add "https://raw.githubusercontent.com/ultimachine/ArduinoAddons/master/package_ultimachine_index.json" to the "Additional Boards Manager URLs".

In the "Boards Manager":
    - For TAZ Pro: Search for "Archim" and install "Archim by UltiMachine"
    - For all others: Search for "RAMBo" and install "RepRap Arduino-compatible Mother Board (RAMBo) by UltiMachine"

Choose the board corresponding to your printer from the "Board" submenu menu of the "Tools" menu. For a TAZ Pro, select "Archim"; for all others, select "RAMBo"

To compile and upload the firmware to your printer, select "Upload" from the "Sketch" menu.