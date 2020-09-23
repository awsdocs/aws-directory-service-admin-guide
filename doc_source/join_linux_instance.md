# Manually Join a Linux Instance<a name="join_linux_instance"></a>

In addition to Amazon EC2 Windows instances, you can also join certain Amazon EC2 Linux instances to your AWS Directory Service for Microsoft Active Directory directory\. The following Linux instance distributions and versions are supported:
+ Amazon Linux AMI 2018\.03\.0
+ Amazon Linux 2 \(64\-bit x86\)
+ Red Hat Enterprise Linux 8 \(HVM\) \(64\-bit x86\)
+ Ubuntu Server 18\.04 LTS & Ubuntu Server 16\.04 LTS
+ CentOS 7 x86\-64
+ SUSE Linux Enterprise Server 15 SP1

**Note**  
Other Linux distributions and versions may work but have not been tested\.

## Join an Instance to Your Directory<a name="join_linux_prereq"></a>

Before you can join either an Amazon Linux, CentOS, Red Hat, or Ubuntu instance to your directory, the instance must first be launched as specified in [Seamlessly Join a Windows EC2 Instance](launching_instance.md)\. 

**Important**  
Some of the following procedures, if not performed correctly, can render your instance unreachable or unusable\. Therefore, we strongly suggest you make a backup or take a snapshot of your instance before performing these procedures\.

**To join a linux instance to your directory**  
Follow the steps for your specific Linux instance using one of the following tabs:

------
#### [ Amazon Linux ]<a name="amazonlinux"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure your Amazon Linux \- 64bit instance is up to date\.

   ```
   sudo yum -y update
   ```

1. Install the required Amazon Linux packages on your Linux instance\.
**Note**  
Some of these packages may already be installed\.   
As you install the packages, you might be presented with several pop\-up configuration screens\. You can generally leave the fields in these screens blank\.  
Amazon Linux 1  

   ```
   sudo yum -y install sssd realmd krb5-workstation
   ```  
Amazon Linux 2  

   ```
   sudo yum -y install sssd realmd krb5-workstation samba-common-tools
   ```
