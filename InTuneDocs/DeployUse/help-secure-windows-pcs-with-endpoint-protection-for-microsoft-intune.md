---
# required metadata

title: Endpoint Protection for Windows PCs| Microsoft Intune
description: Secure your managed computers with Endpoint Protection which provides real-time protection against malware threats.
keywords:
author: NathBarn
manager: muhosabe
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 002241bf-6cd0-4c75-a4f0-891ac7e6721a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: damionw
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Help secure Windows PCs with Endpoint Protection for Microsoft Intune
Microsoft Intune can help you to secure your managed computers in a number of ways, including Endpoint Protection which provides real-time protection against malware threats, keeps malware definitions up-to date, and automatically scans computers. Endpoint Protection also provides tools that help you to manage and monitor malware attacks.

If you have not yet installed the Intune client on your computers, see [Install the Windows PC client with Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

Use the information in the following sections to help you configure, deploy and monitor Endpoint Protection.

## Choose when to use Endpoint Protection
As an IT admin, one of your top priorities is to keep the computers that you manage free of malware and viruses. Before you deploy Intune to Windows PCs in your organization, you should decide how to protect your computers by selecting one of the following options and configuring its associated policy settings:

|I want to:|Endpoint Protection policy settings|More information|
|--------------|---------------------------------------|--------------------|
|Use Microsoft Intune Endpoint Protection only if no third-party endpoint protection application is installed.<br /><br />You can use Microsoft Intune Endpoint Protection on all computers where a third-party endpoint protection application is not installed.|Install Endpoint Protection = **Yes**<br /><br />Enable Endpoint Protection = **Yes**<br /><br />Install Endpoint Protection even if a third-party endpoint protection application is installed = **No**|If a third-party endpoint protection application is detected, Microsoft Intune Endpoint Protection will not be installed, or will be uninstalled if it has already been installed.|
|Use Microsoft Intune Endpoint Protection, even if a third-party endpoint protection application is installed<br /><br />With this approach, you will be running Microsoft Intune Endpoint Protection and the third party endpoint protection application simultaneously. This is not a recommended configuration because of potential performance issues.|Install Endpoint Protection = **Yes**<br /><br />Enable Endpoint Protection = **Yes**<br /><br />Install Endpoint Protection even if a third-party endpoint protection application is installed = **Yes**|Use when:<br /><br />-   You want to switch to using Microsoft Intune Endpoint Protection.<br />-   You deploy a new client that will use Microsoft Intune Endpoint Protection<br />-   You upgrade any client that will use Microsoft Intune Endpoint Protection.|
|Use Intune without Microsoft Intune Endpoint Protection. Instead, you will rely on a third-party endpoint protection application.|Install Endpoint Protection = **No**|If you are not using a third-party endpoint protection application, this configuration is not recommended, as it could expose your organization’s computers to malware or other attacks.<br /><br />Microsoft Intune Endpoint Protection is not installed, and it is uninstalled if it was installed previously.|
To switch from your current endpoint protection application to Microsoft Intune Endpoint Protection, do the following:

1.  Leave your current endpoint protection application running while you deploy the Intune client software to those computers.

2.  Confirm that Microsoft Intune Endpoint Protection is installed and is helping to secure client computers.

3.  Remove the third-party endpoint protection software by:

    -   Use Intune software distribution to deploy a software removal tool provided by the manufacturer of the third-party endpoint protection application. For more information, see [Deploy apps with Microsoft Intune](deploy-apps.md).

    -   Removing the third-party endpoint protection application manually.

> [!NOTE]
> Intune will not automatically uninstall third-party endpoint protection applications.

## How to configure Microsoft Intune Endpoint Protection
Use the following steps to help you configure Endpoint Protection for Microsoft Intune.

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com/), click **Policy** > **Add Policy**.

2.  Expand **Computer Management** and select **Microsoft Intune Agent Settings**. Select **Create and Deploy a Custom Policy** to specify policy for Endpoint Protection settings and then click the **Create Policy** button. You can use recommended settings or customize the settings. If you need more information about how to create and deploy policies, see the [Common Windows PC management tasks with the Microsoft Intune computer client](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md) topic.

  ![Endpoint Protection settings](./media/pol-sa-pc-endpoint-policy.png)

