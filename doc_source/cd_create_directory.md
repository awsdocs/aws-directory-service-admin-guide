# Create an Amazon Cloud Directory<a name="cd_create_directory"></a>

Before you can create a directory in Amazon Cloud Directory, AWS Directory Service requires that you first apply a schema to it\. A directory cannot be created without a schema and typically has one schema applied to it\. However, you use Cloud Directory API operations to apply additional schemas to a directory\. For more information, see [ApplySchema](http://docs.aws.amazon.com/amazoncds/latest/APIReference/API_ApplySchema.html) in the *Amazon Cloud Directory API Reference Guide*\.

**To create a Cloud Directory**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories** and choose **Set up directory**\.

1. Choose **Amazon Cloud Directory**\.

1. For **Name**, type the friendly name of your directory, such as `User Repository`\.

1. Under **Choose or add a new schema**, choose a sample schema from the list or choose **Upload new schema \(JSON\)** to upload a custom schema, and then choose **Next**\. Currently, Cloud Directory provides the following [Sample Schemas](sampleschemastopic.md):

   +  Organization

   +  Person \(User\)

   +  Device

   Sample schemas and newly uploaded schemas are placed in the **In Development** state, by default\. For more information about schema states, see [Schema Lifecycle](lifecycle.md)\. Before a schema can be applied to a directory, it must be converted into the **Published** state\. 

   To successfully publish an AWS sample schema using the console, you must have permissions to the following actions:

   +  `clouddirectory:Get*`

   +  `clouddirectory:List*`

   +  `clouddirectory:CreateSchema`

   +  `clouddirectory:CreateDirectory`

   +  `clouddirectory:PutSchemaFromJson`

   +  `clouddirectory:PublishSchema`

   +  `clouddirectory:DeleteSchema`

   Since sample schemas are read\-only templates provided by AWS, they cannot be published directly\. Instead, when you choose to create a directory based on a sample schema, the console creates a temporary copy of the sample schema you selected and places it in the **In Development** state\. It then creates a copy of that development schema and places it in the **Published** state\. Once published, the development schema is deleted, which is why the `DeleteSchema` action is necessary when publishing a sample schema\.

1. Review the directory information and make any necessary changes\. When the information is correct, choose **Launch**\.