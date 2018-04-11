# Step 1: Create and Configure Your VPC<a name="gsg_create_vpc"></a>

The following sections demonstrate how to create and configure a VPC for use with AWS Directory Service\.

**Topics**
+ [Create a New VPC](#create_vpc)
+ [Add a Second Subnet](#add_subnet)

## Create a New VPC<a name="create_vpc"></a>

This tutorial uses one of the VPC creation wizards to create the following:
+ The VPC
+ One of the subnets
+ An Internet gateway

**To create your VPC using the VPC wizard**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, click **VPC Dashboard**\. If you do not already have any VPC resources, locate the **Your Virtual Private Cloud** area of the dashboard and click **Get started creating a VPC**\. Otherwise, click **Start VPC Wizard**\.

1. Select the second option, **VPC with a Single Public Subnet**, and then click **Select**\.

1. Enter the following information into the wizard and click **Create VPC**\.  
**IP CIDR block**  
`10.0.0.0/16`  
**VPC name**  
`ADS VPC`  
**Public subnet**  
`10.0.0.0/24`  
**Availability Zone**  
**No Preference**  
**Subnet name**  
`ADS Subnet 1`  
**Enable DNS hostnames**  
Leave default selection  
**Hardware tenancy**  
**Default**

1. It takes several minutes for the VPC to be created\. After the VPC is created, proceed to the following section to add a second subnet\.

## Add a Second Subnet<a name="add_subnet"></a>

AWS Directory Service requires two subnets in your VPC, and each subnet must be in a different Availability Zone\. The VPC wizard only creates one subnet, so you must manually create the second subnet, and specify a different Availability Zone than the first subnet\. Create the second subnet by performing the following steps\.

**To create a subnet**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, select **Subnets**, select the subnet with the name `ADS Subnet 1`, and select the **Summary** tab at the bottom of the page\. Make a note of the Availability Zone of this subnet\.

1. Click **Create Subnet** and enter the following information in the **Create Subnet** dialog box and click **Yes, Create**\.  
**Name tag**  
`ADS Subnet 2`  
**VPC**  
Select your VPC\. This is the VPC with the name `ADS VPC`\.  
**Availability Zone**  
Select any Availability Zone other than the one noted in step 2\. The two subnets used by AWS Directory Service must reside in different Availability Zones\.  
**CIDR Block**  
`10.0.1.0/24`