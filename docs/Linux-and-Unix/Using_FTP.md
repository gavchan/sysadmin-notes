# File Transfer Protocol (FTP)

- An old file transfer protocol for exchanging files over a TCP/IP network since the 1970's.
- Base specification is [RFC 959](http://www.ncftp.com/ncftp/rfc959.html), 1985.
- Designed to allow clients to browse the file system, and FTP is a stateful sequence of one or more transactions.
- Client is always responsible for initiating requests.
- Authentication by username/password; de facto standard for guest access using "anonymous" for username and an "email address" for the password.
- Supports **ASCII** for text and "image" for binary data.
- *Base specification does not have any special handling for encrypted communications, so files containing sensitive material should not be sent.*
- **Usernames and passwords are sent in clear text** and the entire FTP transmission could be monitored by potential attackers.

*Source:* http://www.ncftp.com/libncftp/doc/ftp_overview.html

- Should instead use something like `scp` for same security as `ssh`.

# FTP service on Solaris
```
svcs ftp                # Check status of ftp service (default: disabled)
svcadm enable ftp       # Enables FTP
svcs -xv svc:/network/ftp:default       # Run for troubleshooting

ftp
ftp -i                  # Opens FTP and turns off interactive mode so mget/mput
                        # will not ask for confirmation.
```
# Basic FTP commands
```
ftp> open 192.168.40.153
ftp> put filename.txt
ftp> mput *.*
```
## Local
```
ftp> lcd            # Lists local directory, or changes local directory
ftp> !ls            # Lists files in local directory - doesn't work with default Windows cmd.exe FTP
ftp> !dir           # Lists files in local directory - works with Windows cmd.exe FTP
```
## Remote
```
ftp> get            # Retrieves files
ftp> put            # Sends one file
ftp> mput           # Sends multiple files
```
## Transferring directories
- FTP will not automatically create and transfer directories.
- A Bash script could be created to recursively transfer directories with their contents through FTP.

```
if [[ "$1" = "help" ]]; then
  echo "Run with ftpcdir.sh <directory> <host address> <username> <password>"
  exit
fi
find $1 -type d > dirs.txt
find $1 > files.txt
echo open $2 > command.ftp
echo $3 >> command.ftp
echo $4 >> command.ftp
for i in `cat dirs.txt`
do
  if [[ "$i" != '.' ]]; then
    echo mkdir $i >> command.ftp
  fi
done
for i in `cat files.txt`
do
  if [[ "$i" != '.' ]]; then
    echo put $i $i >> command.ftp
  fi
done
echo quit >> command.ftp
ftp -s:command.ftp                  # Only works with Windows Cmd FTP
exit
```
# Changing the FTP Connection message
- Could be done by editing the `/etc/proftpd.conf` file.
- Any change of the file requires restarting the ftp service: `svcadm restart ftp` for changes to take effect.
