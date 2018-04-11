# Add Alternate UPN Suffixes<a name="ms_ad_upn_suffixes"></a>

You can simplify the management of Active Directory \(AD\) login names and improve the user login experience by adding alternate user principal name \(UPN\) suffixes to your AWS Managed Microsoft AD directory\. To do that, you must be logged on with the **Admin** account or with an account that is a member of the **AWS Delegated User Principal Name Suffix Administrators** group\. For more information about this group, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

**To add alternate UPN suffixes**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. Locate an Amazon EC2 instance that is joined to your AWS Managed Microsoft AD directory\. Select the instance and then choose **Connect**\.

1. In the **Server Manager** window, choose **Tools**\. Then choose **Active Directory Domains and Trusts**\. 

1. In the left pane, right\-click **Active Directory Domains and Trusts** and then choose **Properties** \.

1. In the **UPN Suffixes** tab, type an alternative UPN suffix \(such as **sales\.example\.com**\)\. Choose **Add** and then choose **Apply**\.

1. If you need to add additional alternative UPN suffixes, repeat step 5 until you have the UPN suffixes you require\.