# Manage Compliance for AWS Managed Microsoft AD<a name="ms_ad_compliance"></a>

You can use AWS Managed Microsoft AD to support your Active Directory–aware applications, in the AWS Cloud, that are subject to the following compliance requirements\. However, your applications will not adhere to compliance requirements if you use Simple AD or AD Connector\.

## Supported Compliance Standards<a name="supportedcompliancead"></a>

AWS Managed Microsoft AD has undergone auditing for the following standards and is eligible for use as part of solutions for which you need to obtain compliance certification\. 


****  

|  |  | 
| --- |--- |
| ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/FedRAMP.png) | AWS Managed Microsoft AD meets Federal Risk and Authorization Management Program \(FedRAMP\) security requirements and has received a FedRAMP Joint Authorization Board \(JAB\) Provisional Authority to Operate \(P\-ATO\) at the FedRAMP Moderate Baseline\. For more information about FedRAMP, see [FedRAMP Compliance](https://aws.amazon.com/compliance/fedramp/)\. | 
| ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/PCI.png) | AWS Managed Microsoft AD has an Attestation of Compliance for Payment Card Industry \(PCI\) Data Security Standard \(DSS\) version 3\.2 at Service Provider Level 1\. Customers who use AWS products and services to store, process, or transmit cardholder data can use AWS Managed Microsoft AD as they manage their own PCI DSS compliance certification\. For more information about PCI DSS, including how to request a copy of the AWS PCI Compliance Package, see [PCI DSS Level 1](http://aws.amazon.com/compliance/pci-dss-level-1-faqs/)\. Importantly, you must configure fine\-grained password policies in AWS Managed Microsoft AD to be consistent with PCI DSS version 3\.2 standards\. For details on which policies must be enforced, see the section below titled Enable PCI Compliance for Your AWS Managed Microsoft AD Directory\. | 
| ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/HIPAA.jpg) | AWS has expanded its Health Insurance Portability and Accountability Act \(HIPAA\) compliance program to include AWS Managed Microsoft AD as a [HIPAA Eligible Service](https://aws.amazon.com/compliance/hipaa-eligible-services-reference/)\. If you have an executed Business Associate Agreement \(BAA\) with AWS, you can use AWS Managed Microsoft AD to help build your HIPAA\-compliant applications\. AWS offers a [HIPAA\-focused Whitepaper](https://d0.awsstatic.com/whitepapers/compliance/AWS_HIPAA_Compliance_Whitepaper.pdf) for customers who are interested in learning more about how they can leverage AWS for the processing and storage of health information\. For more information, see [HIPAA Compliance](https://aws.amazon.com/compliance/hipaa-compliance/)\. | 

## Shared Responsibility<a name="sharedresponsibilityad"></a>

Security, including FedRAMP, HIPAA and PCI compliance, is a [shared responsibility](https://aws.amazon.com/compliance/shared-responsibility-model/)\. It is important to understand that AWS Managed Microsoft AD compliance status does not automatically apply to applications that you run in the AWS Cloud\. You need to ensure that your use of AWS services complies with the standards\.

For a complete list of all the various AWS compliance programs that AWS Managed Microsoft AD supports, see [AWS Services in Scope by Compliance Program](https://aws.amazon.com/compliance/services-in-scope/)\.

## Enable PCI Compliance for Your AWS Managed Microsoft AD Directory<a name="enablepciad"></a>

To enable PCI compliance for your AWS Managed Microsoft AD directory, you must configure fine\-grained password policies as specified in the PCI DSS Attestation of Compliance \(AOC\) and Responsibility Summary document provided by AWS Artifact\. 

For more information about using fine\-grained password policies, see [Manage Password Policies for AWS Managed Microsoft AD](ms_ad_password_policies.md)\.