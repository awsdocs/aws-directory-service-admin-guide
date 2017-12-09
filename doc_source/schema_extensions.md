# Schema Extensions<a name="schema_extensions"></a>

A schema is the definition of attributes and classes that are part of a distributed directory and is similar to fields and tables in a database\. Schemas include a set of rules which determine the type and format of data that can be added or included in the database\. The User class is one example of a *class* that is stored in the database\. Some example of User class attributes can include the user’s first name, last name, phone number, and so on\. 

Microsoft AD uses schemas to organize and enforce how directory data is stored\. The process of adding definitions to the schema is referred to as “extending the schema\.” Schema extensions make it possible for you to modify the schema of your Microsoft AD directory using a valid LDAP Data Interchange Format \(LDIF\) file\. For more information about AD schemas and how to extend your schema, see the topics listed below\.


+ [Schema Elements](schema_elements.md)
+ [When to Extend Your Microsoft AD Schema](schema_when_to_extend.md)
+ [Tutorial: Extending Your Microsoft AD Schema](tutorial_extending_ad_schema.md)