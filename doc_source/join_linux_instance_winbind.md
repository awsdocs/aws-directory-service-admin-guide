# Manually join a Linux instance using Winbind<a name="join_linux_instance_winbind"></a>

You can use the Winbind service to manually join your Linux instances to an AWS Managed Microsoft AD domain\. This enables your existing on\-premises Active Directory users to use their AD credentials when accessing the Linux instances joined to your AWS Managed Microsoft AD\. The following Linux instance distributions and versions are supported:
+ Amazon Linux AMI 2018\.03\.0
+ Amazon Linux 2 \(64\-bit x86\)
+ Red Hat Enterprise Linux 8 \(HVM\) \(64\-bit x86\)
+ Ubuntu Server 18\.04 LTS & Ubuntu Server 16\.04 LTS
+ CentOS 7 x86\-64
+ SUSE Linux Enterprise Server 15 SP1

**Note**  
Other Linux distributions and versions may work but have not been tested\.

## Join an instance to your directory<a name="join_linux_winbind_prereq"></a>

Before you can join either an Amazon Linux, CentOS, Red Hat, or Ubuntu instance to your directory, the instance must first be launched as specified in [Seamlessly join a Windows EC2 instance](launching_instance.md)\. 

**Important**  
Some of the following procedures, if not performed correctly, can render your instance unreachable or unusable\. Therefore, we strongly suggest you make a backup or take a snapshot of your instance before performing these procedures\.

**To join a linux instance to your directory**  
Follow the steps for your specific Linux instance using one of the following tabs:

------
#### [ Amazon Linux/CENTOS/REDHAT ]<a name="amazonlinux"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure your Linux instance is up to date\.

   ```
   sudo yum -y update
   ```

1. Install the required Samba / Winbind packages on your Linux instance\.

   ```
   sudo yum -y install authconfig samba samba-client samba-winbind samba-winbind-clients
   ```

1. Make a backup of the main `smb.conf` file so you can revert back to it in case of any failure: 

   ```
   sudo cp /etc/samba/smb.conf /etc/samba/smb.bk
   ```

1. Open the original configuration file \[`/etc/samba/smb.conf`\] in a text editor\.

   ```
   sudo vim /etc/samba/smb.conf
   ```

   Fill in your Active directory domain environment information as shown in the below example:

   ```
   [global]
    workgroup = example
    security = ads
    realm = example.com 
    idmap config * : rangesize = 1000000
    idmap config * : range = 1000000-19999999
    idmap config * : backend = autorid
    winbind enum users = no
    winbind enum groups = no
    template homedir = /home/%U@%D
    template shell = /bin/bash
    winbind use default domain = false
   ```

1. Open the hosts file \[`/etc/hosts`\] in a text editor\.

   ```
   sudo vim /etc/hosts
   ```

   Add your Linux instance private IP address as follows:

   ```
   10.x.x.x  Linux_hostname.example.com Linux_hostname
   ```
**Note**  
If you did not specify your IP Address in the `/etc/hosts` file, you might receive the following DNS error while joining the instance to the domain\.:  
`No DNS domain configured for linux-instance. Unable to perform DNS Update. DNS update failed: NT_STATUS_INVALID_PARAMETER`  
This error means that the join was successful but the \[net ads\] command was unable to register the DNS record in DNS\.

1. Join the Linux instance to Active Directory using the net utility\. 

   ```
   sudo net ads join -U join_account@example.com
   ```  
*join\_account@example\.com*  
An account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate directory join privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully qualified DNS name of your directory\.

   ```
   Enter join_account@example.com's password:
   Using short domain name -- example
   Joined 'IP-10-x-x-x' to dns domain 'example.com'
   ```

1. Modify PAM Configuration file, Use the command below to add the necessary entries for winbind authentication:

   ```
   sudo authconfig --enablewinbind --enablewinbindauth  --enablemkhomedir   --update
   ```

1. Set the SSH service to allow password authentication by editing the `/etc/ssh/sshd_config` file\.\.

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

