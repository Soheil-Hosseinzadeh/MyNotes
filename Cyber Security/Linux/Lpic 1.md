This tutorial has been provided with respect to ITProTV course.

## Detecting hardware
We can see a list of pci components by `lspci` command.

We can also see a list of removable devices by `lsusb` command.

>When a piece of hardware is detected it the system gives it a name to interact with it, if the name doesn't show up it means the hardware is detected but the driver is missing.

We can see those names in `/dev` directory.
There are nicknames of devices that the system have given.

The names are defined by a service called `udev`, it's a service that runs in the background.
When the system boots up `udev` identifies the hardware and gives it a name. These names are represented as a file in `/dev` directory.

>In order to override the names we can go to `/etc/udev`.
>The main configuration of `udev` is in `udev.conf` file.
>We can find additional rules about how hardwares to be named in `rules.d` directory.

```bash
┌[friend@fedora]-(/etc/udev)
└$ ls   
hwdb.bin  hwdb.d  rules.d
```

#### kernel modules (hardware drivers)
>Hardware drivers take place somewhere called `kernel modules`.
>The kernel itself isn't very big, but it needs tons of drivers to make all the hardwares work, these drivers are modules that are loaded into the ram to make the hardware function.

We can list the drivers modules by `lsmod` command.
We can search if there is any driver module for some hardware like this: `lsmod | grep nvidia`.

We can remove a kernel module by `rmmod` command.
We actually disable a hardware by removing a module, the hardware is still there and linux can see it, but it just no longer functions.

>Anything done here is temporary. In order to make it permanent we have to make a black list in modprobe.d.
##### What is modprobe?
modprobe is the kernel module probe, it's actually the detector, anytime it sees a new hardware it looks for the appropriate module that goes along with it.

## Linux as a VM

> you can install `open-vm-tools` in vm machines to make them act better in the virtualization that you are using.

```bash
sudo dnf install open-vm-tools
sudo systemctl enable --now open-vm-tools
```

## Linux as a boot process
What happens when we power on the system?

#### Boot process
When you push the power button:
- The mother board gets power and turns on.
- The **CPU** starts executing firmware stored in the motherboard's **BIOS** (or **UEFI**) chip.
- The BIOS (Basic input output system) controls the system at that stage, it initializes things like RAM and CPU and make them up and ready.
**If the system uses Legacy BIOS:**
- The BIOS reads the **first sector of the boot disk** (the **Master Boot Record (MBR)**).
- The MBR contains:
    - a small bootloader
    - the partition table
- The bootloader in the MBR loads the rest of the bootloader (for example, **GRUB 2**).
**If the system uses UEFI:**
- The firmware reads the **EFI System Partition (ESP)**.
- It loads an EFI bootloader executable (such as **GRUB 2**, **systemd-boot**, or another EFI boot manager) from that partition.
- Then the boot loader is launched. The boot loader in most Linux systems is grub version2.
	Grub then locates the actual OS and initializes it. It loads the Linux Kernel and **initramfs** into RAM.
	The kernel begins executing. But there is some problem, The kernel might not yet have the necessary drivers or userspace tools to access the whole operating system from the SSD.
- That's where **initramfs** is used. Instead of booting directly into the real operating system, Linux first boots into a **small temporary filesystem**. That temporary filesystem lives entirely in RAM and is called initial RAM Filesystem. It is a small compressed archive that GRUB loads into memory along with the kernel. Then initramfs will be kernel's temporary root file system.
	It usually contains:
	- storage drivers
	- kernel modules
	- `/init`
	- LVM tools
	- RAID tools
	- encryption tools
	- filesystem drivers
	Kernel then runs the **`/init`** program. This program does tasks like loading kernel modules, detecting storage devices, unlocking encrypted disks, and etc, and at the end it locates the real root filesystem and mounts it as the kernel root filesystem.
- Loading systemd
	After getting to the real root file system, the kernel loads systemd.
	**systemd** is a service which is responsible for running all of the background services that make linux function.
	For example a nice GUI comes up, network adapter launching, sound daemons launching and etc, Systemd controls all of these.
	>Systemd is technically the first program that runs on your computer.
	>It's actually a kind of initialization program.
	>There isn't only systemd, prior to systemd we have had something called **system V init**.

![[Lpic 1-20260627163456256.webp]]

>The Grub has too many configurations options.
>We can see the grub configuration in it's configuration file : `/boot/grub2/grub.cfg`.
>There are instructions in that about how to boot the operating system and what to do.
>Grub is not only the matter of finding the operating system but it also let us to choose which kernel to boot from.

##### What is initrd?
Initrd is a ram disk.

## Configuring GRUB

What does it contain: The location of the OS in the hard drive.
The configuration file of the grub is : `/etc/default/grub`. In this ile we can change the grub configurations then do the following to update the grub.

