# Overview of Managing Access Permissions to Your AWS Directory Service Resources<a name="IAM_Auth_Access_Overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access the resources are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\), and some services \(such as AWS Lambda\) also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\. 

**Topics**
+ [AWS Directory Service Resources and Operations](#CreatingIAMPolicies_DS)
+ [Understanding Resource Ownership](#IAM_Auth_Access_ResourceOwner)
+ [Managing Access to Resources](#IAM_Auth_Access_ManagingAccess)
+ [Specifying Policy Elements: Actions, Effects, Resources, and Principals](#SpecifyingIAMPolicyActions_DS)
+ [Specifying Conditions in a Policy](#SpecifyingIAMPolicyConditions_DS)

## AWS Directory Service Resources and Operations<a name="CreatingIAMPolicies_DS"></a>

In AWS Directory Service, the primary resource is a *directory*\. AWS Directory Service supports directory snapshot resources as well\. However, you can create snapshots only in the context of an existing directory\. Therefore, a snapshot is referred to as a *subresource*\.

These resources have unique Amazon Resource Names \(ARNs\) associated with them as shown in the following table\.


****  

| **Resource Type**  |  **ARN Format**  | 
| --- | --- | 
|  Directory  |  `arn:aws:ds:region:account-id:directory/external-directory-id`  | 
|  Snapshot  |  `arn:aws:ds:region:account-id:snapshot/external-snapshot-id`  | 

AWS Directory Service provides a set of operations to work with the appropriate resources\. For a list of available operations, see [Directory Service Actions](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_Operations.html)\.

## Understanding Resource Ownership<a name="IAM_Auth_Access_ResourceOwner"></a>

A *resource owner* is the AWS account that created a resource\. That is, the resource owner is the AWS account of the *principal entity* \(the root account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create an AWS Directory Service resource, such as a directory, your AWS account is the owner of that resource\.
+ If you create an IAM user in your AWS account and grant permissions to create AWS Directory Service resources to that user, the user can also create AWS Directory Service resources\. However, your AWS account, to which the user belongs, owns the resources\.
+ If you create an IAM role in your AWS account with permissions to create AWS Directory Service resources, anyone who can assume the role can create AWS Directory Service resources\. Your AWS account, to which the role belongs, owns the AWS Directory Service resources\. 

## Managing Access to Resources<a name="IAM_Auth_Access_ManagingAccess"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of AWS Directory Service\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM polices\) and policies attached to a resource are referred to as *resource\-based* policies\. AWS Directory Service supports only identity\-based policies \(IAM policies\)\.

**Topics**
+ [Identity\-Based Policies \(IAM Policies\)](#IAM_Auth_Access_ManagingAccess_IdentityBased)
+ [Resource\-Based Policies](#IAM_Auth_Access_ManagingAccess_ResourceBased)

### Identity\-Based Policies \(IAM Policies\)<a name="IAM_Auth_Access_ManagingAccess_IdentityBased"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create an AWS Directory Service resource, such as a new directory\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. The principal in the trust policy can also be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

   For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

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

For more information about using identity\-based policies with AWS Directory Service, see [Using Identity\-Based Policies \(IAM Policies\) for AWS Directory Service](IAM_Auth_Access_IdentityBased.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-Based Policies<a name="IAM_Auth_Access_ManagingAccess_ResourceBased"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. AWS Directory Service doesn't support resource\-based policies\. 

## Specifying Policy Elements: Actions, Effects, Resources, and Principals<a name="SpecifyingIAMPolicyActions_DS"></a>

For each AWS Directory Service resource, the service defines a set of API operations\. For more information, see [AWS Directory Service Resources and Operations](#CreatingIAMPolicies_DS)\. For a list of available API operations, see [Directory Service Actions](https://docs.aws.amazon.com/directoryservice/latest/devguide/API_Operations.html)\.

To grant permissions for these API operations, AWS Directory Service defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. 

The following are the basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For AWS Directory Service resources, you always use the wildcard character \(\*\) in IAM policies\. For more information, see [AWS Directory Service Resources and Operations](#CreatingIAMPolicies_DS)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `ds:DescribeDirectories` permission allows the user permissions to perform the AWS Directory Service `DescribeDirectories` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action\. This can be either allow or deny\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. AWS Directory Service doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [IAM JSON Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the AWS Directory Service API actions and the resources that they apply to, see [AWS Directory Service API Permissions: Actions, Resources, and Conditions Reference](UsingWithDS_IAM_ResourcePermissions.md)\. 

## Specifying Conditions in a Policy<a name="SpecifyingIAMPolicyConditions_DS"></a>

When you grant permissions, you can use the access policy language to specify the conditions when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to AWS Directory Service\. However, there are AWS condition keys that you can use as appropriate\. For a complete list of AWS keys, see [Available Global Condition Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#AvailableKeys) in the *IAM User Guide*\.  