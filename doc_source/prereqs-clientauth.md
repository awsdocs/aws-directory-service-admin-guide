# Prerequisites<a name="prereqs-clientauth"></a>

To enable mTLS authentication using smart cards for the Amazon WorkSpaces client, you need an operational smart card infrastructure integrated with your self\-managed AD\. For more information on how to set up smart card authentication with Amazon WorkSpaces and AD, see the [Amazon WorkSpaces Administration Guide](https://docs.aws.amazon.com/workspaces/latest/adminguide/smart-cards.html)\.

Before you enable smart card authentication for WorkSpaces, please review the following considerations:
+ [CA certificate requirements](#ca-cert)
+ [User certificate requirements](#user-cert)
+ [Certificate revocation checking process](#ocsp)
+ [Other considerations](#other)

## CA certificate requirements<a name="ca-cert"></a>

AD Connector requires a certificate authority \(CA\) certificate, which represents the issuer of your user certificates, for smart card authentication\. AD Connector matches CA certificates with the certificates presented by your users with their smart cards\. Note the following CA certificate requirements:
+ Before you can register a CA certificate, it must be more than 90 days away from expiration\.
+  CA certificates must be in Privacy\-Enhanced Mail \(PEM\) format\. If you export CA certificates from inside Active Directory, choose Base64\-encoded X\.509 \(\.CER\) as the export file format\.
+ All root and intermediary CA certificates that chain from an issuing CA to user certificates must be uploaded for smart card authentication to succeed\.
+ A maximum of 100 CA certificates can be stored per AD Connector directory
+ AD Connector does not support the RSASSA\-PSS signature algorithm for CA certificates\.

## User certificate requirements<a name="user-cert"></a>

User certificates presented to AD Connector must include the `userPrincipalName (UPN)` of the AD user in the `subjectAltName (SAN)` field of the certificate\.

## Certificate revocation checking process<a name="ocsp"></a>

In order to perform smart card authentication, AD Connector must check the revocation status of user certificates using Online Certificate Status Protocol \(OCSP\)\. To perform certificate revocation checking, an OCSP responder URL must be internet\-accessible\. If using a DNS name, an OCSP responder URL must use a top\-level domain found in the [Internet Assigned Numbers Authority \(IANA\) Root Zone Database](https://www.iana.org/domains/root/db)\. 

AD Connector certificate revocation checking uses the following process:
+ AD Connector must check the Authority Information Access \(AIA\) extension in the user certificate for an OCSP responder URL, then AD Connector uses the URL to check for revocation\.
+ If AD Connector cannot resolve the URL found in the user certificate AIA extension, or find an OCSP responder URL in the user certificate, then AD Connector uses the optional OCSP URL provided during root CA certificate registration\.

  If the URL in the user certificate AIA extension resolves but is unresponsive, then user authentication fails\.
+ If the OCSP responder URL provided during root CA certificate registration cannot resolve, is unresponsive, or no OCSP responder URL was provided, user authentication fails\.

**Note**  
AD Connector requires an **HTTP** URL for the OCSP responder URL\.

## Other considerations<a name="other"></a>

Before enabling smart card authentication in AD Connector, consider the following items:
+ AD Connector uses certificate\-based mutual Transport Layer Security authentication \(mutual TLS\) to authenticate users to Active Directory using hardware or software\-based smart card certificates\. Only common access cards \(CAC\) and personal identity verification \(PIV\) cards are supported at this time\. Other types of hardware or software\-based smart cards might work but have not been tested for use with the WorkSpaces Streaming Protocol\.
+ Smart card authentication replaces username and password authentication to WorkSpaces\.

  If you have other AWS applications configured on your AD Connector directory with smart card authentication enabled, those applications still present the username and password input screen\. 
+ Enabling smart card authentication limits the user session length to the maximum lifetime for Kerberos service tickets\. You can configure this setting using a Group Policy, and is set to 10 hours by default\. For more information on this setting, see [Microsoft documentation](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-lifetime-for-service-ticket)\.