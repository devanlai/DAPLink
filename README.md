# DAPLink
DAPLink is firmware that runs on a microcontroller that is connected according to a Hardware Interface Circuit (HIC) guideline. This provides methods to program and debug an application running on ARM processors via JTAG or SWD. The interface firmware exposes a USB composite device to the host OS with CDC, HID and MSC endpoints. These endpoints are critical when developing software for microcontrollers. Description of endpoints:
* MSC - drag-n-drop programming flash memory
* CDC - virtual com port for log, trace and terminal emulation
* HID - CMSIS-DAP compliant debug channel
* DFU - USB DFU programming flash memory

For more detailed usability information [see the users guide.](docs/USERS-GUIDE.md)

## WebUSB
This fork/experimental branch adds a USB DFU interface that can be used to flash targets from the browser using [WebUSB](https://wicg.github.io/webusb/). The DFU interface can be used standalone with native tools like [dfu-util](http://dfu-util.sourceforge.net/).

This project was done as an experimental proof-of-concept that was a fun exploration, but is no longer necessary because DAPLink incorporates WebUSB support for CMSIS-DAP by multiple means, making it possible to access debug functionality in DAPLink directly from the browser.

### Limitations
* This has only been tested on a limited selection of DAPLink hardware:
  * LPC11U35 interface chips, specifically with the [Seeed Studio Arch Max](https://www.seeedstudio.com/Arch-Max-v1.1-p-2632.html) board.
  * STM32F103RB interface chips, specifically the embedded STLink/v2-1 on the [Nucleo F103RB](http://www.st.com/en/evaluation-tools/nucleo-f103rb.html) board
* This has only been tested on Linux and macOS - Windows will almost certainly require fiddling with [Zadig](http://zadig.akeo.ie/) to load an appropriate WinUSB/libusb driver for the DFU interface.
* The DFU interface cannot be accessed by Chrome on Windows - Chrome's copy of libusb is missing upstream patches to handle control transfers to composite WinUSB devices more robustly.