>The grub itself is stored in `/boot` but it's read-only. 
>There are some script packages to handle the grub update.

In red hat we have:
```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

In Ubuntu we have:
```bash
sudo update-grub2
```

We can see other config files about the grub in `/etc/grub.d`, the `40_custom` file here is used to add extra operating system entries in grub.

## The Linux Shell

Terminal and Shell
>Terminal is the UI and the Shell is the actually command prompt where we type in there commands.

## Managing Processes
We can use the `ps` command to see the processes.
By deault the command shows the processes that has been created in this instance.

To see all the processes with the username across the entire system we can use `-aux` modifier.
```bash
ps -aux
```

We can use `pgrep` in order to search through the processes by the name.
```bash
pgrep bash # searching for the bash process
```

Another example: (using pipeline with grep command)
```bash
ps -aux | grep zsh
```

We can also use the `top` command to see the processes in a live mode (gets updated every few seconds)
```bash
top
```
We can see the processes in order of cpu usage.
We can specifiy the order by typing `P` for CPU and `M` for memory usage based order.

We can kill a process by typing `k` and the PID of the process.

There is also another command `free` to see the memory usage.

##### Putting jobs to back ground
In terminal you can put whatever you are doing in the background as suspended by typing `ctrl + z`.
It gets a number.
We can view the background jobs by `jobs` command.
Later on we can bring on the back ground job by typing `%[job number]`.

We can also use `bg %[job number]` and `fg %[job number]` to run a suspended job in background or in forground.

We can also use `&` sign at the end of a command to put a job in the background and be sure that it is still running.
## Execution Priorities
We can use `nice` command to set priorities for the programs that we run..
For example we can have:
```bash
sudo nice -12 sha256sum /dev/sda5
```
Usually the default value of nice is 10.
The nice value is from -20 to 19 and negative values are considered as higher priorities.

We can also change the nice value of a running program by the following:
```bash
sudo renice [nice-value] [PID] -u [user]
```


We can kill a process that is taking all the resource by this:
```bash
kill [PID]
```
There is more than one way to kill a process, you can view all the different signalls by `kill -l` command.
The most famous ones are `SIGHUP` or reseting the process, `SIGKILL` for terminating the process, `SIGTERM` for asking the program to terminate it itself.

For example inorder to kill a process:
```bash
kill -KILL [PID] #or kill -9 [PID]
```
-9 is the number of the kill signal.

You can use the `killall` command to kill all the process related to the provided program name like this:
```bash
killall chrome
```

## Editing files with nano
The `^` means `ctrl` button and the `M` means `alt` button.

>In order to marking a text in nano we should type `alt + a` or `ctrl + 6`.
>In order to copy in nano we should type `alt + shift + 6`.

#### searching and replacing
In fedora we can press `ctrl + f` to search and `alt + f` to see the next results of the search.

We can also press `al + r` or `ctrl + \` to do search and replacement.


## Editing files with Vi

Vi has 3 modes of operations.
1. visual mode: In this mode you can only view a document
2. insert mode: You can type, get enabled by pressing `i`.
3. command mode: You can issue some commands, get enabled by pressing `:`.

> We can enable numbering in vi by typing this command in command mode: `set number`.

>When we type some new text, we can `esc` then type `ZZ` in order to save the writes and quit. It's like the `:wq` command in command mode.

##### Searching and replacing
We can search in vi by typing `/`. It is case sensitive.

We can also do the search before opening a file like this:
```bash
vi +/<search_string> <file_name>
```

When we do a search in vi, we can type `n` to go to the next matching or we can type `N` to go to the previous matching line.

We can use to forward slashed like this: `:s/<search_string>/<replace_string>` to do a search and replace.

>We can do the search and replace in lines from 1 to 1000 and places by this: `:1,1000s/<search_string>/<replace_string>`.

>We can type this command to reload the file from the filesystem and discard the changes: `:e!`.

>We can do the search and replace in the whole lines in every part of the line by this:
>`:%s/<search_string>/<replace_string>/g`, we can also add `c` to the end of g to enable the confirmation asking for each replacing.

>If you want to copy something to the clipboard in a wayland desktop, you should do this: At first select the text by `v` then type `:w !wl-copy`.

## Customizing Bash
We can have customized commands by `alias`, aliases are like shortcuts and get defined like this:
```bash
alias la='ls -A'
```

We can also define functions in bash that do some commands for us like this:
```bash
# for example in .bashrc we can type:
myfunc() {curl "https://cheat.sh/$1";}
```

>The `$1` means what ever we type after the `myfunc()` function.

## Managing Files
For vieweing the contents of a file we can use `less`. `less` provide us the `:` vim like interface too, for searching and other stuff.

Inorder to see the first parts or last parts of a file we do:
`head -n N <file_name>` to see the first N lines.
`tail -n N <file_name>` to see the last N lines.

We can use `-f` flag to follow the files with `tail` in order to see what ever else that gets added to the file.

## Redirecting Data with Pipes
Some commands like `mkdir` doesn't support getting input from pipes, for these cases we need to use `xargs` to give them their standard desired style inputs like this:
```bash
cat folder_names.txt | xargs mkdir
```

## Redirecting Data with Redirects
With redirects we take the output of one command and write it to some desination which can be a file or a device (however everything is a file in linux).

```bash
ls -lh > lists.txt
```

>By using `>>` we can append to the file instead of overwriting it.

We can throw away the outputs of a command by redirecting it to `/dev/null` :
```bash
ls -lh > /dev/null
```

>We can use numbers before redirects:
>`1>` means to redirect the successes.
>`2>` means to redirect the errors.

```bash
find / -name *.doc 2> /dev/null
```


We can also use `tee` command to see the output in the terminal and also have it saved in a file:
```bash
find / -name *.doc 2> /dev/null | tee list.txt
```

We can also redirect the needed input of a command from a file to the command like this:
```bash
ls -lh > text.txt
sort < text.txt # however this can be done by "sort text.txt" itself, but it was just an example
```

## Filtering Output with Cut

#### Sort
We can use sort command to sort the output of commands.
```bash
ls /bin | sort -r
```

Inorder to make sort work properly we need to specify the column and delimiter.
In order to have the right unique delemiter in the output of command we have to use `tr` (translate) command.

Take a look at this example:
```bash
ls -lh

