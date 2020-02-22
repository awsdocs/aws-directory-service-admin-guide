# Using Identity\-Based Policies \(IAM Policies\) for AWS Directory Service<a name="IAM_Auth_Access_IdentityBased"></a>

This topic provides examples of identity\-based policies in which an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS Directory Service resources\. For more information, see [Overview of Managing Access Permissions to Your AWS Directory Service Resources](IAM_Auth_Access_Overview.md)\.

The sections in this topic cover the following:
+ [Permissions Required to Use the AWS Directory Service Console](#UsingWithDS_IAM_RequiredPermissions_Console)
+ [AWS Managed \(Predefined\) Policies for AWS Directory Service](#IAM_Auth_Access_ManagedPolicies)
+ [Customer Managed Policy Examples](#IAMPolicyExamples_DS)
+ [Using Tags with IAM Policies](#using_tags_with_iam_policies)

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
+ The second statement grants permissions to certain IAM actions\. The access to IAM actions is needed so that AWS Directory Service can read and create IAM roles on your behalf\. The wildcard character \(\*\) at the end of the `Resource` value means that the statement allows permission for the IAM actions on any IAM role\. To limit this permission to a specific role, replace the wildcard character \(\*\) in the resource ARN with the specific role name\. For more information, see [IAM Actions](https://docs.aws.amazon.com/IAM/latest/APIReference/API_Operations.html)\.
+ The third statement grants permissions to a specific set of Amazon EC2 resources that are necessary to allow AWS Directory Service to create, configure, and destroy its directories\. The wildcard character \(\*\) at the end of the `Resource` value means that the statement allows permission for the EC2 actions on any EC2 resource or subresource\. To limit this permission to a specific role, replace the wildcard character \(\*\) in the resource ARN with the specific resource or subresource\. For more information, see [Amazon EC2 Actions](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_Operations.html)

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permission\. When you attach policy to a user, the user is the implicit principal\. When you attach a permission policy to an IAM role, the principal identified in the role's trust policy gets the permissions\.

For a table showing all of the AWS Directory Service API actions and the resources that they apply to, see [AWS Directory Service API Permissions: Actions, Resources, and Conditions Reference](UsingWithDS_IAM_ResourcePermissions.md)\. 

## Permissions Required to Use the AWS Directory Service Console<a name="UsingWithDS_IAM_RequiredPermissions_Console"></a>

For a user to work with the AWS Directory Service console, that user must have permissions listed in the preceding policy or the permissions granted by the Directory Service Full Access Role or Directory Service Read Only role, described in [AWS Managed \(Predefined\) Policies for AWS Directory Service](#IAM_Auth_Access_ManagedPolicies)\.

If you create an IAM policy that is more restrictive than the minimum required permissions, the console won't function as intended for users with that IAM policy\. 

## AWS Managed \(Predefined\) Policies for AWS Directory Service<a name="IAM_Auth_Access_ManagedPolicies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to AWS Directory Service:
+ **AWSDirectoryServiceReadOnlyAccess** – Grants a user or group read\-only access to all AWS Directory Service resources, EC2 subnets, EC2 network interfaces, and Amazon Simple Notification Service \(Amazon SNS\) topics and subscriptions for the root AWS account\. For more information, see [Using AWS Managed Policies with AWS Directory Service](ms_ad_managed_policies.md)\.
+ **AWSDirectoryServiceFullAccess** – Grants a user or group the following: 
  + Full access to AWS Directory Service
  + Access to key Amazon EC2 services required to use AWS Directory Service
  + Ability to list Amazon SNS topics
  + Ability to create, manage, and delete Amazon SNS topics with a name beginning with “DirectoryMonitoring”

  For more information, see [Using AWS Managed Policies with AWS Directory Service](ms_ad_managed_policies.md)\.

In addition, there are other AWS managed policies that are suitable for use with other IAM roles\. These policies are assigned to the roles that are associated with users in your AWS Directory Service directory\. These policies are required for those users to have access to other AWS resources, such as Amazon EC2\. For more information, see [Grant Users and Groups Access to AWS Resources](ms_ad_manage_roles.md)\.

You can also create custom IAM policies that allow users to access the required API actions and resources\. You can attach these custom policies to the IAM users or groups that require those permissions\.

## Customer Managed Policy Examples<a name="IAMPolicyExamples_DS"></a>

In this section, you can find example user policies that grant permissions for various AWS Directory Service actions\. 

**Note**  
All examples use the US West \(Oregon\) Region \(`us-west-2`\) and contain fictitious account IDs\.

**Topics**
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

## Using Tags with IAM Policies<a name="using_tags_with_iam_policies"></a>

You can apply tag\-based resource\-level permissions in the IAM policies you use for most AWS Directory Service API actions\. This gives you better control over what resources a user can create, modify, or use\. You use the `Condition` element \(also called the `Condition` block\) with the following condition context keys and values in an IAM policy to control user access \(permissions\) based on a resource's tags:
+ Use `aws`:`ResourceTag`/**tag\-key**: **tag\-value** to allow or deny user actions on resources with specific tags\.
+ Use `aws`:`ResourceTag`/**tag\-key**: **tag\-value** to require that a specific tag be used \(or not used\) when making an API request to create or modify a resource that allows tags\.
+ Use `aws`:`TagKeys`: \[**tag\-key**, \.\.\.\] to require that a specific set of tag keys be used \(or not used\) when making an API request to create or modify a resource that allows tags\.

**Note**  
The condition context keys and values in an IAM policy apply only to those AWS Directory Service actions where an identifier for a resource capable of being tagged is a required parameter\. 

[Controlling Access Using Tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html) in the *IAM User Guide* has additional information on using tags\. The [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) section of that guide has detailed syntax, descriptions, and examples of the elements, variables, and evaluation logic of JSON policies in IAM\.

The following tag policy example allows all `ds` calls as long as it contains the tag key\-value pair "`fooKey`":"`fooValue`"\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Sid":"VisualEditor0",
         "Effect":"Allow",
         "Action":[
            "ds:*"
         ],
         "Resource":"*",
         "Condition":{
            "StringEquals":{
               "aws:ResourceTag/fooKey":"fooValue"
            }
         }
      },
      {
         "Effect":"Allow",
         "Action":[
            "ec2:*"
         ],
         "Resource":"*"
      }
   ]
}
```

The following resource policy example allows all `ds` calls as long as the resource contains the directory ID "`d-1234567890`"\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Sid":"VisualEditor0",
         "Effect":"Allow",
         "Action":[
            "ds:*"
         ],
         "Resource":"arn:aws:ds:us-east-1:123456789012:directory/d-1234567890"
      },
      {
         "Effect":"Allow",
         "Action":[
            "ec2:*"
         ],
         "Resource":"*"
      }
   ]
}
```

For more information about ARNs, see [Amazon Resource Names \(ARNs\) and AWS Service Namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)\.

The following list of AWS Directory Service API operations support tag\-based resource\-level permissions:
+ [AcceptSharedDirectory](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_AcceptSharedDirectory.html)
+ [AddIpRoutes](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_AddIpRoutes.html)
+ [AddTagsToResource](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_AddTagsToResource.html)
+ [CancelSchemaExtension](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CancelSchemaExtension.html)
+ [CreateAlias](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CreateAlias.html)
+ [CreateComputer](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CreateComputer.html)
+ [CreateConditionalForwarder](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CreateConditionalForwarder.html)
+ [CreateSnapshot](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CreateSnapshot.html)
+ [CreateLogSubscription](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CreateLogSubscription.html)
+ [CreateTrust](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_CreateTrust.html)
+ [DeleteConditionalForwarder](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DeleteConditionalForwarder.html)
+ [DeleteDirectory](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DeleteDirectory.html)
+ [DeleteLogSubscription](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DeleteLogSubscription.html)
+ [DeleteSnapshot](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DeleteSnapshot.html)
+ [DeleteTrust](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DeleteTrust.html)
+ [DeregisterEventTopic](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DeregisterEventTopic.html)
+ [DescribeConditionalForwarders](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeConditionalForwarders.html)
+ [DescribeDomainControllers](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeDomainControllers.html)
+ [DescribeEventTopics](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeEventTopics.html)
+ [DescribeSharedDirectories](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeSharedDirectories.html)
+ [DescribeSnapshots](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeSnapshots.html)
+ [DescribeTrusts](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DescribeTrusts.html)
+ [DisableRadius](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DisableRadius.html)
+ [DisableSso](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_DisableSso.html)
+ [EnableRadius](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_EnableRadius.html)
+ [EnableSso](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_EnableSso.html)
+ [GetSnapshotLimits](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_GetSnapshotLimits.html)
+ [ListIpRoutes](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ListIpRoutes.html)
+ [ListSchemaExtensions](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ListSchemaExtensions.html)
+ [ListTagsForResource](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ListTagsForResource.html)
+ [RegisterEventTopic](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_RegisterEventTopic.html)
+ [RejectSharedDirectory](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_RejectSharedDirectory.html)
+ [RemoveIpRoutes](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_RemoveIpRoutes.html)
+ [RemoveTagsFromResource](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_RemoveTagsFromResource.html)
+ [ResetUserPassword](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ResetUserPassword.html)
+ [RestoreFromSnapshot](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_RestoreFromSnapshot.html)
+ [ShareDirectory](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_ShareDirectory.html)
+ [StartSchemaExtension](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_StartSchemaExtension.html)
+ [UnshareDirectory](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_UnshareDirectory.html)
+ [UpdateConditionalForwarder](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_UpdateConditionalForwarder.html)
+ [UpdateNumberOfDomainControllers](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_UpdateNumberOfDomainControllers.html)
+ [UpdateRadius](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_UpdateRadius.html)
+ [UpdateTrust](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_UpdateTrust.html)
+ [VerifyTrust](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_VerifyTrust.html)