# \(Optional\) Add a value to the new attribute<a name="addvalue"></a>

Use this optional step when you have created a new attribute and want to add a new value to the attribute in your AWS Managed Microsoft AD directory\.

**To add a value to an attribute**

1. Open the Windows PowerShell command line utility and set the new attribute with the following command\. In this example, we will add a new EC2InstanceID value to the attribute for a specific computer\.

   `PS C:\> set-adcomputer -Identity computer name -add @{example-EC2InstanceID = 'EC2 instance ID'}`

1. You can validate if the EC2InstanceID value was added to the computer object by running the following command:

   `PS C:\> get-adcomputer -Identity computer name –Property example-EC2InstanceID`