# Step 4: Verify That the Base Test Lab Is Operational<a name="microsoftadbasestep4"></a>

Use the following procedure to verify that the test lab has been set up successfully before adding on additional test lab guide modules\. This procedure verifies that your Windows Server is configured appropriately, can connect to the corp\.example\.com domain, and be used to administer your AWS Managed Microsoft AD forest\. 

**To verify that the test lab is operational**

1. Sign out of the EC2 instance where you were logged in as the local administrator\. 

1. Back in the Amazon EC2 console, choose **Instances** in the navigation pane\. Then select the instance that you created\. Choose **Connect**\. 

1. In the **Connect To Your Instance** dialog box, choose **Download Remote Desktop File**\. 

1. In the **Windows Security** dialog box, type your administrator credentials for the CORP domain to log in \(for example, **corp\\admin**\)\.

1. Once you are logged in, in the **Start** menu, under **Windows Administrative Tools**, choose **Active Directory Users and Computers**\. 

1. You should see **corp\.example\.com** displayed with all the default OUs and accounts associated with a new domain\. Under **Domain Controllers**, notice the names of the domain controllers that were automatically created when you created your AWS Managed Microsoft AD back in Step 2 of this tutorial\. 

Congratulations\! Your AWS Managed Microsoft AD base test lab environment has now been configured\. You are ready to begin adding the next test lab in the series\.

Next tutorial: [Tutorial: Creating a Trust from AWS Managed Microsoft AD to a Self\-Managed Active Directory Installation on Amazon EC2](ms_ad_tutorial_test_lab_trust.md)