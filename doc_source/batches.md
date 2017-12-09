# Batches<a name="batches"></a>

With Amazon Cloud Directory, it’s often necessary to add new objects or add relationships between new objects and existing objects to reflect changes in a real\-world hierarchy\. Batch operations can make directory tasks like these easier to manage by providing the following benefits:

+ Batch operations can minimize the number of round trips required to write and read objects to and from your directory, improving the overall performance of your application\.

+ Batch write provides the SQL database\-equivalent transaction semantics\. All operations successfully complete, or if any operation has a failure then none of them are applied\.

+ Using batch reference you can create an object and use a reference to the new object for further action such as adding it to a relationship, reducing overhead of using a read operation before a write operation\. 

## BatchWrite<a name="batchwrite"></a>

Use [BatchWrite](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_BatchWrite.html) operations to perform multiple write operations on a directory\. All operations in batch write are executed sequentially\. It works similar to SQL database transactions\. If one of the operation inside batch write fails, the entire batch write has no effect on the directory\. If a batch write fails, a batch write exception occurs\. The exception contains the index of the operation that failed along with exception type and message\. This information can help you identify the root cause for the failure\.

The following API operations are supported as part of batch write:

+ [AddFacetToObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AddFacetToObject.html)

+ [AttachObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachObject.html)

+ [AttachPolicy](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachPolicy.html)

+ [AttachToIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachToIndex.html)

+ [AttachTypedLink](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_AttachTypedLink.html)

+ [CreateIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateIndex.html)

+ [CreateObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_CreateObject.html)

+ [DeleteObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DeleteObject.html)

+ [DetachFromIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachFromIndex.html)

+ [DetachObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachObject.html)

+ [DetachTypedLink](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_DetachTypedLink.html)

+ [RemoveFacetFromObject](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_RemoveFacetFromObject.html)

+ [UpdateObjectAttributes](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateObjectAttributes.html)

### Batch Reference Name<a name="batchreferencename"></a>

