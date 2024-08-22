## 101.1 Determine and configure hardware settings
---
### operating system
A computer is nothing but some hardware. An operating system is a software that manages hardware, sofware and it's resources.

### Firmware
Firmware is something between hardware and software, it is actually a software on the hardware which runs it.

Motherboards needs some firmware to be able to work, the older version of the firmware on the motherboard was called **Bios(basic input / output system)**.
Nowadays we have **UEFI (Unified Extensible Firmware Interface)**. UEFI has a seperate partition called **boot** in linux.

### Peripheral Devices###
**PCI (Peripheral Component Interconnect)** : We can connect hardware cards to the motherboard by PCI ports.

### GPIO ###
**General purpose Input Output** to control other devices. we can usually see these ports in a raspberry pi.

### sysfs ###
It is a pseudo file system directory provided by the Linux Kernel. It has Inforamtion that kernel has in it's memory like:
- Kernel subsystems
- hardware devices
- associated device drivers and ...

> Pseudo file means that it's not the disk but in kernel memory.

to see `sysfs` files, we can enter `/sys` directory.

### udev ###
`udev` or `userspace /dev` is a device manager for the linux kernel. We can use it to interact with our hardware devices. It is also a pseudo file system.
you can enter this directory by :
```bash
cd /dev
```

### dbus ###
D-Bus is a message bus system allowing applications to talk to one another.
It lets the processes to communicate with each other.

### proc ###
`proc` is another pseudo file system. It is where the kernel keeps it's settings and properties.
We can find things like:

- IRQs (interrupt requests)
- I/O Ports
- DMA (direct memory access, faster that I/O ports)
- processes
- network settings
- ...
example:
```bash
# Details about cpu
cat /proc/cpuinfo

# Details about memory
cat /proc/meminfo
```

> the numbers in `/proc` represent the processes.
> any chanes in `/proc` isn't permanent, because it's a pseudo file system.

### basic ls commands ###
- `lsusb` : usb devices
- `lspci` : pci devices connected to computer
- `lsblk` : list block devices like RAM/ROM/hard ...
- `lshw` : list almost everything about the hardware

### Loadable Kernel Modules ###
Linux as any other OS needs drivers to work with hardware. In linux most of these drivers are built-in.
The linux uses `loadable kernel modules (.ko files)` to prevent the kernel from loading all of them at the same time and to decrease the kernel size.

loadable kernel module commands:
```bash 
# To list all modules
lsmod

# To remove a module
sudo rmmod <NAME_OF_MODULE>

# to insert a module
sudo insmod <ADDRESS_OF_MODULE>

#as easier way to insert a module
sudo modprobe <NAME_OF_MODULE>
```
