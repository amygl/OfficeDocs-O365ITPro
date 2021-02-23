---
title: "Block a user from deleting tasks in Microsoft Planner they didn't create"
f1.keywords:
- NOCSH
ms.author: amyglave
author: amyglave
manager: danfi
ms.date: 02/23/2021
audience: Admin
ms.topic: Overview
ms.service: o365-administration
localization_priority: Priority
search.appverid:
- MET150
description: "This article shares information on how admins can block a user from deleting tasks the user didn't create"
---

# Block a user from deleting tasks not created by themselves

Tenant admins can block a specific user from deleting tasks in Microsoft Planner that they did not create.

## Pre-reqs
Download zip file from here

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



## Set user policy

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

.example
PS> Set-PlannerUserPolicy -UserId aadIdOfUser -BlockDeleteTasksNotCreatedBySelf $false
