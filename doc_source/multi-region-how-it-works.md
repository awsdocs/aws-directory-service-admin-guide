# How multi\-Region replication works<a name="multi-region-how-it-works"></a>

With the multi\-Region replication feature, AWS Managed Microsoft AD eliminates the undifferentiated heavy lifting of managing a global AD infrastructure\. When configured, AWS replicates all customer directory data including users, groups, group policies, and schema across multiple AWS Regions\.

Once a new Region has been added, the following operations automatically occur as shown in the illustration:
+ AWS Managed Microsoft AD creates two domain controllers in the selected VPC and deploys them to the new Region in the same AWS account\. Your directory identifier \(`directory_id`\) remains the same across all Regions\. You can add additional domain controllers later if you want\.
+ AWS Managed Microsoft AD configures the networking connection between the primary Region and the new Region\. 
+ AWS Managed Microsoft AD creates a new Active Directory site and gives it the same name as the Region, such as us\-east\-1\. You can also rename this later using the Active Directory Sites and Services tool\.
+ AWS Managed Microsoft AD replicates all AD objects and configurations to the new Region, including users, groups, group policies, AD trusts, organizational units, and AD schema\. Active Directory site links are configured to use [Change Notification](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961787(v=technet.10)?redirectedfrom=MSDN#change-notification)\. With change notification between sites enabled, changes propagate to the remote site with the same frequency that they are propagated within the source site, including changes that warrant urgent replication\.
+ If this is the first Region you've added, AWS Managed Microsoft AD makes all features multi\-Region aware\. For more information, see [Global vs Regional features](multi-region-global-region-features.md)\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/multiregion.png)

## Active Directory sites<a name="multi-region-sites"></a>

Multi\-Region replication supports multiple Active Directory sites \(one AD site per Region\)\. When a new Region is added, it is given the same name as the Region—for example, us\-east\-1\. You can also rename this later using Active Directory Sites and Services\.

## AWS services<a name="multi-region-services"></a>

AWS services such as Amazon RDS for SQL Server and Amazon FSx connect to the local instances of the global directory\. This allows your users to sign in once to AD\-aware applications that run in AWS as well as AWS services like Amazon RDS for SQL Server in any AWS Region\. To do so, users need credentials from AWS Managed Microsoft AD or on\-premises Active Directory when you have a trust with your AWS Managed Microsoft AD\.

You can use the following AWS services with the multi\-Region replication feature\.
+ Amazon EC2
+ Amazon FSx for Windows File Server
+ Amazon RDS for SQL Server
+ Amazon RDS for Oracle
+ Amazon RDS for MySQL
+ Amazon RDS for PostgreSQL
+ Amazon RDS for MariaDB
+ Amazon Aurora for MySQL
+ Amazon Aurora for PostgreSQL

## Failover<a name="multi-region-failover"></a>

In the event that all domain controllers in one Region are down, AWS Managed Microsoft AD recovers the domain controllers and replicates the directory data automatically\. Meanwhile domain controllers in other Regions stay up and running\.