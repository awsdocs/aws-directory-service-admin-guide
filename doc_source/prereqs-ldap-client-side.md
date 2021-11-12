# Prerequisites<a name="prereqs-ldap-client-side"></a>

Before you enable client\-side LDAPS, you need to meet the following requirements\.

**Topics**
+ [Deploy server certificates in Active Directory](#deploy_server_certs_ldap_client_side)
+ [CA certificate requirements](#cert_requirements_ldap_client_side)
+ [Networking requirements](#networking_requirements_ldap_client_side)

## Deploy server certificates in Active Directory<a name="deploy_server_certs_ldap_client_side"></a>

In order to enable client\-side LDAPS, you need to obtain and install server certificates for each domain controller in Active Directory\. These certificates will be used by the LDAP service to listen for and automatically accept SSL connections from LDAP clients\. You can use SSL certificates that are either issued by an in\-house Active Directory Certificate Services \(ADCS\) deployment or purchased from a commercial issuer\. For more information on Active Directory server certificate requirements, see [LDAP over SSL \(LDAPS\) Certificate](https://social.technet.microsoft.com/wiki/contents/articles/2980.ldap-over-ssl-ldaps-certificate.aspx) on the Microsoft website\.

## CA certificate requirements<a name="cert_requirements_ldap_client_side"></a>

A certificate authority \(CA\) certificate, which represents the issuer of your server certificates, is required for client\-side LDAPS operation\. CA certificates are matched with the server certificates that are presented by your Active Directory domain controllers to encrypt LDAP communications\. Note the following CA certificate requirements:
+  To register a certificate, it must be more than 90 days away from expiration\.
+ Certificates must be in Privacy\-Enhanced Mail \(PEM\) format\. If exporting CA certificates from inside Active Directory, choose base64 encoded X\.509 \(\.CER\) as the export file format\.
+ A maximum of five \(5\) CA certificates can be stored per AD Connector directory\.
+ Certificates using the RSASSA\-PSS signature algorithm are not supported\.

## Networking requirements<a name="networking_requirements_ldap_client_side"></a>

AWS application LDAP traffic will run exclusively on TCP port 636, with no fallback to LDAP port 389\. However, Windows LDAP communications supporting replication, trusts, and more will continue using LDAP port 389 with Windows\-native security\. Configure AWS security groups and network firewalls to allow TCP communications on port 636 in AD Connector \(outbound\) and self\-managed Active Directory \(inbound\)\. 