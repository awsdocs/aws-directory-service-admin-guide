# Step 3: Deploy an EC2 Instance to Manage Microsoft AD<a name="microsoftadbasestep3"></a>

For this lab, we are using EC2 instances that have public IP addresses to make it easy to access the management instance from anywhere\. In a production setting, you can use instances that are in a private VPC that are only accessible through a VPN or Amazon Direct Connect link\. There is no requirement the instance have a public IP address\.

In this section, you walk through the various post\-deployment tasks necessary for client computers to connect to your domain using the Windows Server on your new EC2 instance\. You use the Windows Server in the next step to verify that the lab is operational\.

## Create a DHCP Options Set for Your Directory<a name="createdhcpoptionsset"></a>

In this procedure, you set up a DHCP option scope so that EC2 instances in your VPC automatically use your Microsoft AD for DNS resolution\. For more information, see [DHCP Options Sets](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html)\.

**To create a DHCP options set for your directory**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **DHCP Options Sets** in the navigation pane\. Then choose **Create DHCP options set**\.

1. In the **Create DHCP options set** dialog box, provide the following values for your directory:

   + For **Name tag**, type **AWS DS DHCP**\.

   + For **Domain name**, type **corp\.example\.com**\.

   + For **Domain name servers**, type the IP addresses of your AWS provided directory's DNS servers\. To find these addresses, go to the AWS Directory Service console navigation pane, choose **Directories**, choose the applicable directory ID, and on the **Details** page use the IPs that are displayed in **DNS address**\.

   + Leave the settings blank for **NTP servers**, **NetBIOS name servers**, and **NetBIOS node type**\.

1. Choose **Yes, Create**\. The new set of DHCP options appear in your list of DHCP options\.

1. Make a note of the ID of the new set of DHCP options \(**dopt\-*xxxxxxxx***\)\. You need it at the end of this procedure when you associate the new options set with your VPC\.

1. Choose **Your VPCs** in the navigation pane\.

1. Select the **AWS DS DHCP** VPC, choose **Actions**, and then choose **Edit DHCP Options Set**\.

1. In the **Edit DHCP Options Set** dialog box, select the options set that you recorded in Step 5\. Then choose **Save**\.

## Create a Role to Join Windows Instances to Your Microsoft AD Domain<a name="configureec2"></a>

Use this procedure to configure a role that joins an EC2 Windows instance to a domain\. For more information, see [Joining a Windows Instance to an AWS Directory Service Domain](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-join-aws-domain.html)\.

**To configure EC2 to join Windows instances to your domain**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane of the IAM console, choose **Roles**, and then choose **Create role**\.

1. Under **AWS service**, select the **EC2** link, and then click **Next**\.

1. Under **Select your use case**, select **EC2**, and then select **Next**\.

1. In the list of polices, select the **AmazonEC2RoleforSSM** policy, and then select **Next**\.

1. In **Role name**, type a name for the role that describes that it is used for domain join\. In this case use **EC2DomainJoin**, and then select the **Create role** button\.

## Create an EC2 Instance and Automatically Join the Directory<a name="deployec2instance"></a>

In this procedure you set up a Windows Server system in Amazon EC2 that can be used later to administer users, groups, and policies in Active Directory\. 

**To create an EC2 instance and automatically join the directory**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Choose **Launch Instance**\.

1. On the **Step 1** page, next to **Microsoft Windows Server 2016 Base \- ami\-*xxxxxxxx*** choose **Select**\.

1. On the **Step 2** page, select **t2\.micro** \(note, you can choose a larger instance type\), and then choose **Next: Configure Instance Details**\.

1. On the **Step 3** page, do the following:

   + For **Network**, choose the VPC that ends with **AWS\-DS\-VPC** \(for example, **vpc\-*xxxxxxxx* | AWS\-DS\-VPC**\)\.

   + For **Subnet** choose **Public subnet 1**, which should be preconfigured for your preferred Availability Zone \(for example, **subnet\-*xxxxxxxx* | Public subnet1 | *us\-west\-2a***\)\. 

   + For **Auto\-assign Public IP**, choose **Enable** \(if the subnet setting is not set to enable by default\)\.

   + For **Domain join directory**, choose **corp\.example\.com \(d\-*xxxxxxxxxx*\)**\.

   + For **IAM role** choose **EC2DomainJoin**\.

   + Leave the rest of the settings at their defaults\.

   + Choose **Next: Add Storage**\.

1. On the **Step 4** page, leave the default settings, and then choose **Next: Add Tags**\.

1. On the **Step 5** page, choose **Add Tag**\. Under **Key** type **corp\.example\.com\-mgmt** and then choose **Next: Configure Security Group**\.

1. On the **Step 6** page, choose **Select an existing security group**, select **AWS DS RDP Security Group**, and then choose **Review and Launch** to review your instance\.

1. On the **Step 7** page, review the page, and then choose **Launch**\.

1. On the **Select an existing key pair or create a new key pair** dialog box, do the following:

   + Choose **Choose an existing key pair**\.

   + Under **Select a key pair**, choose **AWS\-DS\-KP**\.

   + Select the **I acknowledge\.\.\.** check box\.

   + Choose **Launch Instances**\.

1. Choose **View Instances** to return to the Amazon EC2 console and view the status of the deployment\.

## Install the Active Directory Tools on Your EC2 Instance<a name="installadtools"></a>

You can choose from two methods to install the Active Directory Domain Management Tools on your EC2 instance\. You can use the Server Manager UI \(recommended for this tutorial\) or Windows PowerShell\.

**To install the Active Directory Tools on your EC2 instance \(Server Manager\)**

1. In the Amazon EC2 Console, choose **Instances**, select the instance you just created, and then choose **Connect**\. 

1. In the **Connect To Your Instance** dialog box, choose **Download Remote Desktop File**\. 

1. In the **Windows Security** dialog box, type your local administrator credentials for the Windows Server computer to log in \(for example, **administrator**\)\.

1. From the **Start** menu, choose **Server Manager**\.

1. In the **Dashboard**, choose **Add Roles and Features**\.

1. In the **Add Roles and Features Wizard**, choose **Next**\. 

1. On the **Select installation type** page, choose **Role\-based or feature\-based installation**, and then choose **Next**\.

1. On the **Select destination server** page, make sure that the local server is selected, and then choose **Next**\.

1. On the **Select server roles** page, choose **Next**\. 

1. On the **Select features** page, do the following:

   + Select the **Group Policy Management** check box\.

   + Expand **Remote Server Administration Tools**, and then expand **Role Administration Tools**\.

   + Select the **AD DS and AD LDS Tools** check box\.

   + Select the **DNS Server Tools** check box\.

   + Choose **Next**\.

1. On the **Confirm installation selections** page, review the information, and then choose **Install**\. When the feature installation is finished, the following new tools or snap\-ins will be available in the Windows Administrative Tools folder in the Start menu\. 

   + Active Directory Administrative Center

   + Active Directory Domains and Trusts

   + Active Directory Module for Windows PowerShell

   + Active Directory Sites and Services

   + Active Directory Users and Computers

   + ADSI Edit

   + DNS

   + Group Policy Management

**To install the Active Directory Tools on your EC2 instance \(Windows PowerShell\) \(Optional\)**

1. Start Windows PowerShell\.

1. Type the following command\. 

   `Install-WindowsFeature -Name GPMC,RSAT-AD-PowerShell,RSAT-AD-AdminCenter,RSAT-ADDS-Tools,RSAT-DNS-Server`