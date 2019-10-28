# Installing the Active Directory Administration Tools<a name="ms_ad_install_ad_tools"></a>

To manage your directory from an EC2 Windows instance, you need to install the Active Directory Domain Services and Active Directory Lightweight Directory Services Tools on the instance\. 

**Topics**
+ [Install the Active Directory Administration Tools on Windows Server 2008](#install_ad_tools_win2008)
+ [Install the Active Directory Administration Tools on Windows Server 2012](#install_ad_tools_win2012)
+ [Install the Active Directory Administration Tools on Windows Server 2016](#install_ad_tools_win2016)
+ [Install the Active Directory Administration Tools on Windows Server 2019](#install_ad_tools_win2019)

You can optionally choose to install the Active Directory administration tools using Windows PowerShell\. For example, you can install the Active Directory remote administration tools from a PowerShell prompt using `Install-WindowsFeature RSAT-ADDS`\. For more information, see [Install\-WindowsFeature](https://docs.microsoft.com/en-us/powershell/module/servermanager/install-windowsfeature?view=winserver2012r2-ps) on the Microsoft Website\.

## Install the Active Directory Administration Tools on Windows Server 2008<a name="install_ad_tools_win2008"></a>

**To install the Active Directory administration tools on Windows Server 2008**

1. Open Server Manager by choosing **Start**, **Administrative Tools**, **Server Manager**\.

1. In the **Server Manager** tree pane, select **Features**, and choose **Add Features**, 

1. In the **Add Features Wizard**, open **Remote Server Administration Tools**, **Role Administration Tools**, select **AD DS and AD LDS Tools**, scroll down and select **DNS**, then choose **Next**\.

1. Review the information and choose **Install**\. The feature installation requires that the instance be restarted\. When the instance has restarted, the Active Directory Domain Services and Active Directory Lightweight Directory Services Tools are available on the **Start** menu, under **All Programs** > **Administrative Tools**\.

## Install the Active Directory Administration Tools on Windows Server 2012<a name="install_ad_tools_win2012"></a>

**To install the Active Directory administration tools on Windows Server 2012**

1. Open Server Manager from the Start screen by choosing **Server Manager**\.

1. In the **Server Manager Dashboard**, choose **Add roles and features**, 

1. In the **Add Roles and Features Wizard** choose **Installation Type**, select **Role\-based or feature\-based installation**, and choose **Next**\.

1. Under **Server Selection**, make sure the local server is selected, and choose **Features** in the left navigation pane\.

1. In the **Features** tree, open **Remote Server Administration Tools**, **Role Administration Tools**, select **AD DS and AD LDS Tools**, scroll down and select **DNS Server Tools**, and then choose **Next**\.

1. Review the information and choose **Install**\. When the feature installation is finished, the Active Directory Domain Services and Active Directory Lightweight Directory Services Tools are available on the Start screen in the **Administrative Tools** folder\.

## Install the Active Directory Administration Tools on Windows Server 2016<a name="install_ad_tools_win2016"></a>

**To install the Active Directory administration tools on Windows Server 2016**

1. Open Server Manager from the Start screen by choosing **Server Manager**\.

1. In the **Server Manager Dashboard**, choose **Add roles and features**, 

1. In the **Add Roles and Features Wizard** choose **Installation Type**, select **Role\-based or feature\-based installation**, and choose **Next**\.

1. Under **Server Selection**, make sure the local server is selected, and choose **Features** in the left navigation pane\.

1. In the **Features** tree, open **Remote Server Administration Tools**, **Role Administration Tools**, select **AD DS and AD LDS Tools**, scroll down and select **DNS Server Tools**, and then choose **Next**\.

1. Review the information and choose **Install**\. When the feature installation is finished, the Active Directory tools are available on the Start screen in the **Administrative Tools** folder\.

## Install the Active Directory Administration Tools on Windows Server 2019<a name="install_ad_tools_win2019"></a>

**To install the Active Directory administration tools on Windows Server 2019**

1. Open Server Manager from the Start screen by choosing **Server Manager**\.

1. In the **Server Manager Dashboard**, choose **Add roles and features**, 

1. In the **Add Roles and Features Wizard** choose **Installation Type**, select **Role\-based or feature\-based installation**, and choose **Next**\.

1. Under **Server Selection**, make sure the local server is selected, and choose **Features** in the left navigation pane\.

1. In the **Features** tree, open **Remote Server Administration Tools**, **Role Administration Tools**, select **AD DS and AD LDS Tools**, scroll down and select **DNS Server Tools**, and then choose **Next**\.

1. Review the information and choose **Install**\. When the feature installation is finished, the Active Directory tools are available on the Start screen in the **Administrative Tools** folder\.