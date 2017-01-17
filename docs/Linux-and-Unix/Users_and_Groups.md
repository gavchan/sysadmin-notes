Source: [Oracle Solaris 11.3 Information Library](https://docs.oracle.com/cd/E53394_01/)

# User Accounts

```
useradd -m username
useradd -m username	# simple way to create a new user with username
useradd -c "Common name" -d [home directory, e.g. /export/home/username] -m username
useradd -c "User1" -d -m -u:101 -g:staff User1
```
N.B. Very important to use -m for make, otherwise directory will not be created
```
usermod -c
usermod -u [userid]
usermod -d
```
To delete a user:
```
userdel username
```
Note that user folder must be unmounted before it could be deleted
```
umount dirname 
```

# Password information
```
passwd username
```
- In `/etc/shadow` file stores passwords when using /etc files
- In `/etc/passwd` file when using NIS
- In `people` container when using LDAP
- Default password requirements stored in `/etc/default/passwd` file

# Special UIDs
- UID 0-99: reserved for Oracle Solaris system
- UID 0: root
- UID 1: daemon
- UID 2: bin pseudouser
- UID 60001 and 65534: reserved for nobody and nobody4 (NFS Anonymous users)
- UID 60002: noaccess

## Standard Users

- Interactive in the sense that user can log into the system locally or remotely.
- Will have a home directory associated with it, can be located either on local system or remote file server.

## System Accounts

- Associated with an application process that is installed and running on the system.

  - An application process that listens on a network port for service requests is referred to as a **daemon**.

- These running processes need a way to operate on the system just as standard users do.
- System account usually does not require a home directory.
- Provides a basic level of security to the system by protecting it in the event that the service that the service associated  with the account is violated.

## Root Account

- Called "super user" in previous Solaris releases - owner of most binaries and configuration files.
- Root account in Oracle Solaris 11 is generally configured as an RBAC role.

  - This means it cannot be logged in directly and users must be explicitly granted to access to the account.
  - When you're authenticating to a role, the password must be that of the role.

# UNIX Groups
- Each group has a name, group ID (GID), and a list of usernames that belong to the group.
- Two types of groups:
    - **Primary group:** group that OS assigns files that are created by the user.
    - **Secondary group:** other groups a user belongs to, maximum 1024 supplemental groups.

To display the list of groups for the user:
```
groups username
```
List groups
```
getent group
```
List users in a group
```
getent group groupname
```

Adding and modifying groups
```
groupadd -U user1[,user2]
groupmod
groupdel

useradd -g group-primary
useradd -G group-secondary
getent group
usermod -g group-primary username
usermod -G +group1,group2... username
usermod -G -group2,group3... username
usermod -G "" username    # removes all secondary groups
```

## NSD 2017 Links
- [Setting up user accounts @ Oracle](http://docs.oracle.com/cd/E23824_01/html/821-1451/gkhqx.html)
- [Creating Users 1 Video](https://www.youtube.com/watch?v=n_7uUnTodSY)
- [Creating Users 2 Video](https://www.youtube.com/watch?v=dj_V5XDdYcU)
- [Creating Users 3 Video](https://www.youtube.com/watch?v=bQF1SavzgL8)
- [Finding account information](https://www.youtube.com/watch?v=QBpLUfWOYLs)
- [Changing account policies](https://www.youtube.com/watch?v=EZ4BmS1VM7w)



