# Editing the Trust Relationship for an Existing Role<a name="edit_trust"></a>

You can assign your existing IAM roles to your AWS Directory Service users and groups\. To do this, however, the role must have a trust relationship with AWS Directory Service\. When you use AWS Directory Service to create a role using the procedure in [Creating a New Role](create_role.md), this trust relationship is automatically set\. You only need to establish this trust relationship for IAM roles that are not created by AWS Directory Service\.

**To establish a trust relationship for an existing role to AWS Directory Service**

1. In the navigation pane of the IAM console, choose **Roles**\.

   The console displays the roles for your account\.

1. Choose the name of the role that you want to modify, and select the **Trust relationships** tab on the details page\.

1. Choose **Edit trust relationship**\.

1. Under **Policy Document**, paste the following, and then choose **Update Trust Policy**\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "",
         "Effect": "Allow",
         "Principal": {
           "Service": "ds.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

You can also update this policy document using the IAM CLI\. For more information, see [put\-role\-policy](https://docs.aws.amazon.com/cli/latest/reference/iam/put-role-policy.html) in the *IAM Command Line Reference*\.