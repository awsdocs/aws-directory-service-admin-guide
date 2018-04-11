# Application Compatibility Policy for Simple AD<a name="simple_ad_app_compatibility"></a>

Simple AD is an implementation of Samba that provides many of the basic features of Active Directory\. Due to the magnitude of custom and commercial off\-the\-shelf applications that use Active Directory, AWS does not and cannot perform formal or broad verification of third\-party application compatibility with Simple AD\. Although AWS works with customers in an attempt to overcome any potential application installation challenges they might encounter, we are unable to guarantee that any application is or will continue to be compatible with Simple AD\.

The following third\-party applications are compatible with Simple AD:
+ Microsoft Internet Information Services \(IIS\) on the following platforms:
  + Windows Server 2003 R2
  + Windows Server 2008 R1
  + Windows Server 2008 R2
  + Windows Server 2012
  + Windows Server 2012 R2
+ Microsoft SQL Server:
  + SQL Server 2005 R2 \(Express, Web, and Standard editions\)
  + SQL Server 2008 R2 \(Express, Web, and Standard editions\)
  + SQL Server 2012 \(Express, Web, and Standard editions\)
  + SQL Server 2014 \(Express, Web, and Standard editions\)
+ Microsoft SharePoint:
  + SharePoint 2010 Foundation
  + SharePoint 2010 Enterprise
  + SharePoint 2013 Enterprise

Customers can choose to use AWS Directory Service for Microsoft Active Directory \([AWS Managed Microsoft AD](directory_microsoft_ad.md)\) for a higher level of compatibility based on actual Active Directory\.