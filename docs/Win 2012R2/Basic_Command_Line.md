
- [Command Line Reference](https://commandwindows.com/command3.htm)

### CMD.exe
```
cls         # clear commandline
help        # list commands
dir
dir *.exe /s
find
findstr
netdom
shutdown
```

# Network Commands
```
ipconfig
net
net help
net command ?       # displays syntax of the command
net computer
net localgroup      # equivalent to bash-$ getent groups
net use             # allows connection to another network   
```
# Changing Computer Name
```
netdom renamecomputer compname /newname:a_New_Name
wmic computersystem where caption='currentname' rename newname
```

# Changing the Time/Date/Timezone
```
date
time
tzutil`
```
# Server Configuration Screen
```
sconfig
```
