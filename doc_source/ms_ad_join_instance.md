# Join an EC2 Instance to Your AWS Managed Microsoft AD Directory<a name="ms_ad_join_instance"></a>

You can seamlessly join an EC2 instance to your directory domain when the instance is launched using AWS Systems Manager\. For more information, see [Seamlessly Joining a Windows Instance to an AWS Directory Service Domain](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-join-aws-domain.html) in the *Amazon EC2 User Guide for Windows Instances*\.

If you need to manually join an EC2 instance to your domain, you must launch the instance in the proper Region and security group or subnet, then join the instance to the domain\.

To be able to connect remotely to these instances, you must have IP connectivity to the instances from the network you are connecting from\. In most cases, this requires that an internet gateway be attached to your VPC and that the instance has a public IP address\.

**Topics**
+ [Seamlessly Join a Windows EC2 Instance](launching_instance.md)
+ [Manually Join a Windows Instance](join_windows_instance.md)
+ [Seamlessly Join a Linux EC2 Instance to Your AWS Managed Microsoft AD Directory](seamlessly_join_linux_instance.md)
+ [Manually Join a Linux Instance](join_linux_instance.md)
+ [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)
+ [Create a DHCP Options Set](dhcp_options_set.md)