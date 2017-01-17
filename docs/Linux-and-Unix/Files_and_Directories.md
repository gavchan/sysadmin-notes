
- 3 types of access permission/privileges: read(r), write(w), execute(x) - these are set for the 3 user types: user(u), group(g) and others(o) to give 9 permission types.
- Execute permission should be set for executable files only (binary / shell scripts).
- Access privileges are stored in a file's inode.

# Using Binary and Octal values
- One bit (1:permission granted, 0:permission not granted) is used to set permissions, and a total of 3 bits are needed to indicate file permissions.
- Octal numbers represent these eight 3-bit access values from 0-7.

```
d r w x octal meaning
  0 0 0 0     no permissions
  0 0 1 1     execute permission
  0 1 0 2     write permission
  0 1 1 3     write and execute permission
  1 0 0 4     read permission
  1 0 1 5     read and execute permission
  1 1 0 6     read and write permission
  1 1 1 7     read, write and execute permission
```

# Changing File Access Privileges
```
chmod [options] octal-mode file-list
chmod [options] symbolic-mode file-list
  -R  recursively descend through directories/setting permissions for all within
  -f  force specified access permissions; no error messages if owner

chmod ugo filename (uog is the octal representation for permissions)
chmod 777 filename: rwx permission for user, group and others
chmod 700 filename: rwx permission for user, no permissions for group/others
chmod 755 filename: rwx permission for user, rx permissions for group/others
```

# Symbolic mode:

Who
```
  u: user
  g: group
  o: other
  a: all
  ugo: all
```
Operator
```
  +: add privilege
  -: remove privilege
  =: set privilege
```
Privilege
```
  r: read bit
  w: write bit
  x: execute/search bit
  u: user's current privileges
  g: group's current privileges
  o: other's current privileges
  l: locking privilige bit
  s: sets user or group ID mode bit
  t: sticky bit
```

- Single octal digit using chmod: specifies "others"; user and groups set to 0
- Two octal digits using chmod: specifies "others and groups"; user set to 0

# Access Permissions for Directories

- Read permission: reading contents
- Write permission: allows creation or removing entries from the directory
- Execute permission: permits search but not read/write
- Note that read and write permissions on directories are not meaningful without the search permission, therefore you ust have both the read and execute permissions on a directory to be able to list its contents, similarly with both write and execute permissions.

Default File Access Privileges
- When a new file/directory is created, it sets privilges based on current mask value.
- Default in UNIX is 777 for executable files and directories, 666 for text files.
- System uses Boolean logic to determine permissions.

```
umask [-S] [mask]
  # Execution without argument displays current value of bit mask in octal
  # Bit mask identifies the permission bits that are to be turned off when a new file is being created.
  # Rightmost nine-bits (3 octal digits) are for user, group and others.
  # Leftmost three-bits (1 octal digit) is for special access bit
  -S  displays symbolic value of the mask
```

- `umask` command could be placed in the system startup file `~/.profile` in System V Unix and the `~/.login` or `~/.cshrc` file in BSD
- Authors prefer a mask value of 077 so that new files are always created with full protection in place - files have full access permissions for owner and no permissions for anyone else.
- Mask value of 027 gives default privileges to group members and no permissions to others.

# Special Access Bits

## Set-User-ID (SUID) Bit

- When a command runs, it executes with the effective user ID of the user running the command.
- UNIX allows commands such as `passwd` to change their effective user ID and become privileged in some way so that they can change special files such as `/etc/passwd` without compromising the integrity of the system.
- Every UNIX file has a protection bit called the **SUID bit** associated with it. If this bit is set for a file containing an executable program, the program takes on the privileges of the owner of the file when it executes. *i.e. if file owned by root has its SUID bit set, it runs with superuser privileges* - this occurs with the `passwd` command.
- Other commands with SUID bit set include: `lp, mail, mkdir, mv, ps`
- SUID bit is enabled if the execute bit for the owner is **s** or **S**.
- If both SUID and execute bits are enabled the bit is displayed as **s**.
- If SUID bit is enabled but the execute bit is disabled, the bit is displayed as **S**.

```
chmod 4xxx file-list
chmod u+s file-list
```

- *SUID bit can compromise security of the system if not implemented correctly:* if the permissions of any set-UID program are set to allow write privileges to others, you can change the program in this file or overwrite the existing program with another program.

## Set-Group-ID (SGID) Bit

- Not as dangerous as the SUID bit feautre, because most privileged operations require superuser identity, regardless of current group ID.

```
chmod g+s file-list
chmod ug+s file-list  # sets SUID and SGID using a single chmod command
```

## Sticky Bit
- Can be set for a directory to ensure that an unprivileged user cannot remove or rename files of other users in that directory.
- Must be owner of a directory or have appropriate permissions to set the sticky bit for it.
- Commonly set for shared directories that contain files owned by several users.
- Useful for programs such as compilers, assemblers, editors and commands such as `ls` and `cat`, but care must be taken that not too many programs have this bit set, otherwise system performance will suffer.

```
chmod 1xxx file-list
chmod +t file-list
```

