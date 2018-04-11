# Limits for Amazon Cloud Directory<a name="cd_limits"></a>

The following are the default limits for Cloud Directory\. Each limit is per region unless otherwise noted\.


**Schema and Directory Limits**  

| Limit/Concept | Quantity | 
| --- | --- | 
| Number of attributes per facet \(including required\) | 1000 | 
| Number of facets per object | 5 | 
| Number of unique indexes an object is attached | 3 | 
| Number of facets per schema | 30 | 
| Number of rules per attribute | 5 | 
| Number of attributes with default values per facet | 10 | 
| Number of required attributes per facet | 30 | 
| Number of development schemas | 20 | 
| Number of published schemas | 20 | 
| Number of applied schemas | 5 | 
| Number of directories | 100 | 
| Max page elements | 30  | 
| Max input size \(all inputs combined\) | 200 KB | 
| Max response size \(all outputs combined\) | 1 MB | 
| Schema JSON file size limit | 200 KB | 
| Facet name length | 64 UTF\-8 encoded bytes | 
| Directory name length | 64 UTF\-8 encoded bytes | 
| Schema name length | 64 UTF\-8 encoded bytes | 


**Object Limits**  

| Limit/Concept | Quantity | 
| --- | --- | 
| Number of written objects | 20 per API call  | 
| Number of read objects | 200 per API call | 
| Number of written attribute values | 1000 per API call | 
| Number of read attribute values | 1000 per API call | 
| Path depth | 15 | 
| Max objects in a single page | 30 | 
| Max input size \(all inputs combined\) | 200 KB | 
| Max response size \(all outputs combined\) | 1 MB | 
| Policy size limit | 10 KB | 
| Edge or link name length | 64 UTF\-8 encoded bytes | 
| Value length for indexed attributes | 64 UTF\-8 encoded bytes | 
| Value length for non\-indexed attributes | 2KB | 
| Number of policies attached to an object | 4 | 

## Limits on batch operations<a name="limitsonbatchops"></a>

There are no limits on the number of operations you can call inside a batch\. For more information, see [Limits on Batch operations](batches.md#batchlimits)\.

## Limits that cannot be modified<a name="limitscantbemodified"></a>

Amazon Cloud Directory limits that cannot be changed or increased, include:
+ Facet name length
+ Directory name length
+ Schema name length
+ Max page elements
+ Edge or link name length
+ Value length for indexed attributes

## Increase Your Limit<a name="increase_limit"></a>

Perform the following steps to increase your limit for a region\.

**To request a limit increase for a region**

1. Go to the [AWS Support Center](https://console.aws.amazon.com/support/home#/) page, sign in, if necessary, and click **Open a new case**\.

1. Under **Regarding**, select **Service Limit Increase**\.

1. Under **Limit Type**, select **AWS Directory Service**\.

1. Fill in all of the necessary fields in the form and click the button at the bottom of the page for your desired method of contact\.