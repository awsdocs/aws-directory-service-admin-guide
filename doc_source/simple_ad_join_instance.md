# Join an EC2 instance to your Simple AD directory<a name="simple_ad_join_instance"></a>

You can seamlessly join an EC2 instance to your directory domain when the instance is launched using AWS Systems Manager\. For more information, see [Seamlessly joining a Windows instance to an AWS Directory Service domain](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-join-aws-domain.html) in the *Amazon EC2 User Guide for Windows Instances*\.

If you need to manually join an EC2 instance to your domain, you must launch the instance in the proper Region and security group or subnet, then join the instance to the domain\.

To be able to connect remotely to these instances, you must have IP connectivity to the instances from the network you are connecting from\. In most cases, this requires that an internet gateway be attached to your VPC and that the instance has a public IP address\.

**Topics**
+ [Seamlessly join a Windows EC2 instance](simple_ad_launching_instance.md)
+ [Manually join a Windows instance](simple_ad_join_windows_instance.md)
+ [Seamlessly join a Linux EC2 instance to your Simple AD directory](simple_ad_seamlessly_join_linux_instance.md)
+ [Manually join a Linux instance](simple_ad_join_linux_instance.md)
+ [Delegate directory join privileges for Simple AD](simple_ad_directory_join_privileges.md)
+ [Create a DHCP options set](simple_ad_dhcp_options_set.md)