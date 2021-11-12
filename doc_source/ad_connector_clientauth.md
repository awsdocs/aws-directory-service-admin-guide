# Enable mTLS authentication in AD Connector for use with smart cards<a name="ad_connector_clientauth"></a>

You can use certificate\-based mutual Transport Layer Security \(mTLS\) authentication with smart cards to authenticate users into Amazon WorkSpaces through your self\-managed Active Directory \(AD\) and AD Connector\. When enabled, users select their smart card at the WorkSpaces login screen and enter a PIN to authenticate, instead of using a username and password\. From there, the Windows or Linux virtual desktop uses the smart card to authenticate into AD from the native desktop OS\. 

**Note**  
Smart card authentication in AD Connector is only available in the following regions, and only with WorkSpaces\. Other AWS applications are not supported at this time\.  
US East \(N\. Virginia\)
US West \(Oregon\)
Asia Pacific \(Sydney\)
Asia Pacific \(Tokyo\)
Europe \(Ireland\)
AWS GovCloud \(US\-West\)

**Topics**
+ [Prerequisites](prereqs-clientauth.md)
+ [Enable smart card authentication](enable-clientauth.md)
+ [Manage smart card authentication settings](manage-clientauth.md)