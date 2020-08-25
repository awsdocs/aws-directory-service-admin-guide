# Enable Server\-Side LDAPS Using AWS Managed Microsoft AD<a name="ms_ad_ldap_server_side"></a>

Server\-side LDAPS support encrypts LDAP communications between your commercial or homegrown LDAP\-aware applications and your AWS Managed Microsoft AD directory\. This helps to improve security across the wire and meet compliance requirements using the Secure Sockets Layer \(SSL\) cryptographic protocol\.

## Enable Server\-Side LDAPS<a name="enableserversideldaps"></a>

For detailed instructions on how to set up and configure server\-side LDAPS and your certificate authority \(CA\) server, see [How to Enable Server\-Side LDAPS for Your AWS Managed Microsoft AD Directory](https://aws.amazon.com/blogs/security/how-to-enable-ldaps-for-your-aws-microsoft-ad-directory/) on the AWS Security Blog\. 

You must do most of the setup from the Amazon EC2 instance that you use to manage your AWS Managed Microsoft AD domain controllers\. The following steps guide you through enabling LDAPS for your domain in the AWS Cloud\.

**Topics**
+ [Step 1: Delegate Who Can Enable LDAPS](#grantpermsldaps)
+ [Step 2: Set Up Your Certificate Authority](#setupca)
+ [Step 3: Create a Certificate Template](#createcustomcert)
+ [Step 4: Add Security Group Rules](#addgrouprules)

### Step 1: Delegate Who Can Enable LDAPS<a name="grantpermsldaps"></a>

To enable server\-side LDAPS, you must be a member of the Admins or AWS Delegated Enterprise Certificate Authority Administrators group in your AWS Managed Microsoft AD directory\. Alternatively, you can be the default administrative user \(Admin account\)\. If you prefer, you can have a user other than the Admin account setup LDAPS\. In that case, add that user to the Admins or AWS Delegated Enterprise Certificate Authority Administrators group in your AWS Managed Microsoft AD directory\.

### Step 2: Set Up Your Certificate Authority<a name="setupca"></a>

Before you can enable server\-side LDAPS, you must create a certificate\. This certificate must be issued by a Microsoft enterprise CA server that is joined to your AWS Managed Microsoft AD domain\. Once created, the certificate must be installed on each of your domain controllers in that domain\. This certificate lets the LDAP service on the domain controllers listen for and automatically accept SSL connections from LDAP clients\. 

**Note**  
Server\-side LDAPS with AWS Managed Microsoft AD does not support certificates that are issued by a standalone CA\. It also does not support certificates issued by a third\-party certification authority\.

Depending on your business need, you have the following options for setting up or connecting to a CA in your domain: 
+ **Create a subordinate Microsoft enterprise CA** – \(Recommended\) With this option, you can deploy a subordinate Microsoft enterprise CA server in the AWS Cloud\. The server can use Amazon EC2 so that it works with your existing root Microsoft CA\. For more information about how to set up a subordinate Microsoft enterprise CA, see **Step 4: Add a Microsoft Enterprise CA to your AWS Microsoft AD directory** in [How to Enable Server\-Side LDAPS for Your AWS Managed Microsoft AD Directory](https://aws.amazon.com/blogs/security/how-to-enable-ldaps-for-your-aws-microsoft-ad-directory/)\.
+ **Create a root Microsoft enterprise CA** – With this option, you can create a root Microsoft enterprise CA in the AWS Cloud using Amazon EC2 and join it to your AWS Managed Microsoft AD domain\. This root CA can issue the certificate to your domain controllers\. For more information about setting up a new root CA, see **Step 3: Install and Configure an Offline CA** in [How to Enable Server\-Side LDAPS for Your AWS Managed Microsoft AD Directory](https://aws.amazon.com/blogs/security/how-to-enable-ldaps-for-your-aws-microsoft-ad-directory/)\.

For more information about how to join your EC2 instance to the domain, see [Join an EC2 Instance to Your AWS Managed Microsoft AD Directory](ms_ad_join_instance.md)\.

### Step 3: Create a Certificate Template<a name="createcustomcert"></a>

After your enterprise CA has been set up, you can configure the Kerberos Authentication certificate template\. 

**To create a certificate template**

1. Launch **Microsoft Windows Server Manager**\. Select **Tools > Certification Authority**\.

1. In the **Certificate Authority** window, expand the **Certificate Authority** tree in the left pane\. Right\-click **Certificate Templates**, and choose **Manage**\.

1. In the** Certificate Templates Console** window, right\-click **Kerberos Authentication** and choose **Duplicate Template**\.

1. The **Properties of New Template** window will pop up\.

1. In the** Properties of New Template** window, go to the **Compatibility** tab, and then do the following:

   1. Change **Certification Authority** to the OS that matches your CA\. 

   1. If a **Resulting changes** window pops up, select **OK**\.

   1. Change **Certification recipient** to **Windows 8\.1 / Windows Server 2012 R2**\.
**Note**  
AWS Managed Microsoft AD is powered by Windows Server 2012 R2\.

   1. If a **Resulting changes** windows pops up, select **OK**\.

1. Click the **General **tab and change the **Template display name** to **LDAPOverSSL** or any other name you would prefer\.

1. Click the **Security **tab, and choose **Domain Controllers** in the **Group or user names** section\. In the **Permissions for Domain Controllers** section, verify that the **Allow** check boxes for **Read**, **Enroll**, and **Autoenroll** are checked\.

1. Choose **OK** to create the **LDAPOverSSL** \(or the name you specified above\) certificate template\. Close the **Certificate Templates Console** window\.

1. In the **Certificate Authority** window, right\-click **Certificate Templates**, and choose **New > Certificate Template to Issue**\.

1. In the **Enable Certificate Templates** window, choose **LDAPOverSSL** \(or the name you specified above\), and then choose **OK**\.

### Step 4: Add Security Group Rules<a name="addgrouprules"></a>

In the final step, you must open the Amazon EC2 console and add security group rules\. These rules allow your domain controllers to connect to your enterprise CA to request a certificate\. To do this, you add inbound rules so that your enterprise CA can accept incoming traffic from your domain controllers\. Then you add outbound rules to allow traffic from your domain controllers to the enterprise CA\.

Once both rules have been configured, your domain controllers request a certificate from your enterprise CA automatically and enable LDAPS for your directory\. The LDAP service on your domain controllers is now ready to accept LDAPS connections\. 

**To configure security group rules**

1. Navigate to your Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2](https://console.aws.amazon.com/ec2) and sign in with administrator credentials\.

1. In the left pane, choose **Security Groups** under **Network & Security**\.

1. In the main pane, choose the AWS security group for your CA\.

1. Choose the **Inbound** tab, and then choose **Edit**\.

1. In the **Edit inbound rules** dialog box, do the following:
   + Choose **Add Rule**\. 
   + Choose **All traffic** for **Type** and **Custom** for **Source**\. 
   + Enter your directory’s AWS security group \(for example, sg\-123456789\) in the box next to **Source**\. 
   + Choose **Save**\.

1. Now choose the AWS security group of your AWS Managed Microsoft AD directory\. Choose the **Outbound** tab and then choose **Edit**\.

1. In the **Edit outbound rules** dialog box, do the following:
   + Choose **Add Rule**\. 
   + Choose **All traffic** for **Type** and **Custom** for **Destination**\. 
   + Type your CA's AWS security group in the box next to **Destination**\. 
   + Choose **Save**\.

You can test the LDAPS connection to the AWS Managed Microsoft AD directory using the LDP tool\. The LDP tool comes with the Active Directory Administrative Tools\. For more information, see [Installing the Active Directory Administration Tools](ms_ad_install_ad_tools.md)\.

**Note**  
Before you test the LDAPS connection, you must wait up to 30 minutes for the subordinate CA to issue a certificate to your domain controllers\.

For additional details about server\-side LDAPS and to see an example use case on how to set it up, see [How to Enable Server\-Side LDAPS for Your AWS Managed Microsoft AD Directory](https://aws.amazon.com/blogs/security/how-to-enable-ldaps-for-your-aws-microsoft-ad-directory/) on the AWS Security Blog\.