# Group Managed Service Accounts<a name="ms_ad_key_concepts_gmsa"></a>

With Windows Server 2012, Microsoft introduced a new method that administrators could use to manage service accounts called group Managed Service Accounts \(gMSAs\)\. Using gMSAs, service administrators no longer needed to manually manage password synchronization between service instances\. Instead, an administrator could simply create a gMSA in Active Directory and then configure multiple service instances to use that single gMSA\. 

To grant permissions so users in AWS Managed Microsoft AD can create a gMSA, you must add their accounts as a member of the *AWS Delegated Managed Service Account Administrators* security group\. By default, the Admin account is a member of this group\. For more information about gMSAs, see [Group Managed Service Accounts Overview](https://technet.microsoft.com/en-us/library/hh831782(v=ws.11).aspx) on the Microsoft TechNet website\. 

**Related AWS Security Blog post**
+ [How AWS Managed Microsoft AD Helps to Simplify the Deployment and Improve the Security of Active Directory–Integrated \.NET Applications](https://aws.amazon.com/blogs/security/how-aws-managed-microsoft-ad-helps-to-simplify-the-deployment-and-improve-the-security-of-active-directory-integrated-net-applications/)