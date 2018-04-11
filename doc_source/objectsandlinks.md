# Objects and Links<a name="objectsandlinks"></a>

This section describes objects and links and how the directory identifies them\.

**Topics**
+ [Objects](#objects2)
+ [Links](#links)
+ [Range Filters](#rangefilters)
+ [Accessing Objects](#accessingobjects)

## Objects<a name="objects2"></a>

An object is a basic element of Cloud Directory\. Each object has a globally unique identifier, which is specified by the object Identifier\. An object is a collection of zero or more facets with their attribute keys and values\. An object can be created from one or more facets within a single applied schema or from facets of multiple applied schemas\. During object creation, you must specify all required attribute values\. Objects can have a limited number of facets\. For more information, see [Limits for Amazon Cloud Directory](cd_limits.md)\. 

An object can be a regular object, a policy object, or an index object\. An object can also be a node object or a leaf node object\. The type of the object is inferred from the object type of the facets attached to it\.

## Links<a name="links"></a>

A link is a directed edge between two objects that define a relationship\. Cloud Directory currently supports the following link types\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/cd_objectlinks.png)

### Child Links<a name="childlinks"></a>

A child link creates a parent–child relationship between the objects it connects\. For example, in the above illustration child link **b** connects objects `001` and `003`\. Child links define the hierarchy in Cloud Directory\. Child links have names when they participate in defining the path of the object that the link points to\.

### Attachment Links<a name="attachmentlinks"></a>

An attachment link applies a leaf node policy object to another leaf node or a node object\. Attachment links do not define the hierarchical structure of Cloud Directory\. For example, in the above illustration, attachment link applies the policy stored in policy leaf node object `006` on node object `002` \. Each object can have multiple policies attached but not more than one policy of any given policy type can be attached\.

### Index Links<a name="indexlinks"></a>

Index links provide rich information lookup based on an index object and your defined indexed attributes, thus enabling fast tree traversals and searches within the directory trees\. Conceptually, indexes are similar to nodes with children: The links to the indexed nodes are labeled according to the indexed attributes, rather than being given a label when the child is attached\. However, index links are not parent\-child edges, and have their own set of enumeration API operations\. For more information, see [Indexing and Search](cd_indexing.md)\.

### Typed Links<a name="typedlink"></a>

Typed links are a special type of link\. With a typed link, you can attach any two objects and add attributes to that attachment\. You can use typed links to model relationships between different objects in your directory\. For example, in the illustration above, consider the relationship between object `004`, which represents a user, and object `005`, which represents a device\. We might use a typed link to model an ownership relationship between the two objects\. We could add attributes to the typed link to represent the date of purchase or whether the device is rented or purchased\. 

As with objects, you must create a typed link facet using the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateTypedLinkFacet.html) API to define the typed link structure and its attributes\. Typed link facets require a unique facet name and set of attributes that are associated with the link\. With Cloud Directory, the schema designer can define an ordered set of attributes on the typed link facet\. To view a typed links sample schema, see [Schema Document with Typed Links](completeexample.md#schematyped)\.

Typed link attributes can be used when you need to do any of the following:
+ Represent the relationship between two objects\.
+ Allow for quick filtering of incoming or outgoing typed links\. For more information, see [Typed Link Listing](#typedlinklisting)\.

Consider the following when deciding if typed links are right for your use case: 
+ Typed links cannot be used in path\-based object specification\. Instead, you must select typed links using the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html) or [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html) API operations\.
+ Typed links do not participate in [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html) or [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParentPaths.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParentPaths.html) API operations\. 
+ Typed links between the same two objects and in the same direction may not have the same attribute values\. This can help avoid duplicated typed links between the same objects\.
+ The combined size of all identity attribute values is limited to 64 bytes\. For more information, see [Limits for Amazon Cloud Directory](cd_limits.md)\.

**Related Cloud Directory Blog Article**
+ [Use Amazon Cloud Directory Typed Links to Create and Search Relationships Across Hierarchies](https://aws.amazon.com/blogs/security/new-use-amazon-cloud-directory-typed-links-to-create-and-manage-relationships-in-your-directory/)

#### Typed Link Identity<a name="typedlinkid"></a>

Identity is what uniquely defines whether a typed link can exist between two objects\. The exception is when you connect two objects in one direction with the exact same attribute values\. Attributes must be configured as `REQUIRED_ALWAYS`, since all attributes contribute to identity\.

Typed links that are created from different typed link facets never conflict with each other\. For example, consider the following diagram:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/cd_typedlinks.png)
+ Object `001` has typed links and attributes \(A1 and A2\) with the same attribute values \(x1 and x2\) going to different objects \(`002` and `003`\)\. This operation would succeed\.
+ Objects `002` and `003` have a typed link between them\. This operation would fail because two typed links in the same direction with the same attributes cannot exist between objects\.
+ Objects `001` and `003` have two typed links between them with the same attributes\. However, since the links go in different directions, this operation would succeed\.
+ Objects `002` and `003` have typed links between them with the same value for A1 but different values for A2\. Typed link identity considers all attributes so this operation would succeed\.

#### Typed Link Rules<a name="typedlinkrules"></a>

You can add rules to typed link attributes when you want to add restrictions to link attributes\. These rules are equivalent to rules on object attributes\. For more information, see [Attribute Rules](attributerules.md)\.

#### Typed Link Listing<a name="typedlinklisting"></a>

Cloud Directory provides API operations that you can use to select incoming or outgoing typed links from an object\. You can select a specific subset of typed links rather than iterating over every typed link\. You can also specify a particular typed link facet to filter only typed links of that type\.

You can filter typed links based on the order that the attributes are defined on the typed link facet\. You can provide range filters for multiple attributes\. When providing ranges to a typed link selection, any inexact ranges much be specified at the end\. Any attributes with no range specified are presumed to match the entire range\. Filters are interpreted in the order of the attributes that are defined on the typed link facet, not the order they are supplied to any API calls\.

For example, in the following diagram, consider a Cloud Directory that is used to store information about Employees and their Abilities\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/cd_typedlinklisting.png)

Let’s say we model our employee’s capabilities with a typed link named `EmployeeCapability`, which is configured with two string attributes: `Status` and `Role`\. The following filters are supported on [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html) and [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html) API operations\.
+ Facet = `EmployeeCapability`, Status = `Active`, Role = `Driver`
  + Selects active employees who are drivers\. This filter includes two exact matches\.
+ Facet = `EmployeeCapability`, Status = `Active`
  + Selects all active employees\.
+ Facet = `EmployeeCapability`, Status = `Active`, Role = `A` to `M`
  + Selects active employees with roles starting with `A` through `M`\.
+ Facet = `EmployeeCapability`
  + This selects all typed links of the `EmployeeCapability` type\.

The following filters would **NOT** be supported:
+ Facet = `EmployeeCapability`, Status between `A` to `C`, Role = `Driver`
  + This filter is not allowed because any ranges must appear at the end of the filter\.
+ Facet = `EmployeeCapability`, Role = `Driver`
  + This filter is not allowed because the implicit status range is not an exact match and does not appear at the end of the list of ranges\.
+ Status = `Active`
  + This filter is not allowed because the typed link facet is not specified\.

#### Typed Link Schema<a name="typedlinkschema"></a>

You can create typed link facets in two ways\. You can manage your typed link facets from individual API calls, including [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateTypedLinkFacet.html), [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DeleteTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DeleteTypedLinkFacet.html), and [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateTypedLinkFacet.html)\. You can also upload a JSON document that represents your schema in a single [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_PutSchemaFromJson.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_PutSchemaFromJson.html) API call\. For more information, see [JSON Schema Format](jsonformat.md#json)\. To view a typed links sample schema, see [Schema Document with Typed Links](completeexample.md#schematyped)\.

The types of changes allowed at different phases of the schema development lifecycle are similar to changes that are allowed for object facet manipulation\. Schemas in the development state support any changes\. Schemas in the published state are immutable and no changes are supported\. Only certain changes are allowed to schemas that are applied to a data directory\. Once you set the order and attributes on an applied typed link facet, that order cannot be changed\.

Two other API operations list facets and their attributes:
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetAttributes.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetAttributes.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetNames.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetNames.html)

#### Typed Link Interaction<a name="typedlinkinteraction"></a>

Once a typed link facet has been created, you are ready to start creating and interacting with typed links\. To attach and detach typed links, use the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html) and [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html) API operations\.

The `TypedLinkSpecifier` is a structure that contains all the information to uniquely identify a typed link\. Within that structure you can find `TypedLinkFacet`, `SourceObjectID`, `DestinationObjectID`, and `IdentityAttributeValues`\. These are used to uniquely specify the typed link being operated on\. The [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html) API operation returns a typed link specifier while the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html) API operation accepts one as input\. Similarly, the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html) and [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html) API operations provide typed link specifiers as output\. You can construct a typed link specifier from scratch as well\. The full list of typed link\-related API operations, include the following:
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateTypedLinkFacet.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DeleteTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DeleteTypedLinkFacet.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetTypedLinkFacetInformation.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetTypedLinkFacetInformation.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetNames.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetNames.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetAttributes.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListTypedLinkFacetAttributes.html)
+ [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateTypedLinkFacet.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateTypedLinkFacet.html)

