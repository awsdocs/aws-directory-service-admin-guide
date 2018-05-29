# Amazon Cloud Directory<a name="directory_amazon_cd"></a>

Amazon Cloud Directory is a highly available multi\-tenant directory\-based store in AWS\. These directories scale automatically to hundreds of millions of objects as needed for applications\. This lets operation's staff focus on developing and deploying applications that drive the business, not managing directory infrastructure\. Unlike traditional directory systems, Cloud Directory does not limit organizing directory objects in a single fixed hierarchy\. 

With Cloud Directory, you can organize directory objects into multiple hierarchies to support many organizational pivots and relationships across directory information\. For example, a directory of users may provide a hierarchical view based on reporting structure, location, and project affiliation\. Similarly, a directory of devices may have multiple hierarchical views based on its manufacturer, current owner, and physical location\.

At its core, Cloud Directory is a specialized graph\-based directory store that provides a foundational building block for developers\. With Cloud Directory, developers can do the following:
+ Create directory\-based applications easily and without having to worry about deployment, global scale, availability, and performance
+ Build applications that provide user and group management, permissions or policy management, device registry, customer management, address books, and application or product catalogs
+ Define new directory objects or extend existing types to meet their application needs, reducing the code they need to write
+ Reduce the complexity of layering applications on top of Cloud Directory
+ Manage the evolution of schema information over time, ensuring future compatibility for consumers 

Cloud Directory includes a set of API operations to access various objects and policies stored in your Cloud Directory\-based directories\. For a list of available operations, see [Amazon Cloud Directory API Actions](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_Operations.html)\. For a list of operations and the permissions required to perform each API action, see [Amazon Cloud Directory API Permissions: Actions, Resources, and Conditions Reference](UsingWithDS_IAM_CD_ResourcePermissions.md)\.

**What Cloud Directory Is Not**

Cloud Directory is not a directory service for IT Administrators who want to manage or migrate their directory infrastructure\.

Read the topics in this section to get started creating directories, managing schemas and directory objects\.

For additional resources, see [Cloud Directory Resources](cd_resources.md)\.

**Topics**
+ [Understanding Key Cloud Directory Concepts](cd_key_concepts.md)
+ [Using the Console](cd_using_console.md)
+ [Directory Objects](cd_directory_objects.md)
+ [Schemas](cd_schemas.md)
+ [Indexing and Search](cd_indexing.md)
+ [Using the Cloud Directory APIs](cd_using_api.md)
+ [Amazon Cloud Directory Compliance](cd_compliance.md)
+ [Advanced Features](cd_advanced.md)
+ [Limits for Amazon Cloud Directory](cd_limits.md)
+ [Cloud Directory Resources](cd_resources.md)