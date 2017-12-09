# What Gets Created<a name="create_details_simple"></a>

When you create a directory with Simple AD, AWS Directory Service performs the following tasks on your behalf:

+ Sets up a Samba\-based directory within the VPC\.

+ Creates a directory administrator account with the user name `Administrator` and the specified password\. You use this account to manage your directory\.
**Important**  
Be sure to save this password\. AWS Directory Service does not store this password and it cannot be retrieved or reset\.

+ Creates a security group for the directory controllers\. 

+ Creates an account with the name `AWSAdminD-xxxxxxxx` that has domain admin privileges\. This account is used by AWS Directory Service to perform automated operations for directory maintenance operations, such as taking directory snapshots and FSMO role transfers\. The credentials for this account are securely stored by AWS Directory Service\.