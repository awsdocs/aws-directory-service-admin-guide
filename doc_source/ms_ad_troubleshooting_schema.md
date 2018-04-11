# Schema Extension Errors<a name="ms_ad_troubleshooting_schema"></a>

The following can help you troubleshoot some error messages you might encounter when extending the schema for your AWS Managed Microsoft AD directory\.

## Referral<a name="referral"></a>

**Error**  
*Add error on entry starting on line 1: Referral The server side error is: 0x202b A referral was returned from the server\. The extended server error is: 0000202B: RefErr: DSID\-0310082F, data 0, 1 access points \\tref 1: ‘example\.com’ Number of Objects Modified: 0*

**Troubleshooting**  
Ensure that all of the distinguished name fields have the correct domain name\. In the example above, `DC=example,dc=com` should be replaced with the `DistinguishedName` shown by the cmdlet `Get-ADDomain`\.

## Unable to Read Import File<a name="unabletoread"></a>

**Error**  
*Unable to read the import file\. Number of Objects Modified: 0*

**Troubleshooting**  
The imported LDIF file is empty \(0 bytes\)\. Ensure the correct file was uploaded\.

## Syntax Error<a name="syntaxerror"></a>

**Error**  
*There is a syntax error in the input file Failed on line 21\. The last token starts with 'q'\. Number of Objects Modified: 0*

**Troubleshooting**  
The text on line 21 is not formatted correctly\. The first letter of the invalid text is `A`\. Update line 21 with valid LDIF syntax\. For more information about how to format the LDIF file, see [Step 1: Create Your LDIF File](create.md)\.

## Attribute or Value Exists<a name="attributeorvalue"></a>

**Error**  
*Add error on entry starting on line 1: Attribute Or Value Exists The server side error is: 0x2083 The specified value already exists\. The extended server error is: 00002083: AtrErr: DSID\-03151830, \#1: \\t0: 00002083: DSID\-03151830, problem 1006 \(ATT\_OR\_VALUE\_EXISTS\), data 0, Att 20019 \(mayContain\):len 4 Number of Objects Modified: 0*

**Troubleshooting**  
The schema change has already been applied\.

## No Such Attribute<a name="nosuchattribute"></a>

**Error**  
*Add error on entry starting on line 1: No Such Attribute The server side error is: 0x2085 The attribute value cannot be removed because it is not present on the object\. The extended server error is: 00002085: AtrErr: DSID\-03152367, \#1: \\t0: 00002085: DSID\-03152367, problem 1001 \(NO\_ATTRIBUTE\_OR\_VAL\), data 0, Att 20019 \(mayContain\):len 4 Number of Objects Modified: 0*

**Troubleshooting**  
The LDIF file is trying to remove an attribute from a class, but that attribute is currently not attached to the class\. Schema change was probably already applied\.

**Error**  
*Add error on entry starting on line 41: No Such Attribute 0x57 The parameter is incorrect\. The extended server error is: 0x208d Directory object not found\. The extended server error is: "00000057: LdapErr: DSID\-0C090D8A, comment: Error in attribute conversion operation, data 0, v2580" Number of Objects Modified: 0*

**Troubleshooting**  
The attribute listed on line 41 is incorrect\. Double\-check the spelling\.

## No Such Object<a name="nosuchobject"></a>

**Error**  
*Add error on entry starting on line 1: No Such Object The server side error is: 0x208d Directory object not found\. The extended server error is: 0000208D: NameErr: DSID\-03100238, problem 2001 \(NO\_OBJECT\), data 0, best match of: ’CN=Schema,CN=Configuration,DC=example,DC=com’ Number of Objects Modified: 0*

**Troubleshooting**  
The object referenced by the distinguished name \(DN\) does not exist\.