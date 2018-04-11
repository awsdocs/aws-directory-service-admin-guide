# Manually Join a Linux Instance<a name="simple_ad_join_linux_instance"></a>

In addition to Amazon EC2 Windows instances, you can also join certain Amazon EC2 Linux instances to a Simple AD or AWS Directory Service for Microsoft Active Directory directory\. The following Linux instance distributions and versions are supported:
+ Amazon Linux AMI 2015\.03
+ Red Hat Enterprise Linux 7\.2
+ Ubuntu Server 14\.04 LTS
+ CentOS 7

**Note**  
Other Linux distributions and versions may work but have not been tested\.

## Prerequisites for Joining an Instance to a Simple AD or AWS Managed Microsoft AD Directory<a name="join_linux_prereq"></a>

To join a Linux instance to your directory, the instance must be launched as specified in [Seamlessly Join a Windows EC2 Instance](launching_instance.md)\. 

**Important**  
When using Simple AD, if you create a user account on a Linux instance with the option "Force user to change password at first login," that user will not be able to initially change their password using kpasswd\. In order to change the password the first time, a domain administrator must update the user password using the Active Directory Management Tools\.  
Some of the following procedures, if not performed correctly, can render your instance unreachable or unusable\. Therefore, we strongly suggest you make a backup or take a snapshot of your instance before performing these procedures\.

**To join a Linux instance to a Simple AD or AWS Managed Microsoft AD directory**

1. Connect to the instance using any SSH client\.

1. Configure the Linux instance to use the DNS server IP addresses of the AWS Directory Service\-provided DNS servers\. You can do this either by setting it up in the DHCP Options set attached to the VPC or by setting it manually on the instance\. If you want to set it manually, see [How do I assign a static DNS server to a private Amazon EC2 instance](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-static-dns-rhel-centos-amazon/) in the AWS Knowledge Center for guidance on setting the persistent DNS server for your particular Linux distribution and version\.

1. Make sure the instance is up to date\.  
Amazon Linux \- 64bit/Red Hat \- 64bit/CentOS 7  

   ```
   $ sudo yum -y update
   ```  
Ubuntu \- 64bit  

   ```
   $ sudo apt-get update
   $ sudo apt-get -y upgrade
   ```

1. Install the required packages on your Linux instance\.
**Note**  
Some of these packages may already be installed\.   
As you install the packages, particularly in Ubuntu, you might be presented with several pop\-up configuration screens\. You can generally leave the fields in these screens blank\.  
Amazon Linux 1  

   ```
   $ sudo yum -y install sssd realmd krb5-workstation
   ```  
Amazon Linux 2, Red Hat 7, CentOS 7  

   ```
   $ sudo yum -y install sssd realmd krb5-workstation samba-common-tools
   ```  
Ubuntu \- 64bit  

   ```
   $ sudo apt-get -y install sssd realmd krb5-user samba-common
   ```

1. Join the instance to the directory with the following command\. 

   ```
   $ sudo realm join -U join_account@example.com example.com --verbose
   ```  
*join\_account@example\.com*  
An account in the *example\.com* domain that has domain join privileges\. Enter the password for the account when prompted\. For more information about delegating these privileges, see [Delegate Directory Join Privileges for AWS Managed Microsoft AD](directory_join_privileges.md)\.  
*example\.com*  
The fully\-qualified DNS name of your directory\.

   ```
   ...
    * Successfully enrolled machine in realm
   ```
**Note**  
If you are using Ubuntu 14\.04, and encounter the following error:   
**realm: Couldn't join realm: Failed to enroll machine in realm\. See diagnostics\.**\.   
Complete the following additional steps, and then attempt a domain join to resolve the issue:   

   ```
   $ killall aptd
   $ apt-get install packagekit adcli
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

1. Start the SSSD service\.

   ```
   $ sudo systemctl start sssd.service
   ```

   Alternatively:

   ```
   $ sudo service sssd start
   ```

1. Restart the instance\.

1. After the instance has restarted, connect to it with any SSH client and add the domain admins group to the sudoers list by performing the following steps:

   1. Open the `sudoers` file with the following command:

      ```
      $ sudo vi -f /etc/sudoers
      ```

   1. Do one of the following tasks, depending on which Linux instance distribution you are running:

      1. If you are running Amazon Linux or CentOS, add the following to the bottom of the `sudoers` file and save it\.

         ```
         ## Add the "Domain Admins" group from the example.com domain.
         %Domain\ Admins@example.com ALL=(ALL:ALL) ALL
         ```

         \(The above example uses "\\<space>" to create the Linux space character\.\)

      1. If you are running Ubuntu, add the following to the bottom of the `sudoers` file and save it\.

         ```
         ## Add the "Domain Admins" group from the example.com domain.
         %Domain\\ Admins@example.com ALL=(ALL:ALL) ALL
         ```

         \(The above example uses "\\\\<space>" with two slashes to create the Linux space character\.\)

1. By default, all users in the directory can log in to the instance\. You can allow only specific users to log in to the instance with ad\_access\_filter\. For example:

   ```
   ad_access_filter = (memberOf=cn=admins,ou=Testou,dc=example,dc=com)
   ```  
*memberOf*  
Indicates that users should only be allowed access to the instance if they are a member of a specific group\.  
*cn*  
The canonical name of the group that should have access\. In this example, the group name is *admins*\.  
*ou*  
This is the organizational unit in which the above group is located\. In this example, the OU is *Testou*\.  
*dc*  
This is the domain component of your domain\. In this example, *example*\.  
*dc*  
This is an additional domain component\. In this example, *com*\.

   You must manually add ad\_access\_filter to your sssd\.conf\. After you do this, your sssd\.conf might look like this:

   ```
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

## Connect to the Instance<a name="simple_ad_linux_connect"></a>

When a user connects to the instance using an SSH client, they are prompted for their username\. The user can enter the username in either the `username@example.com` or `EXAMPLE\username` format\. The response will appear similar to the following:

```
login as: johndoe@example.com
johndoe@example.com's password:
Last login: Thu Jun 25 16:26:28 2015 from XX.XX.XX.XX
```