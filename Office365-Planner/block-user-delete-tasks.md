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

## Block a user from deleting tasks they didn't create
.Parameter HostName
The host name of the UserPolicy API for the Planner instance to retrieve. Default: tasks.office.com
.Parameter Authentication
Authentication result of a user with tenant-level administrator privileges.
.Parameter UserAadIdOrPrincipalName
AAD id or UPN for user
.Parameter BlockDeleteTasksNotCreatedBySelf
Whether to block deleting tasks not created by user

.example
PS> Set-PlannerUserPolicy -UserId aadIdOfUser -BlockDeleteTasksNotCreatedBySelf $true



## Unblock a user from deleting tasks they didn't create

.example
PS> Set-PlannerUserPolicy -UserId aadIdOfUser -BlockDeleteTasksNotCreatedBySelf $false

## Get current user policy

.Parameter HostName
The host name of the UserPolicy API for the Planner instance to retrieve. Default tasks.office.com
.Parameter Authentication
Authentication of a user with tenant-level administrator privileges.
.Parameter UserAadIdOrPrincipalName
AAD id or UPN for user

PS> Get-PlannerUserPolicy -UserAadIdOrPrincipalName aadIdOfUser | fl
@odata.context                   : https://tasks.office.com/taskApi/tenantAdminSettings/$metadata#UserPolicy/$entity
id                               : aadIdOfUser
blockDeleteTasksNotCreatedBySelf : False

