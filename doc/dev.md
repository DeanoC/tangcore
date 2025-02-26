## TangCore development setup (draft)

TangCore uses a different approach to development than previous versions of nestang/snestang. Here's a comparison of the two:

Old NESTang/SNESTang architecture:

<img src="snestang.drawio.svg" width="500"/>

TangCore architecture:

<img src="tangcores.drawio.svg" width="500"/>

Here are the differences:
* The firmware runs on FPGA in old NESTang/SNESTang, while it now runs on the BL616 MCU. This saves a fair amount of FPGA resources, which should be used for the gaming cores.
* For core switching, the old NESTang/SNESTang needs to write to the NOR flash chip, which is slow. Now firmware-bl616 uses JTAG protocol to directly write to the FPGA SRAM, which is much faster.
* Before, the cores and roms are stored on the SD card. Now the cores and roms are stored on a USB stick connected to the BL616. Using the USB interface allows us to support more types of USB devices in the future.
* For debugging, we used to rely on UART-over-USB through the BL616. Now we use the debug connector on the FPGA SOM.

Here's a picture of the TangCore development setup:

<img src="tangcores-dev-setup.jpg" width="500"/>

The end user does not need the SOM connector for debugging. Otherwise the seutp is the same as the developement setup.

Debug connection:
* We use the Sipeed RV-debugger dongle to connect the FPGA to PC.
* The FPGA SOM debug port has the following pinout (from top to bottom): GND, BL616_RX, BL616_TX, TDI, TCK, TDO, TMS, 5V0. We connect the TDI, TCK, TDO, TMS pins to the RV-debugger. The RX/TX UART pins are not used for debugging, as they are already used for internal communication between the BL616 and the FPGA.


