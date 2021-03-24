# Primary vs additional Regions<a name="multi-region-global-primary-additional"></a>

With multi\-Region replication, AWS Managed Microsoft AD uses the following two types of Regions to differentiate how global or Regional features should be applied across your directory\.

## Primary Region<a name="multi-region-primary"></a>

The initial Region where you first created your directory is referred to as the *primary* Region\. You can perform only global directory level operations such as creating Active Directory trusts and updating the AD schema from the primary Region\.

The primary Region can always be identified as the first Region showing at the top of the list in the **Multi\-Region replication** section, and ends with **\- Primary**\. For example, **US East \(N\. Virginia\) \- Primary**\. 

Any changes that you make to [Global features](multi-region-global-region-features.md#multi-region-global) while the primary Region is selected will be applied across all Regions\.

You can only add Regions while the primary Region is selected\. For more information, see [Add a replicated Region](multi-region-add-region.md)\.

## Additional Region<a name="multi-region-additional"></a>

Any Regions that you have added to your directory are referred to as *additional* Regions\.

Although some features can be managed globally for all Regions, others are managed individually per Region\. To manage a feature for an additional Region \(non\-primary Region\), you must first select the additional Region from the list in the **Multi\-Region replication** section on the **Directory details** page\. Then you can proceed to manage the feature\. 

Any changes that you make to [Regional features](multi-region-global-region-features.md#multi-region-regional) while an additional Region is selected will be applied only to that Region\.