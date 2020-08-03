# What Gets Created<a name="create_details_simple"></a>

When you create a directory with Simple AD, AWS Directory Service performs the following tasks on your behalf:
+ Sets up a Samba\-based directory within the VPC\.
+ Creates a directory administrator account with the user name `Administrator` and the specified password\. You use this account to manage your directory\.
**Important**  
Be sure to save this password\. AWS Directory Service does not store this password, and it cannot be retrieved\. However, you can reset a password from the AWS Directory Service console or by using the [ResetUserPassword](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ResetUserPassword.html) API\.
+ Creates a security group for the directory controllers\. 
+ Creates an account with the name `AWSAdminD-xxxxxxxx` that has domain admin privileges\. This account is used by AWS Directory Service to perform automated operations for directory maintenance operations, such as taking directory snapshots and FSMO role transfers\. The credentials for this account are securely stored by AWS Directory Service\.
+ Automatically creates and associates an elastic network interface \(ENI\) with each of your domain controllers\. Each of these ENIs are essential for connectivity between your VPC and AWS Directory Service domain controllers and should never be deleted\. You can identify all network interfaces reserved for use with AWS Directory Service by the description: "AWS created network interface for directory *directory\-id*"\. For more information, see [Elastic Network Interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) in the Amazon EC2 User Guide for Windows Instances\.