**Note**  
Attribute references and updating typed links are not supported\. To update a typed link, you must remove it and add the updated version\. 
Typed links cannot contain attributes that do not contribute to identity\.
Batch support for typed links is not yet supported but is planned for release in the near future\.

## Range Filters<a name="rangefilters"></a>

Several Cloud Directory list APIs allow specifying a filter in the form of a range\. These filters allow you to efficiently select subsets of the links attached to the specified node\.

Ranges are generally supplied as a map \(array of key\-value pairs\) whose keys are attribute identifiers and whose values are the corresponding ranges\. This allows filtering links whose identities consist of one or more attributes\. For example, a TypedLink set up to model a Role relationship for determining permissions might have both RoleType and Authorizer attributes\. A [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html) call could then specify ranges to filter the result to RoleType:”Admin” and Authorizer:”Julia”\. The map of ranges used to filter a single list request must contain only attributes that define the link’s identity \(an index’s OrderedIndexedAttributeList or a TypedLink’s IdentityAttributeOrder\), but it need not contain ranges for all of them\. Missing ranges will automatically be filled in with ranges that span all possible values \(from FIRST to LAST\)\.

If you think of each attribute as defining an independent flat domain of values, the range structures define two logical points in that domain — the start and end points — and the range matches all of the possible points in between those points\. The StartValue and EndValue of the range structure define the basis for these two points with the “modes” further refining them to indicating whether each point itself is to be included or excluded from the range\. In the RoleType:”Admin” example above, the values for the RoleType attribute would both be “Admin”, and the modes are both “INCLUSIVE” \(written as \[“Admin” to “Admin”\]\)\. A filter for a ListIndex call where the index is defined on the LastName of a User facet might use StartValue=”D”, StartMode=INCLUSIVE, EndValue:”G”, EndMode:EXCLUSIVE to narrow the listing to names starting with D, E, or F\.

