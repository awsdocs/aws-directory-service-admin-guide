# Tutorial: Setting Up Your Base Microsoft AD Test Lab in AWS<a name="tutorial_ad_base_test_lab"></a>

This tutorial teaches you how to set up your AWS environment to prepare for a new Microsoft AD installation that uses a new EC2 instance running Windows Server 2016\. It then teaches you to use typical Active Directory administration tools to manage your Microsoft AD environment from your Windows system\. By the time you complete the tutorial, you will have set up the network prerequisites and have configured a new Microsoft AD forest\. 

As shown in the following illustration, the lab you create from this tutorial is the foundational component for hands\-on learning about Microsoft AD\. You can later add optional tutorials for more hands\-on experience\. This tutorial series is ideal for anyone who is new to Microsoft AD and wants a test lab for evaluation purposes\. This tutorial takes approximately 1 hour to complete\.

![\[Image NOT FOUND\]](http://alpha-docs-aws.amazon.com/directoryservice/latest/admin-guide/images/tutorialmicrosoftadbase.png)

**[Step 1: Set Up Your AWS Environment for Microsoft AD](microsoftadbasestep1.md)**  
After you've completed your prerequisite tasks, you create and configure a VPC in your EC2 instance\.

**[Step 2: Create Your Microsoft AD Directory in AWS](microsoftadbasestep2.md)**  
In this step, you set up Microsoft AD in AWS for the first time\.

**[Step 3: Deploy an EC2 Instance to Manage Microsoft AD](microsoftadbasestep3.md)**  
Here, you walk through the various post\-deployment tasks necessary for client computers to connect to your new domain and set up a new Windows Server system in EC2\.

**[Step 4: Verify That the Base Test Lab Is Operational](microsoftadbasestep4.md)**  
Finally, as an administrator, you verify that you can log in and connect to Microsoft AD from your Windows Server system in EC2\. Once you've successfully tested that the lab is operational, you can continue to add other test lab guide modules\.