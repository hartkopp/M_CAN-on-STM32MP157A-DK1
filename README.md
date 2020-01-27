# M_CAN-on-STM32MP157A-DK1
### Tutorial to enable and use the two M_CAN IP cores on the STM32MP157A-DK1 dev kit

The [STM32MP157A-DK1 discovery kit](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-mpu-eval-tools/stm32-mcu-mpu-eval-tools/stm32-discovery-kits/stm32mp157a-dk1.html) for the STM32MP157 SoC contains two Bosch M_CAN IP cores (one M_CAN and one MTT_CAN) that support CAN FD.

In opposite to the [STM32MP157C-DK2 discovery kit](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-mpu-eval-tools/stm32-mcu-mpu-eval-tools/stm32-discovery-kits/stm32mp157c-dk2.html) the STM32MP157A-DK1 does not provide a connector (including  CAN Transceiver and SUB-D9 connector) to access the M_CAN CAN controllers. Btw. the STM32MP157C-DK2 provides only the access to **one** of the two available CAN IP cores.

To access the two CAN controllers on the STM32MP157A-DK1 we need to ...
* change the device tree to route the CAN specific pins to the CN2 connector
* connect the CAN pins to CAN transceivers and finally to a SUB-D9 connector

The final setup could probably look like this:
![Transceiver on old IDE cable](/pictures/MCAN-TRX-Hardware.jpg)
Transceiver on old IDE cable