You can view the deployed Endpoint Protection policy on the **All Policies** page of the **Policy** workspace.

## Endpoint Protection service settings

|Policy setting|Details|
|------------------|--------------------|
|**Install Endpoint Protection**|Set to **Yes** to install Endpoint Protection on managed computers. If a third-party endpoint protection application is detected during installation, Endpoint Protection will not be installed unless **Install Endpoint Protection even if a third party endpoint protection application is installed** is set to **Yes**. **Note:** Intune Endpoint Protection is installed on managed computers by default. If you don’t want Endpoint Protection installed on your managed computers, you must explicitly set this policy to **No**. If Endpoint Protection was previously installed and the policy is updated to **No**, then the Endpoint Protection client will be uninstalled.<br />Recommended value: **Yes**|
|**Install Endpoint Protection even if a third party endpoint protection application is installed**|Set to **Yes** to install Microsoft Intune Endpoint Protection even if a third-party endpoint protection application is detected.<br /><br />Recommended value: **Yes**|
|**Enable Endpoint Protection**|Set to **Yes** to enable Microsoft Intune Endpoint Protection on computers which have the Endpoint Protection client.<br /><br />If set to **No**, and Microsoft Intune Endpoint Protection is installed, the Endpoint Protection client user interface is not displayed to users and all protection features are inactive.<br /><br />Recommended value: **Yes**|
|**Disable Client UI**|Set to **Yes** to hide the Microsoft Intune Endpoint Protection client user interface from users (requires a client computer restart to take effect).<br /><br />Recommended value: **No**|
|**Install Endpoint Protection even if a third party endpoint protection application is installed**|Set to **Yes** to force the installation of Microsoft Intune Endpoint Protection, even if a third-party endpoint protection application is detected.<br /><br />Recommended value: **No**|
|**Create a system restore point before malware remediation**|Set to **Yes** to create a Windows System Restore Point before any malware remediation begins.<br /><br />Recommended value: **Yes**|
|**Track resolved malware (days)**|Enables Endpoint Protection to track resolved malware for a specified time so that you can manually check previously infected computers.<br /><br />You can specify a value from 0 to 30 days.<br /><br />Recommended value: **7 days**|
If you have set the policy values for **Install Endpoint Protection** and **Enable Endpoint Protection** to **Yes**, and the policy value for  **Install Endpoint Protection even if a third party endpoint protection application is installed** to **No**, Microsoft Intune Endpoint Protection will detect that another endpoint protection application is installed and will be not be installed, or uninstalled if it is already present however, Microsoft Intune Endpoint Protection does report about the health of the other endpoint protection application in the Intune.

  Real-time protection is how Microsoft Security Essentials alerts you when potential threats such as viruses and spyware are trying to install themselves or run on your PC. The moment this happens, you’ll see a message in the notification area to the far right of the taskbar

### Real-time protection settings

|Policy setting|Details|
|------------------|--------------------|
|**Enable real-time protection**|Enables monitoring and scanning of all files and applications that are accessed. It also blocks any malicious files and applications before they can run on computers.<br /><br />Recommended value: **Yes**|
|**Scan all downloads**|Enables the scanning of all files and attachments that are downloaded from the Internet to computers.<br /><br />Recommended value: **Yes**|
|**Monitor file and program activity on computers**|Enables the monitoring of incoming files and outgoing files, and program activity on computers. With this setting, Endpoint Protection can monitor when files and programs start to run and alert you about any actions they perform or actions that are taken on them.<br /><br />Recommended value: **Yes**|
|**Files monitored**|If **Monitor file and program activity on computers** is enabled, this setting allows you to choose if only incoming, only outgoing, or all files are monitored.<br /><br />Recommended value: **Monitor all files**|
|**Enable behavior monitoring**|Allows Microsoft Intune Endpoint Protection to check for certain patterns of suspicious activity on client computers.<br /><br />Recommended value: **Yes**|
|**Enable Network Inspection System**|Enables Network Inspection System (NIS) on client computers. NIS uses signatures of known vulnerabilities from the [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkId=234249) to help detect and block malicious network traffic.<br /><br />Recommended value: **Yes**|

  ![Realtime settings for Endpoint Protection](./media/pol-sa-pc-policy-realtime.png)

