# Manually Join a Windows Instance<a name="simple_ad_join_windows_instance"></a>

To manually join an existing Amazon EC2 Windows instance to a Simple AD or AWS Directory Service for Microsoft Active Directory directory, the instance must be launched as specified in [Seamlessly Join a Windows EC2 Instance](launching_instance.md)\. 

**To join a Windows instance to a Simple AD or AWS Managed Microsoft AD directory**

1. Connect to the instance using any Remote Desktop Protocol client\.

1. Open the TCP/IPv4 properties dialog box on the instance\.

   1. Open **Network Connections**\.
**Tip**  
You can open **Network Connections** directly by running the following from a command prompt on the instance\.  

      ```
      %SystemRoot%\system32\control.exe ncpa.cpl
      ```

   1. Open the context menu \(right\-click\) for any enabled network connection and then choose **Properties**\.

   1. In the connection properties dialog box, open \(double\-click\) **Internet Protocol Version 4**\.

1. Select **Use the following DNS server addresses**, change the **Preferred DNS server** and **Alternate DNS server** addresses to the IP addresses of the AWS Directory Service\-provided DNS servers, and choose **OK**\.  
![\[Setting DNS server addresses\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/dns_server_addresses.png)

1. Open the **System Properties** dialog box for the instance, select the **Computer Name** tab, and choose **Change**\.
**Tip**  
You can open the **System Properties** dialog box directly by running the following from a command prompt on the instance\.  

   ```
   %SystemRoot%\system32\control.exe sysdm.cpl
   ```

1. In the **Member of** field, select **Domain**, enter the fully qualified name of your AWS Directory Service directory, and choose **OK**\.

1. When prompted for the name and password for the domain administrator, enter the user name and password of an account that has domain join privileges\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.
**Note**  
You can enter either the fully qualified name of your domain or the NetBios name, followed by a backslash \(\\\), and then the user name\.  
If using AWS Managed Microsoft AD, the user name would be **Admin**\. For example, **corp\.example\.com\\admin** or **corp\\admin**\.  
If using Simple AD, the user name would be **Administrator**\. For example, **corp\.example\.com\\administrator** or **corp\\administrator**\.

1. After you receive the message welcoming you to the domain, restart the instance to have the changes take effect\.

Now that your instance has been joined to the domain, you can log into that instance remotely and install utilities to manage the directory, such as adding users and groups\.