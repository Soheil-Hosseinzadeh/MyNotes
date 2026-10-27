## Chapter 1 : Safety and Professionalism ##
### Tools of the Trade ###
Technicians need the right tools to do their job, tools like pc toolkits, moblie toolkits and ... .
### Trobleshooting Theory ###
**steps:**
1. Identify the problem
2. Establish a theory of probable cause
3. Test the theory to determine cause
4. Establish a plan of action to resolve the problem and implement the solution
5. Verify full system functionality and, if applicable, implement preventative measures
6. Document findings, actions, and outcomes
---
## Chapter 2 : The Visible Computer ##
### Primary PC Components ###
### Touring a PC ###
### What is a Computer? ###
---
## Chapter 3 : CPUs ##
### What is a CPU? ###
 > All different commands move along in what we call a `pipline` or also a `core`.

### Modern CPUs
###### Two main distinct features of modern CPUs
1. clock speed
2. cores
###### Different CPUs:
- normal ones (single core, dual core, quad core, ...)
- ARM (Advanced RISC Machine): These kind of chips use Reduced Instruction set Computing architecture instead of the complex instruction sets like in the regular CPUs and this allows us much higher speed in a much lower workload
- APU (Accelerated Processing Unit): A cpu that has graphic processing capabilities combined

### 32-bit vs 64-bit Computing
###### What are x86 or x64?
They actually show the amount of data that cpu can handle and work with in bit units.


| **Instruction Set Architecture (ISA)** | **Supports 32-bit Applications?** | **Supports 64-bit Applications?** |
| :------------------------------------: | :-------------------------------: | :-------------------------------: |
|                **X86**                 |                yes                |                no                 |
|               **X86-64**               |                yes                |                yes                |
|                **x64**                 |                no                 |                yes                |
What is **IA-32** by the way?
That actually stands for Intel Architecture 32 bit. They refer to a X86 base system.

