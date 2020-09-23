# Delegate Directory Join Privileges for Simple AD<a name="simple_ad_directory_join_privileges"></a>

To join a computer to your directory, you need an account that has privileges to join computers to the directory\. 

With Simple AD, members of the **Domain Admins** group have sufficient privileges to join computers to the directory\.

However, as a best practice, you should use an account that has only the minimum privileges necessary\. The following procedure demonstrates how to create a new group called `Joiners` and delegate the privileges to this group that are needed to join computers to the directory\.

You must perform this procedure on a computer that is joined to your directory and has the **Active Directory User and Computers** MMC snap\-in installed\. You must also be logged in as a domain administrator\.

**To delegate join privileges for Simple AD**

1. Open **Active Directory User and Computers** and select your domain root in the navigation tree\.

1. In the navigation tree on the left, open the context menu \(right\-click\) for **Users**, choose **New**, and then choose **Group**\. 

1. In the **New Object \- Group** box, type the following and choose **OK**\.
   + For **Group name**, type **Joiners**\.
   + For **Group scope**, choose **Global**\.
   + For **Group type**, choose **Security**\.

1. In the navigation tree, select your domain root\. From the **Action** menu, choose **Delegate Control**\.

1. On the **Delegation of Control Wizard** page, choose **Next**, and then choose **Add**\.

1. In the **Select Users, Computers, or Groups** box, type `Joiners` and choose **OK**\. If more than one object is found, select the `Joiners` group created above\. Choose **Next**\.

1. On the **Tasks to Delegate** page, select **Create a custom task to delegate**, and then choose **Next**\.

1. Select **Only the following objects in the folder**, and then select **Computer objects**\. 

1. Select **Create selected objects in this folder** and **Delete selected objects in this folder**\. Then choose **Next**\.  
![\[Object type\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/aduc_delegate_join_linux.png)

1. Select **Read** and **Write**, and then choose **Next**\.  
![\[Object type\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/aduc_delegate_join_permissions.png)

1. Verify the information on the **Completing the Delegation of Control Wizard** page and choose **Finish**\. 

1. Create a user with a strong password and add that user to the `Joiners` group\. The user will then have sufficient privileges to connect AWS Directory Service to the directory\.