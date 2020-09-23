# Create a DHCP Options Set<a name="dhcp_options_set"></a>

AWS recommends that you create a DHCP options set for your AWS Directory Service directory and assign the DHCP options set to the VPC that your directory is in\. This allows any instances in that VPC to point to the specified domain and DNS servers to resolve their domain names\.

 For more information about DHCP options sets, see [DHCP Options Sets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_DHCP_Options.html) in the *Amazon VPC User Guide*\.

**To create a DHCP options set for your directory**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **DHCP Options Sets**, and then choose **Create DHCP options set**\.

1. On the **Create DHCP options set** page, enter the following values for your directory:  
**Name**  
An optional tag for the options set\.  
**Domain name**  
The fully qualified name of your directory, such as `corp.example.com`\.  
**Domain name servers**  
The IP addresses of your AWS\-provided directory's DNS servers\.   
You can find these addresses by going to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, selecting **Directories** and then choosing the correct directory ID\.  
**NTP servers**  
Leave this field blank\.  
**NetBIOS name servers**  
Leave this field blank\.  
**NetBIOS node type**  
Leave this field blank\.

1. Choose **Create DHCP options set**\. The new set of DHCP options appears in your list of DHCP options\.

1. Make a note of the ID of the new set of DHCP options \(dopt\-*xxxxxxxx*\)\. You use it to associate the new options set with your VPC\.

**To change the DHCP options set associated with a VPC**

After you create a set of DHCP options, you can't modify them\. If you want your VPC to use a different set of DHCP options, you must create a new set and associate them with your VPC\. You can also set up your VPC to use no DHCP options at all\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. In the navigation pane, choose **Your VPCs**

1. Select the VPC, and then choose **Actions**, **Edit DHCP options set**\.

1. For **DHCP options set**, select an options set or choose **No DHCP options set**, and then choose **Save**\.