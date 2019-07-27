# Step 1: Set Up Your AWS Environment for AWS Managed Microsoft AD<a name="microsoftadbasestep1"></a>

Before you can create AWS Managed Microsoft AD in your AWS test lab, you first need to set up your Amazon EC2 key pair so that all login data is encrypted\.

## Create a Key Pair<a name="createkeypair2"></a>

If you already have a key pair, you can skip this step\. For more information about Amazon EC2 key pairs, see [http://docs\.aws\.amazon\.com/AWSEC2/latest/UserGuide/ec2\-key\-pairs\.html](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)\.

**To create a key pair**

1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, under **Network & Security**, choose **Key Pairs**, and then choose **Create Key Pair**\.

1. For **Key pair name**, type **AWS\-DS\-KP**, and then choose **Create**\.

1. The private key file is automatically downloaded by your browser\. The file name is the name you specified when you created your key pair with an extension of `.pem`\. Save the private key file in a safe place\.
**Important**  
This is the only chance for you to save the private key file\. You need to provide the name of your key pair when you launch an instance and the corresponding private key each time you decrypt the password for the instance\.

## Create a VPC<a name="createvpc"></a>

In this procedure you use a AWS CloudFormation template to create your VPC network\. For more information about how this template works, see [Amazon VPC QuickStart guide](https://aws.amazon.com/quickstart/architecture/vpc/)\. For this tutorial, we will set up a public VPC\. However you can make your VPC a private VPC as long as you create a network path to your VPC with Amazon Direct Connect, or with a Virtual Private Network \(VPN\) connection\.

If you would like to use the default VPC \(172\.31\.0\.0/16\), you can advance to the next section\. All of the AWS CLI and PowerShell examples use custom VPC information\. For more information, see [Amazon Virtual Private Cloud \(Amazon VPC\)](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html)\.

**To create a VPC**

1. Launch the AWS CloudFormation template into your AWS account\. Click [here](https://fwd.aws/mm853) while signed on to your account\.

   The template is launched in the US West \(Oregon\) Region by default\. To change the region, use the region selector in the navigation bar\. This stack takes approximately five minutes to create\.

1. On the **Select Template** page, keep the default setting for the Amazon S3 template URL and then choose **Next**\.

1. On the **Specify Details** page, set the stack name to **AWS\-DS\-VPC**\. Then do the following:
   + Under **Availability Zone Configuration** select two zones in your area\. Then for **Number of Availability Zones** select **2**\.
   + Under **Network Configuration**, set **Create private subnets** to **false**\. Then in **Create additional private subnets with dedicated network ACLs**, select **false**\.
   + Under **Amazon EC2 Configuration**, set **Key pair name** to **AWS\-DS\-KP** or use an existing key pair\.

1. Review your information, and then choose **Next**\.

1. On the **Options** page, choose **Next**\.

1. On the **Review** page, choose **Create**\.

## Create a Security Group for EC2 Instances<a name="createsecuritygroup"></a>

By default, AWS Managed Microsoft AD creates a security group to manage traffic between its domain controllers\. In this procedure, you create a security group that manages traffic within your VPC for your EC2 instances\. You also add a rule that allows RDP \(3389\) inbound from anywhere and for all traffic types inbound from the local VPC\. For more information, see [Amazon EC2 Security Groups for Windows Instances](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-network-security.html)\.

**To create a security group for EC2 instances**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Under **Security**, choose **Security Groups**\.

1. Choose **Create Security Group**\.

1. In the **Create Security Group** dialog box provide the following values:
   + For **Security group name**, type **AWS DS RDP Security Group**\.
   + For **Description**, type **AWS DS RDP Security Group**\.
   + For **VPC**, select the VPC that ends with **AWS\-DS\-VPC**\.

1. Choose **Create**\.

1. Select **AWS DS RDP Security Group**\.

1. Choose the **Inbound Rules** tab below the list of security groups\.

1. Choose **Edit rules**, and then choose **Add Rule**\.

1. In the table, add the following values:
   + For **Type**, choose **RDP \(3389\)**\.
   + For **Protocol**, verify that **TCP \(6\)** is displayed\.
   + For **Port Range**, verify that **3389** is displayed\.
   + For **Source**, specify a single IP address, or an IP address range in CIDR notation \(for example, 203\.0\.113\.5/32\)\. You can also specify the name or ID of another security group in the same region\. This setting determines the traffic that can reach your EC2 instances\. For more information, see [Understand Your Directory’s AWS Security Group Configuration and Use](ms_ad_best_practices.md#understandsecuritygroup)\.

1. Choose **Add Rule**, and then provide the following values:
   + For **Type**, choose **All Traffic**\.
   + For **Protocol**, verify that **All** is displayed\.
   + For **Port Range**, verify that **All** is displayed\.
   + For **Source**, type **10\.0\.0\.0/16**\.

1. Choose **Save rules**\.