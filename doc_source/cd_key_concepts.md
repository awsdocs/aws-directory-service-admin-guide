# Understanding Key Cloud Directory Concepts<a name="cd_key_concepts"></a>

Amazon Cloud Directory is a directory\-based data store that can create various types of objects in a schema\-oriented fashion\. 

## Directory<a name="whatisdirectory"></a>

A directory is a schema\-based data store that contains specific types of objects organized in a multi\-hierarchical structure \(see [Directory Structure](#dirstructure) for more details\)\. For example, a directory of users may provide a hierarchical view based on reporting structure, location, and project affiliation\. Similarly, a directory of devices may have multiple hierarchical views based on its manufacturer, current owner, and physical location\. 

A directory defines the logical boundary for the data store, completely isolating it from all other directories in the service\. It also defines the boundaries for an individual request\. A single transaction or query executes within the context of a single directory\. A directory cannot be created without a schema and typically has one schema applied to it\. However, you can use the Cloud Directory API operations to apply additional schemas to a directory\. For more information, see [http://docs.aws.amazon.com/amazoncds/latest/APIReference/API_ApplySchema.html](http://docs.aws.amazon.com/amazoncds/latest/APIReference/API_ApplySchema.html) in the *Amazon Cloud Directory API Reference Guide*\. 

### Objects<a name="objects"></a>

Objects are a structured data entity in a directory\. An object in a directory is intended to capture metadata \(or attributes\) about a physical or logical entity usually for the purpose of information discovery and enforcing policies\. For example users, devices, applications, AWS accounts, EC2 instances and Amazon S3 buckets can all be represented as different types of objects in a directory\. 

An object’s structure and type information is expressed as a collection of facets\. You can use `Path` or `ObjectIdentifier` to access objects\. Objects can also have attributes, which are a user\-defined unit of metadata\. For example, the user object can have an attribute called *email\-address*\. Attributes are always associated with an object\. 

### Policies<a name="policies"></a>

Policies are a specialized type of object that are useful for storing permissions or capabilities\. Policies offer the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html) API action\. The lookup policy action takes a reference to any object as its starting input\. It then walks up the directory all the way to the root\. The action collects any policy objects that it encounters on each path to the root\. Cloud Directory does not interpret any of these policies in any way\. Instead, Cloud Directory users interpret policies using their own specialized business logic\.

For example, imagine a system that stores employee information\. Employees are grouped together by job function\. We want to establish different permissions for members of the Human Resources Group and the Accounting group\. Members of the Human Resources group will have access to payroll information and the Accounting group will have access to ledger information\. To establish these permissions, we attach policy objects to each of these groups\. When it is time to evaluate a user’s permissions, we can use the `LookupPolicy` API action on that user’s object\. The `LookupPolicy` API action walks the tree from the specified policy object up to the root\. It stops at each node and checks for any attached policies and returns those\.

#### Policy Attachments<a name="policyattachments"></a>

Policies can be attached to other objects in two ways: normal parent\-child attachments and special policy attachments\. Using normal parent\-child attachments, a policy can be attached to a parent node\. This is often useful to provide an easy mechanism to locate policies within your data directory\. Policies cannot have children\. Policies attached via parent\-child attachments will not be returned during `LookupPolicy` API calls\. 

Policy objects can also be attached to other objects via policy attachments\. You can manage these policy attachments using the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachPolicy.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachPolicy.html) and [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachPolicy.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachPolicy.html) API actions\. Policy attachments allow policy nodes to be located when you use the LookupPolicy API\.

#### Policy Schema Specification<a name="policyschemaspec"></a>

In order to start using policies, you must first add a facet to your schema that support creating policies\. To accomplish this, create a facet setting the `objectType` of the facet to POLICY\. Creating objects using a facet with the type POLICY ensures that the object has policy capabilities\.

Policy facets inherit two attributes in addition to any attributes you add to the definition: 
+ **policy\_type** \(String, Required\) – This is an identifier you can provide to distinguish between different policy uses\. If your policies logically fall into clear categories, we encourage setting the policy type attribute appropriately\. The `LookupPolicy` API returns the policy type of attached policies \(see [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_PolicyAttachment.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_PolicyAttachment.html)\)\. This allows easy filtering of the specific policy type that you are looking for\. It also allows you to use policy\_type to decide how the document should be processed or interpreted\. 
+ **policy\_document** \(Binary, Required\) – You can store application specific data in this attribute, such as permission grants associated with the policy\. You can also store application\-related data in normal attributes on your facet, if you prefer\.

#### Policy API Overview<a name="policyapioverview"></a>

A variety of specialized API actions are available for working with policies\. For a list of available operations, see [Amazon Cloud Directory Actions](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_Operations.html)\. 

To create a policy object, use the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateObject.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateObject.html) API action with an appropriate facet:
+ To attach or detach a policy from an object, use the actions `AttachPolicy` and `DetachPolicy` respectively\.
+ To find policies that are attached to objects up the tree, use the `LookupPolicy` API action\.
+ To list the policies that are attached to a particular object, use the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectPolicies.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectPolicies.html) API action\.

For a list of operations and the permissions required to perform each API action, see [Amazon Cloud Directory API Permissions: Actions, Resources, and Conditions Reference](UsingWithDS_IAM_CD_ResourcePermissions.md)\.

## Directory Structure<a name="dirstructure"></a>

Data in a directory is structured hierarchically in a tree pattern consisting of nodes, leaf nodes, and links between the nodes, as shown in the following illustration\. This is useful in application development to model, store, and quickly traverse hierarchical data\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/)![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/)

### Root Node<a name="rootnode"></a>

The root is the top node in a directory that is used to organize the parent and child nodes in the hierarchy\. This is similar to how folders in a file system can contain subfolders and files\.

### Node<a name="node"></a>

A node represents an object that can have child objects\. For example, a node can logically represent a group of managers whereby various user objects are the children, or leaf nodes\. A node object can only have one parent\.

### Leaf Node<a name="leafnode"></a>

A leaf node represents an object with no children that may or may not be directly connected to a parent node\. For example, a user or device object\. A leaf node object can have multiple parents\. While leaf node objects are not required to be connected to a parent node, it is strongly recommended that you do so, since without a path from the root, the object can only be accessed by it’s `NodeId`\. If you misplace the id of such an Object, you will have no way to locate it again\.

### Node Link<a name="link"></a>

The connection between one node and another\. Cloud Directory supports a variety of link types between nodes, including parent\-child links, policy links, and index attribute links\.

## Schema<a name="whatisschema"></a>

A schema is a collection of facets that define what objects can be created in a directory and how they are organized\. A schema also enforces data integrity and interoperability\. A single schema can be applied to more than one directory at a time\. For more information, see [Schemas](cd_schemas.md)\.

### Facet<a name="facets"></a>

A facet is a collection of attributes, constraints, and links defined within a schema\. Combined together, facets define the objects in a directory\. For example, Person and Device can be facets to define corporate employees with association of multiple devices\. For more information, see [Facets](whatarefacets.md)\.

### Sample Schemas<a name="sampleschemas"></a>

The set of sample schemas provided by default in the AWS Directory Service console\. For example, Person, Organization, and Device are all sample schemas\. For more information, see [Sample Schemas](sampleschemastopic.md)\.

### Custom Schemas<a name="customschemas"></a>

One or more schemas defined by a user that can be uploaded from the Schemas section or during the Cloud Directory creation process of the AWS Directory Service console, or created by API calls\.