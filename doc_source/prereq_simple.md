# Simple AD Prerequisites<a name="prereq_simple"></a>

To create a Simple AD directory, you need a VPC with the following: 

+ At least two subnets\. Each of the subnets must be in a different Availability Zone\.

+ The following ports must be open between the two subnets that you deploy your directory into\. This is necessary to allow the domain controllers that AWS Directory Service creates for you to communicate with each other\.

  + TCP/UDP 53 \- DNS

  + TCP/UDP 88 \- Kerberos authentication

  + UDP 123 \- NTP

  + TCP 135 \- RPC

  + UDP 137\-138 \- Netlogon

  + TCP 139 \- Netlogon

  + TCP/UDP 389 \- LDAP

  + TCP/UDP 445 \- SMB

  + TCP 873 \- Rsync

  + TCP 3268 \- Global Catalog

  + TCP/UDP 1024\-65535 \- Ephemeral ports for RPC

+ The VPC must have default hardware tenancy\.

+ The following encryption types must be enabled in the directory: 

  + RC4\_HMAC\_MD5

  + AES128\_HMAC\_SHA1

  + AES256\_HMAC\_SHA1

  + Future encryption types