Batch reference names are supported only for batch writes when you need to refer to an object as part of the intermediate batch operation\. For example, suppose that as part of a given batch write, 10 different objects are being detached and are attached to a different part of the directory\. Without batch reference, you would have to read all 10 object references and provide them as input during reattachment as part of the batch write\. You can use a batch reference to identify the detached resource during attachment\. A batch reference can be any regular string prefixed with the number sign / hashtag symbol \(\#\)\.

For example, in the following code sample, an object with link name `"this-is-a-typo"` is being detached from root with a batch reference name `"ref"` \. Later the same object is attached to the root with the link name as `"correct-link-name"` \. The object is identified with the child reference set to batch reference\. Without the batch reference, you would initially need to get the `objectIdentifier` that is being detached and provide that in the child reference during attachment\. You can use a batch reference name to avoid this extra read\.

```
BatchDetachObject batchDetach = new BatchDetachObject()
        .withBatchReferenceName("ref")
        .withLinkName("this-is-a-typo")
        .withParentReference(new ObjectReference().withSelector("/"));
BatchAttachObject batchAttach = new BatchAttachObject()
        .withParentReference(new ObjectReference().withSelector("/"))
        .withChildReference(new ObjectReference().withSelector("#ref"))
        .withLinkName("correct-link-name");
BatchWriteRequest batchWrite = new BatchWriteRequest()
        .withDirectoryArn(directoryArn)
        .withOperations(new ArrayList(Arrays.asList(batchDetach, batchAttach)));
```

## BatchRead<a name="batchread"></a>

Use [BatchRead](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_BatchRead.html) operations to perform multiple read operations on a directory\. For example, in the following code sample, children of object with reference `“/managers”` is being read along with attributes of object with reference `“/managers/bob”` in a single batch read\.

```
BatchListObjectChildren listObjectChildrenRequest = new BatchListObjectChildren()
        .withObjectReference(new ObjectReference().withSelector("/managers"));
BatchListObjectAttributes listObjectAttributesRequest = new BatchListObjectAttributes()
        .withObjectReference(new ObjectReference().withSelector("/managers/bob"));
BatchReadRequest batchRead = new BatchReadRequest()
        .withConsistencyLevel(ConsistencyLevel.SERIALIZABLE)
        .withDirectoryArn(directoryArn)
        .withOperations(new ArrayList(Arrays.asList(listObjectChildrenRequest, listObjectAttributesRequest)));
BatchReadResult result = cloudDirectoryClient.batchRead(batchRead);
```

BatchRead supports the following API operations:

+ [GetObjectInformation](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_GetObjectInformation.html)

+ [ListAttachedIndices](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListAttachedIndices.html)

+ [ListIncomingTypedLinks](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIncomingTypedLinks.html)

+ [ListIndex](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListIndex.html)

+ [ListObjectAttributes](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectAttributes.html)

+ [ListObjectChildren](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectChildren.html)

+ [ListObjectParentPaths](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectParentPaths.html)

+ [ListObjectPolicies](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectPolicies.html)

+ [ListOutgoingTypedLinks](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListOutgoingTypedLinks.html)

+ [ListPolicyAttachments](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListPolicyAttachments.html)

+ [LookupPolicy](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_LookupPolicy.html)

## Limits on Batch operations<a name="batchlimits"></a>

Each request to the server \(including batched requests\) has a maximum number of resources that can be operated on, regardless of the number of operations in the request\. This allows you to compose batch requests with high flexibility as long as you stay within the resource maximums\. For more information on resource maximums, see [AWS Directory Service Limits](limits.md)\.

Limits are calculated by summing the writes or reads for each single operation inside the Batch​\. For example, the read operation limit is currently 200 objects per API call\. Let’s say you want to compose a batch that adds 9 [ListObjectChildren](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_ListObjectChildren.html) API calls and each call requires reading 20 objects \. Since the total number of read objects \(9 x 20 = 180\) does not exceed 200, the batch operation would succeed\. 

The same concept applies with calculating write operations\. For example, the write operation limit is currently 20\. If you set up your batch to add 2 [UpdateObjectAttributes](http://docs.aws.amazon.com/directoryservice/latest/APIReference/API_UpdateObjectAttributes.html) API calls with 9 write operations each, this would also succeed\. In either case, should the batch operation exceed the limit, then the operation will fail and a `LimitExceededException` will be thrown\.

## Exception handling<a name="exceptionhandling"></a>

Batch operations in Cloud Directory can sometimes fail\. In these cases, it is important to know how to handle such failures\. The method you use to resolve failures differs for write operations and read operations\.

### Batch write operation failures<a name="batchwritefailures"></a>

If a batch write operation fails, Cloud Directory fails the entire batch operation and returns an exception\. The exception contains the index of the operation that failed along with the exception type and message\. If you see `RetryableConflictException`, you can try again with exponential backoff\. A simple way to do this is to double the amount of time you wait each time you get an exception or failure\. For example, if your first batch write operation fails, wait 100 milliseconds and try the request again\. If the second request fails, wait 200 milliseconds and try again\. If the third request fails, wait 400 milliseconds and try again\.

### Batch read operation failures<a name="batchreadfailures"></a>

If a batch read operation fails, the response contains either a successful response or an exception response\. Individual batch read operation failures do not cause the entire batch read operation to fail—Cloud Directory returns individual success or failure responses for each operation\.

**Related Cloud Directory Blog Articles**

+ [Write and Read Multiple Objects in Amazon Cloud Directory by Using Batch Operations](https://aws.amazon.com/blogs/security/write-and-read-multiple-objects-in-amazon-cloud-directory-by-using-batch-operations/)

+ [How to Use Batch References in Amazon Cloud Directory to Refer to New Objects in a Batch Request](https://aws-preview.aka.amazon.com/blogs/security/how-to-use-batch-references-in-amazon-cloud-directory-to-refer-to-new-objects-in-a-batch-request/)