# Tutorial: Setting Up Your Base AWS Managed Microsoft AD Test Lab in AWS<a name="ms_ad_tutorial_test_lab_base"></a>

This tutorial teaches you how to set up your AWS environment to prepare for a new AWS Managed Microsoft AD installation that uses a new EC2 instance running Windows Server 2019\. It then teaches you to use typical Active Directory administration tools to manage your AWS Managed Microsoft AD environment from your Windows system\. By the time you complete the tutorial, you will have set up the network prerequisites and have configured a new AWS Managed Microsoft AD forest\. 

As shown in the following illustration, the lab you create from this tutorial is the foundational component for hands\-on learning about AWS Managed Microsoft AD\. You can later add optional tutorials for more hands\-on experience\. This tutorial series is ideal for anyone who is new to AWS Managed Microsoft AD and wants a test lab for evaluation purposes\. This tutorial takes approximately 1 hour to complete\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/tutorialmicrosoftadbase.png)

**[Step 1: Set Up Your AWS Environment for AWS Managed Microsoft AD](microsoftadbasestep1.md)**  
After you've completed your prerequisite tasks, you create and configure a VPC in your EC2 instance\.

**[Step 2: Create Your AWS Managed Microsoft AD Directory in AWS](microsoftadbasestep2.md)**  
In this step, you set up AWS Managed Microsoft AD in AWS for the first time\.

**[Step 3: Deploy an EC2 Instance to Manage AWS Managed Microsoft AD](microsoftadbasestep3.md)**  
Here, you walk through the various post\-deployment tasks necessary for client computers to connect to your new domain and set up a new Windows Server system in EC2\.

**[Step 4: Verify That the Base Test Lab Is Operational](microsoftadbasestep4.md)**  
Finally, as an administrator, you verify that you can log in and connect to AWS Managed Microsoft AD from your Windows Server system in EC2\. Once you've successfully tested that the lab is operational, you can continue to add other test lab guide modules\.