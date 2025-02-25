# Deprovision & Delete Users Automation
This Box CLI script deprovision a list of users by first transfering user content to the current admin user's root folder under "Employee Archive" (Transfer content default: "Y") before deleting that user.

> For every user, script makes 7 API calls to archive their content and delete the account.


## Setup Pre-Requisites
1. Clone this github repo or download files from the `/examples` directory
   ```bash
   git clone https://github.com/box/boxcli.git
   ```
2. Install PowerShell or .Net core.
   > If you encounter issues make sure you install both dotnet core and PowerShell
    1. For MacOS & Linux, Install the latest version of [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.2).
    2. For Windows, Install the latest version of [dotnet core](https://dotnet.microsoft.com/download).
    
3. Test PowerShell by running the `pwsh` command in your terminal.
   ```bash
   pwsh
   ```
   
	```
	mikechen@mbp create-users-automation % pwsh
	PowerShell 7.2.1
	Copyright (c) Microsoft Corporation.
	
	https://aka.ms/powershell
	Type 'help' to get help.
	
	PS /Users/mikechen>
	```

4. Create an OAuth Application using the [CLI Setup Quick Start][oauth-guide].

[oauth-guide]: https://developer.box.com/guides/cli/quick-start/

## 1. Script Parameters
1. Update the [EmployeeList](Users_Deprovision.ps1#L12) to set your own Employee List CSV Path.
2. Customize the [input file of employee accounts for deletion](Employees_to_delete.csv) by providing their **email** addresses
	* For example, update the [Employees_to_delete.csv](Employees_to_delete.csv) with the following data:
	```
	name,email
	Managed User 1,ManagedUser1@test.com
	```
3. Optional: To skip transfer of user content before deletion, set [TransferContent](Users_Deprovision.ps1#L15) to "N".
4. Optional: Update Archive folder name by changing  [EmployeeArchiveFolderName](Users_Deprovision.ps1#L18) to any name of your choice.

## 2. Run the script
Now all you need to do is run the script. Change the directory to the folder containing the script. In this example, it is the `User Deprovisioning` folder.

```
rvb@lab:~/box-cli/examples/User Deprovisioning$ pwsh
PowerShell 7.2.4
Copyright (c) Microsoft Corporation.

https://aka.ms/powershell
Type 'help' to get help.

PS /home/rvb/box-cli/examples/User Deprovisioning>
```

Run the script:
```bash
./Users_Deprovision.ps1
```


```
PS /home/rvb/box-cli/examples/User Creation & Provisioning> ./Users_Deprovision.ps1
Starting User Deprovisioning script...
```

Once script completes, you will see the following confirmation:

```
....
Transfered employee content Managed User 1 with User ID: 19927131476 to Employee Archive Folder
Deleted user 19927131476
Deleted employee Managed User 1
```

## Logging
Logs are written to a `logs` folder within the folder that contains this script. The logs are named `Users_Deprovision_all.txt` and `Users_Deprovision_errors.txt`. The former contains all log entries and the latter contains only errors.

## Disclaimer
This project is a collection of open source examples and should not be treated as an officially supported product. Use at your own risk.

## License

The MIT License (MIT)

Copyright (c) 2022 Box

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
