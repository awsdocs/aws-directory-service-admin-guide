# Rename Your Directory's Site Name<a name="ms_ad_rename_site"></a>

You can rename your AWS Managed Microsoft AD directory’s default site name so that it matches with your existing Microsoft Active Directory \(AD\) site names\. This makes it faster for AWS Managed Microsoft AD to find and authenticate your existing AD users in your on\-premises directory\. The result is a better experience when users login to AWS resources such as [Amazon EC2](https://aws.amazon.com/ec2/) and [Amazon RDS for SQL Server](https://aws.amazon.com/rds/sqlserver/) instances that you have joined to your AWS Managed Microsoft AD directory\.

To do that, you must be logged in with the **Admin** account or with an account that is a member of the **AWS Delegated Sites and Services Administrators** group\. For more information about this group, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

For additional benefits on renaming your site in relation to trusts, see [Domain Locator Across a Forest Trust](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/domain-locator-across-a-forest-trust/ba-p/395689) on Microsoft's website\.

**To rename the AWS Managed Microsoft AD site name**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Locate an Amazon EC2 instance that is joined to your AWS Managed Microsoft AD directory\. Select the instance and then choose **Connect**\.

1. In the **Server Manager** window, choose **Tools**\. Then choose **Active Directory Sites and Services**\. 

1. In the left pane, expand the **Sites** folder, right\-click the site name \(default is **Default\-Site\-Name**\), and then choose **Rename**\.

1. Type the new site name, and then choose **Enter**\.