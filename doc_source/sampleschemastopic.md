# Sample Schemas<a name="sampleschemastopic"></a>

Cloud Directory comes ready with sample schemas for Organizations, Persons, and Devices\. The following section lists the various sample schemas and lists the differences for each\.

## Organizations<a name="organizationsschema"></a>

The following tables list the facets that are included in the *Organizations* sample schema\.


****  

| **"Organization" Facet ** | **Data Type ** | **Length ** | **Required Behavior? ** | **Description ** | 
| --- | --- | --- | --- | --- | 
| account\_id  | String  | 1024  | N  | Unique id for Organization  | 
| account\_name  | String  | 1024  | N  | Name of Organization  | 
| organization\_status  | String  | 1024  | N  | Status such as 'active', 'suspended', 'inactive', 'closed'  | 
| mailing\_address \(street1\)  | String  | 1024  | N  | A physical mailing address for this company/entity  | 
| mailing\_address \(street2\)  | String  | 1024  | N  | A physical mailing address for this company/entity  | 
| mailing\_address \(city\)  | String  | 1024  | N  | A physical mailing address for this company/entity  | 
| mailing\_address \(state\)  | String  | 1024  | N  | A physical mailing address for this company/entity  | 
| mailing\_address \(country\)  | String  | 1024  | N  | A physical mailing address for this company/entity  | 
| mailing\_address \(postal\_code\)  | String  | 1024 | N  | A physical mailing address for this company/entity  | 
| email  | String  | 1024  | N  | Email id for Organization  | 
| web\_site  | String  | 1024  | N  | Website URL  | 
| telephone\_number  | String  | 1024  | N  | Telephone number for Organization  | 
| description  | String  | 1024  | N  | Description for Organization  | 


****  

| **"Legal\_Entity" Facet ** | **Data Type** | **Length**  | **Required Behavior?**  | **Description** | 
| --- | --- | --- | --- | --- | 
| registered\_company\_name  | String  | 1024  | N  | Legal entity name  | 
| mailing\_address \(street1\)  | String  | 1024  | N  | A physical registered address for this company/entity  | 
| mailing\_address \(street2\)  | String  | 1024  | N  | A physical registered address for this company/entity  | 
| mailing\_address \(city\)  | String  | 1024  | N  | A physical registered address for this company/entity  | 
| mailing\_address \(state\)  | String  | 1024  | N  | A physical registered address for this company/entity  | 
| mailing\_address \(country\)  | String  | 1024  | N  | A physical registered address for this company/entity  | 
| mailing\_address \(postal\_code\)  | String  | 1024  | N  | A physical registered address for this company/entity  | 
| industry\_vertical  | String  | 1024  | N  | Industry Segment  | 
| billing\_currency  | String  | 1024  | N  | Billing currency  | 
| tax\_id  | String  | 1024  | N  | Tax identification number  | 

## Person<a name="personschema"></a>

The following tables list the facets that are included in the *Person* sample schema\.


****  

| **"Person" Facet** | **Data Type** | **Length** | **Required Behavior?** | **Description** | 
| --- | --- | --- | --- | --- | 
| display\_name | String | 1024 | N | The name of the user, suitable for display to end\-users\. | 
| first\_name | String | 1024 | N | The given name of the User, or first name in most western languages | 
| last\_name | String | 1024 | N | The family name of the User, or last name in most western languages | 
| middle\_name | String | 1024 | N | The middle name\(s\) of the User | 
| nickname | String | 1024 | N | The casual way to address the user in real life, such as, "Bob" or "Bobby" instead of "Robert" | 
| email | String | 1024 | N | Email address for the user | 
| mobile\_phone\_number | String | 1024 | N | Phone number for the user | 
| home\_phone\_number | String | 1024 | N | Phone number for the user | 
| username | String | 1024 | Y | unique identifier for the user | 
| profile | String | 1024 | N | A URI that is a uniform resource locator and that points to a location representing the user's online profile \(such as a webpage\) | 
| picture | String | 1024 | N | A URI that is a uniform resource locator that points to a resource location representing the user's image\. | 
| website | String | 1024 | N | URL | 
| timezone | String | 1024 | N | The User's time zone | 
| locale | String | 1024 | N | Used to indicate the User's default location for purposes of localizing such items as currency, date time format, or numerical representations\. | 
| address \(street1\) | String | 1024 | N | A physical mailing address for this user\. | 
| address \(street2\) | String | 1024 | N | A physical mailing address for this user\. | 
| address \(city\) | String | 1024 | N | A physical mailing address for this user\. | 
| address \(state\) | String | 1024 | N | A physical mailing address for this user\. | 
| address \(country\) | String | 1024 | N | A physical mailing address for this user\. | 
| address \(postal\_code\) | String | 1024 | N | A physical mailing address for this user\. | 
| user\_status | String | 1024 | N | Value indicating the user's administrative status | 


****  

| **"Organization\_Person" Facet** | **Data Type** | **Length** | **Required Behavior?** | **Description** | 
| --- | --- | --- | --- | --- | 
| title | String | 1024 | N | Title in organization | 
| preferred\_language | String | 1024 | N | Indicates the user's preferred written or spoken languages and is generally used for selecting a localized user interface\. | 
| employee\_id | String | 1024 | N | A string identifier, typically numeric or alphanumeric, assigned to a person | 
| cost\_center | Integer | 1024 | N | Identifies the cost center | 
| department | String | 1024 | N | Identifies the name of a department | 
| manager  | String | 1024 | N | The user's manager | 
| company\_name | String | 1024 | N | Identifies the name of an organization | 
| company\_address \(street1\) | String | 1024 | N | A physical mailing address for the organization | 
| company\_address \(street2\) | String | 1024 | N | A physical mailing address for the organization | 
| company\_address \(city\) | String | 1024 | N | A physical mailing address for the organization | 
| company\_address \(state\) | String | 1024 | N | A physical mailing address for the organization | 
| company\_address \(country\) | String | 1024 | N | A physical mailing address for the organization | 
| company\_address \(postalCode\) | String | 1024 | N | A physical mailing address for the organization | 

## Device<a name="deviceschema"></a>

The following table lists the facet that is included in the *Device* sample schema\.


****  

| **"Device" Facet** | **Data Type** | **Length** | **Required Behavior?** | **Description** | 
| --- | --- | --- | --- | --- | 
| device\_id | String | 1024 | N | Alpha\-numeric unique device id | 
| name | String | 1024 | N | Friendly name for device | 
| description  | String | 1024 | N | Description for device  | 
| X\.509\_certificates | String | 1024 | N | X\.509 Certificate | 
| device\_version | String | 1024 | N | Device version  | 
| device\_os\_type | String | 1024 | N | Operating System on device | 
| device\_os\_version | String | 1024 | N | Operating System version number on device | 
| serial\_number | String | 1024 | N | Serial number of device | 
| device\_status | String | 1024 | N | Status for device \(such as active, not\_active, suspended, shutdown, off\) | 