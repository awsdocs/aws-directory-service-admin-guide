# Admin Account<a name="admin_permissions"></a>

When you create an AWS Directory Service for Microsoft Active Directory directory, AWS creates an organizational unit \(OU\) that contains all your directory’s objects\. This OU, which has the NetBIOS name that you typed when you created your directory, is located in the domain root\. The domain root is owned and managed by AWS\.

The *admin* account that was created with your Microsoft AD has permissions for the most common administrative activities for your OU:

+ Add, update, or delete users, groups, and computers\. For more information, see [Add Users and Groups \(Simple AD and Microsoft AD\)](creating_ad_users_and_groups.md)\. 

+ Add resources to your domain such as file or print servers, and then assign permissions for those resources to users and groups in your OU\.

+ Create additional OUs and containers\.

+ Delegate authority\. For more information, see [Overview of Managing Access Permissions to Your AWS Directory Service Resources](UsingWithDS_IAM_AccessControl_Overview.md)\.

+ Create and link group policies\.

+ Restore deleted objects from the Active Directory Recycle Bin\.

+ Run AD and DNS Windows PowerShell modules on the Active Directory Web Service\.

+ Create and configure group Managed Service Accounts\. For more information, see [Group Managed Service Accounts](#gmsa)\.

+ Configure Kerberos constrained delegation\. For more information, see [Kerberos Constrained Delegation](#kcd)\.

The admin account also has rights to perform the following domain\-wide activities:

+ Manage DNS configurations \(Add, remove, or update records, zones and forwarders\)\.

+ View DNS event logs\.

+ View security event logs\.

Actions not listed here are not allowed for the admin account\. The admin account also lacks permissions for any directory\-related actions outside of your specific OU, such as on the parent OU\.

**Important**  
AWS Domain Administrators have full administrative access to all domains hosted on AWS\. See your agreement with AWS and the [AWS Data Protection FAQ](https://aws.amazon.com/compliance/data-privacy-faq/) for more information about how AWS handles content, including directory information, that you store on AWS systems\.

## Group Managed Service Accounts<a name="gmsa"></a>

With Windows Server 2012, Microsoft introduced a new method that administrators could use to manage service accounts called group Managed Service Accounts \(gMSAs\)\. Using gMSAs, password synchronization between service instances no longer needed to be manually managed by service administrators\. Instead, an admin could simply create a gMSA in AD and then configure multiple service instances to use that single gMSA\. 

To grant permissions so users in Microsoft AD can create a gMSA, you must add their accounts as a member of the *Managed Service Accounts Admins* security group\. By default, the Admin account is a member of this group\. For more information about gMSAs, see [Group Managed Service Accounts Overview](https://technet.microsoft.com/en-us/library/hh831782(v=ws.11).aspx) on the Microsoft TechNet website\. 

## Kerberos Constrained Delegation<a name="kcd"></a>

Kerberos constrained delegation is a feature in Windows Server that gives service administrators the ability to specify and enforce application trust boundaries by limiting the scope where application services can act on a user’s behalf\. This can be useful when you need to configure which front\-end service accounts can delegate to their back\-end services\. Kerberos constrained delegation also prevents your gMSA from connecting to any and all services on behalf of your AD users, avoiding the potential for abuse by a rogue developer\.

For example, let’s say user jsmith logs into an HR application\. You want the SQL Server to apply jsmith’s database permissions\. However, by default SQL Server opens the database connection using the service account credentials applying hr\-app\-service’s permissions, instead of jsmith’s configured permissions\. To make it possible for the HR payroll application to access the SQL Server database using the jsmith’s credentials you must enable Kerberos constrained delegation for the hr\-app\-service service account on your Microsoft AD directory in AWS\. When jsmith logs on, Active Directory provides a Kerberos ticket that Windows automatically uses when jsmith attempts to access other services in the network\. Kerberos delegation enables the hr\-app\-service account to reuse the jsmith Kerberos ticket when accessing the database, thus applying permissions specific to jsmith when opening the database connection\.

To grant permissions so users in Microsoft AD can configure Kerberos constrained delegation, you must add their accounts as a member of the *Kerberos Delegations Admins* security group\. By default, the Admin account is a member of this group\. For more information about Kerberos constrained delegation, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/en-us/library/jj553400(v=ws.11).aspx) on the Microsoft TechNet website\.