1. After the instance has restarted, connect to it with any SSH client and add the root privileges for a domain user or group to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the required groups or users from your Trusting or Trusted domain as follows, and then save it\.

      ```
      ## Adding Domain Users/Groups.
      %domainname\\AWS\ Delegated\ Administrators ALL=(ALL:ALL) ALL
      %domainname\\groupname ALL=(ALL:ALL) ALL
      domainname\\username ALL=(ALL:ALL) ALL
      %Trusted_DomainName\\groupname ALL=(ALL:ALL) ALL
      Trusted_DomainName\\username ALL=(ALL:ALL) ALL
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

1. Install the required Samba / Winbind packages on your Linux instance\.

   ```
   sudo zypper in -y samba samba-winbind
   ```

1. Make a backup of the main `smb.conf` file so you can revert back to it in case of any failure: 

   ```
   sudo cp /etc/samba/smb.conf /etc/samba/smb.bk
   ```

1. Open the original configuration file \[`/etc/samba/smb.conf`\] in a text editor\.

   ```
   sudo vim /etc/samba/smb.conf
   ```

   Fill in your Active directory domain environment information as shown in the below example:

   ```
   [global]
    workgroup = example
    security = ads
    realm = example.com 
    idmap config * : rangesize = 1000000
    idmap config * : range = 1000000-19999999
    idmap config * : backend = autorid
    winbind enum users = no
    winbind enum groups = no
    template homedir = /home/%U@%D
    template shell = /bin/bash
    winbind use default domain = false
   ```

1. Open the hosts file \[`/etc/hosts`\] in a text editor\.

   ```
   sudo vim /etc/hosts
   ```

   Add your Linux instance private IP address as follows:

   ```
   10.x.x.x  Linux_hostname.example.com Linux_hostname
   ```
**Note**  
If you did not specify your IP Address in the `/etc/hosts` file, you might receive the following DNS error while joining the instance to the domain\.:  
`No DNS domain configured for linux-instance. Unable to perform DNS Update. DNS update failed: NT_STATUS_INVALID_PARAMETER`  
This error means that the join was successful but the \[net ads\] command was unable to register the DNS record in DNS\.

1. Join the Linux instance to the directory with the following command\. 

   ```
   sudo net ads join -U join_account@example.com
   ```  
*join\_account*  
The sAMAccountName in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate directory join privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully\-qualified DNS name of your directory\.

   ```
   Enter join_account@example.com's password:
   Using short domain name -- example
   Joined 'IP-10-x-x-x' to dns domain 'example.com'
   ```

1. Modify PAM Configuration file, Use the command below to add the necessary entries for Winbind authentication:

   ```
   sudo pam-config --add --winbind --mkhomedir
   ```

1. Open the Name Service Switch configuration file \[`/etc/nsswitch.conf`\] in a text editor\.

   ```
   vim /etc/nsswitch.conf
   ```

   Add the Winbind directive as shown below\.

   ```
   passwd: files winbind
   shadow: files winbind
   group:  files winbind
   ```

1. Set the SSH service to allow password authentication by editing the `/etc/ssh/sshd_config` file\.\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vim /etc/ssh/sshd_config
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

1. After the instance has restarted, connect to it with any SSH client and add root privileges for a domain user or group, to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the required groups or users from your Trusting or Trusted domain as follows, and then save it\.

      ```
      ## Adding Domain Users/Groups.
      %domainname\\AWS\ Delegated\ Administrators ALL=(ALL:ALL) ALL
      %domainname\\groupname ALL=(ALL:ALL) ALL
      domainname\\username ALL=(ALL:ALL) ALL
      %Trusted_DomainName\\groupname ALL=(ALL:ALL) ALL
      Trusted_DomainName\\username ALL=(ALL:ALL) ALL
      ```

      \(The above example uses "\\<space>" to create the Linux space character\.\)

------
#### [ Ubuntu ]<a name="ubuntu"></a>

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-ubuntu-debian/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure your Linux instance is up to date\.

   ```
   sudo yum -y update
   ```

   ```
   sudo apt-get -y upgrade
   ```

1. Install the required Samba / Winbind packages on your Linux instance\.

   ```
   sudo apt -y install samba winbind libnss-winbind libpam-winbind
   ```

1. Make a backup of the main `smb.conf` file so you can revert back to it in case of any failure\. 

   ```
   sudo cp /etc/samba/smb.conf /etc/samba/smb.bk
   ```

1. Open the original configuration file \[`/etc/samba/smb.conf`\] in a text editor\.

   ```
   sudo vim /etc/samba/smb.conf
   ```

   Fill in your Active directory domain environment information as shown in the below example:

   ```
   [global]
    workgroup = example
    security = ads
    realm = example.com 
    idmap config * : rangesize = 1000000
    idmap config * : range = 1000000-19999999
    idmap config * : backend = autorid
    winbind enum users = no
    winbind enum groups = no
    template homedir = /home/%U@%D
    template shell = /bin/bash
    winbind use default domain = false
   ```

1. Open the hosts file \[`/etc/hosts`\] in a text editor\.

   ```
   sudo vim /etc/hosts
   ```

   Add your Linux instance private IP address as follows:

   ```
   10.x.x.x  Linux_hostname.example.com Linux_hostname
   ```
**Note**  
If you did not specify your IP Address in the `/etc/hosts` file, you might receive the following DNS error while joining the instance to the domain\.:  
`No DNS domain configured for linux-instance. Unable to perform DNS Update. DNS update failed: NT_STATUS_INVALID_PARAMETER`  
This error means that the join was successful but the \[net ads\] command was unable to register the DNS record in DNS\.

1. Join the Linux instance to Active Directory using the net utility\. 

   ```
   sudo net ads join -U join_account@example.com
   ```  
*join\_account@example\.com*  
An account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate directory join privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully qualified DNS name of your directory\.

   ```
   Enter join_account@example.com's password:
   Using short domain name -- example
   Joined 'IP-10-x-x-x' to dns domain 'example.com'
   ```

1. Modify PAM Configuration file, Use the command below to add the necessary entries for Winbind authentication:

   ```
   sudo pam-auth-update --add --winbind --enable mkhomedir
   ```

1. Open the Name Service Switch configuration file \[`/etc/nsswitch.conf`\] in a text editor\.

   ```
   vim /etc/nsswitch.conf
   ```

   Add the Winbind directive as shown below\.

   ```
   passwd: compat winbind
   group:  compat winbind
   shadow: compat winbind
   ```

1. Set the SSH service to allow password authentication by editing the `/etc/ssh/sshd_config` file\.\.

   1. Open the `/etc/ssh/sshd_config` file in a text editor\.

      ```
      sudo vim /etc/ssh/sshd_config
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

1. After the instance has restarted, connect to it with any SSH client and add root privileges for a domain user or group, to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      sudo visudo
      ```

   1. Add the required groups or users from your Trusting or Trusted domain as follows, and then save it\.

      ```
      ## Adding Domain Users/Groups.
      %domainname\\AWS\ Delegated\ Administrators ALL=(ALL:ALL) ALL
      %domainname\\groupname ALL=(ALL:ALL) ALL
      domainname\\username ALL=(ALL:ALL) ALL
      %Trusted_DomainName\\groupname ALL=(ALL:ALL) ALL
      Trusted_DomainName\\username ALL=(ALL:ALL) ALL
      ```

      \(The above example uses "\\<space>" to create the Linux space character\.\)

------

## Connect to the instance<a name="linux_winbind_connect"></a>

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