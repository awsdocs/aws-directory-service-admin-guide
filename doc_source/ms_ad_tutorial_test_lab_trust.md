# Tutorial: Creating a Trust from AWS Managed Microsoft AD to a Self\-Managed Active Directory Installation on Amazon EC2<a name="ms_ad_tutorial_test_lab_trust"></a>

In this tutorial, you learn how to create a trust between the AWS Directory Service for Microsoft Active Directory forest that you created in the [Base tutorial](ms_ad_tutorial_test_lab_base.md)\. You also learn to create a new native Active Directory forest on a Windows Server in Amazon EC2\. As shown in the following illustration, the lab that you create from this tutorial is the second building block necessary when setting up a complete AWS Managed Microsoft AD test lab\. You can use the test lab to test your pure cloud or hybrid cloud–based AWS solutions\. 

You should only need to create this tutorial once\. After that you can add optional tutorials when necessary for more experience\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/tutorialmicrosoftadtrust.png)

**[Step 1: Set Up Your Environment for Trusts](microsoftadtruststep1.md)**  
Before you can establish trusts between a new Active Directory forest and the AWS Managed Microsoft AD forest that you created in the [Base tutorial](ms_ad_tutorial_test_lab_base.md), you need to prepare your Amazon EC2 environment\. To do that, you first create a Windows Server 2019 server, promote that server to a domain controller, and then configure your VPC accordingly\.

**[Step 2: Create the Trusts](microsoftadtruststep2.md)**  
In this step, you create a two\-way forest trust relationship between your newly created Active Directory forest hosted in Amazon EC2 and your AWS Managed Microsoft AD forest in AWS\. 

**[Step 3: Verify the Trust](microsoftadtruststep3.md)**  
Finally, as an administrator, you use the AWS Directory Service console to verify that the new trusts are operational\.