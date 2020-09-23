# Linux Domain Join Errors<a name="ms_ad_troubleshooting_join_linux"></a>

The following can help you troubleshoot some error messages you might encounter when joining an EC2 Linux instance to your AWS Managed Microsoft AD directory\.

## Linux instances unable to join domain or authenticate<a name="unable-to-join"></a>

Ubuntu 14\.04, 16\.04, and 18\.04 instances *must* be reverse\-resolvable in the DNS before a realm can work with Microsoft AD\. Otherwise, you might encounter one of the following two scenarios:

### Scenario 1: Ubuntu instances that are not yet joined to a realm<a name="ubuntu-not-yet-joined"></a>

For Ubuntu instances that are attempting to join a realm, the `sudo realm join` command might not provide the required permissions to join the domain and might display the following error:

\! Couldn't authenticate to active directory: SASL\(\-1\): generic failure: GSSAPI Error: An invalid name was supplied \(Success\) adcli: couldn't connect to EXAMPLE\.COM domain: Couldn't authenticate to active directory: SASL\(\-1\): generic failure: GSSAPI Error: An invalid name was supplied \(Success\) \! Insufficient permissions to join the domain realm: Couldn't join realm: Insufficient permissions to join the domain

### Scenario 2: Ubuntu instances that are joined to a realm<a name="ubuntu-joined"></a>

For Ubuntu instances that are already joined to a Microsoft AD domain, attempts to SSH into the instance using the domain credentials might fail with following errors:

$ ssh admin@EXAMPLE\.COM@198\.51\.100

no such identity: /Users/username/\.ssh/id\_ed25519: No such file or directory

admin@EXAMPLE\.COM@198\.51\.100's password:

Permission denied, please try again\.

admin@EXAMPLE\.COM@198\.51\.100's password:

If you log in to the instance with a public key and check `/var/log/auth.log`, you might see the following errors about being unable to find the user:

May 12 01:02:12 ip\-192\-0\-2\-0 sshd\[2251\]: pam\_unix\(sshd:auth\): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=203\.0\.113\.0

May 12 01:02:12 ip\-192\-0\-2\-0 sshd\[2251\]: pam\_sss\(sshd:auth\): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=203\.0\.113\.0 user=admin@EXAMPLE\.COM

May 12 01:02:12 ip\-192\-0\-2\-0 sshd\[2251\]: pam\_sss\(sshd:auth\): received for user admin@EXAMPLE\.COM: 10 \(User not known to the underlying authentication module\)

May 12 01:02:14 ip\-192\-0\-2\-0 sshd\[2251\]: Failed password for invalid user admin@EXAMPLE\.COM from 203\.0\.113\.0 port 13344 ssh2

May 12 01:02:15 ip\-192\-0\-2\-0 sshd\[2251\]: Connection closed by 203\.0\.113\.0 \[preauth\]

However, `kinit` for the user still works\. See this example:

ubuntu@ip\-192\-0\-2\-0:\~$ kinit admin@EXAMPLE\.COM Password for admin@EXAMPLE\.COM: ubuntu@ip\-192\-0\-2\-0:\~$ klist Ticket cache: FILE:/tmp/krb5cc\_1000 Default principal: admin@EXAMPLE\.COM

### Workaround<a name="ubuntu-scenarios-workaround"></a>

The current recommended workaround for both of these scenarios is to disable reverse DNS in `/etc/krb5.conf` in the \[libdefaults\] section as shown below:

```
[libdefaults]
default_realm = EXAMPLE.COM
rdns = false
```

## One\-Way Trust Authentication Issue with Seamless Domain Join<a name="1-way-trust-auth-issues"></a>

If you have a one\-way outgoing trust established between your AWS Managed Microsoft AD and your on\-premises AD, you might encounter an authentication issue when attempting to authenticate against the domain joined Linux instance using your trusted AD credentials with Winbind\. 

### Errors<a name="1-way-trust-auth-issues-errors"></a>

Jul 31 00:00:00 EC2AMAZ\-LSMWqT sshd\[23832\]: Failed password for user@corp\.example\.com from xxx\.xxx\.xxx\.xxx port 18309 ssh2

Jul 31 00:05:00 EC2AMAZ\-LSMWqT sshd\[23832\]: pam\_winbind\(sshd:auth\): getting password \(0x00000390\)

Jul 31 00:05:00 EC2AMAZ\-LSMWqT sshd\[23832\]: pam\_winbind\(sshd:auth\): pam\_get\_item returned a password

Jul 31 00:05:00 EC2AMAZ\-LSMWqT sshd\[23832\]: pam\_winbind\(sshd:auth\): request wbcLogonUser failed: WBC\_ERR\_AUTH\_ERROR, PAM error: PAM\_SYSTEM\_ERR \(4\), NTSTATUS: \*\*NT\_STATUS\_OBJECT\_NAME\_NOT\_FOUND\*\*, Error message was: The object name is not found\.

Jul 31 00:05:00 EC2AMAZ\-LSMWqT sshd\[23832\]: pam\_winbind\(sshd:auth\): internal module error \(retval = PAM\_SYSTEM\_ERR\(4\), user = 'CORP\\user'\)

## Workaround<a name="1-way-trust-auth-issues-workaround"></a>

To resolve this issue, you will need to comment out or remove a directive from the PAM module configuration file \(`/etc/security/pam_winbind.conf`\) using the following steps\.

1. Open the `/etc/security/pam_winbind.conf` file in a text editor\.

   ```
   sudo vim /etc/security/pam_winbind.conf
   ```

1. Comment out or remove the following directive **krb5\_auth = yes**\.

   ```
   [global]
   
   cached_login = yes
   krb5_ccache_type = FILE
   #krb5_auth = yes
   ```

1. Stop the Winbind service, and then start it again\.

   ```
   service winbind stop or systemctl stop winbind
   net cache flush 
   service winbind start or systemctl start winbind
   ```