### Chapter 1

Two kinds of programs:
1. **System programs**
2. **Application programs**

> OS is a layer of software on top of the bare hardware to manage all parts of the system, and present the user with an interface or **virtual machine**.

![[Introduction-20241029005718479.webp]]

---
## 1.1 WHAT IS AN OPERATING SYSTEM?

Operating system perform two basically unrelated functions:
1. Extending the machine 
2. Managing the resources

### 1.1.1 The Operating System as an Extended Machine
In this view, the function of the operating system is to present the user with
the equivalent of an **extended machine or virtual machine** that is easier to pro-
gram than the underlying hardware.

### 1.1.2 The Operating System as a Resource Manager
This view of the operating system holds that its primary task is to keep track of
who is using which resource, to grant resource requests, to account for usage, and to mediate conflicting requests from different programs and users.

>Resource management includes multiplexing (sharing) resources in two ways:
>1. Multiplexing **time**
>2. Multiplexing **space**
---
## 1.2 HISTORY OF OPERATING SYSTEMS
---
## 1.3 OPERATING SYSTEM CONCEPTS
The interface between the operating system and the user programs is defined
by the set of ‘‘**extended instructions**’’ that the operating system provides. These extended instructions have been traditionally known as **system calls**, although they can be implemented in several ways.

> The MINIX 3 system calls :
> 1. Those dealing with processes
> 2. Those dealing with the file system

