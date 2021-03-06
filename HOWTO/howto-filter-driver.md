## How to design and use a filter driver

Filter drivers:
- can be **upper** and **lower**
- can be for all devices of a **class** or for one **device**
- can be stacked and the order can be changed

#### Driver stack

| APP  | upper class filters | upper device filters | device driver | lower class filters | lower device filters | hardware |
|------|---------------------|----------------------|---------------|---------------------|----------------------|----------|

### Types of drivers

| Type | Description            | Explanation                                                     |
|------|------------------------|-----------------------------------------------------------------|
| UMDF | WDF User Mode Driver   | there is a framework, limited access to kernel                  |
| KMDF | WDF Kernel Mode Driver | there is a framework, kernel mode with access to INTERNAL IOCTL |
| WDM  | Windows Driver Model   | close to the operating system                                   |

The framework does work for you, but you know how to interface with it

It is wise to build for **kmdf version 1.11**, see [kmdf-version-history](https://docs.microsoft.com/en-us/windows-hardware/drivers/wdf/kmdf-version-history) when functionality of later kmdf versions is not needed 
- A driver for kmdf v1.11 will run on Windows Vista and later.
- Read: [Bye-Bye Co-Installers](https://www.osr.com/nt-insider/2016-issue1/bye-bye-co-installers/)

### Example from MS
[kbfiltr](https://github.com/Microsoft/Windows-driver-samples/tree/master/input/kbfiltr)
- upper class filter
- creates a raw PDO to open a communication channel to the filter driver

### Example from OSR
[CDFilter](https://github.com/OSRDrivers/WDF-I/tree/master/CDFilter)
- upper class filter
- minimal

### Install of filter driver
Right click on **CDFilter.inf** file and select **install**

### Uninstall of filter driver
From an **administrator cmd** run: **devcon classfilter cdrom upper !CDFilter**
- run: **devcon help classfilter** to read proper syntax

### Links
About filters:

- [Filter Drivers](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/filter-drivers)
- [Installing a Filter Driver](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/installing-a-filter-driver)

About drivers:
- [Types of WDM Drivers](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/types-of-wdm-drivers)
- [Differences Between WDM and WDF](https://docs.microsoft.com/en-us/windows-hardware/drivers/wdf/differences-between-wdm-and-kmdf)
- [Choosing a driver model](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)
- [Write your first driver](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/writing-your-first-driver)
- [Developing, Testing, and Deploying Drivers](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/)

WDM development:
- [A simple demo for WDM Driver development](https://www.codeproject.com/Articles/8651/A-simple-demo-for-WDM-Driver-development)
- [Writing WDM Drivers](https://docs.microsoft.com/en-us/windows-hardware/drivers/kernel/writing-wdm-drivers)
