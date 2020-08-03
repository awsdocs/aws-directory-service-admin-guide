# Step 1: Set Up Your Networking Environment<a name="step1_setup_networking"></a>

Before you begin the steps in this tutorial, you must first do the following:
+ Create two new AWS accounts for testing purposes in the same Region\. When you create an AWS account, it automatically creates a dedicated virtual private cloud \(VPC\) in each account\. Take note of the VPC ID in each account\. You will need this later\.
+ Create a VPC peering connection between the two VPCs in each account using the procedures in this step\. 
**Note**  
While there are many ways to connect Directory owner and Directory consumer account VPCs, this tutorial will use the VPC peering method\. For additional VPC connectivity options, see [Network Connectivity](ms_ad_directory_sharing_key_concepts.md#network_connectivity)\.

## Configure a VPC Peering Connection between the Directory Owner and the Directory Consumer account<a name="step1_configure_owner_account_vpc"></a>

The VPC peering connection you will create is between the directory consumer and directory owner VPCs\. Follow these steps to configure a VPC peering connection for connectivity with the directory consumer account\. With this connection you can route traffic between both VPCs using private IP addresses\.

**To create a VPC peering connection between the directory owner and directory consumer account**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. Makes sure to sign in as a user with administrator credentials in the directory owner account\.

1. In the navigation pane, choose **Peering Connections**\. Then choose **Create Peering Connection**\.

1. Configure the following information:
   + **Peering connection name tag**: Provide a name that clearly identifies this connection with the VPC in the directory consumer account\. 
   + **VPC \(Requester\)**: Select the VPC ID for the directory owner account\. 
   + Under **Select another VPC to peer with**, ensure that **My account** and **This region** are selected\.
   + **VPC \(Accepter\)**: Select the VPC ID for the directory consumer account\. 

1. Choose **Create Peering Connection**\. In the confirmation dialog box, choose **OK**\.

Since both VPCs are in the same Region, the administrator of the directory owner account who sent the VPC peering request can also accept the peering request on behalf of the directory consumer account\.

**To accept the peering request on behalf of the directory consumer account**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\. 

1. In the navigation pane, choose **Peering Connections**\.

1. Select the pending VPC peering connection\. \(Its status is Pending Acceptance\.\) Choose **Actions**, **Accept Request**\.

1. In the confirmation dialog, choose **Yes, Accept**\. In the next confirmation dialog box, choose **Modify my route tables now** to go directly to the route tables page\.

Now that your VPC peering connection is active, you must add an entry to your VPC route table in the directory owner account\. Doing so enables traffic to be directed to the VPC in the directory consumer account\.

**To add an entry to the VPC route table in the directory owner account**

1. While in the **Route Tables** section of the Amazon VPC console, select the route table for the directory owner VPC\.

1. Choose the **Routes** tab, choose **Edit**, and then choose **Add another route**\.

1. In the **Destination** column, enter the CIDR block for the directory consumer VPC\.

1. In the **Target** column, enter the VPC peering connection ID \(such as **pcx\-123456789abcde000**\) for the peering connection that you created earlier in the directory owner account\.

1. Choose **Save**\.

**To add an entry to the VPC route table in the directory consumer account**

1. While in the **Route Tables** section of the Amazon VPC console, select the route table for the directory consumer VPC\.

1. Choose the **Routes** tab, choose **Edit**, and then choose **Add another route**\.

1. In the **Destination** column, enter the CIDR block for the directory owner VPC\.

1. In the **Target** column, type in the VPC peering connection ID \(such as **pcx\-123456789abcde001**\) for the peering connection that you created earlier in the directory consumer account\.

1. Choose **Save**\.

Make sure to configure your directory consumer VPCs’ security group to enable outbound traffic by adding the Active Directory protocols and ports to the outbound rules table\. For more information, see [Security Groups for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) and [AWS Managed Microsoft AD Prerequisites](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_getting_started_prereqs.html)\.

**Next Step**

[Step 2: Share Your Directory](step2_share_directory.md)