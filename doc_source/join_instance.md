# Join an EC2 Instance to Your Directory \(Simple AD and Microsoft AD\)<a name="join_instance"></a>

You can seamlessly join an EC2 instance to your directory domain when the instance is launched using the Amazon EC2 Systems Manager\. For more information, see [Seamlessly Joining a Windows Instance to an AWS Directory Service Domain](http://alpha-docs-aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-join-aws-domain.html) in the *Amazon EC2 User Guide for Windows Instances*\.

If you need to manually join an EC2 instance to your domain, you must launch the instance in the proper region and security group or subnet, then join the instance to the domain\.

To be able to connect remotely to these instances, you must have IP connectivity to the instances from the network you are connecting from\. In most cases, this requires that an Internet gateway be attached to your VPC and that the instance has a public IP address\.


+ [Launching an Instance \(Simple AD and Microsoft AD\)](launching_instance.md)
+ [Manually Add a Windows Instance \(Simple AD and Microsoft AD\)](join_windows_instance.md)
+ [Manually Add a Linux Instance \(Simple AD and Microsoft AD\)](join_linux_instance.md)
+ [Delegating Directory Join Privileges \(Simple AD and Microsoft AD\)](directory_join_privileges.md)
+ [Using DNS with Simple AD and Microsoft AD](dns_with_simple_ad.md)
+ [DHCP Options Set](dhcp_options_set.md)