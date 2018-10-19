# Linux Domain Join Errors<a name="ms_ad_troubleshooting_join_linux"></a>

The following can help you troubleshoot some error messages you might encounter when joining an EC2 Linux instance to your AWS Managed Microsoft AD directory\.

## Linux instances unable to join domain or authenticate<a name="unabletojoin"></a>

**Error**  
*\! Couldn't authenticate to active directory: SASL\(\-1\): generic failure: GSSAPI Error: An invalid name was supplied \(Success\) adcli: couldn't connect to msft\.dan\-rg\.com domain: Couldn't authenticate to active directory: SASL\(\-1\): generic failure: GSSAPI Error: An invalid name was supplied \(Success\) \! Insufficient permissions to join the domain realm: Couldn't join realm: Insufficient permissions to join the domain*

**Troubleshooting**  
Edit the sssd\.conf file \(/etc/sssd/sssd\.conf\) and modify the following two sections so they appear as shown below:  

```
[sssd] 
domains = example.com 
config_file_version = 2 
services = nss, pam 
          
[libdefaults]
default_realm = EXAMPLE.COM
rdns = false
```