The start point of a range must always precede or be equal to the end point\. Cloud Directory will return an error if EndValue precedes the StartValue\. The values must also be of the same primitive type as the attribute they are filtering, String values for a String attribute, Integer for an Integer attribute, and so on\. StartValue=“D”, StartMode=EXCLUSIVE, EndValue=“D”, EndMode=INCLUSIVE is invalid, for instance, because the end point includes the value while the start point follows the value\.

There are three special modes that can be used by either start or end points\. The following modes do not require the corresponding value field to be specified, as they imply a position on their own\.
+ **FIRST \-** precedes all possible values in the domain\. When used for the start point, this matches all possible values from the beginning of the domain up to the end point\. When used for the end point, no values in the domain will match the range\.
+ **LAST \-** follows all possible values in the domain\. When used for the end point, this matches all possible values that follow the start point, including missing values\. When used for the start point, no values in the domain will match the range\.
+ **LAST\_BEFORE\_MISSING\_VALUES \-** This mode is only useful for optional attributes where the value may be omitted \(see [Missing values](#missingvalues)\)\. It corresponds to the point between the missing values and the actual domain values\. When used for the end point, this matches all non\-missing domain values that follow the start point\. When used for the start point, it excludes all non\-missing domain values\. If the attribute is a required one, this mode is equivalent to LAST, as there can be no missing values\.

### Multiple range limitations<a name="multiplerangelimits"></a>

Cloud Directory limits patterns where there are multiple attributes in order to guarantee efficient, low\-latency request processing\. Each link with multiple identifying attributes specifies them in a well\-defined order\. For instance, the Role example above defines the RoleType attribute as most significant, and the Authorizer attribute as least significant\. A List request can specify only a single “qualifying” range that is not either 1\) a single value or 2\) spans all possible values \(there can be multiple ranges that match these two requirements\)\. Any ranges for more significant attributes than the qualifying range attribute must specify a single value, and any ranges for less significant ranges must span all possible values\. In the Role example, the filter sets \(RoleType:”Admin”, Authorizer:\[“J” to “L”\]\) \(single value \+ qualifying range\), \(RoleType:\[”Admin” to “User”\]\) \(qualifying range \+ implicit spanning range\), and \(RoleType:\[FIRST to LAST\]\) \(two spanning ranges, one implicit\) are all examples of valid filter sets\. \(RoleType:\[FIRST to LAST\], Authorizer:”Julia”\) is not a valid set, since the spanning range is more significant than the single value range\.

