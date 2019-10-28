# Prerequisites<a name="microsoftadbaseprereq"></a>

If you plan to use only the UI steps in this tutorial to create your test lab, you can skip this prerequisites section and move on to Step 1\. However, if you plan to use either AWS CLI commands or AWS Tools for Windows PowerShell modules to create your test lab environment, you must first configure the following:
+ **IAM user with the access and secret access key** – An IAM user with an access key is required if you want to use the AWS CLI or AWS Tools for Windows PowerShell modules\. If you do not have an access key, see [Creating, Modifying, and Viewing Access Keys \(AWS Management Console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey)\.
+ **AWS Command Line Interface \(optional\)** – Download and [Install the AWS CLI on Windows](https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html)\. Once installed, open the command prompt or Windows PowerShell window, and then type **aws configure**\. Note that you need the access key and secret key to complete the setup\. See the first prerequisite for steps on how to do this\. You will be prompted for the following:
  + AWS access key ID \[None\]: `AKIAIOSFODNN7EXAMPLE`
  + AWS secret access key \[None\]: `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`
  + Default region name \[None\]: `us-west-2`
  + Default output format \[None\]: `json`
+ **AWS Tools for Windows PowerShell** **\(optional\)** – Download and install the latest version of the AWS Tools for Windows PowerShell from [https://aws\.amazon\.com/powershell/](https://aws.amazon.com/powershell/), and then run the following command\. Note that you need your access key and secret key to complete the setup\. See the first prerequisite for the steps on how to do this\.

  `Set-AWSCredentials -AccessKey {AKIAIOSFODNN7EXAMPLE} -SecretKey {wJalrXUtnFEMI/K7MDENG/ bPxRfiCYEXAMPLEKEY} -StoreAs {default}`