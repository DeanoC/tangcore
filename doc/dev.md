## Tangcores development setup (draft)

Tangcores uses a different approach to development than nestang/snestang. Here's a comparison of the two:

NESTang/SNESTang architecture:

<img src="snestang.drawio.svg" width="500"/>

Tangcores architecture:

<img src="tangcores.drawio.svg" width="500"/>

Here are the differences:
* The firmware runs on FPGA in NESTang, while in Tangcores it runs on the BL616 MCU. This saves a fair amount of FPGA resources, which should be used for the gaming cores.
* For core switching, NESTang needs to write to the NOR flash chip, which is slow. In Tangcores the firmware uses JTAG protocol to directly write to the FPGA SRAM, which is much faster.
* For NESTang, the cores and roms are stored on the SD card. For Tangcores, the cores and roms are stored on a USB stick connected to the BL616. Using the USB interface allows us to support more types of USB devices in the future.
* For debugging, NESTang uses the UART-over-USB through the BL616. In Tangcores, we use the debug connector on the FPGA SOM.

Here's a picture of the Tangcores development setup:

<img src="tangcores-dev-setup.jpg" width="500"/>

The end user does not need the SOM connector for debugging. Otherwise the seutp is the same as the developement setup.

Debug connection:
* We use the Sipeed RV-debugger dongle to connect the FPGA to PC.
* The FPGA SOM debug port has the following pinout (from top to bottom): GND, BL616_RX, BL616_TX, TDI, TCK, TDO, TMS, 5V0. We connect the TDI, TCK, TDO, TMS pins to the RV-debugger. The RX/TX UART pins are not used for debugging, as they are already used for internal communication between the BL616 and the FPGA.
* SDRAM1 (bottom sdram connector) pin 39 (SDRAM1_A2, R14) and 40 (SDRAM1_A3, P14) are used as TX and RX for debug UART connection.


