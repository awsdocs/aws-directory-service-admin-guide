# Use Case 4: SSO to Office 365 and Other Cloud Applications<a name="usecase4"></a>

You can use AWS Managed Microsoft AD to provide SSO for cloud applications\. You can use Azure AD Connect to synchronize your users into Azure AD, and then use Active Directory Federation Services \(AD FS\) so that your users can access [Microsoft Office 365](https://aws.amazon.com/blogs/security/how-to-enable-your-users-to-access-office-365-with-aws-microsoft-active-directory-credentials/) and other SAML 2\.0 cloud applications by using their AD credentials\.

[Integrating AWS Managed Microsoft AD with AWS SSO](https://docs.aws.amazon.com/singlesignon/latest/userguide/manage-your-identity-source-ad.html) adds SAML capabilities to your AWS Managed Microsoft AD and / or your on\-premises trusted domains\. Once integrated your users can then use AWS SSO with services that support SAML, including the AWS Management Console and third\-party cloud applications such as Office 365, Concur, and Salesforce without having to configure a SAML infrastructure\. For a demonstration on the process of allowing your on\-premise users to use AWS SSO, see the following YouTube video\.

