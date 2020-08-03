# Share Your Directory<a name="ms_ad_directory_sharing"></a>

AWS Managed Microsoft AD integrates tightly with AWS Organizations to allow seamless directory sharing across multiple AWS accounts\. You can share a single directory with other trusted AWS accounts within the same organization or share the directory with other AWS accounts that are outside your organization\. You can also share your directory when your AWS account is not currently a member of an organization\. 

**Note**  
AWS charges an additional fee for directory sharing\. To learn more, see the [Pricing](https://aws.amazon.com/directoryservice/pricing/) page on the AWS Directory Service web site\.

Directory sharing makes AWS Managed Microsoft AD a more cost\-effective way of integrating with Amazon EC2 in multiple accounts and VPCs\. Directory sharing is available in all [AWS Regions where AWS Managed Microsoft AD](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) is offered\. 

**Note**  
In the AWS China \(Ningxia\) region, this feature is available only when using [AWS Systems Manager](https://aws.amazon.com/systems-manager/) \(SSM\) to seamlessly join your Amazon EC2 instances\.

For more information about directory sharing and how to extend the reach of your AWS Managed Microsoft AD directory across AWS account boundaries, see the following topics\.

**Topics**
+ [Key Directory Sharing Concepts](ms_ad_directory_sharing_key_concepts.md)
+ [Tutorial: Sharing Your AWS Managed Microsoft AD Directory for Seamless EC2 Domain\-Join](ms_ad_tutorial_directory_sharing.md)
+ [Unshare Your Directory](ms_ad_directory_sharing_unshare.md)

**Additional Resources**
+ [Use Case: Share Your Directory to Seamlessly Join Amazon EC2 Instances to a Domain Across AWS Accounts](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/usecase6.html)
+ [AWS Security Blog Article: How to Join Amazon EC2 Instances From Multiple Accounts and VPCs to a Single AWS Managed Microsoft AD Directory](https://aws.amazon.com/blogs/security/how-to-domain-join-amazon-ec2-instances-aws-managed-microsoft-ad-directory-multiple-accounts-vpcs/)
+ [Joining your Amazon RDS DB instances across accounts to a single shared domain](https://aws.amazon.com/blogs/database/joining-your-amazon-rds-instances-across-accounts-to-a-single-shared-domain/)