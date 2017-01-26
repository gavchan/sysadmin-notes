Solaris 11.3 Cheatsheet
=======================

# Useradd
- Administrator requires **User Management Profile**
```
useradd -m username
useradd -m [options] username

    -A authorization [,authorization]       # Assigns authorizations to the user
    -P profile [,profile]                   # Assigns profiles to the user
    -R role [,role]                         # Assigns roles to the user

    -c comment
    -d directory                            # Specifies home directory path for the new user.
    -g group                                # Assigns primary group (GID or name-string)
    -G group [,group]                       # Assigns secondary/supplementary group(s)
    -s shell                                # Assigns shell
    -e expire
```
- User information located in `/etc/passwd`, can be listed with `getent passwd`

# Usermod
- Administrator requires **User Security** profile to modify security attributes.
- Requires **User Management** profile to modify the non-security attributes.
```
usermod -A [+|-]authorization username      # If no prefix, overwrites authorization; +|- add/removes
```

# Userdel
- Requires **User Management** profile to delete user's login
```
userdel -r username                         # Removes user's home directory from the file system.
userdel [options] username                  # Removes user but home directory remains.
```

# Getent
```
getent passwd
getent passwd username
getent group
getent group groupname
getent user_attr                            # Displays auths and profile info for all users
getent user_attr username                   # Displays auths and profiles for username
getent prof_attr                            # Displays profiles
getent auth_attr                            # Displays authorizations
getent exec_attr                            # Displays executable rights

```

# Groupadd
- Administrator requires **User Management Profile**
```
groupadd groupname                          # Creates new group "groupname"
groupadd -U user1[,user2] new_groupname     # Creates new group and adds users to it

    -g gid                                  # Assigns the group id gid for the new group

```
# RBAC
- Roles must be created and assigned to the user before the user can assume the role via `su`

```
roleadd -P "User Management" rolename        # Creates a role named rolename with profile "User Management"

    -c comment
    -e expire
    -f inactive
    -g group                                # Primary group
    -G group[,group...]                     # Secondary group
    -u UID
    -A authorization [,authorization]
    -K key=value

rolemod -K roleauth=user usermx1            # Role authentication uses user password
rolemod -K roleauth=role usermx1            # Role authentication uses role password
passwd usermx1                              # Create password for the role

useradd -R usermx1 user1                    # Assigns usermx1 to a new user user1
usermod -R usermx1 user2                    # Modifies user2 to assign it a role

roledel -r rolename                         # Deletes the role and removes the role's home directory
```

# Solaris Services

```
svcs                                        # List services: report service status
svcs -a                                     # List all services, includes extra disabled services

svcs *dhcp*                                 # Searches for service with "dhcp"
svcs -v servicename                         # Lists verbose information
svcs -l servicename                         # Lists detailed information about instances of system/service3
svcs -p servicename                         # Lists processes

svccfg                                      # Import, export and modify service configurations.

svcadm                                      # Manipulate service instances
svcadm disable telnet
svcadm enable ssh
```
# Networking

```
ifconfig -a
ifconfig net0
ifconfig net0 up
ifconfig net0 down

ping
traceroute url


netcfg                                      # Create and modify network configuration profiles
netcfg> list                                # Lists objects
netcfg> list ncp Automatic                  # Lists the details for the NCP Automatic



