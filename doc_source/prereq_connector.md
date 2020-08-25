# AD Connector Prerequisites<a name="prereq_connector"></a>

To connect to your existing directory with AD Connector, you need the following:

**VPC**  
Set up a VPC with the following:  
+ At least two subnets\. Each of the subnets must be in a different Availability Zone\.
+ The VPC must be connected to your existing network through a virtual private network \(VPN\) connection or AWS Direct Connect\.
+ The VPC must have default hardware tenancy\.
AWS Directory Service uses a two VPC structure\. The EC2 instances which make up your directory run outside of your AWS account, and are managed by AWS\. They have two network adapters, `ETH0` and `ETH1`\. `ETH0` is the management adapter, and exists outside of your account\. `ETH1` is created within your account\.   
The management IP range of your directory's `ETH0` network is chosen programmatically to ensure it does not conflict with the VPC where your directory is deployed\. This IP range can be in either of the following pairs \(as Directories run in two subnets\):  
+ 10\.0\.1\.0/24 & 10\.0\.2\.0/24 
+ 192\.168\.1\.0/24 & 192\.168\.2\.0/24 
We avoid conflicts by checking the first octet of the `ETH1` CIDR\. If it starts with a 10, then we choose a 192\.168\.0\.0/16 VPC with 192\.168\.1\.0/24 and 192\.168\.2\.0/24 subnets\. If the first octet is anything else other than a 10 we choose a 10\.0\.0\.0/16 VPC with 10\.0\.1\.0/24 and 10\.0\.2\.0/24 subnets\.   
The selection algorithm does not include routes on your VPC\. It is therefore possible to have an IP routing conflict result from this scenario\.   
For more information, see the following topics in the *Amazon VPC User Guide*:  
+ [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Introduction.html)
+ [Subnets in your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#VPCSubnet)
+ [Adding a Hardware Virtual Private Gateway to Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_VPN.html)
For more information about AWS Direct Connect, see the [AWS Direct Connect User Guide](https://docs.aws.amazon.com/directconnect/latest/UserGuide/)\.

**Existing Active Directory**  
You'll need to connect to an existing network with an Active Directory domain\.  
AD Connector does not support trust with [Single Label Domains](https://support.microsoft.com/en-us/help/2269810/microsoft-support-for-single-label-domains)\.
The functional level of this domain must be `Windows Server 2003` or higher\. AD Connector also supports connecting to a domain hosted on an Amazon EC2 instance\.  
AD Connector does not support Read\-only domain controllers \(RODC\) when used in combination with the Amazon EC2 domain\-join feature\. 

**Service account**  
You must have credentials for a service account in the existing directory which has been delegated the following privileges:  
+ Read users and groups \- Required
+ Join computers to the domain \- Required only when using Seamless Domain Join and Amazon WorkSpaces
+ Create computer objects \- Required only when using Seamless Domain Join and Amazon WorkSpaces
For more information, see [Delegate privileges to your service account](#connect_delegate_privileges)\. 

**User permissions**  
All Active Directory users must have permissions to read their own attributes\. Specifically the following attributes:  
+ GivenName
+ SurName
+ Mail
+ SamAccountName
+ UserPrincipalName
+ UserAccountControl
+ MemberOf
By default, Active Directory users do have read permission to these attributes\. However, Administrators can alter these permissions over time so you might want to verify your users have these read permissions prior to setting up AD Connector for the first time\.

**IP addresses**  
Get the IP addresses of two DNS servers or domain controllers in your existing directory\.  
AD Connector obtains the `_ldap._tcp.<DnsDomainName>` and `_kerberos._tcp.<DnsDomainName>` SRV records from these servers when connecting to your directory, so these servers must contain these SRV records\. The AD Connector attempts to find a common domain controller that will provide both LDAP and Kerberos services, so these SRV records must include at least one common domain controller\. For more information about SRV records, go to [SRV Resource Records](http://technet.microsoft.com/en-us/library/cc961719.aspx) on Microsoft TechNet\.

**Ports for subnets**  
For AD Connector to redirect directory requests to your existing Active Directory domain controllers, the firewall for your existing network must have the following ports open to the CIDRs for both subnets in your Amazon VPC\.  
+ TCP/UDP 53 \- DNS
+ TCP/UDP 88 \- Kerberos authentication
+ TCP/UDP 389 \- LDAP
These are the minimum ports that are needed before AD Connector can connect to your directory\. Your specific configuration may require additional ports be open\.  
If the DNS servers or Domain Controller servers for your existing Active Directory Domain are within the VPC, the security groups associated with those servers must have the above ports open to the CIDRs for both subnets in the VPC\. 
For additional port requirements, see [AD and AD DS Port Requirements](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772723(v=ws.10)) on Microsoft TechNet\.

**Kerberos preauthentication**  
Your user accounts must have Kerberos preauthentication enabled\. For detailed instructions on how to enable this setting, see [Ensure That Kerberos Pre\-authentication Is Enabled](ms_ad_tutorial_setup_trust_prepare_onprem.md#tutorial_setup_trust_enable_kerberos)\. For general information about this setting, go to [Preauthentication](http://technet.microsoft.com/en-us/library/cc961961.aspx) on Microsoft TechNet\.

**Encryption types**  
AD Connector supports the following encryption types when authenticating via Kerberos to your Active Directory domain controllers:  
+ AES\-256\-HMAC
+ AES\-128\-HMAC
+ RC4\-HMAC

## AWS Single Sign\-On Prerequisites<a name="prereq_aws_sso_ad_connector"></a>

If you plan to use AWS Single Sign\-On \(AWS SSO\) with AD Connector, you need to ensure that the following are true:
+ Your AD Connector is set up in your AWS organization’s master account\.
+ Your instance of AWS SSO is in the same Region where your AD Connector is set up\. 

For more information, see [AWS SSO Prerequisites](https://docs.aws.amazon.com/singlesignon/latest/userguide/prereqs.html) in the AWS Single Sign\-On User Guide\.

## Multi\-Factor Authentication Prerequisites<a name="mfa_prereqs"></a>

To support multi\-factor authentication with your AD Connector directory, you need the following:
+ A [Remote Authentication Dial\-In User Service](https://en.wikipedia.org/wiki/RADIUS) \(RADIUS\) server in your existing network that has two client endpoints\. The RADIUS client endpoints have the following requirements:
  + To create the endpoints, you need the IP addresses of the AWS Directory Service servers\. These IP addresses can be obtained from the **Directory IP Address** field of your directory details\. 
  + Both RADIUS endpoints must use the same shared secret code\.
+ Your existing network must allow inbound traffic over the default RADIUS server port \(1812\) from the AWS Directory Service servers\.
+ The usernames between your RADIUS server and your existing directory must be identical\.

For more information about using AD Connector with MFA, see [Enable Multi\-Factor Authentication for AD Connector](ad_connector_mfa.md)\. 

## Delegate privileges to your service account<a name="connect_delegate_privileges"></a>

To connect to your existing directory, you must have the credentials for your AD Connector service account in the existing directory that has been delegated certain privileges\. While members of the **Domain Admins** group have sufficient privileges to connect to the directory, as a best practice, you should use a service account that only has the minimum privileges necessary to connect to the directory\. The following procedure demonstrates how to create a new group called `Connectors`, delegate the necessary privileges that are needed to connect AWS Directory Service to this group, and then add a new service account to this group\. 

This procedure must be performed on a machine that is joined to your directory and has the **Active Directory User and Computers** MMC snap\-in installed\. You must also be logged in as a domain administrator\.

**To delegate privileges to your service account**

1. Open **Active Directory User and Computers** and select your domain root in the navigation tree\.

1. In the list in the left\-hand pane, right\-click **Users**, select **New**, and then select **Group**\. 

1. In the **New Object \- Group** dialog box, enter the following and click **OK**\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/prereq_connector.html)

1. In the **Active Directory User and Computers** navigation tree, select your domain root\. In the menu, select **Action**, and then **Delegate Control**\. If your AD Connector is connected to AWS Managed Microsoft AD, you will not have access to delegate control at the domain root level\. In this case, to delegate control, select the OU under your directory OU where your computer objects will be created\.

1. On the **Delegation of Control Wizard** page, click **Next**, then click **Add**\.

1. In the **Select Users, Computers, or Groups** dialog box, enter `Connectors` and click **OK**\. If more than one object is found, select the `Connectors` group created above\. Click **Next**\.

1. On the **Tasks to Delegate** page, select **Create a custom task to delegate**, and then choose **Next**\.

1. Select **Only the following objects in the folder**, and then select **Computer objects** and **User objects**\.

1. Select **Create selected objects in this folder** and **Delete selected objects in this folder**\. Then choose **Next**\.  
![\[Object type\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/aduc_delegate_join_linux.png)

1. Select **Read**, and then choose **Next**\.
**Note**  
If you will be using Seamless Domain Join or Amazon WorkSpaces, you must also enable **Write** permissions so that AWS Managed Microsoft AD can create computer objects\.  
![\[Object type\]](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/images/aduc_delegate_join_permissions.png)

1. Verify the information on the **Completing the Delegation of Control Wizard** page, and click **Finish**\. 

1. Create a user account with a strong password and add that user to the `Connectors` group\. This user will be known as your AD Connector service account and since it is now a member of the `Connectors` group it now has sufficient privileges to connect AWS Directory Service to the directory\.

## Test your AD Connector<a name="connect_verification"></a>

For AD Connector to connect to your existing directory, the firewall for your existing network must have certain ports open to the CIDRs for both subnets in the VPC\. To test if these conditions are met, perform the following steps:

**To test the connection**

1. Launch a Windows instance in the VPC and connect to it over RDP\. The instance must be a member of your existing domain\. The remaining steps are performed on this VPC instance\.

1. Download and unzip the [DirectoryServicePortTest](samples/DirectoryServicePortTest.zip) test application\. The source code and Visual Studio project files are included so you can modify the test application if desired\.
**Note**  
This script is not supported on Windows Server 2003 or older operating systems\.

1. From a Windows command prompt, run the DirectoryServicePortTest test application with the following options:
**Note**  
The DirectoryServicePortTest test application can only be used when the domain and forest functional levels are set to Windows Server 2012 R2 and below\.

   ```
   DirectoryServicePortTest.exe -d <domain_name> -ip <server_IP_address> -tcp "53,88,389" -udp "53,88,389"
   ```  
*<domain\_name>*  
The fully qualified domain name\. This is used to test the forest and domain functional levels\. If you exclude the domain name, the functional levels won't be tested\.  
*<server\_IP\_address>*  
The IP address of a domain controller in your existing domain\. The ports will be tested against this IP address\. If you exclude the IP address, the ports won't be tested\.

   This test app determines if the necessary ports are open from the VPC to your domain, and also verifies the minimum forest and domain functional levels\.

   The output will be similar to the following:

   ```
   Testing forest functional level.
   Forest Functional Level = Windows2008R2Forest : PASSED
   
   Testing domain functional level.
   Domain Functional Level = Windows2008R2Domain : PASSED
   
   Testing required TCP ports to <server_IP_address>:
   Checking TCP port 53: PASSED
   Checking TCP port 88: PASSED
   Checking TCP port 389: PASSED
   
   Testing required UDP ports to <server_IP_address>:
   Checking UDP port 53: PASSED
   Checking UDP port 88: PASSED
   Checking UDP port 389: PASSED
   ```

The following is the source code for the DirectoryServicePortTest application\.

```
/*
   Copyright 2010-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.

   This file is licensed under the Apache License, Version 2.0 (the "License").
   You may not use this file except in compliance with the License. A copy of
   the License is located at

    http://aws.amazon.com/apache2.0/

   This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
   CONDITIONS OF ANY KIND, either express or implied. See the License for the
   specific language governing permissions and limitations under the License.
*/
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Text;
using System.Threading.Tasks;
using System.DirectoryServices.ActiveDirectory;
using System.Threading;
using System.DirectoryServices.AccountManagement;
using System.DirectoryServices;
using System.Security.Authentication;
using System.Security.AccessControl;
using System.Security.Principal;

namespace DirectoryServicePortTest
{
    class Program
    {
        private static List<int> _tcpPorts;
        private static List<int> _udpPorts;

        private static string _domain = "";
        private static IPAddress _ipAddr = null;

        static void Main(string[] args)
        {
            if (ParseArgs(args))
            {
                try
                {
                    if (_domain.Length > 0)
                    {
                        try
                        {
                            TestForestFunctionalLevel();

                            TestDomainFunctionalLevel();
                        }
                        catch (ActiveDirectoryObjectNotFoundException)
                        {
                            Console.WriteLine("The domain {0} could not be found.\n", _domain);
                        }
                    }

                    if (null != _ipAddr)
                    {
                        if (_tcpPorts.Count > 0)
                        {
                            TestTcpPorts(_tcpPorts);
                        }

                        if (_udpPorts.Count > 0)
                        {
                            TestUdpPorts(_udpPorts);
                        }
                    }
                }
                catch (AuthenticationException ex)
                {
                    Console.WriteLine(ex.Message);
                }
            }
            else
            {
                PrintUsage();
            }

            Console.Write("Press <enter> to continue.");
            Console.ReadLine();
        }

        static void PrintUsage()
        {
            string currentApp = Path.GetFileName(System.Reflection.Assembly.GetExecutingAssembly().Location);
            Console.WriteLine("Usage: {0} \n-d <domain> \n-ip \"<server IP address>\" \n[-tcp \"<tcp_port1>,<tcp_port2>,etc\"] \n[-udp \"<udp_port1>,<udp_port2>,etc\"]", currentApp);
        }

        static bool ParseArgs(string[] args)
        {
            bool fReturn = false;
            string ipAddress = "";

            try
            {
                _tcpPorts = new List<int>();
                _udpPorts = new List<int>();

                for (int i = 0; i < args.Length; i++)
                {
                    string arg = args[i];

                    if ("-tcp" == arg | "/tcp" == arg)
                    {
                        i++;
                        string portList = args[i];
                        _tcpPorts = ParsePortList(portList);
                    }

                    if ("-udp" == arg | "/udp" == arg)
                    {
                        i++;
                        string portList = args[i];
                        _udpPorts = ParsePortList(portList);
                    }

                    if ("-d" == arg | "/d" == arg)
                    {
                        i++;
                        _domain = args[i];
                    }

                    if ("-ip" == arg | "/ip" == arg)
                    {
                        i++;
                        ipAddress = args[i];
                    }
                }
            }
            catch (ArgumentOutOfRangeException)
            {
                return false;
            }

            if (_domain.Length > 0 || ipAddress.Length > 0)
            {
                fReturn = true;
            }

            if (ipAddress.Length > 0)
            { 
                _ipAddr = IPAddress.Parse(ipAddress); 
            }
            
            return fReturn;
        }

        static List<int> ParsePortList(string portList)
        {
            List<int> ports = new List<int>();

            char[] separators = {',', ';', ':'};

            string[] portStrings = portList.Split(separators);
            foreach (string portString in portStrings)
            {
                try
                {
                    ports.Add(Convert.ToInt32(portString));
                }
                catch (FormatException)
                {
                }
            }

            return ports;
        }

        static void TestForestFunctionalLevel()
        {
            Console.WriteLine("Testing forest functional level.");

            DirectoryContext dirContext = new DirectoryContext(DirectoryContextType.Forest, _domain, null, null);
            Forest forestContext = Forest.GetForest(dirContext);

            Console.Write("Forest Functional Level = {0} : ", forestContext.ForestMode);

            if (forestContext.ForestMode >= ForestMode.Windows2003Forest)
            {
                Console.WriteLine("PASSED");
            }
            else
            {
                Console.WriteLine("FAILED");
            }

            Console.WriteLine();
        }

        static void TestDomainFunctionalLevel()
        {
            Console.WriteLine("Testing domain functional level.");

            DirectoryContext dirContext = new DirectoryContext(DirectoryContextType.Domain, _domain, null, null);
            Domain domainObject = Domain.GetDomain(dirContext);

            Console.Write("Domain Functional Level = {0} : ", domainObject.DomainMode);

            if (domainObject.DomainMode >= DomainMode.Windows2003Domain)
            {
                Console.WriteLine("PASSED");
            }
            else
            {
                Console.WriteLine("FAILED");
            }

            Console.WriteLine();
        }

        static List<int> TestTcpPorts(List<int> portList)
        {
            Console.WriteLine("Testing TCP ports to {0}:", _ipAddr.ToString());

            List<int> failedPorts = new List<int>();

            foreach (int port in portList)
            {
                Console.Write("Checking TCP port {0}: ", port);

                TcpClient tcpClient = new TcpClient();

                try
                {
                    tcpClient.Connect(_ipAddr, port);

                    tcpClient.Close();
                    Console.WriteLine("PASSED");
                }
                catch (SocketException)
                {
                    failedPorts.Add(port);
                    Console.WriteLine("FAILED");
                }
            }

            Console.WriteLine();

            return failedPorts;
        }

        static List<int> TestUdpPorts(List<int> portList)
        {
            Console.WriteLine("Testing UDP ports to {0}:", _ipAddr.ToString());

            List<int> failedPorts = new List<int>();

            foreach (int port in portList)
            {
                Console.Write("Checking UDP port {0}: ", port);

                UdpClient udpClient = new UdpClient();

                try
                {
                    udpClient.Connect(_ipAddr, port);
                    udpClient.Close();
                    Console.WriteLine("PASSED");
                }
                catch (SocketException)
                {
                    failedPorts.Add(port);
                    Console.WriteLine("FAILED");
                }
            }

            Console.WriteLine();

            return failedPorts;
        }
    }
}
```