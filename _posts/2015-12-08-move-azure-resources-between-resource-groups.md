---
layout: post
title:  "Move an Azure Web App to a new Resource Group"
date:   2015-12-08 01:00:00 -0600
---

If you have an Azure Web App that you need to move to a different Resource Group you will need to use the Azure Resource Manager inside of Azure PowerShell. Currently this cannot be done within the Azure Portal.

## Install Azure PowerShell v1.0.x

There is a new AzureResourceManager that is part of Azure PowerShell v1.0.0, so you need to make sure you have the latest Azure PowerShell installed which you can download from their [GitHub releases page][1].

## Install AzureRM

To [install AzureResourceManager][2] open up PowerShell in Administrator mode and type in the following commands:

    Install-Module AzureRM
    Install-AzureRM
    Import-AzureRM

## Using AzureRM

Before we start using AzureRM we need to login using:

```
Login-AzureRmAccount
```

To see a list of your subscriptions you can use:

```
Get-AzureRmSubscription
```

And then you can switch Subscriptions if you need to with:

```
Select-AzureRmSubscription -SubscriptionName BizSpark
```

To get a list of Resource Groups you can use this command:

```
Get-AzureRmResourceGroup
```

And to get a list of Resources you can use this command:

```
Get-AzureRmResource
```

Normally I would like to list just the resources inside of Resource Group like this:

```
Get-AzureRmResource -ResourceGroupName "20151208-group"
```

But there is a [bug][3] currently and so to do any filtering on the `Get-AzureRmResource` command you have to use `-ResourceName` along with it:

```
Get-AzureRmResource -ResourceGroupName "20151208-group" -ResourceName "20151208-webapp"
```

The problem with having to do this though is that it excludes some resources.

### Moving an Azure Web App to a new Resource Group

If you would like to move an Azure Web App to a new Resource Group you need to find it's `ResourceId` using the

```
Get-AzureRmResource
```

command. Most likely that will list a lot of resources, so it can be helpful to narrow them down a bit and store the results in an array so that we can pass the `ResourceId` easily into the `Move-AzureRmResource` command. If we want to select just our web app we can get it using:

```
$r = Get-AzureRmResource -ResourceName "20151208-webapp" -ResourceType "Microsoft.Web/sites" -ResourceGroupName "20151208-group"
```

If you then type in just

```
$r
```

you will see that we only selected one resource (hopefully).

**Note**: *For Web Apps you will also have 3 additional resources for application insights but apparently those can't be moved to a new resource group, so you just need to select the individual Web App. For other resources like VMs you need to move all the resources along with it or it can't be moved to a new Resource Group.*

 and then you can move it to a different Resource Group using:

```
Move-AzureRmResource -DestinationResourceGroupName "20151208-group-b" -ResourceId $r.ResourceId
```

Your PowerShell will then sit there for some time while it moves your app to the new resource.

### Video Walk Through

Here is a video walk though where I show you how I transfer a web app to a new resource group:

<iframe width="560" height="315" src="https://www.youtube.com/embed/YTLokq5riSM?rel=0&amp;controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>


[1]: https://github.com/Azure/azure-powershell/releases
[2]: https://msdn.microsoft.com/en-us/library/mt125356.aspx
[3]: https://github.com/Azure/azure-powershell/issues/1259
