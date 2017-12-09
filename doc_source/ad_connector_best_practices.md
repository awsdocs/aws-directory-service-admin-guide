# Best Practices for AD Connector<a name="ad_connector_best_practices"></a>

We recommend that you follow these best practices for creating your AD Connector:

+ Each AD Connector that you create must use a different service account, even if they are connected to the same directory\.

+ If your on\-premises network has Active Directory sites defined, you must make sure the subnets in the VPC where your AD Connector resides are defined in an Active Directory site, and that there are no conflicts between the subnets in your VPC and the subnets in your other sites\. To discover domain controllers AD Connector uses the Active Directory site whose subnet IP address ranges are close to those in the VPC containing the AD Connector\. If you have a site that has subnets with the same IP address ranges as those in your VPC, the AD Connector will discover the domain controllers in that site, which may not be physically close to your region\. 

+ When using AD Connector, you must ensure that your on\-premises directory is and remains compatible with AWS Directory Services\. For more information on your responsibilities, please see our [shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model)\.