**Note**  
For help with determining the Amazon Linux version you are using, see [Identifying Amazon Linux Images](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/amazon-linux-ami-basics.html#amazon-linux-image-id) in the *Amazon EC2 User Guide for Linux Instances*\.

1. Join the instance to the directory with the following command\. 

   ```
   sudo realm join -U join_account@example.com example.com --verbose
   ```  
*join\_account@example\.com*  
An account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully qualified DNS name of your directory\.

   ```
   ...
    * Successfully enrolled machine in realm
   ```

1. Set the SSH service to allow password authentication\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vi /etc/ssh/sshd_config
      ```

   1. Set the `PasswordAuthentication` setting to `yes`\.

      ```
      PasswordAuthentication yes
      ```

   1. Restart the SSH service\.

      ```
      sudo systemctl restart sshd.service
      ```

      Alternatively:

      ```
      sudo service sshd restart
      ```

1. After the instance has restarted, connect to it with any SSH client and add the AWS Delegated Administrators group to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the following to the bottom of the `sudoers` file and save it\.

      ```
      ## Add the "AWS Delegated Administrators" group from the example.com domain.
      %AWS\ Delegated\ Administrators@example.com ALL=(ALL:ALL) ALL
      ```

      \(The above example uses "\\<space>" to create the Linux space character\.\)

------
#### [ CentOS ]<a name="centos"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure your CentOS 7 instance is up to date\.

   ```
   sudo yum -y update
   ```

1. Install the required CentOS 7 packages on your Linux instance\.
**Note**  
Some of these packages may already be installed\.   
As you install the packages, you might be presented with several pop\-up configuration screens\. You can generally leave the fields in these screens blank\.

   ```
   sudo yum -y install sssd realmd krb5-workstation samba-common-tools
   ```

1. Join the instance to the directory with the following command\. 

   ```
   sudo realm join -U join_account@example.com example.com --verbose
   ```  
*join\_account@example\.com*  
An account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully qualified DNS name of your directory\.

   ```
   ...
    * Successfully enrolled machine in realm
   ```

1. Set the SSH service to allow password authentication\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vi /etc/ssh/sshd_config
      ```

   1. Set the `PasswordAuthentication` setting to `yes`\.

      ```
      PasswordAuthentication yes
      ```

   1. Restart the SSH service\.

      ```
      sudo systemctl restart sshd.service
      ```

      Alternatively:

      ```
      sudo service sshd restart
      ```

1. After the instance has restarted, connect to it with any SSH client and add the AWS Delegated Administrators group to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the following to the bottom of the `sudoers` file and save it\.

      ```
      ## Add the "AWS Delegated Administrators" group from the example.com domain.
      %AWS\ Delegated\ Administrators@example.com ALL=(ALL:ALL) ALL
      ```

      \(The above example uses "\\<space>" to create the Linux space character\.\)

------
#### [ Red Hat ]<a name="redhat"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure the Red Hat \- 64bit instance is up to date\.

   ```
   sudo yum -y update
   ```

1. Install the required Red Hat packages on your Linux instance\.
**Note**  
Some of these packages may already be installed\.   
As you install the packages, you might be presented with several pop\-up configuration screens\. You can generally leave the fields in these screens blank\.

   ```
   sudo yum -y install sssd realmd krb5-workstation samba-common-tools
   ```

1. Join the instance to the directory with the following command\. 

   ```
   sudo realm join -v -U join_account example.com --install=/
   ```  
*join\_account*  
The **sAMAccountName** for an account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully qualified DNS name of your directory\.

   ```
   ...
    * Successfully enrolled machine in realm
   ```

1. Set the SSH service to allow password authentication\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vi /etc/ssh/sshd_config
      ```

   1. Set the `PasswordAuthentication` setting to `yes`\.

      ```
      PasswordAuthentication yes
      ```

   1. Restart the SSH service\.

      ```
      sudo systemctl restart sshd.service
      ```

      Alternatively:

      ```
      sudo service sshd restart
      ```

1. After the instance has restarted, connect to it with any SSH client and add the AWS Delegated Administrators group to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the following to the bottom of the `sudoers` file and save it\.

      ```
      ## Add the "AWS Delegated Administrators" group from the example.com domain.
      %AWS\ Delegated\ Administrators@example.com ALL=(ALL:ALL) ALL
      ```

      \(The above example uses "\\<space>" to create the Linux space character\.\)

------
#### [ SUSE ]<a name="suse"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure your SUSE Linux 15 instance is up to date\.

   1. Connect the package repository\.

      ```
      sudo SUSEConnect -p PackageHub/15.1/x86_64
      ```

   1. Update SUSE\.

      ```
      sudo zypper update -y
      ```

1. Install the required SUSE Linux 15 packages on your Linux instance\.
**Note**  
Some of these packages may already be installed\.   
As you install the packages, you might be presented with several pop\-up configuration screens\. You can generally leave the fields in these screens blank\.

   ```
   sudo zypper -n install realmd adcli sssd sssd-tools sssd-ad samba-client krb5-client
   ```

1. Join the instance to the directory with the following command\. 

   ```
   sudo realm join -U join_account example.com --verbose
   ```  
*join\_account*  
The sAMAccountName in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully\-qualified DNS name of your directory\.

   ```
   …
   realm: Couldn't join realm: Enabling SSSD in nsswitch.conf and PAM failed.
   ```

   Note that both of the following returns are expected\.

   ```
   ! Couldn't authenticate with keytab while discovering which salt to use:
   ! Enabling SSSD in nsswitch.conf and PAM failed.
   ```

1. Manually enable **SSSD** in **PAM**\.

   ```
   sudo pam-config --add --sss
   ```

1. Edit nsswitch\.conf to enable SSSD in nsswitch\.conf

   ```
   sudo vi /etc/nsswitch.conf
   ```

   ```
   passwd: compat sss
   group:  compat sss
   shadow: compat sss
   ```

1. Add the following line to /etc/pam\.d/common\-session to auto create a home directory at initial login

   ```
   sudo vi /etc/pam.d/common-session
   ```

   ```
   session optional        pam_mkhomedir.so skel=/etc/skel umask=077
   ```

1. Reboot the instance to complete the domain joined process\.

   ```
   sudo reboot
   ```

1. Reconnect to the instance using any SSH client to verify the domain join has completed successfully and finalize additional steps\.

   1. To confirm the instance has been enrolled on the domain

      ```
      sudo realm list
      ```

      ```
      example.com
        type: kerberos
        realm-name: EXAMPLE.COM
        domain-name: example.com
        configured: kerberos-member
        server-software: active-directory
        client-software: sssd
        required-package: sssd-tools
        required-package: sssd
        required-package: adcli
        required-package: samba-client
        login-formats: %U@example.com
        login-policy: allow-realm-logins
      ```

   1. To verify the status of SSSD daemon

      ```
      systemctl status sssd
      ```

      ```
      sssd.service - System Security Services Daemon
         Loaded: loaded (/usr/lib/systemd/system/sssd.service; enabled; vendor preset: disabled)
         Active: active (running) since Wed 2020-04-15 16:22:32 UTC; 3min 49s ago
       Main PID: 479 (sssd)
          Tasks: 4
         CGroup: /system.slice/sssd.service
                 ├─479 /usr/sbin/sssd -i --logger=files
                 ├─505 /usr/lib/sssd/sssd_be --domain example.com --uid 0 --gid 0 --logger=files
                 ├─548 /usr/lib/sssd/sssd_nss --uid 0 --gid 0 --logger=files
                 └─549 /usr/lib/sssd/sssd_pam --uid 0 --gid 0 --logger=files
      ```

1. To permit a user access via SSH and console

   ```
   sudo realm permit join_account@example.com
   ```

   To permit a domain group access via SSH and console

   ```
   sudo realm permit -g 'AWS Delegated Administrators'
   ```

   Or to permit all users access

   ```
   sudo realm permit --all
   ```

1. Set the SSH service to allow password authentication\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vi /etc/ssh/sshd_config
      ```

   1. Set the `PasswordAuthentication` setting to `yes`\.

      ```
      PasswordAuthentication yes
      ```

   1. Restart the SSH service\.

      ```
      sudo systemctl restart sshd.service
      ```

      Alternatively:

      ```
      sudo service sshd restart
      ```

1. 13\. After the instance has restarted, connect to it with any SSH client and add the AWS Delegated Administrators group to the sudoers list by performing the following steps:

   1. Open the sudoers file with the following command:

      ```
      sudo visudo
      ```

   1. Add the following to the bottom of the sudoers file and save it\.

      ```
      ## Add the "Domain Admins" group from the awsad.com domain.
      %AWS\ Delegated\ Administrators@example.com ALL=(ALL) NOPASSWD: ALL
      ```

------
#### [ Ubuntu ]<a name="ubuntu"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure your Ubuntu \- 64bit instance is up to date\.

   ```
   sudo apt-get update
   sudo apt-get -y upgrade
   ```

1. Install the required Ubuntu packages on your Linux instance\.
**Note**  
Some of these packages may already be installed\.   
As you install the packages, you might be presented with several pop\-up configuration screens\. You can generally leave the fields in these screens blank\.

   ```
   sudo apt-get -y install sssd realmd krb5-user samba-common packagekit adcli
   ```

1. Disable Reverse DNS resolution and set the default realm to your domain's FQDN\. Ubuntu Instances **must** be reverse\-resolvable in DNS before the realm will work\. Otherwise, you have to disable reverse DNS in /etc/krb5\.conf as follows:

   ```
   sudo vi /etc/krb5.conf
   ```

   ```
   [libdefaults] 
   default_realm = EXAMPLE.COM 
   rdns = false
   ```

1. Join the instance to the directory with the following command\. 

   ```
   sudo realm join -U join_account example.com --verbose
   ```  
*join\_account@example\.com*  
The **sAMAccountName** for an account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully qualified DNS name of your directory\.

   ```
   ...
    * Successfully enrolled machine in realm
   ```

1. Set the SSH service to allow password authentication\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vi /etc/ssh/sshd_config
      ```

   1. Set the `PasswordAuthentication` setting to `yes`\.

      ```
      PasswordAuthentication yes
      ```

   1. Restart the SSH service\.

      ```
      sudo systemctl restart sshd.service
      ```

      Alternatively:

      ```
      sudo service sshd restart
      ```

1. After the instance has restarted, connect to it with any SSH client and add the AWS Delegated Administrators group to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the following to the bottom of the `sudoers` file and save it\.

      ```
      ## Add the "AWS Delegated Administrators" group from the example.com domain.
      %AWS\ Delegated\ Administrators@example.com ALL=(ALL:ALL) ALL
      ```

      \(The above example uses "\\<space>" to create the Linux space character\.\)

------

## Restricting Account Login Access<a name="linux_filter"></a>

Since all accounts are defined in Active Directory, by default, all the users in the directory can log in to the instance\. You can allow only specific users to log in to the instance with ad\_access\_filter in sssd\.conf\. For example:

```
ad_access_filter = (memberOf=cn=admins,ou=Testou,dc=example,dc=com)
```

*memberOf*  
Indicates that users should only be allowed access to the instance if they are a member of a specific group\.

*cn*  
The common name of the group that should have access\. In this example, the group name is *admins*\.

*ou*  
This is the organizational unit in which the above group is located\. In this example, the OU is *Testou*\.

*dc*  
This is the domain component of your domain\. In this example, *example*\.

*dc*  
This is an additional domain component\. In this example, *com*\.

You must manually add ad\_access\_filter to your /etc/sssd/sssd\.conf\.

Open the /etc/sssd/sssd\.conf file in a text editor\.

```
sudo vi /etc/sssd/sssd.conf
```

After you do this, your sssd\.conf might look like this:

```
[sssd]
domains = example.com
config_file_version = 2 
services = nss, pam 

[domain/example.com] 
ad_domain = example.com 
krb5_realm = EXAMPLE.COM 
realmd_tags = manages-system joined-with-samba 
cache_credentials = True 
id_provider = ad 
krb5_store_password_if_offline = True 
default_shell = /bin/bash 
ldap_id_mapping = True 
use_fully_qualified_names = True 
fallback_homedir = /home/%u@%d 
access_provider = ad 
ad_access_filter = (memberOf=cn=admins,ou=Testou,dc=example,dc=com)
```

In order for the configuration to take effect, you need to restart the sssd service:

```
sudo systemctl restart sssd.service
```

Alternatively, you could use:

```
sudo service sssd start
```

## Connect to the Instance<a name="linux_connect"></a>

When a user connects to the instance using an SSH client, they are prompted for their user name\. The user can enter the user name in either the `username@example.com` or `EXAMPLE\username` format\. The response will appear similar to the following, depending on which linux distribution you are using:

**Amazon Linux, Red Hat Enterprise Linux, and CentOS Linux**

```
login as: johndoe@example.com
johndoe@example.com's password:
Last login: Thu Jun 25 16:26:28 2015 from XX.XX.XX.XX
```

**SUSE Linux**

```
SUSE Linux Enterprise Server 15 SP1 x86_64 (64-bit)
 
As "root" (sudo or sudo -i) use the:
  - zypper command for package management
  - yast command for configuration management
 
Management and Config: https://www.suse.com/suse-in-the-cloud-basics
Documentation: https://www.suse.com/documentation/sles-15/
Forum: https://forums.suse.com/forumdisplay.php?93-SUSE-Public-Cloud
 
Have a lot of fun...
```

**Ubuntu Linux**

```
login as: admin@example.com
admin@example.com@10.24.34.0's password:
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.15.0-1057-aws x86_64)
 
* Documentation:  https://help.ubuntu.com
* Management:     https://landscape.canonical.com
* Support:        https://ubuntu.com/advantage
 
  System information as of Sat Apr 18 22:03:35 UTC 2020
 
  System load:  0.01              Processes:           102
  Usage of /:   18.6% of 7.69GB   Users logged in:     2
  Memory usage: 16%               IP address for eth0: 10.24.34.1
  Swap usage:   0%
```