Some useful patterns when filling in the range structures, include:

**Matching a single value**

Specify the value for both StartValue and EndValue, and set both modes to “INCLUSIVE”\.

Example: `StartValue=“Admin”, StartMode=INCLUSIVE, EndValue=“Admin”, EndMode=INCLUSIVE`

**Matching a prefix**

Specify the prefix as the StartValue with INCLUSIVE mode, and the first value after the prefix as EndValue with an EXCLUSIVE mode\.

Example: `StartValue=“Jo”, StartMode=INCLUSIVE, EndValue=“Jp”, EndMode=EXCLUSIVE (“p” is the next character value after “o”)`

**Filtering for Greater Than a value**

Specify the value for StartValue with EXCLUSIVE mode, and LAST as the EndMode \(or LAST\_BEFORE\_MISSING\_VALUES to exclude missing values, if applicable\)\.

Example: `StartValue=127, StartMode=EXCLUSIVE, EndValue=null, EndMode=LAST`

**Filtering for Less Than or equal to a value**

Specify the value for the EndValue with INCLUSIVE mode, and FIRST as the StartMode\. 

### Missing values<a name="missingvalues"></a>

When an attribute is marked as Optional in the schema, it’s value may be “missing” since it need not have been supplied when the facet was attached or the attribute could have been subsequently deleted\. If the object with such a missing value is attached to an index, the index link is still present, but moved to the end of the set of links\. A `[ListIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIndex.html)` call will first return any links where the indexed attributes are all present before returning links where one or more are missing\. This is roughly similar to a relational database NULL value, with these values ordered after non\-NULL values\. You can specify whether a range includes these missing values or not by choosing the LAST or LAST\_BEFORE\_MISSING\_VALUES modes\. For example, you provide a filter to a ListIndex call to return just the missing values in an index by filtering with the range \[LAST\_BEFORE\_MISSING\_VALUES to LAST\]\.

## Accessing Objects<a name="accessingobjects"></a>

Objects in a directory can be accessed either by path or by `objectIdentifier`\.

 **Path:** Every object in a Cloud Directory tree can be identified and found by the pathname that describes how to reach it\. The path starts from the root of the directory \(Node `000` in the previous figure\)\. The path notation begins with the link labeled with a slash \(/\) and follows the child links separated by path separator \(also a slash\) until reaching the last part of the path\. For example, object `005` in the previous figure can be identified using the path `/group/a/d`\. Multiple paths may identify an object, since objects that are leaf nodes can have multiple parents\. The following path can also be used to identify object `005` : /group/b/e

 **ObjectIdentifier:** Every object in the directory has a unique global identifier, which is the `ObjectIdentifier`\. `ObjectIdentifier` is returned as part of the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateObject.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateObject.html) API call\. You can also fetch the `ObjectIdentifier` by using [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetObjectInformation.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetObjectInformation.html) API call\. For example, to fetch the object identifier of object `005`, you can call `GetObjectInformation` with object reference as the path that leads to the object, which is group/b/e or group/a/d\.

```
GetObjectInformationRequest request = new GetObjectInformationRequest()
    .withDirectoryArn(directoryArn)
    .withObjectReference("/group/b/e")
    .withConsistencyLevel(level)
GetObjectInformationResult result = cdClient.getObjectInformation(request)
String objectIdentifier = result.getObjectIdentifier()
```

### Populating Objects<a name="populatingobjects"></a>

New facets can be added to an object using [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AddFacetToObject.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AddFacetToObject.html) API call\. The type of the object is determined based on the facets attached to the object\. Object attachment in a directory works based on the type of the object\. When attaching an object, remember these rules:
+  A leaf node object cannot have children\.
+  A node object can have multiple children\.
+  An object of the policy type cannot have children and can have zero or one parent\.

### Updating Objects<a name="updatingobjects"></a>

You can update an object in multiple ways:

1.  Use the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateObjectAttributes.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateObjectAttributes.html) operation to update individual facet attributes on an object\.

1.  Use the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AddFacetToObject.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AddFacetToObject.html) operation to add new facets to an object\.