### Scan schedule settings

|Policy setting|More information|
|------------------|--------------------|
|**Schedule a daily quick scan**|Schedules a daily quick scan of both frequently used files and important system files on computers. This quick scan has a minimal effect on performance.<br /><br />Recommended value: **Yes**|
|**Run a quick scan if you have missed two consecutive scans**|Configures Endpoint Protection to automatically run a quick scan on computers if they miss two consecutive, scheduled quick scans.<br /><br />Recommended value: **Yes**|
|**Schedule a full scan**|Configures a full scan of all files and resources on the local hard disks of computers. This scan can take some time and can affect computer performance (depending on the number of files and resources scanned).<br /><br />Recommended value: **No**|
|**Run a full scan if you have missed two consecutive full scans**|Configures Endpoint Protection to automatically run a full scan on computers if they miss two consecutive, scheduled full scans.<br /><br />Recommend value: Not configured|

### Scan options settings

|Policy setting|Details|
|------------------|--------------------|
|**Run a full scan after installation of Endpoint Protection**|Configures Endpoint Protection to automatically run a full system scan after it is installed on computers. This scan runs only when computers are idle to minimize the effect on user productivity.<br /><br />Recommended value: **Yes**|
|**Automatically run a full scan when needed to follow up malware removal**|Set to **Yes** to let Endpoint Protection automatically run a full system scan on computers after the removal of malware to help confirm that other files were not affected.<br /><br />Recommended value: **Yes**|
|**Start a scheduled scan only when the computer is idle**|Set to **Yes** to prevent scheduled scans from starting when computers are in use to prevent any loss of user productivity.<br /><br />Recommended value: **Yes**|
|**Check for the latest malware definitions before starting a scan**|Set to **Yes** to let Endpoint Protection automatically check for the latest malware definitions before it starts a scan on computers.<br /><br />Recommended value: **Yes**|
|**Scan archive files**|Set to **Yes** to configure Endpoint Protection to scan for malware in archive files (like .zip or .cab files) on computers.<br /><br />Recommended value: **No**|
|**Scan email messages**|Set to **Yes** to configure Endpoint Protection to scan incoming email messages when they arrive on computers.<br /><br />Recommended value: **Yes**|
|**Scan files opened from network shared folders**|Set to **Yes** to configure Endpoint Protection to scan files that are opened from shared folders on the network. These are typically files that are accessed by using a UNC path. Enabling this feature can cause problems for users who have read-only access because they cannot remove malware.<br /><br />Recommended value: **No**|
|**Scan mapped network drives**|Set to **Yes** to configure Endpoint Protection to scan files on mapped network drives. Enabling this feature can cause problems for users who have read-only access because they cannot remove malware.<br /><br />Recommended value: **No**|
|**Scan removable drives**|Set to **Yes** to configure Endpoint Protection to scan for malware and unwanted software on removable drives, like USB flash drives, when you run a full scan on computers.<br /><br />Recommended value: **Yes**|
|**Limit CPU usage during a scan**|Configures the maximum percentage of CPU usage that can be used during scheduled scans on computers. You can set this value from 1 to 100 percent.<br /><br />Recommended value: **50%**|

### Default actions settings

The **Choose how Endpoint Protection acts on malware of the following alert levels** setting specifies the default action that Endpoint Protection takes when malware of various alert levels is detected. For each alert level, you can remove the malware, quarantine it, or take Microsoft’s recommended action. Recommended value: **Recommended action** which allows Endpoint Protection to prescribe action.   

### Excluded files and folders settings

The **Files and folders to exclude when running a scan or using real-time protection** setting excludes specific files or folders when a scan is run or when real-time protection is used on computers.

### Excluded processes settings

The **Processes to exclude when running a scan or using real-time protection** setting lets you exclude specific processes when a scan is run or from real-time protection. You can exclude only files with the following extensions: **.exe**, **.com** or **.scr**.

### Excluded file types settings

The **File extensions to exclude when running a scan or using real-time protection** lets you exclude specific file name extensions when a scan is run or when real-time protection is used on computers.

