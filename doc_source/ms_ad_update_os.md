# Update your directory operating system<a name="ms_ad_update_os"></a>

Windows Server 2012 R2 powers AWS Managed Microsoft AD, but on October 10, 2023, Windows will end extended support and security updates for this operating system \(OS\) version\. To address this, AWS allows you to upgrade the operating system for your AWS Managed Microsoft ADs from Windows Server 2012 R2 to Windows Server 2019\. With this upgrade, your AWS Managed Microsoft ADs will have mainstream support and improved security\. To update your directories, follow the instructions in [Updating your directory OS to Windows Server 2019](#update-to-windows-2019)\. If you choose not to update your OS now, at a later time  AWS will automatically update it for all eligible directories\.

## Updating your directory OS to Windows Server 2019<a name="update-to-windows-2019"></a>

**To update your directory OS to Windows Server 2019**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/), choose **Directories**\.

1. On the **Directories** page, a flash bar appears to indicate that an OS update is available for AWS Managed Microsoft AD directories\. Beneath the **Directory ID** of each eligible directory, a message states that OS update is available\. Choose the **Directory ID** of the directory that you want to update\.

1. On **Directory details**, under **Operating system version**, choose **Update**, or choose **Update** on the flash bar at the top of the page\.

1. An **Operating system version update** dialog box appears\. If you want to take a snapshot of your directory, check the box next to **Take a directory snapshot before the update**\. Then, choose **Confirm**\. This takes you back to the individual directory page\.

1. A flash bar at the top of the page indicates that your operating system version is being updated\. On **Directory details**, under **Operating system version**, view the total progress of the update and the number of domain controllers completed\.

1. Once all the domain controllers for this directory are updated, a green flash bar appears at the top of the page to indicate that the update was successful\. Under **Operating system version**, Windows Server 2019 displays\.

## Changing your directory OS to Windows Server 2012 R2<a name="update-to-windows-2012"></a>

**Note**  
Your directory must already be updated to Windows Server 2019 to change your OS back to Windows Server 2012 R2\.

**To change your directory operating system to Windows Server 2012 R2**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/), choose **Directories**\.

1. On the **Directories** page, choose the **Directory ID** of the directory that you want to modify\.

1. On **Directory details**, under **Operating system version**, Windows Server 2019 displays\. Next to it, choose **Modify**\.

1. An **Operating system version change** dialog box appears\. If you want to take a snapshot of your directory, check the box next to **Take a directory snapshot before the change**\. Then, choose **Confirm**\.

1. Another dialog box **Feedback on modifying your operating system version** appears\. Choose an option from the drop down menu and then choose **Submit**, or choose **Skip**\. This returns you to the individual directory page\.

1. A flash bar at the top of the page indicates that your operating system version is being modified\. On **Directory details**, under **Operating system version**, view the total progress of the change and the number of domain controllers completed\.

1. Once all the domain controllers for this directory are modified, a green flash bar appears at the top of the page to indicate that the change was successful\. Under **Operating system version**, Windows Server 2012 R2 displays\.

## Updating your multi\-Region directory OS to Windows Server 2019<a name="update-multi-region-to-windows-2019"></a>

**To update your multi\-Region directory OS to Windows Server 2019**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/), choose **Directories**\.

1. On the **Directories** page, a flash bar appears to indicate that an OS update is available for AWS Managed Microsoft AD directories\. Beneath the **Directory ID** of each eligible directory, a message states that OS update is available\. Choose the **Directory ID** of the directory that you want to update\.

1. On **Directory details**, under **Multi\-region replication**, choose the first Region\. This is the primary Region, and must be the first Region that you update\. If you have already updated the first Region, choose the next one\. Then, under **Operating system version**, choose **Update**, or choose **Update** on the flash bar at the top of the page\.

1. An **Operating system version update** dialog box appears\. If you want to take a snapshot of your directory, check the box next to **Take a directory snapshot before the update**\. Then, choose **Confirm**\. This takes you back to the individual directory page\.

1. A flash bar at the top of the page indicates that your operating system version is being updated\. On **Directory details**, under **Operating system version**, view the total progress of the update and the number of regions completed\. Once your selected Region shows as **Completed**, update the next Region by repeating steps 1\-5\.

1. Once all the Regions for this directory are updated, a green flash bar appears at the top of the page to indicate that the update was successful\. Under **Operating system version**, Windows Server 2019 displays\.

## Changing your multi\-Region directory OS to Windows Server 2012 R2<a name="update-multi-region-to-windows-2012"></a>

**Note**  
Your directory must already be updated to Windows Server 2019 to change the OS back to Windows Server 2012 R2\.

**To change your multi\-Region directory operating system to Windows Server 2012 R2**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/), choose **Directories**\.

1. On the **Directories** page, choose the **Directory ID** of the directory that you want to change\.

1. On **Directory details**, under **Multi\-region replication**, choose the first Region\. This is the primary Region, and must be the first Region that you change\. If you have already changed the first Region, choose the next one\. Then, under **Operating system version**, choose **Modify**\.

1. An **Operating system version change** dialog box appears\. If you want to take a snapshot of your directory, check the box next to **Take a directory snapshot before the change**\. Then, choose **Confirm**\. This takes you back to the individual directory page\.

1. A flash bar at the top of the page indicates that your operating system version is being modified\. On **Directory details**, under **Operating system version**, view the total progress of the change and the number of regions completed\. Once your selected Region shows as **Completed**, modify the next Region by repeating steps 1\-5\.

1. Once all the Regions for this directory are changed, a green flash bar appears at the top of the page to indicate that the change was successful\. Under **Operating system version**, Windows Server 2012 R2 displays\.

## Remediating your directory OS update<a name="remediate-os-update"></a>

**To remediate your OS version update**

1. On **Directory details**, under **Operating system version**, next to the **Update failed** message, choose **Remediate**, or choose **Remediate** on the red flash bar at the top of the page\.

1. A **Remediate operating system version update** dialog box appears\. Choose **Retry \(Recommended\)** if you want to continue updating the OS version of your directory to Windows Server 2019\. Choose **Revert** if you want to revert the OS version of your directory to Windows Server 2012 R2\. Then, choose **Confirm**\.

1. You are returned to the individual directory page where you can monitor the progress of the update\.