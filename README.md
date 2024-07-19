# Ostentus
The Ostentus is part of Golioth's "Aludel" platform, a family of devices that makes it easier to connect hardware to the internet using [Golioth's Firmware SDK](https://github.com/golioth/golioth-firmware-sdk) and [cloud platform](https://console.golioth.io). The Aludel family of devices are widely used in [Golioth's Reference Designs](https://projects.golioth.io), which are end-to-end demonstrations of IoT devices targeted at different vertical applications. 

This board acts as a display and input device for Reference Designs. Using a series of simple calls from a Zephyr platform, it's possible to offload readings from the underlying device and push them up to the display without consuming processing cycles on the main processor (such as the nRF9160 on the Elixir). We chose ePaper in order to have a high visibility display that would continue showing a reading when in a low power or off state. Since the QWIIC connector powers the Ostentus as well as sending data, it's possible to power down the entire subsystem of the Ostentus while still operating the underlying Elixir. 

This is released as Revision C of the Ostentus.

## On the board
* Raspberry Pi Pico - Originally chosen during the part shortages of 2022-23, the Pico provides a low cost solution including a programming interface over the USB port + micropython ease-of-use
* ePaper interface
* Accelerometer ([LIS2DH12](https://www.st.com/content/ccc/resource/technical/document/datasheet/12/c0/5c/36/b9/58/46/f2/DM00091513.pdf/files/DM00091513.pdf/jcr:content/translations/en.DM00091513.pdf)) -- Currently unimplemented but targeting "double tap" behaviors in the future
* 3 button capacitive touch controller ([CAP-1203-1](https://www.microchip.com/en-us/product/cap1203))
* QWIIC header for incoming power and i2c
* Downward firing LEDs

## Programming
There are two companion repositories which enable the Ostentus to work:
* [A firmware image for the Pico (`ostentus`)](https://github.com/golioth/ostentus)
  * This contains C and Micropython elements to process incoming i2c commands and control elements on the Ostentus like the ePaper and LEDs
  * [There is a binary available as a release](https://github.com/golioth/ostentus/releases) for easy loading onto the board.
* [A helper library for Zephyr (`libostentus`)](https://github.com/golioth/libostentus)
  * This includes commands and hooks for using i2c to communicate from a main board like the Elixir up to the Ostentus
  * Currently only Zephyr is supported but it should port FreeRTOS or bare metal

## The Aludel form factor

The Aludel form factor (Originally the "Aludel Mini" form factor) is based around the [Bud Boxes CU-1937-MB](https://www.budind.com/product/general-use-boxes/utilibox-style-l-series-utility-boxes-2/cu-1937-mb). This board is designed to affix to the top of this case without the original plastic lid from Bud. The QWIIC connector on backside of the Ostentus is meant to be wired to the Elixir, which has a matching connector. 

### Rev C Photos

![Ostentus_Front_Lit_RevC](https://github.com/user-attachments/assets/023f728b-6769-40fc-a74c-adb07ec1b32a)
![Ostentus_Back_RevC](https://github.com/user-attachments/assets/80250679-b436-4527-9bf3-28893d854fc3)
![Ostentus_Front_RevC](https://github.com/user-attachments/assets/8cdddbff-4d8f-4bb5-bb33-42f0ac376888)


## Purchase

The Ostentus board is not available to purchase. Please contact [devrel@golioth.io](mailto:devrel@golioth.io) if you would like to arrange help with your manufacturing. 

## Hardware Lineage and License

This design was derived from [the Pimoroni Badger 2040](https://shop.pimoroni.com/products/badger-2040?variant=39752959852627)

This board is released under the [CERN OHL-P (v2) license](https://opensource.org/license/cern-ohl-p). See [LICENSE](https://github.com/golioth/ostentus-hw/blob/main/LICENSE) for more info.

Any replication or modification of this design must remove references to Golioth and The Golioth Logo, which is a trademark of Golioth, Inc.
