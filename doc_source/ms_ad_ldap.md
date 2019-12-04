# Enable Secure LDAP \(LDAPS\)<a name="ms_ad_ldap"></a>

Lightweight Directory Access Protocol \(LDAP\) is a standard communications protocol used to read and write data to and from Active Directory\. Some applications use LDAP to add, remove, or search users and groups in Active Directory or to transport credentials for authenticating users in Active Directory\. Every LDAP communication includes a client \(such as an application\) and a server \(such as Active Directory\)\.

By default, communications over LDAP are not encrypted\. This makes it possible for a malicious user to use network monitoring software to view data packets over the wire\. This is why many corporate security policies typically require that organizations encrypt all LDAP communication\.

To mitigate this form of data exposure, AWS Managed Microsoft AD provides an option: You can enable LDAP over Secure Sockets Layer \(SSL\)/Transport Layer Security \(TLS\), also known as LDAPS\. With LDAPS, you can improve security across the wire\. You can also meet compliance requirements by encrypting all communications between your LDAP\-enabled applications and AWS Managed Microsoft AD\.

AWS Managed Microsoft AD provides support for LDAPS in both of the following deployment scenarios:
+ **Server\-side LDAPS** encrypts LDAP communications between your commercial or homegrown LDAP\-aware applications \(acting as LDAP clients\) and AWS Managed Microsoft AD \(acting as an LDAP server\)\. For more information, see [Enable Server\-Side LDAPS Using AWS Managed Microsoft AD](ms_ad_ldap_server_side.md)\.
+ **Client\-side LDAPS** encrypts LDAP communications between AWS applications such as Amazon WorkSpaces \(acting as LDAP clients\) and your self\-managed Active Directory \(acting as LDAP server\)\. For more information, see [Enable Client\-Side LDAPS Using AWS Managed Microsoft AD](ms_ad_ldap_client_side.md)\.

**Topics**
+ [Enable Server\-Side LDAPS Using AWS Managed Microsoft AD](ms_ad_ldap_server_side.md)
+ [Enable Client\-Side LDAPS Using AWS Managed Microsoft AD](ms_ad_ldap_client_side.md)