### Microsoft Active Protection Service Settings
Microsoft Active Protection Service is an online community that helps you decide how to respond to potential threats. The community also helps stop the spread of new malware infections. You can **Join Microsoft Active Protection Service** by selecting **Yes** and then specifying your **Membership Level**:
  - **Basic** - Sends basic information to Microsoft about detected malware. This includes where the software came from, the actions that you apply or that Endpoint Protection applies automatically, and whether the actions were successful.
  - **Advanced** - Sends more information to Microsoft about malware, spyware, and potentially unwanted software. This includes the location of the software, file names, how the software operates, and how it has affected your computer.

You can also **Receive dynamic definitions based on Microsoft Active Protection Service reports**.

## Management tasks for Endpoint Protection
The following tasks help you to carry out various management tasks on managed computers that run Endpoint Protection:
 - Update malware definitions
  - Intune console - From the **Groups** workspace, select the computers you want to update. Click **Remote Tasks** &gt; **Update Malware Definitions**.
  - Managed computer - Start the Endpoint Protection client software from the Windows notification area. Click the **Update** tab, and then click **Update**.
 - Run a malware scan:
  - Intune console - From the **Groups** workspace, select the computers you want to scan. Click **Run a Full Malware Scan** or **Run a Quick Malware Scan**.
  - Managed computer - Start the Endpoint Protection client software from the Windows notification area. Select **Quick**, **Full**, or **Custom**, and then click **Scan now**.

You can view the status of a remote task by clicking the **Remote Tasks** link in the bottom right corner of the Intune console. The **Remote Task Status** dialog box lists current remote tasks, task status, device name, any reported errors, and provides a link to troubleshooting information, if appropriate.

## Monitor Endpoint Protection
You monitor the status of malware on your computers by using the **Protection** workspace of the [Microsoft Intune administration console](https://manage.microsoft.com/). This workspace contains two pages:
 - **Protection Overview** - Displays important issues as links that you can click for more information. Issues that might be displayed include:
  - **Malware instances that need follow-up** – Click the link to see a list of malware issues including the follow up action that needs to be taken to resolve the issue. You can further drill into this list to see which computers are affected.
  - **Computers with malware that need follow-up** – Click the link to see all computers with unresolved malware issues including the follow up action that needs to be taken to resolve the issue.
  - **Devices that are not protected** – Click the link to see computers that are not protected by any endpoint protection software, either because no software is installed, or because there is an error. Select a computer to view more details.
  - **Devices with another endpoint protection application running** – Click the link to see computers that are running a third-party endpoint protection application.
 - **All Malware** -  Displays a list of all active malware found on your computers. You can drill into this list to see all computers that are affected by a particular piece of malware, or you can select one of the following tasks:
  - **View Properties** – Opens a page with more information about the selected malware.
  - **Learn About This Malware** – Opens a topic from the Microsoft Malware Protection Center with more information about the malware.

> [!IMPORTANT]
> The **Protection** workspace is not displayed in the administrator console until you have installed the client and are managing at least one computer client.

  ![Monitor Endpoint Protection](./media/pol-sa-ep-monitor.png)

### How to view Recent Detection Paths for malware on computers
Intune can display the paths of up to 10 most recently detected instances of malware on a device. The **Recent Detection Path** is disabled by default. To enable this view:

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com/) go **Groups** > **All Devices** . **Malware**.

2.  Right-click a column header. A list of available columns appears.

3.  Mark the **Recent Detection Paths** checkbox in the list. The **Recent Detection Paths** column appears and displays up to 10 most recent malware instances monitored on the device.

## Run a malware scan or update malware definitions on a computer
Intune can run either a full or quick malware scan using Endpoint Protection or Windows Defender on a remote managed PC that is installed with the Intune client.

1. In the [Microsoft Intune administration console](https://manage.microsoft.com/) go **Groups** > **Overview** > **All Devices** > **All Computers**, and select the computer you want to target.

2. Click the **Remote Tasks** drop-down list and then select the task. The task to run on the remote computer.




## Need more help?
For further help and support, see [Troubleshoot Endpoint Protection in Microsoft Intune](/intune/troubleshoot/troubleshoot-endpoint-protection-in-microsoft-intune).

### See Also
[Policies to protect Windows PCs](policies-to-protect-windows-pcs-in-microsoft-intune.md)
