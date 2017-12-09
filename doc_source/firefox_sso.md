# Single Sign\-On for Firefox<a name="firefox_sso"></a>

To allow Mozilla's Firefox browser to support single sign\-on, add your access URL \(e\.g\., https://*<alias>*\.awsapps\.com\) to the list of approved sites for single sign\-on\. This can be done manually, or automated with a script\.


+ [Manual Update for Single Sign\-On](#firefox_sso_manual)
+ [Automatic Update for Single Sign\-On](#firefox_sso_script)

## Manual Update for Single Sign\-On<a name="firefox_sso_manual"></a>

To manually add your access URL to the list of approved sites in Firefox, perform the following steps on the client computer\.

**To manually add your access URL to the list of approved sites in Firefox**

1. Open Firefox and open the `about:config` page\.

1. Open the `network.negotiate-auth.trusted-uris` preference and add your access URL to the list of sites\. Use a comma \(,\) to separate multiple entries\.  
![\[Internet Explorer automatic logon setting\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/firefox_sso_config.png)

## Automatic Update for Single Sign\-On<a name="firefox_sso_script"></a>

As a domain administrator, you can use a script to add your access URL to the Firefox `network.negotiate-auth.trusted-uris` user preference on all computers on your network\. For more information, go to [https://support\.mozilla\.org/en\-US/questions/939037](https://support.mozilla.org/en-US/questions/939037)\.