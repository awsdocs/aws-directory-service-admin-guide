# When to Extend Your AWS Managed Microsoft AD Schema<a name="ms_ad_schema_when_to_extend"></a>

You can extend your AWS Managed Microsoft AD schema by adding new object classes and attributes\. For example, you might do this if you have an application that requires changes to your schema in order to support single sign\-on capabilities\. 

You can also use schema extensions to enable support for applications that rely on specific Active Directory object classes and attributes\. This can be especially useful in the case where you need to migrate corporate applications that are dependent on AWS Managed Microsoft AD, to the AWS cloud\.

Each attribute or class that is added to an existing Active Directory schema must be defined with a unique ID\. That way when companies add extensions to the schema, they can be guaranteed to be unique and not to conflict with each other\. These IDs are referred to as AD Object Identifiers \(OIDs\) and are stored in AWS Managed Microsoft AD\.

To get started, see [Tutorial: Extending Your AWS Managed Microsoft AD Schema](ms_ad_tutorial_extend_schema.md)\.

## Related Topics<a name="schemaextend_related"></a>
+ [Extend Your Schema](ms_ad_schema_extensions.md)
+ [Schema Elements](ms_ad_key_concepts_schema.md#ms_ad_schema_elements)