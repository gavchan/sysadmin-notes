# Microsoft Resources
- [Windows Server Overview](https://msdn.microsoft.com/library/dn636873(v=vs.85).aspx)
- [Windows Server Blog](https://blogs.technet.microsoft.com/windowsserver/)
- [Windows Server TechNet Library](https://technet.microsoft.com/en-us/library/bb625087.aspx)

- [Access and Information Protection with WS 2012R2](https://technet.microsoft.com/en-us/library/dn761715)

# Installation options
- [MS WS2012R2 Installation Options](https://technet.microsoft.com/en-us/library/hh831786)
- [Windows Server 2012 Unattended Installation @ Seaman's Blog](https://www.derekseaman.com/2012/07/windows-server-2012-unattended.html)

## New Installation of Windows Core
- Windows Core Install starts in cmd.exe
- If close automatically, can enter <Ctrl><Alt><Del> to run Task Manager and run a new task.
- Some available programs:
```
taskmgr
regedit
timedate.cpl
intl.cpl
msinfo32
sconfig.cmd
```

## Convert Server Core to Server with GUI
To use Windows PowerShell to convert from a Server Core installation to a Server with a GUI installation
Determine the index number for a Server with a GUI image (for example, SERVERDATACENTER, not SERVERDATACENTERCORE) with: `Get-WindowsImage -ImagePath <path to wim>\install.wim`

Run: `Install-WindowsFeature Server-Gui-Mgmt-Infra,Server-Gui-Shell –Restart –Source c:\mountdir\windows\winsxs`

Alternatively, if you want to use Windows Update as the source instead of a WIM file, use this Windows PowerShell cmdlet:
`Install-WindowsFeature Server-Gui-Mgmt-Infra,Server-Gui-Shell –Restart`

*If you get the following error message when trying the above installations:*
```
Error: 0x800f081f

The source files could not be found.
Use the "Source" option to specify the location of the files that are required to restore the feature. For more information
on specifying a source location, see http://go.microsoft.com/fwlink/?LinkId=243077.
```
**See this link to solve the issue.** [link here from Microsoft](https://support.microsoft.com/en-us/kb/2913316)

First get the index number of desired installation for Non-core:

```
dism /get-wiminfo /wimfile:d:\sources\install.wim
```

Next can run the command with the index number:

```
Install-WindowsFeature Server-Gui-Mgmt-Infra,Server-Gui-Shell -Restart -Source wim:d:\sources\install.wim:2
```

## Convert Server with GUI to Server Core
To convert to a Server Core installation with Windows PowerShell: run the following cmdlet:
```
Uninstall-WindowsFeature Server-Gui-Mgmt-Infra -Restart
```

## Features on Demand
In previous versions of Windows, even if a server role or feature was disabled, the binary files for it were still present on the disk, consuming space. In Windows Server 2012, not only can you disable a role or feature, but you can also completely remove its files, a state shown as “removed” in Server Manager or “disabled with payload removed” in Dism.exe.

- To reinstall a role or feature that been completely removed, you must have access to an installation source.

- To completely remove a role or feature, use `–Remove` with the `Uninstall-WindowsFeature` cmdlet of Windows PowerShell. For example, to completely remove Windows Explorer, Internet Explorer, and dependent components, run the following Windows PowerShell command:

```Uninstall-WindowsFeature Server-Gui-Shell -Remove
```

To install a role or feature that has been completely removed, use the Windows PowerShell `–Source` option of the `Install-WindowsFeature` Server Manager cmdlet. The –Source option specifies a path to a WIM image and the index number of the image. If you do not specify a –Source option, Windows will use Windows Update by default. Offline VHDs cannot be used as a source for installing roles or features which have been completely removed.

Only component sources from the exact same version of Windows are supported. For example, a component source derived from the Windows Server Developer Preview is not a valid installation source for a server running Windows Server 2012.

To install a removed role or feature using a WIM image, use the steps and Windows PowerShell cmdlets:
Run `Get-windowsimage –imagepath <path to wim>\install.wim`, and make note of the index of the Windows Server 2012 image.

`Install-WindowsFeature <featurename> -Source wim:<path>:<index>`, where:
Featurename is the name of the role or feature from Get-WindowsFeature
Path is the path to the WIM mount point
Index is the index of the server image from Step 1.
For example: `Install-WindowsFeature <featurename> -Source wim:d:\sources\install.wim:4`
