# Consistency Levels<a name="consistencylevels"></a>

Amazon Cloud Directory is a distributed directory store\. Data is distributed to multiple servers in different Availability Zones\. A successful write request updates the data on all servers\. Data is eventually available on all servers, usually within a second\. To aid users of the service, Cloud Directory offers two consistency levels for read operations\. This section describes the different consistency levels and eventually consistent nature of Cloud Directory\.

## Read Isolation Levels<a name="readisolationlevels"></a>

When reading data from Cloud Directory, you must specify the isolation level you want to read from\. Different isolation levels have tradeoffs between latency and data freshness\.

+ **EVENTUAL \- **The snapshot isolation level reads whatever data is immediately available**\. **It provides the lowest latency of any isolation level\.** **It also provides a potentially old view of the data in the directory\. EVENTUAL isolation does not provide read\-after\-write consistency\. This means it is not guaranteed that you will be able to read data immediately after writing it\.

+ **SERIALIZABLE \- **The serializable isolation level provides the highest level of consistency offered by Cloud Directory\. Reads done at the SERIALIZABLE isolation level ensure that you receive data from any successful writes\. If a change has been made to the data that you requested and that change is not yet available, the system rejects your request with `RetryableConflictException`\. We recommend that you retry these exceptions \(see the following section\)\. When successfully retried, SERIALIZABLE reads offer read\-after\-write consistency\.

## Write Requests<a name="writerequests"></a>

Cloud Directory ensures that multiple write requests are not concurrently updating the same object or objects\. If two write requests are found to be operating on the same objects, one of the operations fails with a `RetryableConflictException`\. We recommend that you retry these exceptions \(see the section below\)\.

**Note**  
`RetryableConflictException` responses received during write operations cannot be used to detect race conditions\. Given a use case that has been shown to precipitate this situation, there is no guarantee that an exception will always occur\. Whether an exception occurs or not depends on the order of each request being processed internally\.

## RetryableConflictExceptions<a name="retryable"></a>

When performing write operations or read operations with a SERIALIZABLE isolation level after a write on the same object, Cloud Directory may respond with a `RetryableConflictException`\. This exception indicates that Cloud Directory servers have not yet processed the contents of the previous write\. These situations are transient and remedy themselves quickly\. It’s important to note that the `RetryableConflictException` cannot be used to detect any type of read\-after\-write consistency\. There is no guarantee a particular use case will cause this exception\.

We recommend that you configure your Cloud Directory clients to retry the `RetryableConflictException`\. This configuration provides error\-free behavior during operation\. The following sample code demonstrates how this configuration can be made in Java\.

```
      RetryPolicy retryPolicy = new RetryPolicy(new CloudDirectoryRetryCondition(),
        		PredefinedRetryPolicies.DEFAULT_BACKOFF_STRATEGY,
        		PredefinedRetryPolicies.DEFAULT_MAX_ERROR_RETRY,
                true);

        ClientConfiguration clientConfiguration = new ClientConfiguration().withRetryPolicy(retryPolicy);
        
		
		AmazonCloudDirectory client = new AmazonCloudDirectory (
				new BasicAWSCredentials(…), clientConfiguration);


	public static class CloudDirectoryRetryCondition extends SDKDefaultRetryCondition {

		@Override
		public boolean shouldRetry(AmazonWebServiceRequest originalRequest, AmazonClientException exception,
				int retriesAttempted) {
			
			if (exception.getCause() instanceof RetryableConflictException) {
				return true;
			}
			
			return super.shouldRetry(originalRequest, exception, retriesAttempted);
		}
	}
```