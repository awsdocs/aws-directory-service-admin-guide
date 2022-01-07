# Deploy additional domain controllers<a name="ms_ad_deploy_additional_dcs"></a>

Deploying additional domain controllers increases the redundancy, which results in even greater resilience and higher availability\. This also improves the performance of your directory by supporting a greater number of Active Directory requests\. For example, you can now use AWS Managed Microsoft AD to support multiple \.NET applications that are deployed on large fleets of Amazon EC2 and Amazon RDS for SQL Server instances\.

When you first create your directory, AWS Managed Microsoft AD deploys two domain controllers across multiple Availability Zones, which is required for highly availability purposes\. Later, you can easily deploy additional domain controllers via the AWS Directory Service console by just specifying the total number of domain controllers that you want\. AWS Managed Microsoft AD distributes the additional domain controllers to the Availability Zones and VPC subnets on which your directory is running\. 

For example, in the below illustration, DC\-1 and DC\-2 represent the two domain controllers that were originally created with your directory\. The AWS Directory Service console refers to these default domain controllers as **Required**\. AWS Managed Microsoft AD intentionally locates each of these domain controllers in separate Availability Zones during the directory creation process\. Later, you might decide to add two more domain controllers to help distribute the authentication load over peak login times\. Both DC\-3 and DC\-4 represent the new domain controllers, which the console now refers to as **Additional**\. As before, AWS Managed Microsoft AD again automatically places the new domain controllers in different Availability Zones to ensure your domain's high availability\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/ms_ad_additionaldcs.png)

This process eliminates the need for you to manually configure directory data replication, automated daily snapshots, or monitoring for the additional domain controllers\. It's also easier for you to migrate and run mission critical Active Directory–integrated workloads in the AWS Cloud without having to deploy and maintain your own Active Directory infrastructure\. You can also deploy or remove additional domain controllers for AWS Managed Microsoft AD using the [UpdateNumberOfDomainControllers](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_UpdateNumberOfDomainControllers.html) API\.

**Note**  
Additional domain controllers is a Regional feature of AWS Managed Microsoft AD\. If you are using [Multi\-Region replication](ms_ad_configure_multi_region_replication.md), the following procedures must be applied separately in each Region\. For more information, see [Global vs Regional features](multi-region-global-region-features.md)\.

## Add or remove additional domain controllers<a name="addremovedcs"></a>

Use the following procedure to deploy or remove additional domain controllers in your AWS Managed Microsoft AD directory\.

**Note**  
If you have configured your AWS Managed Microsoft AD to enable LDAPS, any additional domain controllers you add will also have LDAPS enabled automatically\. For more information, see [Enable secure LDAP \(LDAPS\)](ms_ad_ldap.md)\.

**To add or remove additional domain controllers**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservicev2/) navigation pane, choose **Directories**\.

1. On the **Directories** page, choose your directory ID\.

1. On the **Directory details** page, do one of the following:
   + If you have multiple Regions showing under **Multi\-Region replication**, select the Region where you want to add or remove domain controllers, and then choose the **Scale & share** tab\. For more information, see [Primary vs additional Regions](multi-region-global-primary-additional.md)\.
   + If you do not have any Regions showing under **Multi\-Region replication**, choose the **Scale & share** tab\.

1. In the **Domain controllers** section, choose **Edit**\.

1. Specify the number of domain controllers to add or remove from your directory, and then choose **Modify**\. 

1. When AWS Managed Microsoft AD completes the deployment process, all domain controllers show **Active** status, and both the assigned Availability Zone and VPC subnets appear\. New domain controllers are equally distributed across the Availability Zones and subnets where your directory is already deployed\.

**Note**  
After deploying additional domain controllers, you can reduce the number of domain controllers to two, which is the minimum required for fault\-tolerance and high availability purposes\.

**Related AWS Security Blog Article**
+ [How to increase the redundancy and performance of your AWS Directory Service for AWS Managed Microsoft AD by adding domain controllers](https://aws.amazon.com/blogs/security/how-to-increase-the-redundancy-and-performance-of-your-aws-directory-service-for-microsoft-ad-directory-by-adding-domain-controllers/)

## Use Amazon CloudWatch metrics to determine when to add domain controllers<a name="scaledcs"></a>

Load balancing across all of your domain controllers is important for the resilience and performance of your directory\. To help you optimize the performance of your domain controllers in AWS Managed Microsoft AD, we recommend that you first monitor important metrics in CloudWatch to form a baseline\. During this process, you analyze your directory over time to identify your average and peak directory utilization\. After determining your baseline, you can monitor these metrics on a regular basis to help determine when to add a domain controller to your directory\. For more information, see [Monitor your domain controllers with performance metrics](ms_ad_monitor_dc_performance.md)\.

The following metrics are important to monitor on a regular basis\. For a full list of available domain controller metrics in CloudWatch, see [AWS Managed Microsoft AD performance counters](#performance-counters)\. 
+ Domain controller\-specific metrics, such as:
  + Processor
  + Memory
  + Logical Disk
  + Network Interface
+ AWS Managed Microsoft AD directory\-specific metrics, such as:
  + LDAP searches
  + Binds
  + DNS queries
  + Directory reads
  + Directory writes

For instructions on how to set up domain controller metrics using the CloudWatch console, see [How to automate AWS Managed Microsoft AD scaling based on utilization metrics](https://aws.amazon.com/blogs/security/how-to-automate-aws-managed-microsoft-ad-scaling-based-on-utilization-metrics/) in the AWS Security Blog\. For general information about metrics in CloudWatch, see [Using Amazon CloudWatch metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) in the *Amazon CloudWatch User Guide*\. 

For general information about domain controller planning, see [Capacity planning for Active Directory Domain Services](https://docs.microsoft.com/en-us/windows-server/administration/performance-tuning/role/active-directory-server/capacity-planning-for-active-directory-domain-services) on the Microsoft website\.

### AWS Managed Microsoft AD performance counters<a name="performance-counters"></a>

The following table lists all performance counters available in Amazon CloudWatch for tracking domain controller and directory performance in AWS Managed Microsoft AD\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_deploy_additional_dcs.html)