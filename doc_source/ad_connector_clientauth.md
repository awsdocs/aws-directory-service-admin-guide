# Enable smart card authentication in AD Connector<a name="ad_connector_clientauth"></a>

You can use smart cards to authenticate users into Amazon WorkSpaces through your on\-premises Active Directory \(AD\) and AD Connector\. When enabled, users select their smart card at the WorkSpaces login screen and enter a PIN to authenticate, instead of using a username and password\. From there, the Windows or Linux virtual desktop uses the smart card to authenticate into AD from the native desktop OS\. 

**Note**  
Smart card authentication in AD Connector is only available in the AWS GovCloud \(US\-West\) region, and only with Amazon WorkSpaces\. Other AWS applications are not supported\.

## Prerequisites<a name="prerequisites"></a>

To enable smart card authentication for Amazon WorkSpaces, you need an operational smart card infrastructure integrated with your on\-premises AD\. For more information on how to set up smart card authentication with Amazon WorkSpaces and AD, see the [Amazon WorkSpaces Administration Guide](https://docs.aws.amazon.com/workspaces/latest/adminguide/smart-cards.html)\.

Before you enable smart card authentication for Amazon WorkSpaces, please review the following considerations:
+ [CA certificate requirements](#ca-cert)
+ [User certificate requirements](#user-cert)
+ [Certificate revocation checking process](#ocsp)
+ [Other considerations](#other)

### CA certificate requirements<a name="ca-cert"></a>

AD Connector requires a certificate authority \(CA\) certificate, which represents the issuer of your user certificates, for smart card authentication\. AD Connector matches CA certificates with the certificates presented by your users with their smart cards\. Note the following CA certificate requirements:
+ Before you can register a CA certificate, it must be more than 90 days away from expiration\.
+  CA certificates must be in Privacy\-Enhanced Mail \(PEM\) format\. If you export CA certificates from inside Active Directory, choose Base64\-encoded X\.509 \(\.CER\) as the export file format\.
+ All root and intermediary CA certificates that chain from an issuing CA to user certificates must be uploaded for smart card authentication to succeed\.
+ A maximum of 100 CA certificates can be stored per AD Connector directory
+ AD Connector does not support the RSASSA\-PSS signature algorithm for CA certificates\.

### User certificate requirements<a name="user-cert"></a>

User certificates presented to AD Connector must include the `userPrincipalName (UPN)` of the AD user in the `subjectAltName (SAN)` field of the certificate\.

### Certificate revocation checking process<a name="ocsp"></a>

In order to perform smart card authentication, AD Connector must check the revocation status of user certificates using Online Certificate Status Protocol \(OCSP\)\. To perform certificate revocation checking, an OCSP responder URL must be internet\-accessible\. If using a DNS name, an OCSP responder URL must use a top\-level domain found in the [Internet Assigned Numbers Authority \(IANA\) Root Zone Database](https://www.iana.org/domains/root/db)\. 

AD Connector certificate revocation checking uses the following process:
+ AD Connector must check the Authority Information Access \(AIA\) extension in the user certificate for an OCSP responder URL, then AD Connector uses the URL to check for revocation\.
+ If AD Connector cannot resolve the URL found in the user certificate AIA extension, or find an OCSP responder URL in the user certificate, then AD Connector uses the optional OCSP URL provided during root CA certificate registration\.

  If the URL in the user certificate AIA extension resolves but is unresponsive, then user authentication fails\.
+ If the OCSP responder URL provided during root CA certificate registration cannot resolve, is unresponsive, or no OCSP responder URL was provided, user authentication fails\.

**Note**  
AD Connector requires an **HTTP** URL for the OCSP responder URL\.

### Other considerations<a name="other"></a>

Before enabling smart card authentication in AD Connector, consider the following items:
+ Smart card authentication replaces username and password authentication to Amazon WorkSpaces\.

  If you have other AWS applications configured on your AD Connector directory with smart card authentication enabled, those applications still present the username and password input screen\. 
+ Enabling smart card authentication limits the user session length to the maximum lifetime for Kerberos service tickets\. You can configure this setting using a Group Policy, and is set to 10 hours by default\. For more information on this setting, see [Microsoft documentation](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-lifetime-for-service-ticket)\.

## Enabling smart card authentication<a name="enable-clientauth"></a>

To enable smart card authentication, use the following steps to import your certificate authority \(CA\) certificates into AD Connector using the AWS Directory Service [API](https://docs.aws.amazon.com/directoryservice/latest/devguide/welcome.html) or [CLI](https://docs.aws.amazon.com/cli/latest/reference/ds/index.html)\. And then enable smart card authentication for Amazon WorkSpaces on your AD Connector\. 
+ [STEP 1: Enable Kerberos constrained delegation for the AD Connector service account](#step1)
+ [STEP 2: Register the CA certificate in AD Connector](#step2)
+ [STEP 3: Verify your CA certificate registration status](#step3)
+ [STEP 4: Enable smart card authentication for Amazon WorkSpaces](#step4)

## STEP 1: Enable Kerberos constrained delegation for the AD Connector service account<a name="step1"></a>

To use smart card authentication with AD Connector, you must enable **Kerberos Constrained Delegation \(KCD\)** for the AD Connector Service account to the LDAP service in the on\-premises AD\. directory\.

Kerberos Constrained Delegation is a feature in Windows Server\. This feature enables administrators to specify and enforce application trust boundaries by limiting the scope where application services can act on a user’s behalf\. For more information, see [Kerberos constrained delegation](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_key_concepts_kerberos.html)\. 

1. Use the `SetSpn` command to set a Service Principal Name\(SPN\) for the AD Connector service account in the on\-premises AD\. This enables the service account for delegation configuration\.

   The SPN can be any service or name combination but not a duplicate of an existing SPN\. The `-s` checks for duplicates\.

   ```
   setspn -s my/spn service_account
   ```

1. In **AD Users and Computers**, right\-click on the AD Connector service account and select **Properties\.**

1. Choose the **Delegation** tab\.

1. Choose the **Trust this user for delegation to specified service only** and **Use any authentication protocol** radio buttons\.

1. Choose **Add** and then **Users or Computers** to locate the domain controller\. 

1. Choose **OK** to display a list of available services used for delegation\.

1. Choose the **ldap** service type and click **OK**\. 

1. Click **OK** again to save the configuration\.

1. Repeat this process for other domain controllers in AD\. Alternatively you can automate the process using PowerShell\.

## STEP 2: Register the CA certificate in AD Connector<a name="step2"></a>

To register your CA certificate in AD Connector, use the following CLI command:

```
aws ds register-certificate --directory-id your_directory_id --certificate-data file://your_file_path --type ClientCertAuth --Client-Cert-Auth-Settings '{"OCSPUrl":"http://your_OCSP_address"}'
```

For the certificate data, point to the location of your CA certificate\. To provide a secondary OCSP responder address, use the optional `ClientCertAuthSettings` object\. The response provides a certificate ID\.

## STEP 3: Verify your CA certificate registration status<a name="step3"></a>

To verify the status of a CA certificate registration or a list of registered CA certificates, run the following command:

```
aws ds list-certificates --directory-id your_directory_id
```

If the status value returns `Registered`, you have successfully registered your certificate\.

## STEP 4: Enable smart card authentication for Amazon WorkSpaces<a name="step4"></a>

To enable smart card authentication for Amazon WorkSpaces in AD Connector, use the following CLI command:

```
aws ds enable-client-authentication --directory-id your_directory_id --type SmartCard
```

If successful, AD Connector returns an `HTTP 200` response with an empty HTTP body\.