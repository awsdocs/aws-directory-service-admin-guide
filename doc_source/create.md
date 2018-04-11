# Step 1: Create Your LDIF File<a name="create"></a>

An LDIF file is a standard plain text data interchange format for representing [LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) \(Lightweight Directory Access Protocol\) directory content and update requests\. LDIF conveys directory content as a set of records, one record for each object \(or entry\)\. It also represents update requests, such as Add, Modify, Delete, and Rename, as a set of records, one record for each update request\. 

The AWS Directory Service imports your LDIF file with the schema changes by running the `ldifde.exe` application on your AWS Managed Microsoft AD directory\. Therefore, you'll find it helpful to understand the LDIF script syntax\. For more information, see [LDIF Scripts](https://msdn.microsoft.com/en-us/library/ms677268(v=vs.85).aspx)\. 

Several third\-party LDIF tools can extract, clean\-up, and update your schema updates\. Regardless of which tool you use, it is important to understand that all identifiers used in your LDIF file must be unique\. 

We highly recommend that you review the following concepts and tips prior to creating your LDIF file\.
+ **Schema elements** – Learn about schema elements such as attributes, classes, object IDs, and linked attributes\. For more information, see [Schema Elements](ms_ad_key_concepts_schema.md#ms_ad_schema_elements)\.
+ **Sequence of items** – Make sure that the order in which the items in your LDIF file are laid out follow the [Directory Information Tree \(DIT\)](https://en.wikipedia.org/wiki/Directory_information_tree) from the top down\. The general rules for sequencing in an LDIF file include the following: 
  + Separate items with a blank line\.
  + List child items after their parent items\. 
  + Ensure that items such as attributes or object classes exist in the schema\. If they are not present, you must add them to the schema before they can be used\. For example, before you can assign an attribute to a class, the attribute must be created\. 
+ **Format of the DN** – For each new instruction in the LDIF file, define the distinguished name \(DN\) as the first line of the instruction\. The DN identifies an Active Directory object within the Active Directory object’s tree and must contain the domain components for your directory\. For example, the domain components for the directory in this tutorial are `DC=example,DC=com`\.

  The DN also must contain the common name \(CN\) of the Active Directory object\. The first CN entry is the attribute or class name\. Next, you must use `CN=Schema,CN=Configuration`\. This CN ensures that you are able to extend the Active Directory schema\. As mentioned before, you cannot add or modify Active Directory objects’ content\. The general format for a DN follows\.

  ```
  dn: CN=[attribute or class name],CN=Schema,CN=Configuration,DC=[domain_name]
  ```

  For this tutorial, the DN for the new Shoe\-Size attribute would look like:

  ```
  dn: CN=Shoe-Size,CN=Schema,CN=Configuration,DC=example,DC=com
  ```
+ **Warnings** – Review the warnings below before you extend your schema\.
  + Before you extend your Active Directory schema, it is important to review Microsoft's warnings on the impact of this operation\. For more information, see [What You Must Know Before Extending the Schema](https://msdn.microsoft.com/en-us/library/ms677995(v=vs.85).aspx)\.
  + You cannot delete a schema attribute or class\. Therefore, if you make a mistake and don’t want to restore from backup, you can only disable the object\. For more information, see [Disabling Existing Classes and Attributes](https://msdn.microsoft.com/en-us/library/ms675903(v=vs.85).aspx)\.

To learn more about how LDIF files are constructed and see a sample LDIF file that can be used for testing AWS Managed Microsoft AD schema extensions, see the article [How to Extend your AWS Managed Microsoft AD directory Schema](https://aws.amazon.com/blogs/security/how-to-add-more-application-support-to-your-microsoft-ad-directory-by-extending-the-schema/) on the AWS Security Blog\.

**Next Step**

[Step 2: Import Your LDIF File](import.md)