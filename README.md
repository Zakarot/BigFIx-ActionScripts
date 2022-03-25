# BigFix

Uploads of my favorite or most useful bes tasks and fixlets. Common snippets of actionscript or relevance are listed here:

# Common Relevance for most tasks

/*Windows*/(name of it contains "Win") of operating system
/*Is Windows 10*/(name of it = "Win10") of operating system
/*Windows10 Release*/(name of it = "Win10", releaseid of it = "1803") of operating system

# Fixlet Debugger Queries for Application Name/Version

(values "DisplayName" of it, values "DisplayVersion" of it) whose (it as string as lowercase contains "Webex" as string as lowercase) of keys of keys "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" of (x64 registries;x32 registries)

(values "DisplayName" of it, values "DisplayVersion" of it) of keys of keys "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" of (x64 registries;x32 registries)

# Install Relevance Example

not exists (values "DisplayName" whose (it as string = "Cisco Webex Meetings Desktop App") of it, values "DisplayVersion" whose (it as string as version >= "33.6.4.15" as string as version) of it) of keys of keys "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" of (x64 registries;x32 registries)

# Common Install Action code snippets

action uses wow64 redirection false

MSI flags:
	/qn REBOOT=ReallySuppress /norestart

Run As User
	override wait
	hidden=true
	runas=currentuser
	completion=process
	wait <command>

# Update Relevance Example

exists (values "DisplayName" whose (it as string = "Cisco Webex Meetings Desktop App") of it, values "DisplayVersion" whose (it as string as version < "33.6.4.15" as string as version) of it) of keys of keys "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" of (x64 registries;x32 registries)

# Uninstall Relevance Example

exists (values "DisplayName" whose (it as string = "Cisco Webex Meetings Desktop App") of it) of keys of keys "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" of (x64 registries;x32 registries)

# Automatic Uninstall Action based on registry

waithidden "{pathname of system folder & "\msiexec.exe"}" /x {name of keys whose( (exists values "DisplayName" whose(it as string as lowercase = "Cisco Webex Meetings Desktop App" as lowercase) of it) AND (exists values whose(it as string as lowercase starts with "msiexec") of it) ) of keys "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall" of ( x64 registries; x32 registries )} /qn REBOOT=ReallySuppress /norestartUninstall
