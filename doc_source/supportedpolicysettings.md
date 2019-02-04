# Supported Policy Settings<a name="supportedpolicysettings"></a>

AWS Managed Microsoft AD includes five fine\-grained policies with a non\-editable precedence value\. The policies have a number of properties you can configure to enforce the strength of passwords, and account lock\-out actions in the event of login failures\. You can assign the policies to zero or more Active Directory groups\. If an end\-user is a member of multiple groups and receives more than one password policy, Active Directory enforces the policy with the lowest precedence value\.

## AWS Pre\-Defined Password Policies<a name="supportedpwdpolicies"></a>

The following table lists the five policies included in your AWS Managed Microsoft AD directory and their assigned precedence value\. For more information, see [Precedence](#precedence)\.


****  

| Policy name | Precedence | 
| --- | --- | 
| CustomerPSO\-01 | 10 | 
| CustomerPSO\-02 | 20 | 
| CustomerPSO\-03 | 30 | 
| CustomerPSO\-04 | 40 | 
| CustomerPSO\-05 | 50 | 

### Password Policy Properties<a name="passwordpolicyprop"></a>

You may edit the following properties in your password policies to conform to the compliance standards that meet your business needs\.
+ Policy name
+ [Enforce password history](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/enforce-password-history)
+ [Minimum password length](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/minimum-password-length)
+ [Minimum password age](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/minimum-password-age)
+ [Maximum password age](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/maximum-password-age)
+ [Store passwords using reversible encryption](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/store-passwords-using-reversible-encryption)
+ [Password must meet complexity requirements](https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)

You cannot modify the precedence values for these policies\. For more details about how these settings affect password enforcement, see [AD DS: Fine\-Grained Password Policies](https://technet.microsoft.com/en-us/library/cc770394(v=ws.10).aspx) on the *Microsoft TechNet* website\. For general information about these policies, see [Password Policy](https://technet.microsoft.com/en-us/library/hh994572(v=ws.11).aspx) on the *Microsoft TechNet* website\.

## Account Lockout Policies<a name="supportedlockoutpolicies"></a>

You may also modify the following properties of your password policies to specify if and how Active Directory should lockout an account after login failures:
+ Number of failed logon attempts allowed
+ Account lockout duration
+ Reset failed logon attempts after some duration

For general information about these policies, see [Account Lockout Policy](https://technet.microsoft.com/en-us/library/hh994563(v=ws.11).aspx) on the *Microsoft TechNet* website\.

## Precedence<a name="precedence"></a>

Policies with a lower precedence value have higher priority\. You assign password policies to Active Directory security groups\. While you should apply a single policy to a security group, a single user may receive more than one password policy\. For example, suppose `jsmith` is a member of the HR group and also a member of the MANAGERS group\. If you assign **CustomerPSO\-05** \(which has a precedence of 50\) to the HR group, and **CustomerPSO\-04** \(which has a precedence of 40\) to MANAGERS, **CustomerPSO\-04** has the higher priority and Active Directory applies that policy to `jsmith`\.

If you assign multiple policies to a user or group, Active Directory determines the resultant policy as follows:

1. A policy you assign directly to the user object applies\.

1. If no policy is assigned directly to the user object, the policy with the lowest precedence value of all policies received by the user as a result of group membership applies\.

For additional details, see [AD DS: Fine\-Grained Password Policies](https://technet.microsoft.com/en-us/library/cc770394(v=ws.10).aspx) on the *Microsoft TechNet* website\.