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

### Software setup

In fact the STM wiki is very good and up-to-date, so it can be followed to set up your system to build your own Linux kernel: [Installing the Linux kernel](https://wiki.st.com/stm32mpu/wiki/STM32MP1_Developer_Package#Installing_the_Linux_kernel)

The key points:
* Install the SDK
* Install the Linux kernel source

**Before compiling the kernel** with the cross compiler from the SDK **the following 3 patches need to be copied** to the existing 30 patches in the `linux-stm32mp-4.19-r0` directory:

* [0031-stm32mp157a-dk1-dts-add-two-M_CAN-pin-assignment-sup.patch](/patches/0031-stm32mp157a-dk1-dts-add-two-M_CAN-pin-assignment-sup.patch) (dts tree mod: route CAN pins to CN2)
* [0032-stm32mp157a-dk1-config-fix-CAN-driver-support.patch](/patches/0032-stm32mp157a-dk1-config-fix-CAN-driver-support.patch) (modification of default config for -better CAN support)
* [0033-can-m_can-implement-errata-Needless-activation-of-MR.patch](/patches/0033-can-m_can-implement-errata-Needless-activation-of-MR.patch) ([missing M_CAN patch](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/commit?h=linux-4.19.y&id=486954277fc1e18da5cf6c3110296b443cdecbaa) from [4.19.y stable](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/log/?h=linux-4.19.y) tree)

The 3 patches can be found in the [patches](/patches) directory.

After copying the 3 patches to the `linux-stm32mp-4.19-r0` directory just follow the steps in the [README.HOW_TO.txt](https://wiki.st.com/stm32mpu/nsfr_img_auth.php/b/b9/Linux.README.HOW_TO.txt) which can also be found in that directory to build and finally install the new kernel on the traget. **The README.HOW_TO.txt helper file is THE reference for the Linux kernel build** states the wiki - and they are right.

### Hardware setup




