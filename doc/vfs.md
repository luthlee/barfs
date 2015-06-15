File System and Virtual File System
=============================

The concept of file system and virtual file system is explained quite well in this [link][1] (see also [IBM][2]). 
**File system** organizes files into logical hierarchical structures with directories, soft links and so on which are held in blocks on physical devices. While we access the files through the file system tree, it is rather the task of the block device (i.e., devices that contain file systems) driver to locate the block that corresponds to the requested file on the device. 
**Virtual file system (VFS)** is an abstract layer that separates the real file systems from the operating system and system services. It specifies an interface (or a "contract") between the kernel and a concrete file system. The latter (often built as a loadable kernel module) will present a common interface to VFS, so that all details of each Linux file system appear identical to the rest of the Linux kernel. As a result, VFS allows you to transparently mount many different file systems at the same time. See following figure, Individual file systems can be ext2, ext3, etc.
![Linux file system architecture](http://www.ibm.com/developerworks/library/l-linux-filesystem/figure1.gif)
**Filesystem in Userspace (FUSE)** makes it easy to build customized file system without involving kernel programming. It also allows the file system to run the userspace. The components of FUSE is explained in [here][3] and depicted in the following figure. In short, it contains three components: i) *fuse.ko* kernel module that hooks into VFS as well as device */dev/fuse* (above FUSE in between kernel and userspace); ii) a library *libfuse* that manages communications with the kernel module; iii) a *user-supplied* component that actaully implements the filesystem (operations on the file).
![FUSE structure](http://fuse.sourceforge.net/doxygen/490px-FUSE_structure.svg.png)

Tutorial of Writing a FUSE Filesystem
==============================

[Here][4] is a good tutorial of how to write a customized FUSE and understand the fuse library. Our requirement of **barfs (Burn-After-Reading File System)** mainly concerns the *close* operation of the file. Meanwhile we also need to solve the other logical conflicts and dependencies.

[1]: http://www.science.unitn.it/~fiorella/guidelinux/tlk/node94.html "The File system"
[2]: http://www.ibm.com/developerworks/library/l-linux-filesystem/ "IBM Anatomy of the Linux file system"
[3]: http://lwn.net/Articles/68104/ "FUSE implementation"
[4]: http://www.cs.nmsu.edu/~pfeiffer/fuse-tutorial/ "Writing a FUSE Filesystem: a Tutorial"
