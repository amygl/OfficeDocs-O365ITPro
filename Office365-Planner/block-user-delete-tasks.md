---
title: "Block a user from deleting tasks in Microsoft Planner they didn't create"
f1.keywords:
ms.author: amyglave
author: amyglave
manager: danfi
ms.date: 02/23/2021
audience: Admin
ms.topic: Overview
ms.service: o365-administration
localization_priority: Priority
search.appverid:
description: "This article shares information on how admins can block a user from deleting tasks the user didn't create"
---

# Block a user from deleting tasks not created by themselves

Tenant admins can block a specific user from deleting tasks in Microsoft Planner that they did not create.

## Requirements

You need to do the following first:

- You must be a global admin to run the PowerShell script for exporting your Planner user data.
- You need to download and unzip the [Planner tenant admin files](https://go.microsoft.com/fwlink/?linkid=871954). These three files are the PowerShell modules and the PowerShell script file needed to block or unblock the user.

    > [!NOTE]
    > By downloading this package, you agree to the enclosed license and terms.

**TODO: update the zip file link**

## Unblock your files

You will need to "unblock" three of the files you downloaded in the Planner User Data Export script package in order to user them in PowerShell. This is because by default, executing scripts downloaded from the Internet is not allowed. The files you need to unblock are:

- plannertenantadmin.psm1
- microsoft.identitymodel.clients.activedirectory.dll
- microsoft.identitymodel.clients.activedirectory.windowsforms.dll

Do the following to unblock these files:

1. In File Explorer, go to the location in which you unzipped your files.
2. Right-click on one of the unzipped files noted above, and click Properties.
3. On the General tab, select **Unblock**.

    ![unblock-files](media/unblock-files.png) 

4. Select **OK**.

5. Repeat these steps for the remaining two files.

## Import the powershell module

1. Start Windows PowerShell. In PowerShell, type the following to enable running scripts downloaded from the internet for this session only. It may prompt you to confirm by typing "Y".

   `PS> Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope Process`

2. Type the following to run the PlannerTenantAdmin PowerShell script. This will import a module with the required cmdlet to run the export.

   `PS> Import-module "<location of the .psm1 file>"`

   For example, if you file is stored in C:\AdminScript, you would type:

   `PS> Import-module "C:\AdminScript\PlannerTenantAdmin.psm1"`

## Block a user from deleting tasks they didn't create
1. Use the Set-PlannerUserPolicy cmdlet to block a user from deleting Planner tasks that they didn't create.

   `PS> Set-PlannerUserPolicy -UserAadIdOrPrincipalName <user's AADId or UPN> -BlockDeleteTasksNotCreatedBySelf $true`

    |Parameter|Description|
    |---|---|
    |-UserAadIdOrPrincipalName|Use either the Azure Active Directory ID or the UPN of the user for which you want to export content.|
    |-BlockDeleteTasksNotCreatedBySelf|Whether or not to block the user from deleting tasks not created by themselves.|
    |-HostName|You only need to use this parameter if you access Planner though a host name other than *task.</span>office.</span>com*. For example, if you access Planner through *tasks.</span>office365.</span>us*, include *-HostName tasks.</span>office365</span>.us* in your command.|

    For example, the following will block a user from deleting tasks in Planner that they didn't create.

    `PS> Set-PlannerUserPolicy -UserAadIdOrPrincipalName amyg@contoso.onmicrosoft.com -BlockDeleteTasksNotCreatedBySelf $true`

2. You'll be prompted to authenticate. Log in as yourself (the global admin), not the user you want to block.

## Unblock a user from deleting tasks they didn't create

1. Use the Set-PlannerUserPolicy cmdlet to unblock a user from deleting Planner tasks that they didn't create.

   `PS> Set-PlannerUserPolicy -UserAadIdOrPrincipalName <user's AADId or UPN> -BlockDeleteTasksNotCreatedBySelf $false`

    |Parameter|Description|
    |---|---|
    |-UserAadIdOrPrincipalName|Use either the Azure Active Directory ID or the UPN of the user for which you want to export content.|
    |-BlockDeleteTasksNotCreatedBySelf|Whether or not to block the user from deleting tasks not created by themselves.|
    |-HostName|You only need to use this parameter if you access Planner though a host name other than *task.</span>office.</span>com*. For example, if you access Planner through *tasks.</span>office365.</span>us*, include *-HostName tasks.</span>office365</span>.us* in your command.|

    For example, the following will block a user from deleting tasks in Planner that they didn't create.

    `PS> Set-PlannerUserPolicy -UserAadIdOrPrincipalName amyg@contoso.onmicrosoft.com -BlockDeleteTasksNotCreatedBySelf $false`

2. You'll be prompted to authenticate. Log in as yourself (the global admin), not the user you want to block.

## Get user's current policy

Check a user's current policy with the Get-PlannerUserPolicy cmdlet.

`PS> Get-PlannerUserPolicy -UserAadIdOrPrincipalName <user's AADId or UPN>`

|Parameter|Description|
|---|---|
|-UserAadIdOrPrincipalName|Use either the Azure Active Directory ID or the UPN of the user for which you want to export content.|
|-HostName|You only need to use this parameter if you access Planner though a host name other than *task.</span>office.</span>com*. For example, if you access Planner through *tasks.</span>office365.</span>us*, include *-HostName tasks.</span>office365</span>.us* in your command.|

For example, the following will get a user's current policy
`PS> Get-PlannerUserPolicy -UserAadIdOrPrincipalName amyg@contoso.onmicrosoft.com | fl
@odata.context                   : https://tasks.office.com/taskApi/tenantAdminSettings/$metadata#UserPolicy/$entity
id                               : amyg@contoso.onmicrosoft.com
blockDeleteTasksNotCreatedBySelf : False`

