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

# guess a verb
Get-Command -verb *command # or
gcm -verb *command
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
N.B `LogName` is positional parameter, its value 
must be passed in the first position. But you do 
not have to actually type the `–LogName` parameter 
name, that part is optional.
#### syntax
Using `space` or `tab` as delimiter, a command should be like this
```powershell
Get-EventLog -LogName Application
command/alias -para.name para.value
```
#### multi paras
Some parameters accept more than one value. In the 
Help file Syntax section, these are designated by 
a double-square-bracket notation in the parameter 
value type.
```powershell
-ComputerName <String[]>
```
This indicates that the `–ComputerName` parameter 
can accept one or more string values. Use a 
comma-separated list to specify multiple values. 
You do not have to enclose the values in quotation 
marks unless the values themselves contain a comma 
or white space, such as a space or tab character
```powershell
Get-EventLog –ComputerName LON-CL1,LON-DC1
```
#### Parenthetical Commands
There are other ways to specify multiple values 
such as using parenthetical commands. We will 
explore this technique in more detail later, but 
generally it works as follows:

Assume a text file includes one computer name per line:
```
LON-CL1
LON-DC1
```
If that file was named C:\computers.txt, you could use it in a parenthetical command as follows:
```powershell
Get-EventLog –LogName Application –ComputerName (Get-Content C:\computers.txt)
# the Get-Content is cat
Get-Content filename # full name, eqs to...
cat filename # eqs to...
type filename 
```
### summary about the syntax

- using alias instead of full name
- omitting parameter names entirely for positional 
parameters and pass only the parameter values in 
the appropriate positions
- typing only enough of each parameter name for the shell to determine the single parameter that you mean  

for example, these 2 commands are the same
```powershell
Get-Service –Name BITS –ComputerName LON-DC1
gsv BITS –Comp LON-DC1
```
### Using `Show-Command`
The `Show-Command` cmdlet enables you to generate 
commands quickly in Windows PowerShell through a 
GUI and is a helpful learning tool if you're 
working in the console. It is effectively the same 
functionality as the command pane in the ISE.

However, cmdlets like `Get-Help` and `Get-Command` 
give you fuller information about the syntax, so 
they are really better ways to learn the syntax. 
They also provide usage scenarios and examples 
that can help provide additional context and 
explanation.

Usage (the only usage)
```powershell
Show-Command -Name Get-WinEvent # OR
Show-Command Get-WinEvent
```
### Using `-WhatIf` and `-Confirm`
Running a command with the `-WhatIf` parameter 
does not actually execute the command, but causes 
the shell to display a message indicating what the 
command would have done if it had executed. 

The `-Confirm` parameter causes a command to pause 
execution and ask the user whether the command 
should continue before performing the action.

Each command has an internal setting called the confirm impact that is set by the command's developer to Low, Medium, or High. Windows PowerShell provides two built-in settings, or preference variables, that you can use to control the confirm impact and confirmation behavior of a command:
- `$ConfirmPreference`
- `$WhatIfPreference`

The default level for `$ConfirmPreference` is set 
to High when you start a new shell session. You 
can set `$ConfirmPreference` to Low or Medium, but 
that setting is preserved **only for the current 
shell session**.

When the command runs, Windows PowerShell checks 
its internal confirm impact level and if that 
level is **equal to or higher** than your 
`$ConfirmPreference` setting, Windows PowerShell 
performs the confirmation action automatically.

Therefore, to have the command prompt you to 
continue or halt execution, set the 
`$ConfirmPreference` preference to be less than 
the command's confirm impact. For example, if the 
internal confirm impact is set to Medium, you 
would set $ConfirmPreference as follows:
```powershell
$ConfirmPreference = "Low" 
```
For commands that have a **High** internal confirm 
impact, the default behavior is to auto-confirm 
and you will not be prompted to confirm how you 
want the command to execute. You can override this 
by specifying `-Confirm:$false`.

To view the current values of the `-Whatif` or 
`-Confirm` preference variables you can simply 
type `$ConfirmPreference` or `$WhatifPreference` 
at the console. 

View more details in the Help file by typing 
```powershell
help about_preference_variables -showwindow`
```
## Pipeline
### What is pipeline
Windows PowerShell runs commands in a pipeline. 
```powershell
Get-Service # single-command pipeline.

# multi-command pipeline.
Get-Service | Out-File ServiceList.txt # eqs to
Get-Service `
>>  Out-File ServiceList.txt
# type a single logical command line over multiple 
# physical lines
```
### Objects
Most Windows PowerShell commands do not generate 
files or text as output. Instead, they generate 
**objects**. Object is a generic word that 
describes a kind of in-memory data structure.

The properties of object are referred to as 
**members**, some of the members of the object will be shown on screen. Using `Get-Members` to 
show the members of the object returned by pipeline

For example, this will show all of the member of 
the object output by pipeline
```powershell
Get-Service | Get-Member
```
Using `Where-Object` (alias `where`) to locate a certain object
The properties of object are referred to as 
**members**, some of the members of the object will be shown on screen. Using `Get-Members` to 
show the members of the object returned by pipeline

For example, this will show all of the member of 
the object output by pipeline
```powershell
Get-Service | Get-Member
```
Using `Where-Object` (alias `where`) to locate a certain object

Try these interesting commands
```powershell
Get-Service | Where-Object Status -eq "Stop"
Get-Service | Get-Member
Get-Service | Get-Member | Get-Member 
Get-Service | Get-Member | Where-Object MemberType -eq "Method" 
Get-Service | Get-Member | Get-Member | Get-Member
```

Other useful commands using pipeline
```powershell
| format-table -wrap | OutputFile ""
```
### Sorted Objects
Using ``Sort-Object``(alias ``Sort``) to sort the object by 
``-Property``, using ``-Desc`` to sort the objects in descending
order, for examples

```powershell
Get-Service | Sort -Property Status # -Property can be omited
Get-Service | Sort Status, Name # sort for 2 or more properties
Get-Service | Sort -Desc
```

Using the ``hash table`` to sort one property in ascending order
and another property in descending order, for example:
```powershell
Get-Service `
Sort-Object -Property @{Expression = "Status"; Descending = $True}, @{Expression = "DisplayName"; Descending = $False}
```

By default, string properties are sorted without regard to case. 
However, parameters of Sort-Object enable you to specify a case-sensitive sort, 
a specific culture’s sorting rules, and other options. Refer to ``man Sort-Object``

**NOTICE THAT THE OBJECTS ARE PASSED THROUGH THE PIPELINE**