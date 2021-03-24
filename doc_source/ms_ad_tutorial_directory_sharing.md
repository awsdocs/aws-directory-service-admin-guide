# Tutorial: Sharing your AWS Managed Microsoft AD directory for seamless EC2 domain\-join<a name="ms_ad_tutorial_directory_sharing"></a>

This tutorial shows you how to share your AWS Managed Microsoft AD directory \(the directory owner account\) with another AWS account \(the directory consumer account\)\. Once the networking prerequisites have been completed, you will share a directory between two AWS accounts\. Then you'll learn how to seamlessly join an EC2 instance to a domain in the directory consumer account\.

We recommend that you first review directory sharing key concepts and use case content before you start work on this tutorial\. For more information, see [Key directory sharing concepts](ms_ad_directory_sharing_key_concepts.md)\.

The process for sharing your directory differs depending on whether you share the directory with another AWS account in the same AWS organization or with an account that is outside of the AWS organization\. For more information about how sharing works, see [Sharing methods](ms_ad_directory_sharing_key_concepts.md#sharing_methods)\.

This workflow has four basic steps\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/directory_sharing_tutorial3.png)

**[Step 1: Set up your networking environment](step1_setup_networking.md)**  
In the directory owner account, you set up all of the networking prerequisites necessary for the directory sharing process\. 

**[Step 2: Share your directory](step2_share_directory.md)**  
While signed in with directory owner administrator credentials, you open the AWS Directory Service console and start the share directory workflow, which sends an invitation to the directory consumer account\.

**[Step 3: Accept shared directory invite \(optional\)](step3_accept_invite.md)**  
While signed in with directory consumer administrator credentials, you open the AWS Directory Service console and accept the directory sharing invite\.

**[Step 4: Test seamlessly joining an EC2 instance for Windows Server to a domain](step4_test_ec2_access.md)**  
Finally, as the directory consumer administrator, you attempt to join an EC2 instance to your domain and verify that it works\.

**Additional resources**
+ [Use case: Share your directory to seamlessly join Amazon EC2 instances to a domain across AWS accounts](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/usecase6.html)
+ [AWS Security Blog Article: How to Join Amazon EC2 Instances From Multiple Accounts and VPCs to a Single AWS Managed Microsoft AD Directory](https://aws.amazon.com/blogs/security/how-to-domain-join-amazon-ec2-instances-aws-managed-microsoft-ad-directory-multiple-accounts-vpcs/)