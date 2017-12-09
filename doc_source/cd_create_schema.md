# Create a Schema<a name="cd_create_schema"></a>

Amazon Cloud Directory supports uploading of a compliant JSON file for schema creation\. You can also create, read, update, and delete schemas using the Cloud Directory APIs\. For more information about schema API operations, see the [Amazon Cloud Directory API Reference Guide](http://docs.aws.amazon.com/amazoncds/latest/APIReference/welcome.html)\.

To create a new schema, you can either create your own JSON file from scratch or download one of the existing schemas listed in the console\. Then upload it as a custom schema\. For more information, see [Custom Schemas](customschematopic.md)\. Choose either of the procedures below, depending on your preferred method\. 

**To create a custom schema**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, choose **Schemas**\.

1. Create a JSON file with all of your new schema definitions\. For more information about how to format a JSON file, see [JSON Schema Format](jsonformat.md#json)\. 

1. In the console, choose **Upload new schema \(JSON\)**, select the new JSON file that you just created, and then choose **OK**\. 

   This adds a new schema to your schema library and place it in the **In Development** state\. For more information about schema states, see [Schema Lifecycle](lifecycle.md)\.

**To create a custom schema based on an existing one in the console**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Schemas**\.

1. In the table listing the schemas, select the schema you want to edit, and then choose **Download schema**\.

1. Rename the JSON file, edit it as needed, and then save the file\. For more information about how to format a JSON file, see [JSON Schema Format](jsonformat.md#json)\. 

1. In the console, choose **Upload new schema \(JSON\)**, select the JSON file that you just edited, and then choose **OK**\.

   This adds a new schema to your schema library and place it in the **In Development** state\. For more information about schema states, see [Schema Lifecycle](lifecycle.md)\.