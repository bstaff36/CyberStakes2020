
# Boot Riddle

## Challenge
* Category: Forensics
* Points: 100

This floppy disk image boots, but instead of a flag we see some silly riddle...

### Hints
* If only we could inspect the device's memory while it is running...
* QEMU's monitor or Bochs' debugger might be useful to read up on.


## Solution

untar your file `$ tar xzvf files.tar.gz`

Attach the floppy to a VM. Just like we did in bootcamp.

The screen now outputs a message:
![message](boot.png)

It is telling us a memory address for the flag.

So lets dump the memory of the VM. But first lets get the name of the VM

```
$ VBoxManage list vms  
"test-ubuntu_desktop" {6f6d43ac-b1da-4010-afe2-9d1f305c9912}
```
Ok. Now lets get the memory of that VM
```
$ VBoxManage debugvm "test-ubuntu1804_desktop" dumpvmcore --filename=out.elf
```

At this point, you could probably load the memory into a Ghidra or gdb and look at **0x7DC0**

But I found it quicker to open it up in a hex editor and quickly found the flag.

**ACI{REALmode} **
