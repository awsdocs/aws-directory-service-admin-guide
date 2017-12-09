# Using Identity\-Based Policies \(IAM Policies\) for AWS Directory Service<a name="UsingWithDS_IAM_AccessControl_IdentityBased"></a>

This topic provides examples of identity\-based policies in which an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS Directory Service resources\. For more information, see [Overview of Managing Access Permissions to Your AWS Directory Service Resources](UsingWithDS_IAM_AccessControl_Overview.md)\.

The sections in this topic cover the following:

+ [Permissions Required to Use the AWS Directory Service Console](#UsingWithDS_IAM_RequiredPermissions_Console)

+ [AWS Managed \(Predefined\) Policies for Amazon Cloud Directory and AWS Directory Service](#UsingWithDS_IAM_AccessControl_ManagedPolicies)

+ [Customer Managed Policy Examples](#IAMPolicyExamples_DS)

The following shows an example of a permissions policy\.

```
{
  "Version" : "2012-10-17",
  "Statement" : [
    {
      "Action" : [
        "ds:CreateDirectory"
      ],
      "Effect" : "Allow",
      "Resource" : "*"
    },
    
    {
      "Action" : [
        "iam:PassRole", 
        "iam:GetRole", 
        "iam:CreateRole", 
        "iam:PutRolePolicy"
       ],
      "Effect" : "Allow",
      "Resource" : "*"
    },
    
    {
      "Action" : [
        "ec2:DescribeSubnets",
        "ec2:DescribeVpcs",
        "ec2:CreateSecurityGroup",
        "ec2:DeleteSecurityGroup",
        "ec2:CreateNetworkInterface",
        "ec2:DescribeNetworkInterfaces",
        "ec2:DeleteNetworkInterface",
        "ec2:AuthorizeSecurityGroupIngress",
        "ec2:AuthorizeSecurityGroupEgress",
        "ec2:RevokeSecurityGroupIngress",
        "ec2:RevokeSecurityGroupEgress"
      ],
      "Effect" : "Allow",
      "Resource" : "*"
    }
  ]
}
```

The policy includes the following:

+ The first statement grants permission to create a AWS Directory Service directory\. AWS Directory Service doesn't support permissions for this particular action at the resource\-level\. Therefore, the policy specifies a wildcard character \(\*\) as the `Resource` value\.

+ The second statement grants permissions to certain IAM actions\. The access to IAM actions is needed so that AWS Directory Service can read and create IAM roles on your behalf\. The wildcard character \(\*\) at the end of the `Resource` value means that the statement allows permission for the IAM actions on any IAM role\. To limit this permission to a specific role, replace the wildcard character \(\*\) in the resource ARN with the specific role name\. For more information, see [IAM Actions](http://alpha-docs-aws.amazon.com/IAM/latest/APIReference/API_Operations.html)\.

+ The third statement grants permissions to a specific set of Amazon EC2 resources that are necessary to allow AWS Directory Service to create, configure, and destroy its directories\. The wildcard character \(\*\) at the end of the `Resource` value means that the statement allows permission for the EC2 actions on any EC2 resource or subresource\. To limit this permission to a specific role, replace the wildcard character \(\*\) in the resource ARN with the specific resource or subresource\. For more information, see [EC2 Actions](http://alpha-docs-aws.amazon.com/AWSEC2/latest/APIReference/API_Operations.html)

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permission\. When you attach policy to a user, the user is the implicit principal\. When you attach a permission policy to an IAM role, the principal identified in the role's trust policy gets the permissions\.

For a table showing all of the Amazon Cloud Directory or AWS Directory Service API actions and the resources that they apply to, see [Amazon Cloud Directory API Permissions: Actions, Resources, and Conditions Reference](UsingWithDS_IAM_CD_ResourcePermissions.md) or [AWS Directory Service API Permissions: Actions, Resources, and Conditions Reference](UsingWithDS_IAM_ResourcePermissions.md)\. 

## Permissions Required to Use the AWS Directory Service Console<a name="UsingWithDS_IAM_RequiredPermissions_Console"></a>

For a user to work with the AWS Directory Service console, that user must have permissions listed in the policy above or the permissions granted by the Directory Service Full Access Role or Directory Service Read Only role, described in [AWS Managed \(Predefined\) Policies for Amazon Cloud Directory and AWS Directory Service](#UsingWithDS_IAM_AccessControl_ManagedPolicies)\.

If you create an IAM policy that is more restrictive than the minimum required permissions, the console won't function as intended for users with that IAM policy\. 

## AWS Managed \(Predefined\) Policies for Amazon Cloud Directory and AWS Directory Service<a name="UsingWithDS_IAM_AccessControl_ManagedPolicies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](http://alpha-docs-aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon Cloud Directory:

+ **AmazonCloudDirectoryReadOnlyAccess** – Grants a user or group read\-only access to all Amazon Cloud Directory resources\. For more information, see [Using AWS Managed Policies with AWS Directory Service](roles.md)\.

+ **AmazonCloudDirectoryFullAccess** – Grants a user or group full access to Amazon Cloud Directory\. For more information, see [Using AWS Managed Policies with AWS Directory Service](roles.md)\.

The following AWS managed policies, which you can attach to users in your account, are specific to AWS Directory Service:

+ **AWSDirectoryServiceReadOnlyAccess** – Grants a user or group read\-only access to all AWS Directory Service resources, EC2 subnets, EC2 network interfaces, and AWS SNS topics and subscriptions for the root AWS account\. For more information, see [Using AWS Managed Policies with AWS Directory Service](roles.md)\.

+ **AWSDirectoryServiceFullAccess** – Grants a user or group the following: 

  + Full access to AWS Directory Service

  + Access to key Amazon EC2 services required to use AWS Directory Service

  + Ability to list Amazon Simple Notification Service topics

  + Ability to create, manage, and delete Amazon Simple Notification Service topics with a name beginning with “DirectoryMonitoring”

  For more information, see [Using AWS Managed Policies with AWS Directory Service](roles.md)\.

In addition, there are other AWS\-managed policies that are suitable for use with other IAM roles\. These policies are assigned to the roles associated with users in your Amazon Cloud Directory or other AWS Directory Service directory and are required in order for those users to have access to other AWS resources, such as Amazon EC2\. For more information, see [Grant Users and Groups Access to AWS Resources](manage_roles.md)\.

You can also create custom IAM policies that allow users to access the required API actions and resources\. You can attach these custom policies to the IAM users or groups that require those permissions\.

## Customer Managed Policy Examples<a name="IAMPolicyExamples_DS"></a>

In this section, you can find example user policies that grant permissions for various AWS Directory Service actions\. 

**Note**  
All examples use the US West \(Oregon\) Region \(`us-west-2`\) and contain fictitious account IDs\.


+ [Example 1: Allow a User to Perform Any Describe Action on Any AWS Directory Service Resource](#IAMPolicyExamples_DS_perform_describe_action)
+ [Example 2: Allow a User to Create a Directory](#IAMPolicyExamples_DS_create_directory)

### Example 1: Allow a User to Perform Any Describe Action on Any AWS Directory Service Resource<a name="IAMPolicyExamples_DS_perform_describe_action"></a>

The following permissions policy grants permissions to a user to run all of the actions that begin with `Describe`\. These actions show information about an AWS Directory Service resource, such as a directory or snapshot\. Note that the wildcard character \(\*\) in the `Resource` element indicates that the actions are allowed for all AWS Directory Service resources owned by the account\. 

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action":"ds:Describe*",
 7.          "Resource":"*"
 8.       }
 9.    ]
10. }
```

### Example 2: Allow a User to Create a Directory<a name="IAMPolicyExamples_DS_create_directory"></a>

The following permissions policy grants permissions to allow a user to create a directory and all other related resources, such as snapshots and trusts\. In order to do so, permissions to certain Amazon EC2 services are also required\.

```
 1. {
 2.    "Version":"2012-10-17",
 3.    "Statement":[
 4.       {
 5.          "Effect":"Allow",
 6.          "Action": [
 7.                 "ds:Create*",
 8.                 "ec2:AuthorizeSecurityGroupEgress",
 9.                 "ec2:AuthorizeSecurityGroupIngress",
10.                 "ec2:CreateNetworkInterface",
11.                 "ec2:CreateSecurityGroup",
12.                 "ec2:DeleteNetworkInterface",
13.                 "ec2:DeleteSecurityGroup",
14.                 "ec2:DescribeNetworkInterfaces",
15.                 "ec2:DescribeSubnets",
16.                 "ec2:DescribeVpcs",
17.                 "ec2:RevokeSecurityGroupEgress",
18.                 "ec2:RevokeSecurityGroupIngress"
19.                   ],
20.          "Resource":"*"
21.          ]
22.       }
23.    ]
24. }
```