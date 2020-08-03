# Enhance Your AWS Managed Microsoft AD Network Security Configuration<a name="ms_ad_network_security"></a>

The AWS Security Group that is provisioned for the AWS Managed Microsoft AD directory is configured with the minimum inbound network ports required to support all known use cases for your AWS Managed Microsoft AD directory\. For more information on the provisioned AWS Security Group, see [What Gets Created](ms_ad_getting_started_what_gets_created.md)\.

To further enhance the network security of your AWS Managed Microsoft AD directory you can modify the AWS Security Group based on common scenarios listed below\.

**Topics**
+ [AWS Applications Only Support](#aws_apps_support)
+ [AWS Applications Only with Trust Support](#aws_apps_trust_support)
+ [AWS Applications and Native Active Directory Workload Support](#aws_apps_native_ad_support)
+ [AWS Applications and Native Active Directory Workload Support with Trust Support](#aws_apps_native_ad_trust_support)

## AWS Applications Only Support<a name="aws_apps_support"></a>

All user accounts are provisioned only in your AWS Managed Microsoft AD to be used with supported AWS applications, such as the following:
+ Amazon Chime
+ Amazon Connect
+ Amazon QuickSight
+ AWS Single Sign\-On
+ Amazon WorkDocs
+ Amazon WorkMail
+ AWS Client VPN
+ AWS Management Console

You can use the following AWS Security Group configuration to block all non\-essential traffic to your AWS Managed Microsoft AD domain controllers\.

**Note**  
The following are not compatible with this AWS Security Group configuration:  
Amazon EC2 instances
Amazon FSx
Amazon RDS for MySQL
Amazon RDS for Oracle
Amazon RDS for PostgreSQL
Amazon RDS for SQL Server
Amazon WorkSpaces
Active Directory trusts
Domain joined clients or servers

**Inbound Rules**

None\.

**Outbound Rules**

None\.

## AWS Applications Only with Trust Support<a name="aws_apps_trust_support"></a>

All user accounts are provisioned in your AWS Managed Microsoft AD or trusted Active Directory to be used with supported AWS applications, such as the following:
+ Amazon Chime
+ Amazon Connect
+ Amazon QuickSight
+ AWS Single Sign\-On
+ Amazon WorkDocs
+ Amazon WorkMail
+ AWS Client VPN
+ AWS Management Console

You can modify the provisioned AWS Security Group configuration to block all non\-essential traffic to your AWS Managed Microsoft AD domain controllers\.

**Note**  
The following are not compatible with this AWS Security Group configuration:  
Amazon EC2 instances
Amazon FSx
Amazon RDS for MySQL
Amazon RDS for Oracle
Amazon RDS for PostgreSQL
Amazon RDS for SQL Server
Amazon WorkSpaces
Active Directory trusts
Domain joined clients or servers
This configuration requires you to ensure the “On\-premise CIDR” network is secure\.
TCP 445 is used for trust creation only and can be removed after the trust has been established\.
TCP 636 is only required when LDAP over SSL is in use\. 

**Inbound Rules**


****  

| Protocol | Port range | Source | Type of traffic | Active Directory usage | 
| --- | --- | --- | --- | --- | 
| TCP & UDP  | 53 | On\-premise CIDR | DNS | User and computer authentication, name resolution, trusts  | 
| TCP & UDP  | 88 | On\-premise CIDR | Kerberos | User and computer authentication, forest level trusts | 
| TCP & UDP  | 389 | On\-premise CIDR | LDAP | Directory, replication, user and computer authentication group policy, trusts | 
| TCP & UDP  | 464 | On\-premise CIDR | Kerberos change / set password | Replication, user and computer authentication, trusts | 
| TCP | 445 | On\-premise CIDR | SMB / CIFS | Replication, user and computer authentication, group policy trusts | 
| TCP | 135 | On\-premise CIDR | Replication | RPC, EPM | 
| TCP | 636 | On\-premise CIDR | LDAP SSL | Directory, replication, user and computer authentication group policy, trusts | 
| TCP | 49152 \- 65535 | On\-premise CIDR | RPC | Replication, user and computer authentication, group policy, trusts | 
| TCP | 3268 \- 3269 | On\-premise CIDR | LDAP GC & LDAP GC SSL | Directory, replication, user and computer authentication group policy, trusts | 
| UDP | 123 | On\-premise CIDR | Windows Time | Windows Time, trusts | 

**Outbound Rules**


****  

| Protocol | Port range | Source | Type of traffic | Active Directory usage | 
| --- | --- | --- | --- | --- | 
| All | All | On\-premise CIDR | All traffic |  | 

## AWS Applications and Native Active Directory Workload Support<a name="aws_apps_native_ad_support"></a>

User accounts are provisioned only in your AWS Managed Microsoft AD to be used with supported AWS applications, such as the following:
+ Amazon Chime
+ Amazon Connect
+ Amazon EC2 instances
+ Amazon FSx
+ Amazon QuickSight
+ Amazon RDS for MySQL
+ Amazon RDS for Oracle
+ Amazon RDS for PostgreSQL
+ Amazon RDS for SQL Server
+ AWS Single Sign\-On
+ Amazon WorkDocs
+ Amazon WorkMail
+ Amazon WorkSpaces
+ AWS Client VPN
+ AWS Management Console

You can modify the provisioned AWS Security Group configuration to block all non\-essential traffic to your AWS Managed Microsoft AD domain controllers\.

**Note**  
Active Directory trusts cannot be created and maintained between your AWS Managed Microsoft AD directory and on\-premise domain\.
It requires you to ensure the “Client CIDR” network is secure\.
TCP 636 is only required when LDAP over SSL is in use\. 
If you want to use an Enterprise CA with this configuration you will need to create an outbound rule “TCP, 443, CA CIDR”\.

**Inbound Rules**


****  

| Protocol | Port range | Source | Type of traffic | Active Directory usage | 
| --- | --- | --- | --- | --- | 
| TCP & UDP  | 53 | Client CIDR | DNS | User and computer authentication, name resolution, trusts  | 
| TCP & UDP  | 88 | Client CIDR | Kerberos | User and computer authentication, forest level trusts | 
| TCP & UDP  | 389 | Client CIDR | LDAP | Directory, replication, user and computer authentication group policy, trusts | 
| TCP & UDP | 445 | Client CIDR | SMB / CIFS | Replication, user and computer authentication, group policy trusts | 
| TCP & UDP  | 464 | Client CIDR | Kerberos change / set password | Replication, user and computer authentication, trusts | 
| TCP | 135 | Client CIDR | Replication | RPC, EPM | 
| TCP | 636 | Client CIDR | LDAP SSL | Directory, replication, user and computer authentication group policy, trusts | 
| TCP | 49152 \- 65535 | Client CIDR | RPC | Replication, user and computer authentication, group policy, trusts | 
| TCP | 3268 \- 3269 | Client CIDR | LDAP GC & LDAP GC SSL | Directory, replication, user and computer authentication group policy, trusts | 
| TCP | 9389 | Client CIDR | SOAP | AD DS web services | 
| UDP | 123 | Client CIDR | Windows Time | Windows Time, trusts | 
| UDP | 138 | Client CIDR | DFSN & NetLogon | DFS, group policy | 

**Outbound Rules**

None\.

## AWS Applications and Native Active Directory Workload Support with Trust Support<a name="aws_apps_native_ad_trust_support"></a>

All user accounts are provisioned in your AWS Managed Microsoft AD or trusted Active Directory to be used with supported AWS applications, such as the following:
+ Amazon Chime
+ Amazon Connect
+ Amazon EC2 instances
+ Amazon FSx
+ Amazon QuickSight
+ Amazon RDS for MySQL
+ Amazon RDS for Oracle
+ Amazon RDS for PostgreSQL
+ Amazon RDS for SQL Server
+ AWS Single Sign\-On
+ Amazon WorkDocs
+ Amazon WorkMail
+ Amazon WorkSpaces
+ AWS Client VPN
+ AWS Management Console

You can modify the provisioned AWS Security Group configuration to block all non\-essential traffic to your AWS Managed Microsoft AD domain controllers\.

**Note**  
It requires you to ensure the “On\-premise CIDR” and “Client CIDR” networks are secure\.
TCP 445 with the “On\-premise CIDR” is used for trust creation only and can be removed after the trust has been established\.
TCP 445 with the “Client CIDR” should be left open as it is required for Group Policy processing\. 
TCP 636 is only required when LDAP over SSL is in use\. 
If you want to use an Enterprise CA with this configuration you will need to create an outbound rule “TCP, 443, CA CIDR”\.

**Inbound Rules**


****  

| Protocol | Port range | Source | Type of traffic | Active Directory usage | 
| --- | --- | --- | --- | --- | 
| TCP & UDP  | 53 | On\-premise CIDR | DNS | User and computer authentication, name resolution, trusts  | 
| TCP & UDP  | 88 | On\-premise CIDR | Kerberos | User and computer authentication, forest level trusts | 
| TCP & UDP  | 389 | On\-premise CIDR | LDAP | Directory, replication, user and computer authentication group policy, trusts | 
| TCP & UDP  | 464 | On\-premise CIDR | Kerberos change / set password | Replication, user and computer authentication, trusts | 
| TCP | 445 | On\-premise CIDR | SMB / CIFS | Replication, user and computer authentication, group policy trusts | 
| TCP | 135 | On\-premise CIDR | Replication | RPC, EPM | 
| TCP | 636 | On\-premise CIDR | LDAP SSL | Directory, replication, user and computer authentication group policy, trusts | 
| TCP | 49152 \- 65535 | On\-premise CIDR | RPC | Replication, user and computer authentication, group policy, trusts | 
| TCP | 3268 \- 3269 | On\-premise CIDR | LDAP GC & LDAP GC SSL | Directory, replication, user and computer authentication group policy, trusts | 
| UDP | 123 | On\-premise CIDR | Windows Time | Windows Time, trusts | 
| TCP & UDP  | 53 | Client CIDR | DNS | User and computer authentication, name resolution, trusts  | 
| TCP & UDP  | 88 | Client CIDR | Kerberos | User and computer authentication, forest level trusts | 
| TCP & UDP  | 389 | Client CIDR | LDAP | Directory, replication, user and computer authentication group policy, trusts | 
| TCP & UDP | 445 | Client CIDR | SMB / CIFS | Replication, user and computer authentication, group policy trusts | 
| TCP & UDP  | 464 | Client CIDR | Kerberos change / set password | Replication, user and computer authentication, trusts | 
| TCP | 135 | Client CIDR | Replication | RPC, EPM | 
| TCP | 636 | Client CIDR | LDAP SSL | Directory, replication, user and computer authentication group policy, trusts | 
| TCP | 49152 \- 65535 | Client CIDR | RPC | Replication, user and computer authentication, group policy, trusts | 
| TCP | 3268 \- 3269 | Client CIDR | LDAP GC & LDAP GC SSL | Directory, replication, user and computer authentication group policy, trusts | 
| TCP | 9389 | Client CIDR | SOAP | AD DS web services | 
| UDP | 123 | Client CIDR | Windows Time | Windows Time, trusts | 
| UDP | 138 | Client CIDR | DFSN & NetLogon | DFS, group policy | 

**Outbound Rules**


****  

| Protocol | Port range | Source | Type of traffic | Active Directory usage | 
| --- | --- | --- | --- | --- | 
| All | All | On\-premise CIDR | All traffic |  | 