# Schema Elements<a name="schema_elements"></a>

Attributes, classes and objects are the basic elements that are used to build object definitions in the schema\. The following provides details about schema elements that are important to know before you begin the process to extend your Microsoft AD schema\. 

**Attributes**  
Each schema attribute, which is similar to a field in a database, has several properties that define the characteristics of the attribute\. For example, the property used by LDAP clients to read and write the attribute is `LDAPDisplayName`\. The `LDAPDisplayName` property must be unique across all attributes and classes\. For a complete list of attribute characteristics, see [Characteristics of Attributes](https://msdn.microsoft.com/en-us/library/ms675578(v=vs.85).aspx) on the MSDN website\. For additional guidance on how to create a new attribute, see [Defining a New Attribute](https://msdn.microsoft.com/en-us/library/ms675883(v=vs.85).aspx) on the MSDN website\.

**Classes**  
The classes are analogous to tables in a database and also have several properties to be defined\. For example, the `objectClassCategory` defines the class category\. For a complete list of class characteristics, see [Characteristics of Object Classes](https://msdn.microsoft.com/en-us/library/ms675579(v=vs.85).aspx) on the MSDN website\. For more information about how to create a new class, see [Defining a New Class](https://msdn.microsoft.com/en-us/library/ms675884(v=vs.85).aspx) on the MSDN website\.

**Object identifier \(OID\)**  
Each class and attribute must have an OID that is unique for all of your objects\. Software vendors must obtain their own OID to ensure uniqueness\. Uniqueness avoids conflicts when the same attribute is used by more than one application for different purposes\. To ensure uniqueness, you can obtain a root OID from an ISO Name Registration Authority\. Alternatively, you can obtain a base OID from Microsoft\. For more information about OIDs and how to obtain them, see [Object Identifiers](https://msdn.microsoft.com/en-us/library/ms677614(v=vs.85).aspx) on the MSDN website\.

**Schema linked attributes**  
Some attributes are linked between two classes with forward and back links\. The best example is groups\. When you look at a group it shows you the members of the group; if you look at a user you can see what groups it belongs to\. When you add a user to a group, Active Directory creates a forward link to the group\. Then Active Directory adds a back link from the group to the user\. A unique link ID must be generated when creating an attribute that will be linked\. For more information, see [Linked Attributes](https://msdn.microsoft.com/en-us/library/ms677270(v=vs.85).aspx) on the MSDN website\. 

## Related Topics<a name="schemaelements_related"></a>

+ [When to Extend Your Microsoft AD Schema](schema_when_to_extend.md)

+ [Tutorial: Extending Your Microsoft AD Schema](tutorial_extending_ad_schema.md)