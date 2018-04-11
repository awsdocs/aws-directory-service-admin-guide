# Create a DHCP Options Set<a name="dhcp_options_set"></a>

AWS recommends that you create a DHCP options set for your AWS Directory Service directory and assign the DHCP options set to the VPC that your directory is in\. This allows any instances in that VPC to point to the specified domain and DNS servers to resolve their domain names\.

 For more information about DHCP options sets, see [DHCP Options Sets](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_DHCP_Options.html) in the *Amazon VPC User Guide*\.

**To create a DHCP options set for your directory**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **DHCP Options Sets** in the navigation pane, and choose **Create DHCP options set**\.

1. In the **Create DHCP options set** dialog box, enter the following values for your directory:  
**Name tag**  
An optional tag for the options set\.  
**Domain name**  
The fully\-qualified name of your directory, such as `corp.example.com`\.  
**Domain name servers**  
The IP addresses of your directory's DNS servers\. These are the IP addresses of your AWS\-provided directory\. You can find these addresses by going to the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, selecting **Directories** and then choosing the correct directory ID\.  
**NTP servers**  
Leave this field blank\.  
**NetBIOS name servers**  
Leave this field blank\.  
**NetBIOS node type**  
Leave this field blank\.

1. Choose **Yes, Create**\. The new set of DHCP options appears in your list of DHCP options\.

1. Make a note of the ID of the new set of DHCP options \(dopt\-*xxxxxxxx*\)\. You need it to associate the new options set with your VPC\.

**To change the DHCP options set associated with a VPC**

After you create a set of DHCP options, you can't modify them\. If you want your VPC to use a different set of DHCP options, you must create a new set and associate them with your VPC\. You can also set up your VPC to use no DHCP options at all\.

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **Your VPCs** in the navigation pane\.

1. Select the VPC, and choose **Edit DHCP Options Set** from the **Actions** list\.

1. In the **DHCP Options Set** list, select the desired options set from the list, and choose **Save**\.