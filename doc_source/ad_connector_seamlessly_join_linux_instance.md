# Seamlessly Join a Linux EC2 Instance to Your AD Connector Directory<a name="ad_connector_seamlessly_join_linux_instance"></a>

This procedure seamlessly joins a Linux EC2 instance to your AD Connector directory\.

The following Linux instance distributions and versions are supported:
+ Amazon Linux AMI 2018\.03\.0
+ Amazon Linux 2 \(64\-bit x86\)
+ Red Hat Enterprise Linux 8 \(HVM\) \(64\-bit x86\)
+ Ubuntu Server 18\.04 LTS & Ubuntu Server 16\.04 LTS
+ CentOS 7 x86\-64
+ SUSE Linux Enterprise Server 15 SP1

**Note**  
Distributions prior to Ubuntu 14 and Red Hat Enterprise Linux 7 do not support the seamless domain join feature\.

## Prerequisites<a name="ad_connector_seamless-linux-prereqs"></a>

Before you can set up seamless domain join to a Linux EC2 instance, you need to complete the procedures in this section\.

### Select Your Seamless Domain Join Service Account<a name="ad_connector_seamless-linux-prereqs-select"></a>

You can seamlessly join Linux computers to your on\-premises Active Directory domain through AD Connector\. To do that, you must create a user account with create computer account permissions to join the computers to the domain\. You can use your AD Connector service account if you prefer\. Or you can use any other account that has sufficient privileges to join computers to the domain\. Although members of the *Domain Admins* or other groups might have sufficient privileges to join computers to the domain, we do not recommend these\. As a best practice, we recommend that you use a service account that has the minimum privileges necessary to join computers to the domain\.

