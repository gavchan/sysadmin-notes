**Links**
- [Oracle Linux Tips and Tricks: Using SSH](https://blogs.oracle.com/linux/entry/oracle_linux_tips_and_tricks)

# Secure Shell (SSH) and Secure Copy (SCP)
- Developed in 1995, provided security through encryption.
- Unlike `telnet` and `ftp`, user credentials and file contents are encrypted.
- Also used by **Secure Copy** (`scp`)

# Oracle Solaris SSH
- [OpenSSH in Solaris 11.3](https://blogs.oracle.com/darren/entry/openssh_in_solaris_11_3)
    - For Solaris 11.3 both OpenSSH and SunSSH are both supplied.
    - SunSSH: `pkg:/network/ssh`
    - OpenSSH: `pkg:/network/openssh`
    - Both packages deliver the same `svc:/network/ssh:default`

# Configuring SSH
- SSH configuration stored in `/etc/ssh/sshd_conf` file.
- Ensure `StrictModes yes` for secure permissions on users .ssh directory.
# Using SSH on Oracle Solaris
- SSH is automatically installed and enabled by default with root access disabled.
- Can check with `svcs ssh` and/or `ps -ef|grep ssh`
- Can enable/disable with:
```
svcadm disable ssh
svcadm enable ssh
```
# Using SCP
- Syntax:
```
scp /localpath/localfilename remoteuser@remotehost:/remotepath/remotefilename
```

# Connecting with Microsoft Windows OS
- [Setting up SSH Server on Microsoft Windows](http://docs.oracle.com/cd/E11857_01/install.111/e15838/appdx_setting_up_ssh.htm)
