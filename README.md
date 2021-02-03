# IntuneManagement with PowerShell and WPF UI

This PowerShell scripts are using Intune PowerShell module, Microsoft Graph APIs and AzureRM PowerShell module to manage objects in Intune and Azure. The scripts has a simple WPF UI and it supports operations like Export, Import, Copy and Download.

This makes it easy to backup or clone a complete Intune environment. The scripts will export and import assignments and support import/export between environments. The scripts will create a migration table during export and use that for importing in other environments. It will create groups if they are missing in the environment for import.

![Screenshot](/IntuneManagement.PNG?raw=true)

**Note:** The base PowerShell script is only a host for extensions. It is only used as a framework for basic UI, logging etc. The functionality is located in the extension modules which makes it easy to add/remove features.

## Change log
**Version 2**

**Breaking changes**
* Removed support for AzureRM

**New features**
* Support for Az module for Azure objects (Conditional access, Company Branding and MDM/MAM settings)
* Reload - Reloads all modules 

**Fixes**
* Allow more than 9 Conditional Access policies. Issue [#5](https://github.com/Micke-K/IntuneManagement/issues/5)
* Include WIP policies. Issue [#7](https://github.com/Micke-K/IntuneManagement/issues/7)
* Import is not working. Issue [#6](https://github.com/Micke-K/IntuneManagement/issues/6) and [#4](https://github.com/Micke-K/IntuneManagement/issues/4)
* Intune module can now be install with scope user. Issue [#8](https://github.com/Micke-K/IntuneManagement/issues/8)

## Intune objects
* Administrative Templates
* App Protection/Configuration policies
* Applications
* Autopilot profiles
* Baseline Security profiles
* Compliance policies
* Configuration Items
* Enrollment Status Page profiles
* Intune Branding (Company Portal)
* PowerShell scripts (Supports download of PowerShell script)
* Terms and Conditions

**Note:** The Intune PowerShell module are using the BETA version of the Graph API which might change at any time.

## Azure objects
* Conditional Access
* Company Branding
* MDM/MAM app settings

**Note:** Azure objects are not using the Microsoft Graph API. They are using undocumented APIs which might not be supported and change at any time.

## Prerequisites
* .Net 4.7
* Intune PowerShell Module
  * Install by running 'Install-Module -Name Microsoft.Graph.Intune'
* Az PowerShell Module
  * Install by running 'Install-Module -Name Az -AllowClobber'
* Permissions in Azure to manage objects in Intune and Azure 

## References
* [Microsoft Graph API](https://docs.microsoft.com/en-us/graph/api/overview?toc=./ref/toc.json&view=graph-rest-beta) 
* [Microsoft Intune PowerShell Module](https://github.com/microsoft/Intune-PowerShell-SDK)
* [Az PowerShellModule](https://docs.microsoft.com/en-us/powershell/azure/new-azureps-module-az)

## Acknowledgments
The app enryption and upload is based on [PowerShell Intune Examples](https://github.com/microsoftgraph/powershell-intune-samples)

## Known Issues
The scripts are using two separate PowerShell modules for accessing Intune and Azure. This can cause multiple logins since they are authenticating to two different apps in azure and the authentication token for Intune PowerShell module have no permissions on the Azure objects.

The support for import/export between environments is limited. Only groups in assignments are supported in this version. Additional objects like users, locations, notifications etc. will not be migrated and might cause the import to fail.

The script will create a group if it is missing in the destination environment. It will create a security group with manual assigned members. This might not always be the desired case e.g. original group was synched from AD or it was a dynamic group.

## TIP

Download [Microsoft.WindowsAPICodePack](https://www.nuget.org/packages/WindowsAPICodePack-Core) and [Microsoft.WindowsAPICodePack.Shell](https://www.nuget.org/packages/WindowsAPICodePack-Shell) and copy the DLLs into the script folder to get a nicer folder dialog.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