To delegate an account with the minimum privileges necessary to join computers to the domain, you can run the following PowerShell commands\. You must run these commands from a domain\-joined Windows computer with the [Installing the Active Directory Administration Tools](ms_ad_install_ad_tools.md) installed\. In addition, you must use an account that has permission to modify the permissions on your Computers OU or container\. The PowerShell command sets permissions that allow the service account to create computer objects in your domain’s default computers container\. If you prefer using a graphical user interface \(GUI\) you can use the manual process that is described in [Delegate privileges to your service account](prereq_connector.md#connect_delegate_privileges)\.

```
$AccountName = 'awsSeamlessDomain'
# DO NOT modify anything below this comment.
# Getting Active Directory information.
Import-Module 'ActiveDirectory'
$Domain = Get-ADDomain -ErrorAction Stop
$BaseDn = $Domain.DistinguishedName
$ComputersContainer = $Domain.ComputersContainer
$SchemaNamingContext = Get-ADRootDSE | Select-Object -ExpandProperty 'schemaNamingContext'
[System.GUID]$ServicePrincipalNameGuid = (Get-ADObject -SearchBase $SchemaNamingContext -Filter { lDAPDisplayName -eq 'Computer' } -Properties 'schemaIDGUID').schemaIDGUID
# Getting Service account Information.
$AccountProperties = Get-ADUser -Identity $AccountName
$AccountSid = New-Object -TypeName 'System.Security.Principal.SecurityIdentifier' $AccountProperties.SID.Value
# Getting ACL settings for the Computers container.
$ObjectAcl = Get-ACL -Path "AD:\$ComputersContainer" 
# Setting ACL allowing the service account the ability to create child computer objects in the Computers container.
$AddAccessRule = New-Object -TypeName 'System.DirectoryServices.ActiveDirectoryAccessRule' $AccountSid, 'CreateChild', 'Allow', $ServicePrincipalNameGUID, 'All'
$ObjectAcl.AddAccessRule($AddAccessRule)
Set-ACL -AclObject $ObjectAcl -Path "AD:\$ComputersContainer"
```

If you prefer using a graphical user interface \(GUI\) you can use the manual process to described in [Delegate privileges to your service account](prereq_connector.md#connect_delegate_privileges)\.

### Create the Secrets to Store the Domain Service Account<a name="seamless-linux-prereqs-create-secrets"></a>

You can use AWS Secrets Manager to store the domain service account\.

**To create secrets and store the domain service account information**

1. Sign in to the AWS Management Console and open the AWS Secrets Manager console at [https://console\.aws\.amazon\.com/secretsmanager/](https://console.aws.amazon.com/secretsmanager/)\.

1. Choose **Store a new secret**\. 

1. On the **Store a new secret** page, do the following:

   1. Under **Select secret type**, choose **Other type of secrets**\.

   1. Under **Specify the key/value pairs to be stored in the secret**, do the following:

      1. In the first box, enter **awsSeamlessDomainUsername**\. On the same row, in the next box, enter the user name for your service account\. For example, if you used the PowerShell command previously, the service account name would be `awsSeamlessDomain`\.
**Note**  
You must enter **awsSeamlessDomainUsername** exactly as it is\. Make sure there are not any leading or ending spaces\. Otherwise the domain join will fail\. 

      1. Choose **Add row**\.

      1. On the new row, in the first box, enter **awsSeamlessDomainPassword**\. On the same row, in the next box, enter the password for your service account\.
**Note**  
You must enter **awsSeamlessDomainPassword** exactly as it is\. Make sure there are not any leading or ending spaces\. Otherwise the domain join will fail\. 

      1. Under **Select the encryption key**, choose **DefaultEncryptionKey** from the menu\. Secrets Manager always encrypts the secret when you choose this option, and provides it at no charge to you\. You also may choose a key you created\.

      1. Choose **Next**\.

1. Under **Secret name**, enter a secret name that includes your directory ID using the following format **aws/directory\-services/*d\-xxxxxxxxx*/seamless\-domain\-join**\. This will be used to retrieve secrets in the application\.
**Note**  
You must enter **aws/directory\-services/*d\-xxxxxxxxx*/seamless\-domain\-join** exactly as it is but replace *d\-xxxxxxxxxx* with your directory ID\. Make sure that there are no leading or ending spaces\. Otherwise the domain join will fail\. 

1. Leave everything else set to defaults, and then choose **Next**\.

1. Under **Configure automatic rotation**, choose **Disable automatic rotation**, and then choose **Next**\.

1. Review the settings, and then choose **Store** to save your changes\. The Secrets Manager console returns you to the list of secrets in your account with your new secret now included in the list\. 

1. Choose your newly created secret name from the list, and take note of the **Secret ARN** value\. You will need it in the next section\.

### Create the Required IAM Policy and Role<a name="seamless-linux-prereqs-create-policy"></a>

Use the following prerequisite steps to create a custom policy that allows read\-only access to your Secrets Manager seamless domain join secret \(which you created earlier\), and to create a new LinuxEC2DomainJoin IAM role\. 

#### Create the Secrets Manager IAM Read Policy<a name="seamless-linux-prereqs-create-policy-step1"></a>

You use the IAM console to create a policy that grants read\-only access to your Secrets Manager secret\.

**To create the Secrets Manager IAM read policy**

1. Sign in to the AWS Management Console as a user that has permission to create IAM policies\. Then open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Policies**\.

1. Choose **Create policy**\.

1. Choose the **JSON** tab and copy the text from the following JSON policy document\. Then paste it into the **JSON** text box\.
**Note**  
Make sure you replace the `Resource` ARN with the actual ARN of the secret that you created earlier\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "secretsmanager:GetSecretValue",
                   "secretsmanager:DescribeSecret"
               ],
               "Resource": [
                   "arn:aws:secretsmanager:us-east-1:############:secret:aws/directory-service/d-xxxxxxxxxx/seamless-domain-join-example"
               ]
           }
       ]
   }
   ```

1. When you are finished, choose **Review policy**\. The [Policy Validator](https://docs.aws.amazon.com/https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_policy-validator.html) reports any syntax errors\.

1. On the **Review policy** page, enter a policy name, such as **SM\-Secret\-Linux\-DJ\-*d\-xxxxxxxxxx*\-Read**\. Review the **Summary** section to see the permissions that your policy grants\. Then choose **Create policy** to save your changes\. The new policy appears in the list of managed policies and is now ready to attach to an identity\.

**Note**  
We recommend you create one policy per secret\. Doing so ensures that instances only have access to the appropriate secret and minimizes the impact if an instance is compromised\. 

#### Create the LinuxEC2DomainJoin Role<a name="seamless-linux-prereqs-create-policy-step2"></a>

You use the IAM console to create the role that you will use to domain join your Linux EC2 instance\.

**To create the LinuxEC2DomainJoin role**

1. Sign in to the AWS Management Console as a user that has permission to create IAM policies\. Then open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Roles**\.

1. In the content pane, choose **Create role**\.

1. Under **Select type of trusted entity**, choose **AWS service**\.

1. Under **Choose a use case** choose **EC2**, and then choose **Next: Permissions**\.

1. For **Filter policies**, do the following:

   1. Enter **AmazonSSMManagedInstanceCore**\. Then select the check box for that item in the list\.

   1. Enter **AmazonSSMDirectoryServiceAccess**\. Then select the check box for that item in the list\.

   1. Enter **SM\-Secret\-Linux\-DJ\-*d\-xxxxxxxxxx*\-Read** \(or the name of the policy that you created in the previous procedure\)\. Then select the check box for that item in the list\.
**Note**  
AmazonSSMDirectoryServiceAccess provides the permissions to join instances to an Active Directory managed by AWS Directory Service\. AmazonSSMManagedInstanceCore provides the minimum permissions necessary to use the AWS Systems Manager service\. For more information about creating a role with these permissions, and for information about other permissions and policies you can assign to your IAM role, see [Create an IAM Instance Profile for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html) in the *AWS Systems Manager User Guide*\.

1. Choose **Next: Tags**\.

1. \(Optional\) Add one or more tag key\-value pairs to organize, track, or control access for this role\. Then choose **Next: Review**\.

1. Next to **Role name**, enter a name for your new role, such as **LinuxEC2DomainJoin** or another name that you prefer\.

1. \(Optional\) For **Role description**, enter a description\.

1. Choose **Create role**\.

## Seamlessly Join Your Linux EC2 Instance<a name="ad_connector_seamless-linux-join-instance"></a>

Now that you have configured all of the prerequisite tasks, you can use the following procedure to seamlessly join your Linux EC2 instance\.

**To seamlessly join your Linux EC2 instance**

1. Sign in to the AWS Management Console and open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the Region selector in the navigation bar, choose the same Region as the existing directory\.

1. Choose **Launch Instance**\.

1. On the **Step 1** page, choose **Select** for the appropriate Amazon Machine Image \(AMI\)\.
**Note**  
The AMI used must have AWS Systems Manager \(SSM Agent\) version 2\.3\.1644\.0 or higher\. To check the installed SSM Agent version in your AMI by launching an instance from that AMI, see [Getting the currently installed SSM Agent version](https://docs.aws.amazon.com/systems-manager/latest/userguide/ssm-agent-get-version.html)\. If you need to upgrade the SSM Agent, see [Installing and configuring SSM Agent on EC2 instances for Linux](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-install-ssm-agent.html)\. 

1. On the **Step 2** page, select the appropriate instance type, and then choose **Next: Configure Instance Details**\. 

1. On the **Step 3** page, do the following, and then choose **Next: Add Storage**: 

   1. For **Network**, choose the VPC that your directory was created in\. 

   1. For **Subnet**, choose one of the public subnets in your VPC\. The subnet that you choose must have all external traffic routed to an internet gateway\. If this is not the case, you won't be able to connect to the instance remotely\. 

   1. For **Auto\-assign Public IP**, choose **Enable**\. For more information about public and private IP addressing, see [Amazon EC2 Instance IP Addressing](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-instance-addressing.html) in the *Amazon EC2 User Guide for Windows Instances*\. 

   1. For **Domain join directory**, choose your domain from the list\. 

   1. For **IAM role**, choose the IAM role that you previously created in the prerequisites section **Step 2: Create the LinuxEC2DomainJoin Role**\. 

1. On both the **Step 4** and **Step 5** pages, leave the default settings or make changes as needed\. Then choose **Next** on each\. 

1. On the **Step 6** page, select a security group that has been configured to allow remote access to the instance from your network\. Then choose **Review and Launch**\. 

1. On the **Step 7** page, choose **Launch**, choose a key pair, and then choose **Launch Instance**\.

**Note**  
If you are performing a seamless domain join with SUSE Linux, a reboot is required before authentications will work\. To reboot SUSE from the Linux terminal, type **sudo reboot**\.