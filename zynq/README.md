How I run my zturn myir board
=============================

- I don't use the FSBL. [https://github.com/andreamerello/fpga-hacks/blob/master/zynq/boot-without-fsbl.md]

- I use a patched u-boot [https://github.com/andreamerello/u-boot-zynq]

- I use my kernel tree [https://github.com/andreamerello/linux-zynq-stable]

- When hacking, I load kernel/DT via TFTP, and I have a bunch of scripts to manage this, module upload via SCP, serial terminal, etc.. [https://github.com/andreamerello/linux-embedded-tools]

- When hacking by remote, I use a little Cortex-M board to drive the "reset" pin of my myir board (in case it hangs). It's attached to my home workstation via USB. The firwmare is [https://github.com/andreamerello/uakeh]

- For the FPGA design, I refer to my workmate Francesco stuff [https://github.com/francescodiotalevi/projects/tree/master/P2012_07_XZy/zturn] my fork [https://github.com/andreamerello/projects/blob/master/P2012_07_XZy/zturn/README.md]

Note: I don't load any bitstream on the FPGA at boot time. I want to do it later, from the OS, but I didn't tried it yet.

Right now I successfully loaded a bitstream from u-boot, as per instruction from Xilinx website

    U-Boot> fatload mmc 0 0x4000000 bitstream.bit
    U-Boot> fpga loadb 0 0x4000000 <bitstream file size>

Boot without bitstream is possible, and the following peripherals work:
- USB
- Ethernet
- SD card
- CAN (not tested)
- console USB/UART

The following peripherals cannot work until the bitstream is loaded because they need signals routed on EMIOs:
- Accelerometer
- Temperature sensor

The following peripherals cannot work without a proper FPGA IP:
- HDMI

I have not checked if the following peripherals could work:
- JTAG
- QSPI memory
- buzzer
- button
- LEDs