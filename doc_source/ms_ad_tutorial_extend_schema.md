# Tutorial: Extending Your AWS Managed Microsoft AD Schema<a name="ms_ad_tutorial_extend_schema"></a>

In this tutorial, you will learn how to extend the schema for your AWS Directory Service for Microsoft Active Directory directory, also known as AWS Managed Microsoft AD, by adding unique *attributes* and *classes* that meet your specific requirements\. AWS Managed Microsoft AD schema extensions can only be uploaded and applied using a valid LDIF \(Lightweight Directory Interchange Format\) script file\.

Attributes \(attributeSchema\) define the fields in the database while classes \(classSchema\) define the tables in the database\. For example, all of the user objects in Active Directory are defined by the schema class *User* while the individual properties of a user, such as email address or phone number, are each defined by an attribute\. 

If you wanted to add a new property, such as Shoe\-Size, you would define a new attribute, which would be of type *integer*\. You could also define lower and upper limits like 1 to 20\. Once the Shoe\-Size attributeSchema object has been created, you would then alter the *User* classSchema object to contain that attribute\. Attributes can be linked to multiple classes\. Shoe\-Size could also be added to the *Contact* class for example\. For more information about Active Directory schemas, see [When to Extend Your AWS Managed Microsoft AD Schema](ms_ad_schema_when_to_extend.md)\.

This workflow has three basic steps\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/)

**[Step 1: Create Your LDIF File](create.md)**  
First, you create an LDIF file and define the new attributes and any classes that the attributes should be added to\. You use this file for the next phase of the workflow\.

**[Step 2: Import Your LDIF File](import.md)**  
In this step, you use the AWS Directory Service console to import the LDIF file to your Microsoft AD environment\.

**[Step 3: Verify If The Schema Extension Was Successful](verify.md)**  
Finally, as an administrator, you use an EC2 instance to verify that the new extensions appear in the Active Directory Schema Snap\-in\.