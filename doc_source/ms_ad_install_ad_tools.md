# Installing the Active Directory Administration Tools<a name="ms_ad_install_ad_tools"></a>

To manage your directory from an EC2 Windows instance, you need to install the Active Directory Domain Services and Active Directory Lightweight Directory Services Tools on the instance\. Use the following procedure to install these tools on either Windows Server 2012, Windows Server 2016, or Windows Server 2019\.

You can optionally choose to install the Active Directory administration tools using Windows PowerShell\. For example, you can install the Active Directory remote administration tools from a PowerShell prompt using `Install-WindowsFeature RSAT-ADDS`\. For more information, see [Install\-WindowsFeature](https://docs.microsoft.com/en-us/powershell/module/servermanager/install-windowsfeature?view=winserver2012r2-ps) on the Microsoft Website\.

## Install the Active Directory Administration Tools on Windows Server 2012 through Windows Server 2019<a name="install_ad_tools_winserver"></a>

**To install the Active Directory administration tools on Windows Server 2012 through Windows Server 2019**

1. Open Server Manager from the Start screen by choosing **Server Manager**\.

1. In the **Server Manager Dashboard**, choose **Add roles and features**, 

1. In the **Add Roles and Features Wizard** choose **Installation Type**, select **Role\-based or feature\-based installation**, and choose **Next**\.

1. Under **Server Selection**, make sure the local server is selected, and choose **Features** in the left navigation pane\.

1. In the **Features** tree, open **Remote Server Administration Tools**, **Role Administration Tools**, select **AD DS and AD LDS Tools**, scroll down and select **DNS Server Tools**, and then choose **Next**\.

1. Review the information and choose **Install**\. When the feature installation is finished, the Active Directory Domain Services and Active Directory Lightweight Directory Services Tools are available on the Start screen in the **Administrative Tools** folder\.