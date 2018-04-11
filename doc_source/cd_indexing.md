# Indexing and Search<a name="cd_indexing"></a>

Amazon Cloud Directory supports two methods of indexing: Value based and type based\. Value\-based indexing is the most common form\. With it you can index and search for objects in the directory based on the values of object attributes\. With type\-based indexing, you can index and search for objects in the directory based on object types\. Facets help define object types\. For more information about schemas and facets, see [Schemas](cd_schemas.md) and [Facets](whatarefacets.md)\.

Indexes in Cloud Directory enable simple listing of other objects by those objects' attribute or facet values\. Each index is defined at creation to work with a specific named attribute or facet\. For example, an index may be defined on the “email” attribute of the “Person” facet\. Indexes are first\-class objects, which means that clients can create, modify, list, and delete them flexibly according to the application logic’s needs\.

Conceptually, indexes are similar to nodes with children, where the links to the indexed nodes are labeled according to the indexed attributes, rather than being given a label when the child is attached\. However, index links are not parent\-child edges, and have their own set of enumeration API operations\.

It’s important to understand that indexes in Cloud Directory are not automatically populated as they might be in other systems\. Instead, you use API calls to directly attach and detach objects to or from the index\. Although this is a bit more work, it gives you flexibility to define varying index scopes\. For example, you can define an index that tracks only direct children of a specific node\. Or you can define an index that tracks all objects in a given branch under a local root, such as all nodes in a department\. You can also do both at the same time\.

**Index lifecycle**

You can use the following API calls to help with the development lifecycle of indexes\. 

1. You create indexes with the `[CreateIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateIndex.html)` API call\. You supply an index definition structure that describes the attributes on attached objects that the index will track\. The definition also indicates whether or not the index should enforce uniqueness\. The result is an object ID for the new index, which should immediately be attached to your hierarchy like any other object\. For example, this can be a branch dedicated to holding indexes\.

1. You attach objects to the index manually with the `[AttachToIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachToIndex.html)` API call\. The index then automatically tracks the values of its defined attributes on each attached object\.

1. To use the indexes to search for objects with more efficient enumeration, call `[ListIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIndex.html)` and specify a range of values that you are interested in\.

1. Use the `[ListAttachedIndices](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListAttachedIndices.html)` API call to enumerate the indexes that are attached to a given object\.

1. Use the `[DetachFromIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachFromIndex.html)` API call to remove objects from the index manually\.

1. Once you detach all objects from the index, you can delete the index with the `[DeleteObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DeleteObject.html)` API call\.

There is no limit on the number of indexes within a directory, other than the limit on the space used by all objects\. Indexes and their attachments do consume space, but it is similar to that consumed by nodes and parent–child links\. There is a limit on the number of indexes that can be attached to a given object\. For more information, see [Limits for Amazon Cloud Directory](cd_limits.md)\.

**Facet\-Based Indexing**

With facet\-based indexing and search, you can optimize your directory searches by searching only a subset of your directory\. To do this, you use a schema *facet*\. For example, instead of searching across all the user objects in your directory, you can search only the user objects that contain an employee facet\. This efficiency helps reduce the latency time and amount of data retrieved for the query\. 

With facet\-based indexing, you can use the Cloud Directory index API operations to create and attach an index to the facets of objects\. You can also list the index results and then filter those results based on certain facets\. This can effectively reduce query times and the amount of data by narrowing the search scope to only objects that contain a certain type of facet\.

The `“facets”` attribute that is used with the `[CreateIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateIndex.html)` and `[ListIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIndex.html)` API calls surfaces the collection of facets that are applied to an object\. This attribute is available for use only with the `CreateIndex` and `ListIndex` API calls\. As shown in the following sample code, the schema ARN uses the directory’s region, owner account, and directory ID to reference the Cloud Directory schema\. This service\-provided schema does not appear in listings\.

```
String cloudDirectorySchemaArn = String.format(“arn:aws:clouddirectory:%s:%s:directory/%s/schema/CloudDirectory/1.0", region, ownerAccount, directoryId);
```

For example, the following sample code creates a facet\-based index specific to your AWS account and directory where you could enumerate all objects that are created with the facet `SalesDepartmentFacet`\. 

**Note**  
Make sure to use the “facets” value within the parameters as shown below\. Instances of “facets” shown in the sample code refer to a value that is provided and controlled by the Cloud Directory service\. You can use these for indexing but can have read\-only access\.

```
// Create a facet-based index
String cloudDirectorySchemaArn = String.format(“arn:aws:clouddirectory:%s:%s:directory/%s/schema/CloudDirectory/1.0",
    region, ownerAccount, directoryId);

facetIndexResult = clouddirectoryClient.createIndex(new CreateIndexRequest() 
  .withDirectoryArn(directoryArn) 
  .withOrderedIndexedAttributeList(List(new AttributeKey()     
        .withSchemaArn(cloudDirectorySchemaArn)     
        .withFacetName("facets")     
        .withName("facets"))) 
        .withIsUnique(false) 
        .withParentReference("/") 
        .withLinkName("MyFirstFacetIndex"))
facetIndex = facetIndexResult.getObjectIdentifier()

// Attach objects to the facet-based index
clouddirectoryClient.attachToIndex(new AttachToIndexRequest().withDirectoryArn(directoryArn)
  .withIndexReference(facetIndex).withTargetReference(userObj))

// List all objects
val listResults = clouddirectoryClient.listIndex(new ListIndexRequest()
  .withDirectoryArn(directoryArn)
  .withIndexReference(facetIndex)
  .getIndexAttachments()

// List the index results filtering for a certain facet
val filteredResults = clouddirectoryClient.listIndex(new ListIndexRequest()
  .withDirectoryArn(directoryArn)
  .withIndexReference(facetIndex)
  .withRangesOnIndexedValues(new ObjectAttributeRange()
    .withAttributeKey(new AttributeKey()
      .withFacetName("facets")
      .withName("facets")
      .withSchemaArn(cloudDirectorySchemaArn))
    .withRange(new TypedAttributeValueRange()
      .withStartMode(RangeMode.INCLUSIVE)
      .withStartValue("MySchema/1.0/SalesDepartmentFacet")
      .withEndMode(RangeMode.INCLUSIVE)
      .withEndValue("MySchema/1.0/SalesDepartmentFacet")
    )))
```

**Unique vs Nonunique Indexes**

Unique indexes differ from nonunique indexes in enforcing uniqueness of the indexed attribute values for objects that are attached to the index\. For example, you might want to populate Person objects into two indexes, a unique one on an “email” attribute, and a nonunique one on a “lastname” attribute\. The lastname index allows many Person objects with the same last name to be attached\. On the other hand, the `AttachToIndex` call that targets the email index returns a `LinkNameAlreadyInUseException` error if a Person with the same email attribute is already attached\. Note that the error does not remove the Person object itself\. Consequently, an application might create the Person, attach it to the hierarchy, and attach it to indexes, all in a single batch request\. This ensures that if uniqueness is violated on any of the indexes, the object and all of its attachments are rolled back automatically\.