# Manage Microsoft AD Compliance<a name="ms_ad_compliance"></a>

You can use AWS Microsoft AD to support your Active Directory–aware applications, in the AWS Cloud, that are subject to the following compliance requirements\. However, your applications will not adhere to compliance requirements if you use Simple AD or AD Connector\.

## Supported Compliance Standards<a name="supportedcompliancead"></a>

AWS Microsoft AD has undergone auditing for the following standards and is eligible for use as part of solutions for which you need to obtain compliance certification\. 


****  

|  |  | 
| --- |--- |
| ![\[Image NOT FOUND\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/PCI.png) | AWS Microsoft AD has an Attestation of Compliance for Payment Card Industry \(PCI\) Data Security Standard \(DSS\) version 3\.2 at Service Provider Level 1\. Customers who use AWS products and services to store, process, or transmit cardholder data can use AWS Microsoft AD as they manage their own PCI DSS compliance certification\. For more information about PCI DSS, including how to request a copy of the AWS PCI Compliance Package, see [PCI DSS Level 1](http://aws.amazon.com/compliance/pci-dss-level-1-faqs/)\. Importantly, you must configure fine\-grained password policies in AWS Microsoft AD to be consistent with PCI DSS version 3\.2 standards\. For details on which policies must be enforced, see [Enable PCI Compliance for Your AWS Microsoft AD Directory](#enablepciad)\. | 
| ![\[Image NOT FOUND\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/HIPAA.jpg) | AWS has expanded its Health Insurance Portability and Accountability Act \(HIPAA\) compliance program to include AWS Microsoft AD as a [HIPAA Eligible Service](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/)\. If you have an executed Business Associate Agreement \(BAA\) with AWS, you can use AWS Microsoft AD to help build your HIPAA\-compliant applications\. AWS offers a [HIPAA\-focused Whitepaper](https://d0.awsstatic.com/whitepapers/compliance/AWS_HIPAA_Compliance_Whitepaper.pdf) for customers who are interested in learning more about how they can leverage AWS for the processing and storage of health information\. For more information, see [HIPAA Compliance](https://aws.amazon.com/compliance/hipaa-compliance/)\. | 

## Shared Responsibility<a name="sharedresponsibilityad"></a>

Security, including HIPAA and PCI compliance, is a [shared responsibility](https://aws.amazon.com/compliance/shared-responsibility-model/)\. It is important to understand that AWS Microsoft AD compliance status does not automatically apply to applications that you run in the AWS Cloud\. You need to ensure that your use of AWS services complies with the standards\. 

## Enable PCI Compliance for Your AWS Microsoft AD Directory<a name="enablepciad"></a>

To enable PCI compliance for your AWS Microsoft AD directory, you must configure fine\-grained password policies as specified in the PCI DSS Attestation of Compliance \(AOC\) and Responsibility Summary document provided by AWS Artifact\. 

For more information about using fine\-grained password policies, see [Manage Fine\-Grained Password Policies in Microsoft AD](ms_ad_password_policies.md)\.

## Security Logs<a name="securitylogsad"></a>

Security logs from AWS Microsoft AD domain controller instances are archived for a year\. In the event of an audit to investigate a breach or other security event, you can request a copy of your security logs by contacting [AWS Support](https://aws.amazon.com/premiumsupport/)\. 

AWS logs the following events for compliance\. 


****  

| Monitoring category | Policy setting | Audit state | 
| --- | --- | --- | 
| Account Logon | Audit Credential Validation  | Success, Failure | 
| Account Management | Audit Computer Account Management  | Success, Failure | 
|  | Audit Other Account Management Events | Success, Failure | 
|  | Audit Security Group Management | Success, Failure | 
|  | Audit User Account Management | Success, Failure | 
| Detailed Tracking | Audit Process Creation | Success | 
| DS Access | Audit Directory Service Access | Success, Failure | 
|  | Audit Directory Service Changes | Success, Failure | 
| Logon/Logoff | Audit Account Lockout Success | Success, Failure | 
|  | Audit Logoff | Success | 
|  | Audit Logon | Success, Failure | 
|  | Audit Special Logon | Success | 
| Object Access | Audit Removable Storage | Success, Failure | 
|  | Audit Central Access Policy Staging | Success, Failure | 
| Policy Change | Audit Policy Change | Success, Failure | 
|  | Audit Authentication Policy Change | Success | 
|  | Audit Authorization Policy Change | Success, Failure | 
| Privilege Use | Audit Sensitive Privilege Use | Success, Failure | 
| System | Audit IPsec Driver | Success, Failure | 
|  | Audit Other System Events | Success, Failure | 
|  | Audit Security State Change | Success, Failure | 
|  | Audit Security System Extension | Success, Failure | 
|  | Audit System Integrity | Success, Failure | 