1.  Use the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_RemoveFacetFromObject.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_RemoveFacetFromObject.html) operation to delete existing facets from an object\.

### Deleting Objects<a name="deletingobjects"></a>

An attached object must meet certain conditions before you can delete it from a directory:

1.  You must detach the object from the tree\. You can detach an object only when it doesn’t have any children\. If the object has children, you must detach all the children first\.

1.  You can delete a detached object only if all the attributes on that object are deleted\. You can delete attributes on an object by deleting each facet attached to that object\. You can fetch a list of facets attached to an object by calling [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetObjectInformation.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetObjectInformation.html)\.

1.  An object must also have no parent, no policy attachments, and no index attachments\.

Because an object must be fully detached from the tree to be deleted, you must use the object identifier to delete it\.

### Querying Objects<a name="queryobjects"></a>

This section discusses various elements relevant for querying objects in a directory\.

#### Directory Traversal<a name="directorytraversal"></a>

Because Cloud Directory is a tree, you can query objects from the top down using the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectChildren.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectChildren.html) API operation or from the bottom up using the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParents.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParents.html) API operation\.

#### Policy Lookup<a name="policylookup"></a>

Given an object reference, the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html) API operation returns all the policies that are attached along its path \(or paths\) to the root in a top\-down fashion\. Any of the paths that are not leading up to the root are ignored\. All policy type objects are returned\.

If the object is a leaf node, it can have multiple paths to the root\. This call returns only one path for each call\. To fetch additional paths, use the pagination token\. 

#### Index Querying<a name="indexquerying"></a>

Cloud Directory supports rich index querying functionality with the use of the following ranges:
+ **FIRST \- **Starts from the first indexed attribute value\. The start attribute value is optional\.
+ **LAST \- **Returns attribute values up to the end of the index, including the missing values\. The end attribute value is optional\.
+ **LAST\_BEFORE\_MISSING\_VALUES \- **Returns attribute values up to the end of index, excluding missing values\.
+ **INCLUSIVE \- **Includes the attribute value being specified\.
+ **EXCLUSIVE \- **Excludes the attribute value being specified\.

#### Parent Path Listing<a name="parentpath"></a>

Using the [http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParentPaths.html](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParentPaths.html) API call, you can retrieve all available parent paths for any type of object \(node, leaf node, policy node, index node\)\. This API operation can be helpful when you need to evaluate all parents for an object\. The call returns all the objects from the directory root until the requested object\. It also returns the number of paths based on user\-defined `MaxResults`, in case of multiple paths to the parent\. The order of the paths and nodes returned is consistent among multiple API calls unless the objects are deleted or moved\. Paths not leading to the directory root are ignored from the target object\.

For an example on how this works, let's say a directory has an object hierarchy similar to the illustration shown below\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/cd_parent_path.png)

The numbered shapes represent the different objects\. The number of arrows between that object and the directory root \(`000`\) represent the complete path and would be expressed in the output\. The following table shows requests and responses from queries made to specific leaf node objects in the hierarchy\. 


**Example queries on objects**  

| Request | Response | 
| --- | --- | 
| 004, PageToken: null, MaxResults: 1 | \[\{/group/a/c\], \[000, 001, 002, 004\]\}\], PageToken: null | 
| 005, PageToken: null, MaxResults: 2 | \[\{/group/a/d, \[000, 001, 002, 005\]\}, \{ /group/b/e, \[000, 001, 003, 005\]\}\], PageToken: null In this example, object `005` has both nodes `002` and `003` as parents\. Also, since `MaxResults` is 2, both paths display objects in a list\.  | 
| 005, PageToken: null, MaxResults: 1 | \[\{/group/a/d, \[000, 001, 002, 005\]\}\], PageToken: <encrypted\_next\_token> | 
| 005, PageToken: <encrypted\_next\_token>, MaxResults: 1 | \[\{/group/b/e, \[000, 001, 003, 005\]\}\], PageToken: null In this example, object `005` has both nodes `002` and `003` as parents\. Also, since `MaxResults` is 1, multiple paginated calls with page tokens will be made to get all paths with a list of objects\.  | 
| 006, PageToken: null, MaxResults: 1 | \[\{/group/b/f, \[000, 001, 003, 006\]\}\], PageToken: null | 
| 007, PageToken: null, MaxResults: 1 | \[\{/group/a/index, \[000, 001, 002, 007\]\}\], PageToken: null | 