A great site for creating a simulated PC and checking if everything fits or not: [pcpartpicker.com](https://pcpartpicker.com) 
### Installing and Troubleshooting a CPU
> Before everything and any touch make sure to use electrostatic discharge protection (ESD)

###### Connection mechanisms between CPUs and their sockets:
1. LGA : Land Grid Array (for Intel)
2. PGA: Pin Grid Array (for AMD)
---
## Chapter 4 : RAM

![[CompTIA A+ (220-1101)-20260115063511669.webp]]

##### Different Types of RAMs:
1. **SDRAM** : Synchronous dynamic random access memory (very old)
   Synchronous means that it's synchronized to the same clock of the crystal system, actually in any given click of the clock, the ram also can do something for us!
   This kind of ram is the only one that has got 2 notches rather than 1.

2. **DDR SDRAM** : Double data rate SDRAM
   For each clicking of the clock this kind of ram would give us two bits of information. So it would have a speed twice the clock speed of the motherboard (clock speed).
   
   ![[CompTIA A+ (220-1101)-20260115070118354.webp]]

2. **DDR2** : Double data rate 2
   Actually DDR2 was twice as fast as DDR.
   ![[CompTIA A+ (220-1101)-20260115070938093.webp]]
   
3. **DDR3** : Double data rate 3
   
   ![[CompTIA A+ (220-1101)-20260115072121407.webp]]

4. **DDR4** : Double 
   When we are talking about DDR4 we have Bandwidth and MT/s which means the actually amount of data that's being moved, not necessarily just the clicks of the clock.
   
   ![[CompTIA A+ (220-1101)-20260115073305890.webp]]

### RAM Capacity

##### What is dual channel technology?
When we are using channels we can actually talk to both sticks of the ram at once.

> In each dual channel we need to make sure to use identical stick rams, rams with the same speed and capacity.

![[CompTIA A+ (220-1101)-20260117135102911.webp]]

### RAM features

Rams work in bytes and that's why we have 8 chips so that each one is responsible for 1 bit!
![[CompTIA A+ (220-1101)-20260117140318857.webp]]
But there are some rams that have one extra chip! That's known for parity or ECC chip.
##### Parity vs. error correction code (ECC)
This is used to make sure that what ever the ram is doing is right.

> With **parity** we can have one of the other 8 chips be bad. (older and not used much today)
> With **ECC** we can have two of the other 8 chips be bad.

ECC is great and extremely expensive and we can put it on motherboards that are designed to use it!

We tend to see ECC motherboards in servers more than anything else.
##### Small outline dual inline memory module (SO-DIMM)
This kind of rams are mostly used in places that long sticks can't be used like in laptops.
![[CompTIA A+ (220-1101)-20260117143928145.webp|581]]

##### Serial presence detect (SPD) chip
![[CompTIA A+ (220-1101)-20260117144601579.webp]]
It's a little tiny chip on the RAM sticks. It allows the system to query the ram chip to figure out the ram capacity, technology, speed, model number and ... .
> Tools like CPU-Z read SPD information.


### Virtual Memory(RAM)
To use some space of the hard drive as the RAM space to avoid **Out of Memory errors**.
> Usually referred to as swap file.

---
## Chapter 5: Firmware

### Basic input / output services (BIOS)
We need to speak to some hardware devices even before booting into the OS.
In every motherboard there is a little bit of programming built into a chip that's designed to let you talk to the assumed hardware of the computer, This is called **BIOS**.

> **Bios programs are code.**
> **Bios is actually a Firmware which means it's burned onto a chip.**

![[CompTIA A+ (220-1101)-20260117184353472.webp]]

![[CompTIA A+ (220-1101)-20260117184532143.webp]]

### Power-On Self-Test (POST)
As soon as the CPU gets enough voltage it starts running and the first thing that it does is running some part of BIOS which is called **POST**.

> Post is a simple program in BIOS that comes up before anything else to diagnose and check hardware devices.
> It kind of broadcast a diagnostic to all the parts of the motherboard and they all go into their own internal diagnostic and send back a response to the CPU. If everything is fine a **BEEP** sound can be usually heard from the motherboard to show a proper booting.

##### What if there was something wrong?
 We would get to some POST errors in different ways:
 - **BEEP CODES** : Special Beep sounds 
 - **Display code** : Post error codes that show up in plain English on the screen 

In some bad situations the system might not be able to do any of the two above things, and just nothing comes up. In this situations we use something called **POST card**.
###### POST card
A board with two hexadecimal digit readout that we just plug into the system and watch what shows up.

![[CompTIA A+ (220-1101)-20260117193555007.webp]]

> The post codes of the Post card are only valid as the computer's booting up, once the OS comes up we will be free to ignore it.


### System Setup

A more modern updated BIOS is UEFI: **Unified Extensible Firmware Interface**

> remember: Bios is designed to talk to the assumed hardware of the computer.

System Setup is another part of BIOS which is an interface which by we can make changes to the changeable parts of the bios.

We can get into the system setup before the OS is booting by usually pressing keys like `delete` or `F2`.

Nowadays we have `Flash ROM` chips for BIOS. Flash means to reprogram.

> **RTC :** real time Clock, each computer needs to have it.

Informations like RTC, some systemsetups settings and ... need always electricity, that's where we need battery on motherboards to always have electricity.

> If a motherboard's battery doesn't work, we will get to some serious problems like: wrong system time, missing some system setup settings, resetting of some settings to default, non-recognition of some hardware and ...

---
## Chapter 7: Motherboards

Every motherboard has got something called `Chipset`. 
A motherboard is actually nothing but a chipset. The chipset of a motherboard determines the Ram capacity, USB capabilities, CPU architecture and more.

We have more than one chip for a single CPU model.

---
## Chapter 8: Power Supply

> They convert AC power to DC power.

### Connectors
##### Primary ATX main power connector
![[CompTIA A+ (220-1101)-20260203125012060.webp]]

It's got 2 pieces: The original one had 20-pins (the left one in the picture) but the modern power supplies needed more power so they added a 4-pin connector (the right one in the picture)

> **3 main voltage:** yellow(12 volt), red(5 volt), orange(3.3 volt)

##### ATX12V extension power
Over time it was discovered that we need more power and electricity for the motherboard so ATX12V came up as an extension of the original ATX power.
![[CompTIA A+ (220-1101)-20260203140320341.webp]]
These connectors are also plugged into the mother board. some motherboards need 4 pins, some 6 pins and some all of them.



The above connectors are just used for the motherboard itself.
Inside the case we've got hard drives, video cards and ..., so for all of these we need some power connectors.

##### Molex
The oldest general purpose connector. (12v, 5v)
![[CompTIA A+ (220-1101)-20260203140730853.webp]]

##### Mini Connector
Used for components like floppy drives.
![[CompTIA A+ (220-1101)-20260203141127044.webp]]

##### SATA power connector
It's used primarily for hard drives.
![[CompTIA A+ (220-1101)-20260203141243230.webp]]

##### PCIe Power connector
Used for Video cards.
![[CompTIA A+ (220-1101)-20260203143620113.webp]]


> The power supplies don't work efficiently and don't deliver as much wattage as they say so we gotta be sure to buy a power supply with some thing called **80 plus rating system** which means it is going to deliver at least 80% of the wattage which is said.
---
## Chapter 8: Mass Storage Technologies

> An atom: The smallest amount of storage that exist in a mass storage.
> In hard drives -> sector
> In SSDs -> block
> In optical media -> track

##### LBA: logical block addressing
Some hardware and software device driver that acts as an interface between OS and all storage devices and allocates as much block as is needed to save a file into some storage device.
> LBA is inherent to all operating systems and all mass storage devices.

##### Magnetic Disk Drives
> The language to talk with hard disk drives is **Advanced Technology Attachment (ATA)**.
> **Serial ATA (SATA)** is the physical interface (connector) for this language.
> ![[CompTIA A+ (220-1101)-20260203172437292.webp]]

##### Solid-state drives (SSDs)
Some SSDs also use SATA connector like the HDD.
But some other which are called M2 are different, they use  **SATA** or **NVMe** interfaces.
(the right M2 with 2 notches is SATA!)
![[CompTIA A+ (220-1101)-20260203182306913.webp]]

> NVMe is much faster that SATA, and it doesn't have any LBA like ATA interfaces and everything is controlled by the system itself.

##### Small Computer Systems Interface (SCSI)
This is another interface that was used for hard drives. SCSI was ATA competitor.
Today when we talk about SCSI we mean Serial attached SCSI:
![[CompTIA A+ (220-1101)-20260203190035963.webp]]

##### internet SCSI (iSCSI)
**iSCSI (Internet Small Computer Systems Interface)** is **a network protocol**, not a physical connector or drive interface.
It lets you access **remote storage over an IP network** as if it were a **local disk**.

---
## Chapter 9: Implementing Mass Storage
### RAID (Redundant Array of Inexpensive Disks)
It's a type of drive organization by which we use multiple drives instead of one.
There are two nice thing about RAID:
1. **Speed**
2. **Data redundancy**: Storing extra information derived from the original data so that lost data can be reconstructed if a disk fails.

##### RIAD Levels
- **RAID 0 (STRIPING)** : It requires an absolute minimum of 2 drives
  When a file is getting saved each part of it is saved in one of the drives.
  ![[CompTIA A+ (220-1101)-20260203234153100.webp]]
- **RAID 1 (MIRRORING)**: We use 2 drives (or even 4 drives)
  Putting another copy of the file in the second drive.
  ![[CompTIA A+ (220-1101)-20260205010638408.webp]]
  In most cases RAID one is slow.
- **RAID 2,3,4**: They are built with focusing on providing Redundancy and also having enough speed.
- **RAID 5:** The most popular one which works with parity mechanism.
  It require a minimum of 3 drives although more drives can be added.
  
  We save the first piece of the data in one drive and the second piece in some other drive. Then by doing some math stuff we can find something called parity value of these 2 pieces of data, we save this parity value in some other drive. Now if any of those pieces get lost, we are able to recover that piece by the other piece and the parity value.
  
  The parity value has the exact size as the other 2 pieces have.
  ![[CompTIA A+ (220-1101)-20260205012052283.webp]]
  >We are able to rebuild the data only if we just lose **one** of the drives. (not more)
- **RAID 6**: It requires a minimum of 4 drives.
  Again we put the first two piece of data in 2 different drives and compute the parity value of those 2 pieces and put this parity value in 2 other drives.
  ![[CompTIA A+ (220-1101)-20260205012731151.webp]]
  >We can lose up to 2 drives and still be able to rebuild the lost data.  

We can also use combinations of these RAID levels:
- **RAID 10:** Striping mirrors
  Works at least with 4 drives
  ![[CompTIA A+ (220-1101)-20260205013626587.webp]]
  ![[CompTIA A+ (220-1101)-20260205013709892.webp]]
  
  >We are free to lose one of the mirror drives in both mirror sides.
  >note: We can't lose a whole mirror side! that's where we get to RAID 0+1.

- **RAID 0+1**: mirror of striped
  It requires at least 4 drives.
  ![[CompTIA A+ (220-1101)-20260205014123778.webp]]
  
  >We can lose one complete striped pair on either side and we are ok.
  >If we lose one on each side we wouldn't be able to rebuild the mirror!


##### How to use RAID?
1. **Hardware**: By motherboard (Built in or like a card to snap into the motherboard)
   We can set the setting about it often through the system setup (BIOS)
2. **Software**: From the operating system itself.
   Most operating systems support some levels of RAID built in.

> There is some kind of advanced RAID which can be called **proprietary** format which are not any particular form of RAID and each company builds it for themselves in the way they want. (for efficiency and reasons like that)

### Hardware RAID

Hardware RAID requires a controller to configure the raid arrays. This controller can be an snap card or built-in to the motherboard.

To use Hardware RAID, we have to change the mode from **AHCI** to **RAID**.
>AHCI (Advanced Host Controller Interface) is a technical standard allowing software to communicate with SATA hard drives and SSDs.

![[CompTIA A+ (220-1101)-20260223140601906.webp]]

The Hardware RAID has it's own system setup, so when we change the mode to RAID after rebooting the system, it's system setup shows up as you see below:
![[CompTIA A+ (220-1101)-20260224184530771.webp]]

In this window we can configure our drives to use any version of RAID that we need.

**What is Hot spare ?**
A **hot spare** is an **extra standby disk** inside a RAID system that automatically replaces a failed drive.
It just waits there — powered on and ready.

Imagine you have:
- RAID 5 with 3 active disks
- 1 extra disk configured as _hot spare_
If one disk fails:
1. RAID controller detects failure.
2. It automatically activates the hot spare.
3. It starts **rebuilding** lost data onto that spare disk.
4. System continues running (no shutdown).

> The **Hot swappable** term means that we can remove and replace the drive without shutting down the system.


### Software RAID in storage Spaces

In software RAID we are letting the operating system to handle the things for us.
There are two parts to do the raid stuff in windows:
1. Disk mamangement:
   We can do the mirror and stripping in this part.
2. Storage space:
   In this part we can do different kind of raids, and the great point is that it uses virtual disks so at the end disk management sees nothing but the one abstraction drive which is the result of the RAID.
   ![[CompTIA A+ (220-1101)-20260224210155103.webp]]
   
   >**Three-way mirror** is microsoft proprietary RAID, It works efficiently even with drives of different sizes. It needs at least 5 drives, and can protect us from 2 simultaneous drive failures.
   
>The maximum size of the pool that we can set in windows storage space can be larger than the real available space, because it uses with virtual disks!
>If you set some size larger than the available one, once the physical real space got full, writing to the storage will fail and windows will warn to add more drives into the pool.


>Software RAID is slower and uses the CPU, but with a hardware RAID controller we have got more speed and no need to use CPU.

### Encryption mass storage
For some security reasons we may need to encrypt out storage.
There are two types of storage encryption:
1. File based encryption
   This is specifically encrypting some file or folder through your filesystem.
2. Disk based encryption
   This is encrypting the whole disk drive. For example in windows we can encrypt the whole C drive. (Although it may be just a partition of a disk not the whole hard disk)

>In windows we use **Encrypting File System(EFS)** which is built in NTFS, so you can use it in NTFS partitions.

![[CompTIA A+ (220-1101)-20260321013619843.webp]]

>In windows we can also encrypt a partition by **Bitlocker**.
>In mac os there is something for this called **file vaults**.

**Trusted Platform Module** 
In disk encryption, inorder for this to work there is some kind of key (lock) which is called **TPM**.
TPM is actually a chip that is plugged in or soldered into a motherboard, it has a very robust key in it that without that key you are never able to unlock your drive.

TPM can get turned on/off via system setup. (check the picture below for example)

![[CompTIA A+ (220-1101)-20260321014120293.webp]]

>In order to use Bitlocker, we need to have TPM turned on before, otherwise it is not going to work.

There is something else in windows called **Bitlocker to go** which is designed for removable media. It doesn't need any TPM module and uses a password key that the user gives.

---
## Chapter 10: Essential Peripherals

### USB Standards

![[CompTIA A+ (220-1101)-20260321015305685.webp]]

##### Different USB connectors
![[CompTIA A+ (220-1101)-20260325145454922.webp]]

![[CompTIA A+ (220-1101)-20260325145720343.webp]]

![[CompTIA A+ (220-1101)-20260325145905560.webp]]

> USB mini-B is usually used for cameras, video recorders and stuff like that.

![[CompTIA A+ (220-1101)-20260325150055459.webp]]

 ![[CompTIA A+ (220-1101)-20260325150119234.webp]]



> Different ports have different colors to show the USB version.

### Understanding USB
**USB controller**: It is some kind of built-in network in the motherboard that controls the USB inputs. 

> All USB devices connect to built-in USB controllers, which are in charge of all connected USB devices.

>USB Type-A is generally a downstream connection(connected to system); USB Type-B is generally an upstream connection(connected to the device).

>USB Type-C automatically configures the upstream and downstream connections.

### Optical Media
We can break it down into 3 groups: 
1. CDs
2. DVDs
3. Bluray

#### CD
>CD(compact disk) was built originally to only store music by microscopic tiny little pits and then nice shiny spots where are ones and zeros.

>CD-ROM was created to allow us to store files through the **ISO-9660 file system** structure(also called CD File System: CDFS).

>CD-R (write once) was also created to allow us to write data into it, but then we couldn't erase it.

>CD-RW then came up with the capability of rewriting data.

![[CompTIA A+ (220-1101)-20260404144654175.webp]]

#### Digital video/versatile disk (DVD)
DVD was originally designed to play movies.

>DVD-ROM: It's read only memory, and still popular these days.

![[CompTIA A+ (220-1101)-20260404145531134.webp]]

>DVD+R: This is a burned once DVD.

>DVD+RW

We may also see DVD-R and some weird stuff like that, they are all just different standards.

#### Blu-ray Disk
![[CompTIA A+ (220-1101)-20260404150106917.webp]]

### Expansion Cards
**PCI**: peripheral component interconnect devices are the ones that we usually connect to our mother board slots.

The new version of PCI is its updated standard with high bandwidth communication which is called: **PCIe**: Peripheral component interconnect express

>PCIe slots have different primary formats called **PCIe lanes**: **x1, x4, x8, x16**
>The more lanes you have the more traffic you can get through.

---
## Chapter 17: Display Technologies

### Monitor Technologies
#### LCD (Liquid Crystal Display)
**Pixel**: Picture element
It consists of three individual elements that emit red, green and blue. Colors are just such a cover over the LCDs.
Each one of those elements are actually a **Liquid Crystal Display** (LCD).

>If we put electricity on each of those three (LCD) elements, it goes clear and light can go through it.

>LCD can either let light pass or block light. So all LCD monitors have to have some kind of backlighting to them.

>On the first generation of LCDs we had **Cold cathode fluorescent lamp (CCFL)** as the backlight.
>Although in todays systems **Light-emitting diodes (LEDs)** are used as the backlights.

**Different technologies of LCD panels**
- TN panel
- IPS (In place switching): It has a very wide range of view

>Panels generally run from 200-500 nits (nit is the measure of lightness)

>LCDs with CCFL need AC power, that's why we use **Invertors** (DC to AC converter) in CCFL LCDs.

#### OLED (Organic LED)
Consider the RGB pixel that we had. Each one of the three parts is a light bulb, a red, a green and a red light bulb.

>You can make really thin monitors with OLED, that's why smart devices have OLED screens.

#### Digital Light Processing (DLP)
We have a grid of zillions of really tiny mirrors instead of individual pixels.
Mirrors are set up in a grid that defines the resolution.

One way to do DLP is like this:
We have a light source that is going through a color wheel that's spinning out RGB colors, so those lights turning on and off very quickly, and hitting the big grid of mirrors and then reflex out and make all the different colors.

DLP is popular with projectors.

### Graphics Cards and Connections
#### Connectors
**VGA**: 15 pins in 3 rows, it's always a blue connector
![[CompTIA A+ (220-1101)-20260516211558257.webp]]

>The problem of VGA: it's an analog signal. The monitor has to convert it into digital and update all the individual pixels, because it need digital signals.

**DVI**: The first digital connector.
![[CompTIA A+ (220-1101)-20260516212011431.webp]]

>The connector with a cross and 4 dot at the right are called **DVI-I**(digital and analog), the deliver analog signal too, so that you can use an DVI to VGA adapter to get analog signal.

But there some other DVI ports with a dash at right side, they only deliver digital signal.
![[CompTIA A+ (220-1101)-20260516212609691.webp]]

DVI was amazing for a long time but there was one problem with it: We still had to go through configuration to make it to work.

**HDMI** (High Definition Multimedia Interface):
HDMI is not used only for video, it also does sound.

**Display Port**: Some new dedicated ports used for videos.
We can see them on modern video cards.
![[CompTIA A+ (220-1101)-20260516214709442.webp]]

![[CompTIA A+ (220-1101)-20260516214753015.webp]]

### Resolutions and Aspect Ratios

#### 4 by 3 aspect ratio

![[CompTIA A+ (220-1101)-20260516232631151.webp]]

![[CompTIA A+ (220-1101)-20260516232706128.webp]]

![[CompTIA A+ (220-1101)-20260516232719303.webp]]

![[CompTIA A+ (220-1101)-20260516235801159.webp]]

#### 16 by 10 aspect ratio
It tied into golden ratio.
![[CompTIA A+ (220-1101)-20260517000046876.webp]]

![[CompTIA A+ (220-1101)-20260517000116034.webp]]

#### High definition (HD)

**720p**
![[CompTIA A+ (220-1101)-20260517000614809.webp]]

![[CompTIA A+ (220-1101)-20260517000831115.webp]]

**1080p**
Its resolution is 1920 * 1080

**4k**
Its is: 3840 * 2160

**5k**
Its resolution is 5120 * 2880



### Installing a graphic card

The picture below is about a riser card.
![[CompTIA A+ (220-1101)-20260517004544334.webp]]
**Riser card**:
>A riser card plugs into your main expansion bus and gives you an extra slot for another PCIe component like another second GPU.

### Projectors

Prjectors use two technologies
They use either **DLP** or **LCD**.

>For dark places projectors with around 1000 lumnes are appropriate.
>For a place with a lot of light, we are gonna need 2500 lumens.

---
## Chapter 18: Essentials of Networking

### Introduction to Networking
##### Ethernet
The most popular networking we use.
Ethernet defines what kind of cabling to use, what kind of hubs, .... It also defines speeds.

>Ethernet also defines something important which is we can only make our data in discrete chunks of 1500 bytes.

>Each of these chunks is called a **Frame**.

##### Media access control (MAC) address
MAC is used to uniquely identify every system on the local area network.

> 48 bit address.
> 12 hexadecimal characters.

For a mac address with 12 hexadecimal characters we have:
**OEM ID**: the first 6 characters
If someone wants to make network cards, he gets a fixed OEM ID and is free to spin up all the other character to make as much network cards as he wants.

To see the mac address in windows: `ipconfig /all`
To see the mac address in Linux: `ifconfig`

##### Ethernet Frame
![[CompTIA A+ (220-1101)-20260518140653499.webp]]
An ethernet Frame has got source and destination mac addresses.
**FCS**: is nothing but a checker that is used at the destination and compared with the data itself to know if the data came in in good order.

### Hubs vs. Switches

**Hub**: Acts like a repeater and sends back the FRAME that has received from D to other computers.
![[CompTIA A+ (220-1101)-20260519164433294.webp]]

>If the bandwidth of hub is 10Mb/s as most and if A wants to send data to B and C wants send data to D, then each connection is going to be done with 5Mb/s.

**Switch**: write down the MAC address of connected computers in their table and filter the traffic based on the MAC address.
>Switches provide full bandwidth for all nodes.

When A wants to send data to B, a **direct physical connection** is created by the switch from port 2 to 3.
![[CompTIA A+ (220-1101)-20260519165253258.webp|665]]

### WANs and Routers

##### Wide Area network (WAN)
A network which consists of multiple interconnected LANs.

In order for LANs to be able to communicate to each other we need **Router** to send traffic between LANs.

**Logical Address**: It's an address that indentifies a LAN.
**Physical Address**: It was an address that identifies the computer itself which we know as MAC address.

We use **IP addressing** as this logical address.
>Every device has got an IP in a local area network, with a fixed part in IP and a unique part for each device in that LAN.

![[CompTIA A+ (220-1101)-20260519174112175.webp]]

### Cables and Connectors

#### Coaxial cable
![[CompTIA A+ (220-1101)-20260519174540124.webp]]

When we talk about coaxial cables we use something called **RG ratings**.
There are different types of coaxial cables: RG-59, RG-58, RG-6.

RG-59 and RG-6 are used very much in the cabling world both for video and networking.
![[CompTIA A+ (220-1101)-20260519174931203.webp]]

##### F-type Connectors
![[CompTIA A+ (220-1101)-20260519175240042.webp]]


##### RG-58
The only type of coaxial cable that was used in the networking world was **RG-58**.
It was very thin.

It used a connector called **BNC connector**:
![[CompTIA A+ (220-1101)-20260519182242735.webp]]

#### Twisted pair
It is the predominant type of cable in networking world.
![[CompTIA A+ (220-1101)-20260519183035222.webp]]

>UTP has a maximum distance of 100m.

There are lots of different versions of UTP cables:
##### Telephone cable
Telephone cables have two pairs and a connector called **RJ-11**.
![[CompTIA A+ (220-1101)-20260519195135008.webp]]

##### RJ-45
The right one in the picture below is RJ-45 which has 4 pairs.
![[CompTIA A+ (220-1101)-20260519195324906.webp]]

##### Shielded twisted pair (STP)
The RG-45 with Shield:
![[CompTIA A+ (220-1101)-20260519195635809.webp]]


There is something else that we classify the UTP cables according to, which is **Cat (category) ratings**:

| Cat version | Speed                                    |
| :---------: | :--------------------------------------- |
|    CAT 5    | 100 Mbps                                 |
|   CAT 5e    | 1 Gbps                                   |
|    CAT 6    | 1Gbps (up to 100m) or 10Gbps (up to 55m) |
|   CAT 6a    | 10 Gbps (at 100m segments)               |



#### Fiber optic (fiber) cable
![[CompTIA A+ (220-1101)-20260519200935384.webp]]

There two types of Fiber optic:
- Multimode (uses LED to propagate the signal)
- Singlemode (uses lasers to propagate over many many kilometers of distance)
>In networking environments we usually see multimode (like the in the last picture we saw)

##### Connectors
![[CompTIA A+ (220-1101)-20260519203746617.webp]]

The connectors are in pairs, because one is for sending and the other for receiving data.

#### Plenum ratings
It's about the ability of cables to resist fire. 

1. **PVC (non plenum) rated cable**: This is like the most burnable one.
2. **Plenum-rated cable**: This type is much more resistant to fire.
3. **Riser-rated cable**: This type is an intermediate one.

### Crimping Cables
In this part crimping a Cat5e with an RJ-45 connector is examined.
![[CompTIA A+ (220-1101)-20260520013251141.webp]]

>While crimping a cable with the connector the order of the pairs and their colors is important.

There are two standards for this purpose: **TIA 568A/TIA 568B**.
We consider the numbers of the connector pins from right to left when the tap of the connector is on the bottom.

>Colors matter, according to the TIA 568A/ TIA 568B standards we should crimp the pairs like below:
![[CompTIA A+ (220-1101)-20260520014134207.webp]]


There are two different types of cabling with the above standards:
- **Straight-through cable**: It has same standard on each end.
- **Crossover cable**: It has different standards on each end.
  In this way we can plug two computers directly to each other.
---
## Chapter 19: Local Area Networking

### IP
Every started from 1970-1980 where we had many individual LANs in USA and they wanted to connect them to each other.

In the old days they were connected through telephone lines, which was designed by an organization called **ARPANET**.
![[CompTIA A+ (220-1101)-20260520192252722.webp]]

They decided to assign a number (the IP address) to each computer. 

Each IP address does:
1. Identify which LAN you are a part of
2. Give you a unique host ID

IP has a kind of hierarchical behavior like below:
![[CompTIA A+ (220-1101)-20260520193445308.webp]]

Different IP classes:
![[CompTIA A+ (220-1101)-20260520193357670.webp]]

>Note: IP addresses will never end with 0 or 255!
>Because an IP address that ends with 0 identifies the entire LAN.

##### Subnet mask
A subnet mask can be something like: 255.255.255.0 which indentifies the network id part of and IP address.

If you want a computer to be connected to the internet, you are going to:
1. Give it an IP address
2. Give it a subnet mask
3. Give it a default gateway (the router ip address which usually ends with 1)


### Dynamic IP Addressing
**Dynamic host configuration protocol (DHCP)**: A way to provide dynamic IP addressing

When you connect to the network, you don't set any ip address, or subnet maks and ..., because when you connect to the network, **DHCP server** does it all for you.

>Home routers act like DHCP servers.

![[CompTIA A+ (220-1101)-20260520215650315.webp]]

##### Automatic Private IP Addressing (APIPA)
if a DHCP client can't find the DHCP server, it will use an APIPA address.
By default APIPA always set a 169.254.X.X address.
>This is a class B address.

In this way if the DHCP server of a LAN goes down, they all at least can communicate to each other so that they all have this constant part in their IP addresses: 169.254.X.X, which make them nodes of a single LAN with address 169.254.0.0 .

### IPv6
We ran out of IPv4 so we started to use IPv6.
An example of IPv6 address:
**`2001:0db8:85a3:0000:0000:8a2e:0370:7334`**

>It is a 128-bit address with 8 groups seperated by : sign.

We have two different IP addresses:
1. **Link local address**: It's distinct, always start with **`fe80:0000:0000:0000`** and the last half of address is automatically generated by the system itself.
   When you boot a computer that is IPv6 capable, it will have a link local address.
2. **Global unicast address (Internet address)**: It's taken from the actual router itself. The router broadcast the first half of the address and the computer automatically generates the second half.


>The right half of IPv6 address is called **prefix** which is like an IPv4 subnet mask.

### Port Numbers
It's what gets us to the right application.
It changes from 0 to 65535.

We are always going to have source and destination port numbers.
![[CompTIA A+ (220-1101)-20260527211411258.webp]]


We have 3 types of port numbers:
1. **Well known ports**: 0-1023
2. **Registered ports**: 1024-49151
3. **Dynamic/ephemeral ports**: 49152-65535

![[CompTIA A+ (220-1101)-20260527212855953.webp]]

### TCP, UDP, and ICMP

**Protocol**: It's a set of rules that allow different things to work together.

We organize packets by protocol data units (PDUs).
#### TCP/IP (Transmission control protocol/Internet protocol)

>It is a connection based protocol.
>At first something called handshake is done at this protocol.
>The PDU at this point is called **TCP segment**.

#### User Datagram Protocol (UDP)

>It is a connectionless protocol.
>There is no handshake.
>The PDU at this point is called **UDP datagram**.

#### Internet Control Message Protocol (ICMP)

>It's connectionless and always a **single packet**.

### Underestanding DNS (Domain name server)

DNS is an domain name resolver. It gets the IP of the domain that some client tend to request to.

>DNS replaced something called **Hosts file**. Host file lasted as the primary way to reslove names into the mid 1990s.
>Every computer still has a host file.

Back in the old days, if you wanted to join the internet, you would type in your ip address and give your computer some name and then submit that. And then every morning at 3 a.m., that host file was distributed to every single computer on the internet.

DNS works like the picture below, when we request to some domain name through our browser, at first the DNS resolver queries the domain name's IP through a hierarchical servers.
![[CompTIA A+ (220-1101)-20260528033129724.webp]]

>Our computer and the DNS server (DNS reslover) also store the ip of the requested domains for some time, to make the query for that domain name faster. This is called Cahcing.

![[CompTIA A+ (220-1101)-20260528033657553.webp]]

#### Security by DNS
Imagine we own the domain `example.com`.
Someone sends some email and claims that it's from our domain, for example from `admin@example.com`.
Or there can be someother problem too. We may send some email from our domain, but someone at the middle of the route, changes our email.
>By DNS we can verify the authenticity of not only the messages themselves but the senders of the messages.

The Internet's original email protocols were designed in the 1970s and had almost no security built in.
So modern email systems added:
1. SPF
2. DKIM
3. DMARC

All these methods uses Domain name servers.
##### SPF (Sender Policy Framework)
Checks:
> "Was this email sent from an authorized mail server?"
##### DKIM (DomainKeys Identified Mail)
Checks:
> "Was this email modified after it was sent?"
> "Did the owner of the domain sign it?"

DKIM uses public-key (stored in DNS) cryptography.
Sender computes a hash of the email body and signs the hash with its private key.
Receiver gets the email. Looks up DKIM key for the domain from DNS. Then recalculates the hash and uses the DKIM key to verify the signature.
##### DMARC (Domain-based Message Authentication, Reporting and Conformance)
Checks:
> "What should I do if SPF and DKIM fail?"
> "Send reports back to the domain owner."

Domain is actually a policy, the owner of the domain published a DNS record in DNS server by which determine what has to happen if the authentication fails.


### Working with DNS

>DNS is provided by the DHCP server.

One of the best DNS problem solvers is a tool called `nslookup`.
We can use this tool to resolve domain names into Ips, by DNS servers.

We can choose a particular DNS server by this command:
```bash
server 8.8.8.8
```

and we can search for the ip of a specific domain name.
If the result is timeouts, then The DNS server is probably having some issues, or might having the wrong address.


### Routers
We can use the console port of a router to configure it.
![[CompTIA A+ (220-1101)-20260611135238823.webp]]

### Virtual LANs (VLANs)
A VLAN takes one physical switch and electronically turns it into two or more switches.
It literally seperates the local area network into two, three or more local area networks.

>In order to configure a switch, we need to give an ip address. This is what we called a **managed switch**.

>For example a managed switch can get its ip address via router's DHCP.
>So all you have to do is just typing its ip address and entering to the switch's web interface configuration.

This is an example of the Switch configuration:
![[CompTIA A+ (220-1101)-20260611213032059.webp]]

#### What is port security?
By enabling port security for some ports of the switch, we are actually telling the switch to memorize the mac addresses of the devices connected to those ports, and don't other devices with different mac addresses to be connected via those ports.

>No other computer can connect to via that port expect the one that switch has identified during enabling port security.

Example of enabling port security:
![[CompTIA A+ (220-1101)-20260612094914600.webp]]

#### Software-defined networking (SDN)
The traditional network devices needed to be manually configured and reconfigured for changes.
In order to fix this issue in industry SDN came up with the idea of separating the control plain from the data plane on the devices.
In this case we still have the switches that are programmable and have the data flowing through them, but we have a separate device or server that does all the controlling of the devices.

By SDN we have:
- Reduction of manual configuration
- Ease of access to central management of all of our network devices
- A very large and dynamic scalability to our network



![[CompTIA A+ (220-1101)-20260611214805813.webp]]

---
## Chapter 20: Wireless Networking
### Wireless Network Hardware
Wireless devices all are working with a standard called **IEEE 802.11**.

#### Wireless access point (WAP)
WAPs act as a bridge between the wireless network and an Ethernet network.

When working with wireless networks we are going to need wireless network card.
![[CompTIA A+ (220-1101)-20260618003946518.webp]]

All of our devices like laptops, tablet and phones have 802.11 network cards built-in to them.

SSID: service set identifier

#### Ad hoc mode in wireless networks
We don't have any wireless access points, we just have multiple NICs.
One NIC (for example a laptop) can say I want to setup a **wireless Ad hoc network**, then all the others will treate that system kind of like a wireless access point.

#### Antennas
There are 3 types of antennas:
1. **Omni-directional**: It's just like a piece of metal that sticks up..
   Omni directional's radiation pattern is like a big ball.
2. **Dipole**: It consists of two Omni-directional antennas that are pointing exactly opposite of each other.
   It propagates signals like a big flat circle. (something like a stomped donut)
   ![[CompTIA A+ (220-1101)-20260618012312732.webp]]
   
   ![[CompTIA A+ (220-1101)-20260618012414418.webp]]
3. **Patch**: The radiation signal is going to be like a half of a big fuzzy ball.
   ![[CompTIA A+ (220-1101)-20260618011853546.webp]]
4.  **Highly directional (Yagi)**: It's propagation signal is kind of straight forward. (like a  really stretched american football)
   ![[CompTIA A+ (220-1101)-20260618011119073.webp]]
   
   ![[CompTIA A+ (220-1101)-20260618011145683.webp]]

5. **Parabolic**:It's another alternative for very very long highly directional throws.
   ![[CompTIA A+ (220-1101)-20260618011404638.webp]]

### Wi-Fi Standards

We have many extensions of 802.11 standard.
802.11 works based on **Industrial, scientific and medical (ISM) radio bands**.
The 802.11 uses 2.4 GHz and 5 GHz band of the ISM bands.

>We are not using an exact frequency, but we are using a band, which is actually a range of radio frequencies.

##### 2.4 GHz band is : 2.412 - 2.4884 GHz

There are 14 pre-made channels in 802.11 standard.
Each channel takes a different piece of this band.
![[CompTIA A+ (220-1101)-20260618135726446.webp]]

These channels are used where we have multiples WAPs and devices to avoid stomping on each other.

##### 5GHz band: 5.150 - 5.875 GHz
In this band channels are a little more complicated.
The channel numbers don't span out normally. A lot of channel numbers are skipped.
There aren't any odd numbers.
![[CompTIA A+ (220-1101)-20260618140138280.webp]]

#### 802.11 extensions
![[CompTIA A+ (220-1101)-20260618141144421.webp]]

##### 802.11g
802.11g standard had the good things from the a and b extensions, it was also backward compatible with only 802.11b.

##### 802.11n
802.11n could run on both bands. It was backward compatible with any other wireless NIC out there like the a, b and g extensions.
802.11n also used something called **MIMO (mulitple in/ multiple out)**. It allows a single WAP to use multiple antennas to change it's radiation signal in such a way that it kind of zeros in on the device. (like zooming on one device)
##### 802.11ac (Wi-Fi 5)
It is fast.
It imporved the MIMO to something called **Multiuser MIMO (MU-MIMO)** where Instead of having just one client that we can zoom in at a time, it can zoom in on multiple clients at a time (depending to the number of radios it has in it).
802.11ac has got a 2.4GHz radio too, but it has nothing to do with it, it's used only for backward compatibility with older versions of Wi-Fi.

