# Linux File System

[Linux file systems explained @ Ubuntu](https://help.ubuntu.com/community/LinuxFilesystemsExplained)

  - Journaling file systems prevent inconsistency and are faster at file system checks than non-journaled file systems.
  - Some journaling file systems can prevent corruption as well by writing the data twice.

[Linux file system hierarchy](http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/c23.html)

- Central concepts of a file system:
    - `superblock`: contains info about the file system as a whole such as size.
    - `inode`: contains info about a file, except its name; contains numbers of several data blocks.
    - `name`: stored in the directory together with the number of the inode.
    - `directory entry`: consists of a filename and the number of the inode.
    - `data blocks`: used to store data in the file.
    - `indirect blocks`: dynamically allocated blocks that contain additional data for an inode.

# Unix File System

*Source unknown*
```
Parts of a Unix directory tree. See the FSSTND standard (Filesystem standard)

/                     Root
|---root              The home directory for the root user
|---home              Contains the user's home directories
|    |----ftp         Users include many services as listed here
|    |----httpd
|    |----samba
|    |----user1
|    |----user2
|---bin               Commands needed during bootup that might be needed by normal users
|---sbin              Like bin but commands are not intended for normal users.  Commands run by LINUX.
|---proc              This filesystem is not on a disk.  Exists in the kernels imagination (virtual).  This directory
|    |                Holds information about kernel parameters and system configuration.
|    |----1           A directory with info about process number 1.  Each process
|                     has a directory below proc.  
|---usr               Contains all commands, libraries, man pages, games and static files for normal
|    |                operation.
|    |----bin         Almost all user commands.  some commands are in /bin or /usr/local/bin.
|    |----sbin        System admin commands not needed on the root filesystem.  e.g., most server
|    |                programs.
|    |----include     Header files for the C programming language.  Should be below /user/lib for
|    |                consistency.
|    |----lib         Unchanging data files for programs and subsystems
|    |----local       The place for locally installed software and other files.
|    |----man         Manual pages
|    |----info        Info documents
|    |----doc         Documentation for various packages
|    |----tmp
|    |----X11R6       The X windows system files.  There is a directory similar to usr below this
|    |                directory.
|    |----X386        Like X11R6 but for X11 release 5
|---boot              Files used by the bootstrap loader, LILO.  Kernel images are often kept here.
|---lib               Shared libraries needed by the programs on the root filesystem
|    |----modules     Loadable kernel modules, especially those needed to boot the system after
|                     disasters.
|---dev               Device files for devices such as disk drives, serial ports, etc.
|---etc               Configuration files specific to the machine.
|    |----skel        When a home directory is created it is initialized with files from this directory
|    |----sysconfig   Files that configure the linux system for networking, keyboard, time, and more.
|---var               Contains files that change for mail, news, printers log files, man pages, temp files
|    |----file
|    |----lib         Files that change while the system is running normally
|    |----local       Variable data for programs installed in /usr/local.
|    |----lock        Lock files.  Used by a program to indicate it is using a particular device or file
|    |----log         Log files from programs such as login and syslog which logs all logins,
|    |                logouts, and other system messages.
|    |----run         Files that contain information about the system that is valid until the system is
|    |                next booted
|    |----spool       Directories for mail, printer spools, news and other spooled work.
|    |----tmp         Temporary files that are large or need to exist for longer than they should in
|    |            /tmp.
|    |----catman      A cache for man pages that are formatted on demand
|---mnt               Mount points for temporary mounts by the system administrator.
|---tmp               Temporary files.  Programs running after bootup should use /var/tmp.
```


