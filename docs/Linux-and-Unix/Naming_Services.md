[Oracle: What is a Naming Service?](https://docs.oracle.com/cd/E23824_01/html/821-1455/a00intro-21293.html#scrolltoc)

- Performs lookups of stored information, including usernames, passwords, access permissions, group membership etc.
- Can be stored locally or in a central network-based repository/database.
- Fundamental to computing networks, provides following functionality:

    - Associates (binds names with objects)
    - Resolves names to objects
    - Removes bindings
    - Lists names
    - Renames information

- Network information service enables systems to be identified by common names instead of numerical addresses.
- `/etc/inet/hosts` stores network address of every system in the network, including itself.
- **Client-server computing**: A network information service stores network information on a server, which can be queried by any system (clients).
- Naming allows for a more flexible identification of divisions/subnets that could be spread across different physical networks.

## Oracle Solaris Naming Services

- Domain Name System (DNS)
- `/etc` files: the original UNIX naming system
- Network Information Service (NIS)
- Lightweight Directory Access Protocol (LDAP)

- When managing user accounts for a large site, consider using a name or directory service such as LDAP or NIS - these allow user account information to be stored in a centralized manner instead of in every system's `/etc` files. 

## DNS
- The *DNS* is a hierarchical, distributed database, implemented on a TCP/IP network and is primarily used to look up IP addresses for Internet host names and host names for IP addresses.
- DNS clients request information about a host name from name server(s) and wait for a response. DNS servers respond to requests from a information cache.
- DNS makes communication simpler by using machine names instead of numerical IP addresses.

## NIS
- Developed independently of DNS.
- Focuses on making network administration more manageable by providing centralized control over a variety of network information.
- Stores information about network, machine names and addresses, users, network services.
- Collection of information known as **NIS namespace**.
- Stored in **NIS maps**, designed to replace `/etc/` files.

#### LDAP
- [LDAP @ Wikipedia](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol)
- Open, vendor-neutral, industry standard application protocol for accessing and maintaining distributed directory information services over an IP network.
- Commonly used to provide a central place to store usernames and passwords. Allows different applications and services to connect to the LDAP server to validate users.
