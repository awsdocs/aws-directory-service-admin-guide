# Amazon Cloud Directory API Permissions: Actions, Resources, and Conditions Reference<a name="UsingWithDS_IAM_CD_ResourcePermissions"></a>

When you are setting up [Access Control](UsingWithDS_IAM_AuthNAccess.md#UsingWithDS_IAM_AccessControl) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), you can use the following table as a reference\. The each Amazon Cloud Directory API operation, the corresponding actions for which you can grant permissions to perform the action, the AWS resource for which you can grant the permissions\.  You specify the actions in the policy's `Action` field and the resource value in the policy's `Resource` field\. 

You can use AWS\-wide condition keys in your Amazon Cloud Directory policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys](http://alpha-docs-aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `clouddirectory:` prefix followed by the API operation name \(for example, `clouddirectory:CreateDirectory`\)\.