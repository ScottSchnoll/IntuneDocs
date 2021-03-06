---
# required metadata

title: Help protect iOS devices with Activation Lock bypass | Microsoft Intune
description: Microsoft Intune can help you manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices.
keywords:
author: robstackmsft
manager: jeffgilb
ms.date: 07/12/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: bb49e926-15c4-4f01-b6eb-cee6f7ee1984

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: joglocke
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Help protect iOS devices with Activation Lock bypass for Microsoft Intune
Microsoft Intune can help you manage iOS Activation Lock, a feature of the Find My iPhone app for iOS 7.1 and later devices. Activation Lock is enabled automatically when the Find My iPhone app is used on a device. After it is enabled, the user's Apple ID and password must be entered before anyone can:

-   Turn off Find My iPhone

-   Erase the device

-   Reactivate the device

## How Activation Lock affects you
While Activation Lock helps secure iOS devices and improves the chances of recovery if they are lost and stolen, this capability can present you, as an IT admin, with a number of challenges. For example:

-   One of your users sets up Activation Lock on a device. The user then leaves the company and returns the device. Without the user's Apple ID and password, there is no way to reactivate the device.

-   You need a report of all devices that have Activation Lock enabled.

-   During a device refresh in your organization, you want to reassign some devices to a different department. You can only reassign devices that do not have Activation Lock enabled.

To help solve these problems, Apple introduced Activation Lock bypass in iOS 7.1. This lets you remove the Activation Lock from supervised devices without the user's Apple ID and password. Supervised devices can generate a device-specific Activation Lock bypass code, which is stored on Apple's activation server.

> [!TIP]
> Supervised mode for iOS devices lets you use the Apple Configurator Tool to lock down a device to limit functionality to specific business purposes. Supervised mode is generally only for corporate-owned devices.

## How Intune helps you manage Activation Lock
Intune can request the Activation Lock status of both supervised and unsupervised devices that run iOS 7.1 and later. For supervised devices only, Intune can retrieve the Activation Lock bypass code and directly issue it to the device. If the device has been wiped, you can directly access the device using the code as the user name, and a blank password).

**The business benefits of this are**:

-   The user gets the security benefits of the Find My iPhone app.

-   You can enable the user to do their work knowing that when the device needs to be re-purposed, you can retire or unlock it.

## How to use Activation Lock bypass from the Intune admin console
> [!IMPORTANT]
> After you bypass the Activation Lock on a device, it will automatically apply a new Activation Lock if the Find My iPhone app is opened. Because of this, **you should be in physical possession of the device before you follow this procedure**.

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com), choose **Groups** &gt; **All Devices** &gt; **All Corporate-owned Devices**.

2.  Select the device whose Activation Lock you want to bypass. Choose **Activation Lock Bypass**.

3.  Read the warning message. Choose **Yes** to proceed.

You can examine the status of the unlock request on the details page for the device.

## How to see which devices are using Activation Lock
You can see which devices are using Activation Lock in two ways:

-   Run the **Mobile Device Inventory Reports**. This report displays the columns **Activation Lock Status** and **Supervised** to indicate the state of devices. The values for **Supervised** are **Yes** or **No**, and the values for **Activation Lock Status** are:

    -   Enabled with bypass code

    -   Enabled without bypass code (device is not supervised)

    -   Enabled without bypass code (device cannot be reached)

    -   Not enabled

    The **Activation Lock Status** field is blank for devices that do not run iOS 7.1 or later.

-   Select a device in a groups view, you can see the Activation Lock status in the device details pane.

    If you select a device in the **All Corporate-owned Devices** node, and Activation Lock is enabled for the device, you can also see the bypass code. This code can be used to manually issue an Activation Lock bypass.

	> [!IMPORTANT]
	>Intune takes inventory from devices for Activation Lock every 7 days. Because of this, devices might not immediately be displayed with their Activation Lock status in the Intune console.


### See also
[Retire devices](retire-devices-from-microsoft-intune-management.md)
[Help protect your devices with remote lock and passcode reset](use-remote-lock-and-passcode-reset-in-microsoft-intune.md)
