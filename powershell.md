# PowerShell commands
## basic commands
### help commands
```powershell
# get the help of the command
get-help cmd # full name, eqs to...
help cmd # eqs to
man cmd

get-help cmd -full # for full info.
get-help cmd -example # get some examples.
get-help cmd -online # get the latest info online
get-help -ShowWindow # start the help window

# get the about_ book
get-help about -online
# get the alias of the command
get-alias [cmd]
```
### familiar folder commands
```powershell
get-ChildItem # full name, eqs to... 
dir # eqs to...
ls
dir -recurse # all subfolder

Set-Location folder # full name, eqs to...
cd folder # eqs to
chdir folder

Set-Item folder # full name, eqs to...
mkdir folder
```
### modules 
```powershell
Get-Command #discover cmd, all cmd
Get-Verb # get verb cmd
```
Noun command examples: `Get-ChildItem` (`ls`), `Get-Process`

Gussing the command
```powershell
Get-Command *commmand # or
gcm *command
```
### parameters
```powershell
# take the Get-Eventlog for eg.
Get-EventLog    [-LogName] <string> # mandatory
                [[-InstanceId] <long[]>] #optional
                [-ComputerName <string[]>] 
                [-Newest <int>]  
                [-After <datetime>] 
                [-Before <datetime>]
                [-UserName <string[]>]
                [-Index <int[]>]
                [-EntryType {Error| Information | FailureAudit | SuccessAudit | Warning}] 
                [-Source <string[]>]
                [-Message <string>]
                [-AsBaseObject]
                [<CommonParameters>]
```
N.B `LogName` is positional parameter, its value must be passed in the first position. But you do not have to actually type the `–LogName` parameter name, that part is optional.


