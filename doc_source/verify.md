# Step 3: Verify If The Schema Extension Was Successful<a name="verify"></a>

After you have finished the import process, it is important to verify that schema updates were applied to your directory\. This is especially critical before you migrate or update any application that relies on the schema update\. You can do this using a variety of different LDAP tools or by writing a test tool that issues the appropriate LDAP commands\. 

This procedure uses the Active Directory Schema Snap\-in and/or PowerShell to verify that the schema updates were applied\. You must run these tools from a computer that is domain joined to your AWS Managed Microsoft AD\. This can be a Windows server running in your on\-premises network with access to your virtual private cloud \(VPC\) or through a virtual private network \(VPN\) connection\. You can also run these tools on an Amazon EC2 Windows instance \(see [How to launch a new EC2 instance with Seamless Domain Join](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-join-aws-domain.html#join-domain-console)\)\.

**To verify using the Active Directory Schema Snap\-in**

1. Install the Active Directory Schema Snap\-In using the instructions on the [TechNet](https://technet.microsoft.com/en-us/library/cc732110.aspx) website\. 

1. Open the Microsoft Management Console \(MMC\) and expand the **AD Schema** tree for your directory\. 

1. Navigate through the **Classes** and **Attributes** folders until you find the schema changes that you made earlier\.

**To verify using PowerShell**

1. Open a PowerShell window\.

1. Use the `Get-ADObject` cmdlet as shown below to verify the schema change\. For example:

   `get-adobject -Identity 'CN=Shoe-Size,CN=Schema,CN=Configuration,DC=example,DC=com' -Properties *`

**Optional Step**

[\(Optional\) Add a value to the new attribute](addvalue.md)