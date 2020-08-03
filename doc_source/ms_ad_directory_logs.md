# Review Your AWS Managed Microsoft AD Directory Logs<a name="ms_ad_directory_logs"></a>

Security logs from AWS Managed Microsoft AD domain controller instances are archived for a year\. You can also configure your AWS Managed Microsoft AD directory to forward domain controller logs to Amazon CloudWatch Logs in near real time\. For more information, see [Enable Log Forwarding](ms_ad_enable_log_forwarding.md)\.

AWS logs the following events for compliance\. 


****  

| Monitoring category | Policy setting | Audit state | 
| --- | --- | --- | 
| Account Logon | Audit Credential Validation  | Success, Failure | 
|  | Audit Other Account Logon Events | Success, Failure | 
| Account Management | Audit Computer Account Management  | Success, Failure | 
|  | Audit Other Account Management Events | Success, Failure | 
|  | Audit Security Group Management | Success, Failure | 
|  | Audit User Account Management | Success, Failure | 
| Detailed Tracking | Audit DPAPI Activity | Success, Failure | 
|  | Audit PNP Activity | Success | 
|  | Audit Process Creation | Success, Failure | 
| DS Access | Audit Directory Service Access | Success, Failure | 
|  | Audit Directory Service Changes | Success, Failure | 
| Logon/Logoff | Audit Account Lockout | Success, Failure | 
|  | Audit Logoff | Success | 
|  | Audit Logon | Success, Failure | 
|  | Audit Other Logon/Logoff Events | Success, Failure | 
|  | Audit Special Logon | Success, Failure | 
| Object Access | Audit Other Object Access Events | Success, Failure | 
|  | Audit Removable Storage | Success, Failure | 
|  | Audit Central Access Policy Staging | Success, Failure | 
| Policy Change | Audit Policy Change | Success, Failure | 
|  | Audit Authentication Policy Change | Success, Failure | 
|  | Audit Authorization Policy Change | Success, Failure | 
|  | Audit MPSSVC Rule\-Level Policy Change | Success | 
|  | Audit Other Policy Change Events | Failure | 
| Privilege Use | Audit Sensitive Privilege Use | Success, Failure | 
| System | Audit IPsec Driver | Success, Failure | 
|  | Audit Other System Events | Success, Failure | 
|  | Audit Security State Change | Success, Failure | 
|  | Audit Security System Extension | Success, Failure | 
|  | Audit System Integrity | Success, Failure | 