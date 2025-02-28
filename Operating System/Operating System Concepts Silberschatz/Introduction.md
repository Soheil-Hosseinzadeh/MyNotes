### Chapter 1

An operating system is software that manages a computer's hardware.
It also provides a basis for application programs and acts as an **intermediary** between the computer user and the computer hardware.

> A fundamental responsibility of an operating system is to allocate resources like CPU, memory, I/O devices, and storage to programs.

An operating system must be created piece by piece, each of these pieces should be a well-delineated portion of the system, with carefully defined inputs, outputs, and functions.

In this chapter we provide a general overview of the major components of a computer system as well as the functions provided by the operating system.

---
## 1.1 What operating systems Do

A computer system can be divided roughly into four components: 
1. **hardware**
2. **operating system**
3. **application programs**
4. **user**

> We can also view a computer system as consisting of **hardware**, **software**, and **data** .

> The operating system controls the hardware and coordinates it's use among the various application programs for the various users.

> An operating system provides an **environment** within which other programs can do useful work.

![[Introduction-20240928174709594.webp]]

### 1.1.1 User View

**Personal computers** : 
- Designed for one user
- The goal is to maximize the work that the user is performing
- The operating system in these systems is designed :
  1. for **ease of use**
  2. with some attention paid to **performance and security**
  3. with none attention paid to **resource utilization**

**Mobile computers** :
- Typically connected to networks through wireless technologies
- Consisting of a touch screen and etc .

**Computers with no user view** :
some computers have little or no user view 
- for example: **embedded computers**, **automobiles**
- These systems may have numeric keypads and may turn indicator lights on or off to show status
- These system's operating systems and applications are designed primarily to run without user intervention 


### 1.1.2 System View

The operating system is the most involved with the hardware.

###### Resource allocator
> We can view an operating system as a **resource allocator**.
> The operating system acts as the manager of these resources.

###### Control program
> An operating system controls the various I/O devices and user programs.
> The operating system is a **control program** that manages the execution of user programs, operations and control of I/O devices .

### 1.1.3 Defining Operating Systems

Computers are present everywhere like within toasters, cars, ships, spacecraft, homes, and businesses.

##### Moore's Law
In the 1960s, Moore's Law predicted that the number of transistors on an integrated circuit would double every 18 months, and that prediction has held true.

> Operating systems exist because the offer a reasonable way to solve the problem of creating a usable computing system.

> The **fundamental goal** of computer systems is to execute programs and to make solving user problems easier. Computer hardware is constructed toward this goal.

Application program were developed because working with bare hardware is hard.
These programs require some common operations like :
- **Controlling functions** like controlling the I/O devices
- **Resource allocating functions** and ...

So All these common functions are brought together into one piece of software called : **Operating System**

#### A more common definition
The operating system is the one program running at all times on the computer (usually called the **kernel**) .

##### Two types of programs
1. `system programs` :
   Associated with the OS, but are not necessarily part of the kernel
2. `application programs`:
   Include all programs not associated with the operation of the system

##### Middleware
A set of software frameworks that provide additional services to application developers.

> So, the OS includes 
> - The always running time **kernel**, 
> - **Middleware frameworks**(that ease application development)
> - **System programs**(that aid in managing the system while it is running)

---

## 1.2 Computer-System Organization