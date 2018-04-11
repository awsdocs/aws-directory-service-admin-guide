# Using the Cloud Directory APIs<a name="cd_using_api"></a>

Amazon Cloud Directory includes a set of API operations that enable programmatic access to Cloud Directory capabilities\. You can use the [Amazon Cloud Directory API Reference Guide](http://docs.aws.amazon.com/directoryservice/latest/APIReference/welcome.html) to learn how to make requests to the Cloud Directory API for creating and managing the various elements\. It also covers the components of requests, the content of responses, and how to authenticate requests\.

Cloud Directory provides all necessary API operations that enable developers to build new applications\. It provides the following categories of API calls:
+ Create, read, update, delete \(CRUD\) for schema
+ CRUD for facet
+ CRUD for directories
+ CRUD for objects \(nodes, policies, etc\.\)
+ CRUD for Index definition
+ Batch read, batch write

## How Billing Works With Cloud Directory APIs<a name="billingcdapis"></a>

Billing for API calls vary based on the specific types of API calls being made\. There are specific billing rates for Eventually Consistent Read API calls, Strongly Consistent Read API calls, and Write API calls\. Metadata API calls are free\. 

Strongly Consistent operations are used for read\-after\-write consistency when reading a value\. Eventually Consistent operations are used for retrieving a value while updates are running\. With Eventually Consistent operations retrieved results might not be the most accurate since the specific host you are reading the value from is still processing updates\. However, the latency for such read operations are low when you retrieve a performance call\. 

When reading data from Cloud Directory, you must specify either an Eventually Consistent Read or Strongly Consistent Read type operation\. The read type is based on consistency level\. The two consistency levels are EVENTUAL for Eventually Consistent Reads and SERIALIZABLE for Strongly Consistent Reads\. For more information, see [Consistency Levels](consistencylevels.md)\. 

The following table lists all of the Cloud Directory APIs and how they can impact billing for your AWS account\.


****  

| API | Eventually Consistent Read 1 | Strongly Consistent Read 2 | Write 3 | Metadata 4 | 
| --- | --- | --- | --- | --- | 
| AddFacetToObject |  |  | X |  | 
| ApplySchema |  |  |  | X | 
| AttachObject |  |  | X |  | 
| AttachPolicy |  |  | X |  | 
| AttachToIndex |  |  | X |  | 
| AttachTypedLink |  |  | X |  | 
| BatchRead | X | X |  |  | 
| BatchWrite |  |  | X |  | 
| CreateDirectory |  |  | X |  | 
| CreateFacet |  |  |  | X | 
| CreateIndex |  |  | X |  | 
| CreateObject |  |  | X |  | 
| CreateSchema |  |  |  | X | 
| CreateTypedLinkFacet |  |  |  | X | 
| DeleteDirectory |  |  |  | X | 
| DeleteFacet |  |  |  | X | 
| DeleteObject |  |  | X |  | 
| DeleteSchema |  |  |  | X | 
| DetachFromIndex |  |  | X |  | 
| DetachObject |  |  | X |  | 
| DetachPolicy |  |  | X |  | 
| DetachTypedLink |  |  | X |  | 
| DeleteTypedLinkFacet |  |  |  | X | 
| DisableDirectory |  |  |  | X | 
| EnableDirectory |  |  | X |  | 
| GetAppliedSchemaVersion |  |  |  | X | 
| GetDirectory |  |  |  | X | 
| GetFacet |  |  |  | X | 
| GetObjectAttributes | X | X |  |  | 
| GetObjectInformation | X | X |  |  | 
| GetSchemaAsJson |  |  |  | X | 
| GetTypedLinkFacetInformation |  |  |  | X | 
| ListAppliedSchemaArns |  |  |  | X | 
| ListAttachedIndices | X | X |  |  | 
| ListDevelopmentSchemaArns |  |  |  | X | 
| ListDirectories |  |  |  | X | 
| ListFacetAttributes |  |  |  | X | 
| ListFacetNames |  |  |  | X | 
| ListIncomingTypedLinks | X | X |  |  | 
| ListIndex | X | X |  |  | 
| ListObjectAttributes | X | X |  |  | 
| ListObjectChildren | X | X |  |  | 
| ListObjectParentPaths | X |  |  |  | 
| ListObjectParents | X | X |  |  | 
| ListObjectPolicies | X | X |  |  | 
| ListOutgoingTypedLinks | X | X |  |  | 
| ListPolicyAttachments | X | X |  |  | 
| ListPublishedSchemaArns |  |  |  | X | 
| ListTagsForResource |  |  |  | X | 
| ListTypedLinkFacetAttributes |  |  |  | X | 
| ListTypedLinkFacetNames |  |  |  | X | 
| LookupPolicy | X |  |  |  | 
| PublishSchema |  |  |  | X | 
| PutSchemaFromJson |  |  |  | X | 
| RemoveFacetFromObject |  |  | X |  | 
| TagResource |  |  |  | X | 
| UntagResource |  |  |  | X | 
| UpdateFacet |  |  |  | X | 
| UpdateObjectAttributes |  |  | X |  | 
| UpdateSchema |  |  |  | X | 
| UpdateTypedLinkFacet |  |  |  | X | 
| UpgradeAppliedSchema |  |  |  | X | 
| UpgradePublishedSchema |  |  |  | X | 

1 Eventually Consistent Read APIs are called with the EVENTUAL consistency level

2 Strongly Consistent Read APIs are called with the SERIALIZABLE consistency level

3 Write APIs are billed as write API calls

4 Metadata APIs are NOT billed but are categorized as Metadata API calls

For additional information about billing, see [Amazon Cloud Directory Pricing](https://aws.amazon.com/cloud-directory/pricing/)\.