#result     
total 8.0K
-rw-r--r--. 1 friend friend 23 Oct  1 13:30 folder_names.txt
drwxr-xr-x. 1 friend friend  0 Oct  1 13:41 great
-rw-r--r--. 1 friend friend 47 Oct  1 14:15 myfile
drwxr-xr-x. 1 friend friend  0 Oct  1 13:41 Soheil
drwxr-xr-x. 1 friend friend  0 Oct  1 13:41 stuff
drwxr-xr-x. 1 friend friend  0 Oct  1 13:41 wow
```

We want to sort the output by the names in reverse order.
For that we first need to squeeze the delimiters of multiple spaces all to one space, then we need to specify the delimiter and the column we want to sort with respect to in sort command:
```bash
ls -lh | tr -s " " | sort -t " " -r -k 9

#result
drwxr-xr-x. 1 friend friend 0 Oct 1 13:41 wow
drwxr-xr-x. 1 friend friend 0 Oct 1 13:41 stuff
drwxr-xr-x. 1 friend friend 0 Oct 1 13:41 Soheil
-rw-r--r--. 1 friend friend 47 Oct 1 14:15 myfile
drwxr-xr-x. 1 friend friend 0 Oct 1 13:41 great
-rw-r--r--. 1 friend friend 23 Oct 1 13:30 folder_names.txt
total 8.0K
```

#### Cut
With cut command we can choose the parts that we want from an output.
Let's continue the previous example:
```bash
ls -lh | tr -s " " | sort -t " " -r -k 9 | cut -d " " -f 8,9

#result
13:41 wow
13:41 stuff
13:41 Soheil
14:15 myfile
13:41 great
13:30 folder_names.txt
```

## Filtering Output With Grep
We can use grep with regular expresions like this:
```bash
ls | grep -E "Documents|Desktop"
```

In regex the `^` shows the first of a line and `$` the end of a line.

## Working With Checksums
We can run `ls /usr/bin/*sum` too see what kind of sums our linux os does have.

```bash
sha256sum <file_name>
```

`md5sum` is considered compromised and is not safe. `Sha1` is also considered as compromised as well.
>We have to use something stronger like `sha256` or `sha128` that aren't compromised yet and also have the needed speed and efficiency.

If we have a checksum file, we have verfiy the checksum file in the directory where the files are available like this:
```bash
sha256sum --check checksum.txt
```


## Locating Commands With Which

#### type
We can use the `type` command to see what is the command we are running, a function or a binary executable file in somewhere or etc. (We can figure out the origin of the command)
```bash
type uname
```

#### locate
It is the fastest way to find a file across your hard drive.
```bash
locate <file_name>
```

>Locate maintains a database of all the files across the hard drive.
>Inorder to build that database at first time time that we install `locate` we should do: `sudo updatedb`.

If we add some new file, it is possible that the locate database does get updated until some other time, so in order to see the latest result we need to update the database our self.

#### whereis
This command search your `$PATH` for the provided file name.
```bash
whereis vim  
vim: /usr/bin/vim /usr/share/vim /usr/share/man/man1/vim.1.**gz**
```

`-b`: looking for binary files.
`-m`: looking for man files.
`-s`: looking for source codes.

#### which
The which command is similar to whereis but it is going to show the first result from the PATH that is probably the one that gets run when we type the relative command.
```bash
which uname
/usr/bin/uname
```

We can use `-a` flag to see all the results too.

