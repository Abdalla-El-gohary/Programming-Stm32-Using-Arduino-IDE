## 1- Install STM32CubeProgrammer
Download from the offical website

```bash
    https://www.st.com/en/development-tools/stm32cubeprog.html
```

## 2- Install Arduino IDE
Download the appimage from the offical website (Linux
AppImage 64 bits (X86-64))

```bash
   https://www.arduino.cc/en/software
```
Before we can launch the editor, we need to first make it an executable file. This is done by:

- right-click the file,
- choose Properties,
- select Permissions tab,
- tick the Allow executing file as program box.

![Alt Text](https://docs.arduino.cc/cec5dab5c3891762d78e57260fdc7317/linux-installation.gif)

You can now double click the file to launch the Arduino IDE 2 on your Linux machine. 

### Install STM32 Add-on to Arduino IDE
- In your Arduino IDE, go to File > Preferences

- Add the URL below to Additional Board Manager URLs text box:

```bash
    https://github.com/stm32duino/BoardManagerFiles/raw/main/package_stmicroelectronics_index.json
```
![Alt Text](../Guide-Photos/STM32_addon.jpg)

- Go to Tools > Board > Boards Manager

- Search for STM32, select latest version and click Install.

![Alt Text](../Guide-Photos/board_manager_install.png)

- Once the installation is completed, quit and restart the Arduino IDE.




## 3-Upload the bootloader using STM32CubeProgrammer 

- Clone the bootloader github repository or download the bin file only
```bash
    https://github.com/rogerclarkmelbourne/STM32duino-bootloader/blob/master/binaries/generic_boot20_pc13.bin
```

- Connect to the stm via St-Link

![Alt Text](../Guide-Photos/stlink-with-stm.jpg)

- Open STM32CubeProgrammer

![Alt Text](../Guide-Photos/stmcubeprogrammer-guide-stlink.jpg)

- connect to STM, browse the bootloader path, and start uploading the bootloader

![Alt Text](../Guide-Photos/stmcubeprogrammer-guide.jpg)

### If you don't have an ST-Link, you can use a TTL instead to upload the bootloader

- Switch the STM to programming mode and connect it via TTL

![Alt Text](../Guide-Photos/Blue-Pill-Operating-Modes.png)

![Alt Text](../Guide-Photos/STM32-with-USB-to-Serial-TTL.png)

- Upload the bootloader, then make sure to switch the STM back to operation mode.


### Note: The bootloader only needs to be uploaded once. After it’s uploaded, you can proceed to upload sketches or code to the board directly using the Arduino IDE.

## 4- Editing Udev Rules
- Edit /etc/udev/rules.d/45-maple.rules. 
```bash
    sudo nano /etc/udev/rules.d/45-maple.rules
```
- write that rules
```bash
  ATTRS{idProduct}=="1001", ATTRS{idVendor}=="0110", MODE="664", GROUP="plugdev"
  ATTRS{idProduct}=="1002", ATTRS{idVendor}=="0110", MODE="664", GROUP="plugdev"
  ATTRS{idProduct}=="0003", ATTRS{idVendor}=="1eaf", MODE="664", GROUP="plugdev" SYMLINK+="maple", ENV{ID_MM_DEVICE_IGNORE}="1"
  ATTRS{idProduct}=="0004", ATTRS{idVendor}=="1eaf", MODE="664", GROUP="plugdev" SYMLINK+="maple", ENV{ID_MM_DEVICE_IGNORE}="1"
```

## 5- Setup Arduino IDE
- Connect STM32 Blue Pill to your computer USB port.

![Alt Text](../Guide-Photos/Programming-STM32F103-Board-(Blue-Pill)-using-USB-Port.jpg)

- From the Tools > Board > STM32 Board, select Generic STM32F1 series

![Alt Text](../Guide-Photos/F103_board_b.png)

- Select Tools > Board Part Number > Blue Pill F103C8

![Alt Text](../Guide-Photos/F103_part.png)

- Under USB Support, select CDC (generic "Serial" supersede U(S)ART)

![Alt Text](../Guide-Photos/F103_USB_Support_b.png)

- Under Upload method, select Maple DFU Bootloader 2.0

![Alt Text](../Guide-Photos/STM32F103C8T6-USB-Bootloader-Arduino-Config.png)

- Compile the sketch and upload
