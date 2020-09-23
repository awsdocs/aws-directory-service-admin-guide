# Step 2: Share Your Directory<a name="step2_share_directory"></a>

Use the following procedures to begin the directory sharing workflow from within the directory owner account\. 

**To share your directory from the directory owner account**

1. Sign into the AWS Management Console with administrator credentials in the directory owner account and open the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) at https://console\.aws\.amazon\.com/directoryservicev2/\.

1. In the navigation pane, choose **Directories**\.

1. Choose the directory ID of the AWS Managed Microsoft AD directory that you want to share\.

1. On the **Directory details** page, choose the **Scale & share** tab\.

1. In the **Shared directories** section, choose **Actions**, and then choose **Create new shared directory**\.

1. On the **Choose which AWS accounts to share with** page, choose one of the following sharing methods depending on your business needs:

   1. **Share this directory with AWS accounts inside your organization** – With this option you can select the AWS accounts you want to share your directory with from a list showing all the AWS accounts inside your AWS organization\. You must enable trusted access with AWS Directory Service before you share a directory\. For more information, see [How to Enable or Disable Trusted Access](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrate_services.html#orgs_how-to-enable-disable-trusted-access)\.
**Note**  
To use this option, your organization must have **All features** enabled, and your directory must be in the organization master account\.

      1. Under **AWS accounts in your organization**, select the AWS accounts that you want to share the directory with and click **Add**\. 

      1. Review the pricing details, and then choose **Share**\.

      1. Proceed to [Step 4](step4_test_ec2_access.md) in this guide\. Because all AWS accounts are in the same organization, you do not need to follow Step 3\.

   1. **Share this directory with other AWS accounts** \- With this option, you can share a directory with accounts inside or outside your AWS organization\. You can also use this option when your directory is not a member of an AWS organization and you want to share with another AWS account\.

      1. In **AWS account ID\(s\)**, enter all the AWS account IDs that you want to share the directory with, and then click **Add**\.

      1. In **Send a note**, type a message to the administrator in the other AWS account\. 

      1. Review the pricing details, and then choose **Share**\.

      1. Proceed to Step 3\. 

**Next Step**

[Step 3: Accept Shared Directory Invite \(Optional\)](step3_accept_invite.md)