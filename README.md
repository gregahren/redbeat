FORMAT: 1A
HOST: https://twebapp.pro4erp.com/pb

# Pro.4 ERP API
This is Pro.4 ERP api documentation.
First of all replace URL **https://twebapp.pro4erp.com** with your server URL.
Secondly get token from server with your username and password and use this JWT token with your next requests in request Headers: 
**Authenticate: Bearer MY_JWT_TOKEN**

Please substring (**.substring(6)**) all json responses from server before converting string to JSON objects.
We add those characters (**")]}`,\n"**) to response for JSON Hijacking Protection (https://docs.angularjs.org/api/ng/service/$http#json-vulnerability-protection)

NOTE: This document is a **work in progress**.

## Authentication [/s/api/auth/login]

### Get user companies [POST /s/api/auth/usercompanies]
Return companies that user belongs to.
If you want to login into the app with another user company use company "Id" as optional parameter **idcompany**. 

+ Attributes
    + username: myusername (string, required) - Pro4 user Username
    + password: mypassword (string, required) - Pro4 user password

+ Request (application/json)
        
        {
          "username": "myusername",
          "password": "mypassword"
        }

+ Response 200 (application/json)

        [
            {
              "Id": "186b431d-4a13-4829-94d3-93657b8f0bf3",
              "dbcompany_name": "Pro-Bit Pro.4, storitve d.o.o."
            }
        ]

### Authenticate [POST]
Returns a specific Token for Authentication.

If you want to login into the app with another user company use optional parameter **idcompany**.

+ Attributes
    + username: myusername (string, required) - Pro4 user Username
    + password: mypassword (string, required) - Pro4 user password
    + idcompany: user_company_id (string, optional) - If this key is not sent, user is logged in with default company

+ Request (application/json)
        
        {
          "username": "myusername",
          "password": "mypassword",
          "idcompany": "my_company_id"
        }
    
    
+ Response 200 (application/json)

        {
          "token": "eyJ0eXAiO76743b4jbsbfdsfsfsf.eyJjdXJyZW50X2NvbXBhbnlfaWQiOiI2YzAyNGRlOS0xZjY5LTQ3ZDQtYTcxMS0zNDFjNWUwMTk0ZjciLCJpZF91c2VyIjoiYTE0MTkyNTctOTEyNC00Nzk5LTgwOWYtZGExOWE2ODFlZGMzIiwiY3VsdHVyZV9uYW1lIjoic2xfU0kiLCJpYXQiOjE0NzczMDc2MDEsImxhbmd1YWdlX2NvZGUiOiJzbF9TSSIsIlBSTzNVc2VyIjpudWxsLCJpZF9zdXBlcmNvbXBhbnkiOiJlODkwN2FiNi01MDc1LTQ1YzEtYWM4Yi03Y2RjMzQ2Yjg0NTgiLCJleHAiOjE0NzczOTQwMDEsImlzU2VydmljZSI6dHJ1ZSwiaXNNb2JpbGUiOmZhbHNlLCJpc0Rlc2t0b3AiOmZhbHNlfQ.mB2mxiRe4-ih1gDFU52mN1q4a09FpBsBvDdA-s8kDZE",
          "url": "dash",
          "userData": {
            "DesktopClientId": null,
            "currentCompanyName": "Test s.p",
            "first_name": "Test",
            "id_user": "user_uid",
            "language_code": "sl_SI",
            "last_name": "User",
            "username": "test@mycompany"
          }
        }
        

# Group CRM 

# Partner  [/s/api/v1/crmpartner{?page}{?per}{?dateFrom}]
Partner API.

## Get Partner [GET /s/api/v1/crmpartner/{partner_ident}]
To receive specific Partner`s data by Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + partner_ident: 66763207 (number) ... Partner`s identification code - in DB as IdPartner

    
+ Response 200 (application/json)
    + Attributes (CRMPartner GET ONE response)

## Partner Collection [GET]
To receive Partner`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + dateFrom (optional, string) ... Minimum date of change limiter (dd.mm.yyyy format)
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CRMPartner GET response)

## Delete Partner[DELETE /s/api/v1/crmpartner/{partner_ident}]
To delete Partner`s data from DB by Ident.

+ Parameters
    + partner_ident: 66763207 (number) ... Partner`s identification code - in DB as IdPartner
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Partner[POST]
To create new Partner.

+ Request (application/json)
    + Attributes (CRMPartner CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Partner[PUT]
To update Partner.

+ Request (application/json)
    + Attributes (CRMPartner UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
        

# Contact [/s/api/v1/crmcontact{?page}{?per}]
Contacts`s API documentation. 
**This Api Documentation is work in progress !**.
    
## Get Contact [GET /s/api/v1/crmcontact/{contact_id}]
To receive all Contacts`s data.

+ Parameters
    + contact_id:36267  (number) ... Contacts`s ID
    
+ Response 200 (application/json)
    + Attributes (Get Full Contacts)
      

## Delete Contact [DELETE /s/api/v1/crmcontact/{contact_id}]
This API is intended to delete Contact.

+ Parameters
    + contact_id: 36267 (number) ... Contacts`s ID

+ Response 200 (application/json)
    + Attributes (Delete Base)

## Contact Collection [GET]
Get all Contacts.
+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of partners per page
    
+ Response 200 (application/json)
    + Attributes (Contacts Collection)

## Create Contact [POST]
To create new Contact.
+ Request (application/json)
    + Attributes (Create Contacts Few)
        
+ Response 200 (application/json)
    + Attributes (Create Full Contacts Response)

## Update Contact [PUT]
Updating a Contact.
+ Request (application/json)
    + Attributes (Update Contacts Few)
        
+ Response 200 (application/json)
    + Attributes (Update Full Contacts Response)
    

# CRMSalesData [/s/api/v1/crmsalesdata{?page}{?per}]
CRM Partner Sales data API documentation. 

## Create CRMSalesData [POST]
To create new partner sales data.

+ Request (application/json)
    + Attributes (Create CRMSalesData)
    + Headers
    
            Authenticate: Bearer token_string
        
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
    
# PartnerBankAccount [/s/api/v1/crmpartnerbankaccount{?page}{?per}]
 CRM Partner Bank Account documentation.
 
## Get PartnerBankAccount [GET /s/api/v1/crmpartnerbankaccount/{AccountNumber}]
To receive all Contacts`s data.

+ Parameters
    + AccountNumber:666666666  (number) ... Account number
    
+ Response 200 (application/json)
    + Attributes (Get Full Accounts)
    
## PartnerBankAccount Collection [GET]
To receive PartnerBankAccount data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CRMPartnerBankAccount GET response)

## Delete PartnerBankAccount [DELETE /s/api/v1/crmpartnerbankaccount/{AccountNumber}]
To delete Partners bank account from DB by Account number

+ Parameters
    + AccountNumber: 66763207 (number) ... Account number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create PartnerBankAccount[POST]
To create new PartnerBankAccount.

+ Request (application/json)
    + Attributes (CRMPartnerBankAccount CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update PartnerBankAccount[PUT]
To update Partner bank account.

+ Request (application/json)
    + Attributes (CRMPartnerBankAccount UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)    


# Group CB - ClasificationBase

# Reminder [/s/api/v1/cbcodificationclausereminder{?page}{?per}]
Reminders`s API documentation. 
**This Api Documentation is work in progress !**.

## Get Reminder [GET /s/api/v1/cbcodificationclausereminder/{reminder_id}]
To receive specific Reminders`s data by reminder ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + reminder_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -Reminder ID

+ Response 200 (application/json)
    + Attributes (Get ONE Reminder)
    
## Reminder Collection [GET]
To receive Reminders`s data. If parameters page and per are not specified their default value is 0 and 100.

+ Request
    + Headers
    
            Authenticate: Bearer token_string
+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of reminders per page

    
+ Response 200 (application/json)
    + Attributes (Get Full Reminders)
    
## Delete Reminder [DELETE /s/api/v1/cbcodificationclausereminder/{reminder_id}]
To delete all Reminders`s data.

+ Request
    + Headers
    
            Authenticate: Bearer token_string
+ Parameters
    + reminder_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16` (string) - Reminder ID

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Reminder [POST]
To create new Reminder.

+ Request (application/json)
    + Attributes (Create Reminders Few)
    + Headers
    
            Authenticate: Bearer token_string
        
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update Reminder [PUT]
Updating a Reminder.
+ Request (application/json)
    + Attributes (Reminder UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)


+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
# IOP [/s/api/v1/cbcodificationclausebalancestatement{?page}{?per}]
IOPS API documentation. 
**This Api Documentation is work in progress !**.

## Get IOP [GET /s/api/v1/cbcodificationclausebalancestatement{iop_id}]
To receive specific IOP`s data by IOP ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + iop_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - IOP ID

    
+ Response 200 (application/json)
    + Attributes (Get ONE IOP)
    
## IOP Collection [GET]
To receive IOP (Clause balance statement) data. If parameters page and per are not specified their default value is 0 and 100.

+ Request
    + Headers
    
            Authenticate: Bearer token_string
+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of iop per page

    
+ Response 200 (application/json)
    + Attributes (Get Full IOP)
    
    
## Delete IOP [DELETE /s/api/v1/cbcodificationclausebalancestatement/{iop_id}]
To delete all IOP`s data.

+ Request
    + Headers
    
            Authenticate: Bearer token_string
+ Parameters
    + iop_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - IOP ID

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create IOP [POST]
To create new IOP (Clause balance statement).

+ Request (application/json)
    + Attributes (Create IOP Few)
    + Headers
    
            Authenticate: Bearer token_string
        
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update IOP [PUT]
Updating IOP (Clause balance statement).
+ Request (application/json)
    + Attributes (IOP UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
# Email [/s/api/v1/cbcodificationclauseemail{?page}{?per}]
Email API documentation. 
**This Api Documentation is work in progress !**.

## Get Email [GET /s/api/v1/cbcodificationclauseemail/{email_id}]
To receive specific Email data by Email ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + email_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - EMAIL ID

    
+ Response 200 (application/json)
    + Attributes (Get ONE Email)
    
## Email Collection [GET]
To receive Email data. If parameters page and per are not specified their default value is 0 and 100.

+ Request
    + Headers
    
            Authenticate: Bearer token_string
+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of Email per page

+ Response 200 (application/json)
    + Attributes (Get Full Email)
    
## Delete Email [DELETE /s/api/v1/cbcodificationclauseemail/{email_id}]
To delete all Email`s data.

+ Request
    + Headers
    
            Authenticate: Bearer token_string
+ Parameters
    + email_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Email ID

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Email [POST]
To create new Email.

+ Request (application/json)
    + Attributes (Create EMAIL Few)
    + Headers
    
            Authenticate: Bearer token_string
        
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update Email [PUT]
Updating Email.
+ Request (application/json)
    + Attributes (EMAIL UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
        
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
# Product [/s/api/v1/cbproduct{?page}{?per}]
Product API. 
**This Api Documentation is work in progress !**.

## Get Product [GET /s/api/v1/cbproduct/{product_id}]
To receive specific Product data by Product ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + product_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Product ID

    
+ Response 200 (application/json)
    + Attributes (PRODUCT GET ONE response)

## Product Collection [GET]
To receive Product`s data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (PRODUCT GET response)
    
## Delete Product [DELETE /s/api/v1/cbproduct/{product_id}]
To delete all Product data.
+ Parameters
    + product_id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd`(string) - Product ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)

## Create Product [POST]
To create new Product.
+ Request (application/json)
    + Attributes (Product CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

## Update Product [PUT]
Updating Product.
+ Request (application/json)
    + Attributes (PRODUCT UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
    
# Cost Center [/s/api/v1/cbcostcenter{?page}{?per}]
Cost Center API. 
**This Api Documentation is work in progress !**.

## Get Cost Center [GET /s/api/v1/cbcostcenter/{costcenter_id}]
To receive specific Cost Center data by Cost Center ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + costcenter_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16` (string) - Cost Center ID

    
+ Response 200 (application/json)
    + Attributes (CostCenter GET ONE response)

## Cost Center Collection [GET]
To receive Cost Center`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CostCenter GET response)

## Delete Cost Center [DELETE /s/api/v1/cbcostcenter/{costcenter_id}]
To delete Cost Center`s data from DB by ID.

+ Parameters
    + costcenter_id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd`(string) - CostCenter`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Cost Center [POST]
To create new Cost Center.

+ Request (application/json)
    + Attributes (CostCenter CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Cost Center [PUT]
To update Cost Center.

+ Request (application/json)
    + Attributes (CostCenter UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
 
# Cost Organisation Unit [/s/api/v1/cborgunit{?page}{?per}]
Cost Organisation Unit API. 
**This Api Documentation is work in progress !**.

## Get Cost Organisation Unit [GET /s/api/v1/cborgunit/{costcenter_id}]
To receive specific Cost Organisation Unit data by Cost Organisation Unit ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + costcenter_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16` (string) - Cost Organisation Unit ID

    
+ Response 200 (application/json)
    + Attributes (CostCenter GET ONE response)

## Cost Organisation Unit Collection [GET]
To receive Cost Organisation Unit`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CostCenter GET response)

## Delete Cost Organisation Unit [DELETE /s/api/v1/cborgunit/{costcenter_id}]
To delete Cost Organisation Unit`s data from DB by ID.

+ Parameters
    + costcenter_id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd`(string) - CostCenter`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Cost Organisation Unit [POST]
To create new Cost Organisation Unit.

+ Request (application/json)
    + Attributes (CostCenter CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Cost Organisation Unit [PUT]
To update Cost Organisation Unit.

+ Request (application/json)
    + Attributes (CostCenter UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Cost Carrier [/s/api/v1/cbcostcarrier{?page}{?per}]
Cost Carrier API. 
**This Api Documentation is work in progress !**.

## Get Cost Carrier [GET /s/api/v1/cbcostcarrier/{costcarrier_id}]
To receive specific Cost Carrier data by Cost Carrier`s ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + costcarrier_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Cost Carrier`s ID

    
+ Response 200 (application/json)
    + Attributes (CostCarrier GET ONE response)

## Cost Carrier Collection [GET]
To receive Cost Carrier`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CostCarrier GET response)

## Delete Cost Carrier [DELETE /s/api/v1/cbcostcarrier/{codification_id}]
To delete Cost Carrier`s data from DB by ID.

+ Parameters
    + codification_id: `a2826ba7-1354-4a78-be51-6d901dc1aac1` (string) - Codificaiton`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Cost Carrier [POST]
To create new Cost Carrier.

+ Request (application/json)
    + Attributes (CostCarrier CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Cost Carrier[PUT]
To update Cost Carrier.

+ Request (application/json)
    + Attributes (CostCarrier UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
# Workplace [/s/api/v1/cbworkplace{?page}{?per}]
Workplace API. 
**This Api Documentation is work in progress !**.

## Get Workplace [GET /s/api/v1/cbworkplace/{workplace_id}]
To receive specific Workplace data by Workplace ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + workplace_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee1`(string) - Workplace ID

    
+ Response 200 (application/json)
    + Attributes (Workplace GET ONE response)

## Workplace Collection [GET]
To receive Workplace`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (Workplace GET response)

## Delete Workplace [DELETE /s/api/v1/cbworkplace/{workplace_id}]
To delete Workplace`s data from DB by ID.

+ Parameters
    + workplace_id: `8bf7263b-7480-4e07-8afb-8420ac3ca642`(string) - Workplace`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Workplace [POST]
To create new Workplace.

+ Request (application/json)
    + Attributes (Workplace CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Workplace [PUT]
To update Workplace.

+ Request (application/json)
    + Attributes (Workplace UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Booking type [/s/api/v1/cbbookingtype{?page}{?per}]
Bookingtype API. 
**This Api Documentation is work in progress !**.

## Get Booking type [GET /s/api/v1/cbbookingtype/{bookingtype_id}]
To receive specific Booking type data by Booking type ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string

+ Parameters
    + bookingtype_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Bookingtype ID

+ Response 200 (application/json)
    + Attributes (Bookingtype GET ONE response)

## Booking type Collection [GET]
To receive Bookingtype`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (Bookingtype GET response)

## Delete Booking type [DELETE /s/api/v1/cbbookingtype/{bookingtype_id}]
To delete Booking type`s data from DB by ID.

+ Parameters
    + bookingtype_id: `8bf7263b-7480-4e07-8afb-8420ac3ca642`(string) - Bookingtype`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)

## Create Booking type [POST]
To create new Booking type.

+ Request (application/json)
    + Attributes (Bookingtype CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Booking type [PUT]
To update Booking type.

+ Request (application/json)
    + Attributes (Bookingtype UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Account [/s/api/v1/cbaccount{?page}{?per}]
Account API. 
**This Api Documentation is work in progress !**.

## Get Account [GET /s/api/v1/cbaccount/{cbaccount_id}]
To receive specific Account data by Account ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + cbaccount_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Account ID

    
+ Response 200 (application/json)
    + Attributes (Account GET ONE response)

## Account Collection [GET]
To receive Account`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (Account GET response)

## Delete Account [DELETE /s/api/v1/cbaccount/{cbaccount_id}]
To delete Account`s data from DB by ID.

+ Parameters
    + cbaccount_id: `fb13e588-d81f-4651-8b94-e69fca45731d` (string) -Account`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Account [POST]
To create new Account.

+ Request (application/json)
    + Attributes (Account CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Account [PUT]
To update Account.

+ Request (application/json)
    + Attributes (Account UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Product type [/s/api/v1/cbproducttype{?page}{?per}]
Product type API. 
**This Api Documentation is work in progress !**.

## Get Product type [GET /s/api/v1/cbproducttype/{cbproduttype_id}]
To receive specific Product type data Product type ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + cbproduttype_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16` (string) - Product type ID

    
+ Response 200 (application/json)
    + Attributes (ProductType GET ONE response)

## Product type Collection [GET]
To receive Product type`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (ProductType GET response)

## Delete Product type [DELETE /s/api/v1/cbproducttype/{cbproduttype_id}]
To delete Product type`s data from DB by ID.

+ Parameters
    + cbproduttype_id: `dccde67e-cc40-4d44-a89f-b302c4f60cd1`(string) - Product type`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Product type [POST]
To create new Product type.

+ Request (application/json)
    + Attributes (ProductType CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Product type [PUT]
To update Product type.

+ Request (application/json)
    + Attributes (ProductType UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Department  [/s/api/v1/cbdepartment{?page}{?per}]
Department API. 
**This Api Documentation is work in progress !**.

## Get Department [GET /s/api/v1/cbdepartment/{cbdepartment_id}]
To receive specific Department data with Department ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + cbdepartment_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Department ID

    
+ Response 200 (application/json)
    + Attributes (Department GET ONE response)

## Department Collection [GET]
To receive Department`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (Department GET response)

## Delete Department[DELETE /s/api/v1/cbdepartment/{cbdepartment_id}]
To delete Department`s data from DB by ID.

+ Parameters
    + cbdepartment_id: `dccde67e-cc40-4d44-a89f-b302c4f60cd1` (string) - Department`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Department[POST]
To create new Department.

+ Request (application/json)
    + Attributes (Department CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Department[PUT]
To update Department.

+ Request (application/json)
    + Attributes (Department UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Payout place  [/s/api/v1/cbpayoutplace{?page}{?per}]
Payout place API. 
**This Api Documentation is work in progress !**.

## Get Payout place [GET /s/api/v1/cbpayoutplace/{cbpayoutplace_id}]
To receive specific Payout place data with Payout place ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + cbpayoutplace_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - Payout place ID

    
+ Response 200 (application/json)
    + Attributes (PayoutPlace GET ONE response)

## Payout place Collection [GET]
To receive Payout place`s data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (PayoutPlace GET response)

## Delete Payout place[DELETE /s/api/v1/cbpayoutplace/{cbpayoutplace_id}]
To delete Payout place`s data from DB by ID.

+ Parameters
    + cbpayoutplace_id: `dccde67e-cc40-4d44-a89f-b302c4f60cd1`(string) - Payout place`s ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create Payout place[POST]
To create new Payout place.

+ Request (application/json)
    + Attributes (PayoutPlace CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
## Update Payout place[PUT]
To update Payout place.

+ Request (application/json)
    + Attributes (PayoutPlace UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
    
# Group HRM

# HRM Workplace [/s/api/v1/hrmworkplace{?page}{?per}]
HRMWorkplace API. 
**This Api Documentation is work in progress !**.

## Get HRM Workplace [GET /s/api/v1/hrmworkplace/{workplacecode_id}]
To receive specific HRM Workplace data with HRM Workplace ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + workplacecode_id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - HRM Workplace ID

    
+ Response 200 (application/json)
    + Attributes (HrmWorkplace GET ONE response)

## HRM Workplace Collection [GET]
To receive HRMWorkplace data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HrmWorkplace GET response)
    
## Delete HRM Workplace [DELETE /s/api/v1/hrmworkplace/{workplacecode_id}]
To delete all Product data.
+ Parameters
    + workplacecode_id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd`(string) - HRMWorkPlace ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)

## Create  HRM Workplace [POST]
To create new  HRM Workplace.
+ Request (application/json)
    + Attributes ( HRM Workplace CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

## Update HRM Workplace [PUT]
Updating HRM Workplace.
+ Request (application/json)
    + Attributes (HRM Workplace UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
 
# HRMCBWorker [/s/api/v1/hrmcbworker{?page}{?per}]
HRMCBWorker API. 
**This Api Documentation is work in progress !**.

## Get HRMCBWorker [GET /s/api/v1/hrmcbworker/{hrmcbworker_ident}]
To receive specific HRMCBWorker data with HRMCBWorker IDENT

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmcbworker_ident: `0001`(string) - HRMCBWorker IDENT

    
+ Response 200 (application/json)
    + Attributes (HRMCBWorker GET ONE response)

##HRMCBWorker Collection [GET]
To receive HRMCBWorker data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMCBWorker GET response)
    
## Delete HRM HRMCBWorker [DELETE /s/api/v1/hrmcbworker/{hrmcbworker_ident}]
To delete all HRMCBWorker data.
+ Parameters
    + hrmcbworker_ident: `0001`(string) - HRMCBWorker IDENT
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMCBWorker [POST]
To create new  HRMCBWorker.

+ Request (application/json)
    + Attributes (HRMCBWorker CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMCBWorker [PUT]
Updating HRMCBWorker.
+ Request (application/json)
    + Attributes (HRMCBWorker UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerEmployment [/s/api/v1/hrmworkeremployment{?page}{?per}{?IdWorker}]
HRMWorkerEmployment API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerEmployment [GET /s/api/v1/hrmworkeremployment/{id}]
To receive specific HRMWorkerEmployment data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerEmployment GET ONE response)

##HRMWorkerEmployment Collection [GET]
To receive HRMWorkerEmployment data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerEmployment GET response)
    
## Delete HRM HRMWorkerEmployment [DELETE /s/api/v1/hrmworkeremployment/{id}]
To delete all HRMWorkerEmployment data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerEmployment [POST]
To create new  HRMWorkerEmployment.

+ Request (application/json)
    + Attributes (HRMWorkerEmployment CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerEmployment [PUT]
Updating HRMWorkerEmployment.
+ Request (application/json)
    + Attributes (HRMWorkerEmployment UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerVacation [/s/api/v1/hrmworkervacation{?page}{?per}{?IdWorker}]
HRMWorkerVacation API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerVacation [GET /s/api/v1/hrmworkervacation/{id}]
To receive specific HRMWorkerVacation data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerVacation GET ONE response)

##HRMWorkerVacation Collection [GET]
To receive HRMWorkerVacation data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker

+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerVacation GET response)
    
## Delete HRM HRMWorkerVacation [DELETE /s/api/v1/hrmworkervacation/{id}]
To delete all HRMWorkerVacation data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerVacation [POST]
To create new  HRMWorkerVacation.

+ Request (application/json)
    + Attributes (HRMWorkerVacation CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerVacation [PUT]
Updating HRMWorkerVacation.
+ Request (application/json)
    + Attributes (HRMWorkerVacation UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)



# HRMWorkerCalculatedEmployment [/s/api/v1/hrmworkercalculatedemployment{?page}{?per}{?IdWorker}]
HRMWorkerCalculatedEmployment API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerCalculatedEmployment [GET /s/api/v1/hrmworkercalculatedemployment/{id}]
To receive specific HRMWorkerCalculatedEmployment data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerCalculatedEmployment GET ONE response)

##HRMWorkerCalculatedEmployment Collection [GET]
To receive HRMWorkerCalculatedEmployment data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker

+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerCalculatedEmployment GET response)
    
## Delete HRM HRMWorkerCalculatedEmployment [DELETE /s/api/v1/hrmworkercalculatedemployment/{id}]
To delete all HRMWorkerCalculatedEmployment data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerCalculatedEmployment [POST]
To create new  HRMWorkerCalculatedEmployment.

+ Request (application/json)
    + Attributes (HRMWorkerCalculatedEmployment CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerCalculatedEmployment [PUT]
Updating HRMWorkerCalculatedEmployment.
+ Request (application/json)
    + Attributes (HRMWorkerCalculatedEmployment UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerFamilyMember [/s/api/v1/hrmworkerfamilymember{?page}{?per}{?IdWorker}]
HRMWorkerFamilyMember API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerFamilyMember [GET /s/api/v1/hrmworkerfamilymember/{id}]
To receive specific HRMWorkerFamilyMember data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerFamilyMember GET ONE response)

##HRMWorkerFamilyMember Collection [GET]
To receive HRMWorkerFamilyMember data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerFamilyMember GET response)
    
## Delete HRM HRMWorkerFamilyMember [DELETE /s/api/v1/hrmworkerfamilymember/{id}]
To delete all HRMWorkerFamilyMember data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerFamilyMember [POST]
To create new  HRMWorkerFamilyMember.

+ Request (application/json)
    + Attributes (HRMWorkerFamilyMember CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerFamilyMember [PUT]
Updating HRMWorkerFamilyMember.
+ Request (application/json)
    + Attributes (HRMWorkerFamilyMember UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerEducation [/s/api/v1/hrmworkereducation{?page}{?per}{?IdWorker}]
HRMWorkerEducation API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerEducation [GET /s/api/v1/hrmworkereducation/{id}]
To receive specific HRMWorkerEducation data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerEducation GET ONE response)

##HRMWorkerEducation Collection [GET]
To receive HRMWorkerEducation data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerEducation GET response)
    
## Delete HRM HRMWorkerEducation [DELETE /s/api/v1/hrmworkereducation/{id}]
To delete all HRMWorkerEducation data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerEducation [POST]
To create new  HRMWorkerEducation.

+ Request (application/json)
    + Attributes (HRMWorkerEducation CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerEducation [PUT]
Updating HRMWorkerEducation.
+ Request (application/json)
    + Attributes (HRMWorkerEducation UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerHabilitation [/s/api/v1/hrmworkerhabilitation{?page}{?per}{?IdWorker}]
HRMWorkerHabilitation API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerHabilitation [GET /s/api/v1/hrmworkerhabilitation/{id}]
To receive specific HRMWorkerHabilitation data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerHabilitation GET ONE response)

##HRMWorkerHabilitation Collection [GET]
To receive HRMWorkerHabilitation data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerHabilitation GET response)
    
## Delete HRM HRMWorkerHabilitation [DELETE /s/api/v1/hrmworkerhabilitation/{id}]
To delete all HRMWorkerHabilitation data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerHabilitation [POST]
To create new  HRMWorkerHabilitation.

+ Request (application/json)
    + Attributes (HRMWorkerHabilitation CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerHabilitation [PUT]
Updating HRMWorkerHabilitation.
+ Request (application/json)
    + Attributes (HRMWorkerHabilitation UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerDisability [/s/api/v1/hrmworkerdisability{?page}{?per}{?IdWorker}]
HRMWorkerDisability API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerDisability [GET /s/api/v1/hrmworkerdisability/{id}]
To receive specific HRMWorkerDisability data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerDisability GET ONE response)

##HRMWorkerDisability Collection [GET]
To receive HRMWorkerDisability data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerDisability GET response)
    
## Delete HRM HRMWorkerDisability [DELETE /s/api/v1/hrmworkerdisability/{id}]
To delete all HRMWorkerDisability data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerDisability [POST]
To create new  HRMWorkerDisability.

+ Request (application/json)
    + Attributes (HRMWorkerDisability CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerDisability [PUT]
Updating HRMWorkerDisability.
+ Request (application/json)
    + Attributes (HRMWorkerDisability UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMWorkerMedicalExamination [/s/api/v1/hrmworkermedicalexamination{?page}{?per}{?IdWorker}]
HRMWorkerMedicalExamination API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerMedicalExamination [GET /s/api/v1/hrmworkermedicalexamination/{id}]
To receive specific HRMWorkerMedicalExamination data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerMedicalExamination GET ONE response)

##HRMWorkerMedicalExamination Collection [GET]
To receive HRMWorkerMedicalExamination data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerMedicalExamination GET response)
    
## Delete HRM HRMWorkerMedicalExamination [DELETE /s/api/v1/hrmworkermedicalexamination/{id}]
To delete all HRMWorkerMedicalExamination data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerMedicalExamination [POST]
To create new  HRMWorkerMedicalExamination.

+ Request (application/json)
    + Attributes (HRMWorkerMedicalExamination CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerMedicalExamination [PUT]
Updating HRMWorkerMedicalExamination.
+ Request (application/json)
    + Attributes (HRMWorkerMedicalExamination UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerAbsence [/s/api/v1/hrmworkerabsence{?page}{?per}{?IdWorker}]
HRMWorkerAbsence API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerAbsence [GET /s/api/v1/hrmworkerabsence/{id}]
To receive specific HRMWorkerAbsence data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerAbsence GET ONE response)

##HRMWorkerAbsence Collection [GET]
To receive HRMWorkerAbsence data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerAbsence GET response)
    
## Delete HRM HRMWorkerAbsence [DELETE /s/api/v1/hrmworkerabsence/{id}]
To delete all HRMWorkerAbsence data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerAbsence [POST]
To create new  HRMWorkerAbsence.

+ Request (application/json)
    + Attributes (HRMWorkerAbsence CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerAbsence [PUT]
Updating HRMWorkerAbsence.
+ Request (application/json)
    + Attributes (HRMWorkerAbsence UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerPastEmployment [/s/api/v1/hrmworkerpastemployment{?page}{?per}{?IdWorker}]
HRMWorkerPastEmployment API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerPastEmployment [GET /s/api/v1/hrmworkerpastemployment/{id}]
To receive specific HRMWorkerPastEmployment data with  ID

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerPastEmployment GET ONE response)

##HRMWorkerPastEmployment Collection [GET]
To receive HRMWorkerPastEmployment data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    + IdWorker (optional, guid) ... Filter employments by IdWorker
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerPastEmployment GET response)
    
## Delete HRM HRMWorkerPastEmployment [DELETE /s/api/v1/hrmworkerpastemployment/{id}]
To delete all HRMWorkerPastEmployment data.
+ Parameters
    + id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerPastEmployment [POST]
To create new  HRMWorkerPastEmployment.

+ Request (application/json)
    + Attributes (HRMWorkerPastEmployment CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerPastEmployment [PUT]
Updating HRMWorkerPastEmployment.
+ Request (application/json)
    + Attributes (HRMWorkerPastEmployment UPDATE request)
    + Headers
    
            Authenticate: Bearer token_string
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

    
    
# HRMClass-Tarifni razredi [/s/api/v1/hrmclass{?page}{?per}]
HRMClass API. 
**This Api Documentation is work in progress !**.

## Get HRMClass [GET /s/api/v1/hrmclass/{hrmclass_ident}]
To receive specific HRMClass data with HRMClass Identification number

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclass_ident: `11` - HRMClass Identification number

    
+ Response 200 (application/json)
    + Attributes (HRMClass GET ONE response)


##HRMClass Collection [GET]
To receive HRMClass data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMClass GET response)
    
## Delete HRMClass [DELETE /s/api/v1/hrmclass/{hrmclass_ident}]
To delete all HRMClass data.
+ Parameters
    + hrmclass_ident: `11` (string) - HRMClass Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMClass [POST]
To create new  HRMClass.

+ Request (application/json)
    + Attributes (HRMClass CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMClass [PUT]
Updating HRMClass.
+ Request (application/json)
    + Attributes (HRMClass UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMClassPl-Plačni razredi [/s/api/v1/hrmclasspl{?page}{?per}]
HRMClassPl API. 
**This Api Documentation is work in progress !**.

## Get HRMClassPl [GET /s/api/v1/hrmclasspl/{hrmclasspl_ident}]
To receive specific HRMClassPl data with HRMClassPl Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: `11` - HRMClassPl Identification number

    
+ Response 200 (application/json)
    + Attributes (HRMClass GET ONE response)


##HRMClassPl Collection [GET]
To receive HRMClassPl data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMClass GET response)
    
## Delete HRMClassPl [DELETE /s/api/v1/hrmclasspl/{hrmclasspl_ident}]
To delete all HRMClassPl data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMClassPl Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMClassPl [POST]
To create new  HRMClassPl.

+ Request (application/json)
    + Attributes (HRMClass CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMClassPl [PUT]
Updating HRMClassPl.
+ Request (application/json)
    + Attributes (HRMClass UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMClassP-Premijski razredi [/s/api/v1/hrmclassp{?page}{?per}]
HRMClassP API. 
**This Api Documentation is work in progress !**.

## Get HRMClassP [GET /s/api/v1/hrmclassp/{hrmclassp_ident}]
To receive specific HRMClassP data with HRMClassP Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclassp_ident: `11` - HRMClassP Identification number

    
+ Response 200 (application/json)
    + Attributes (HRMClass GET ONE response)


##HRMClassP Collection [GET]
To receive HRMClassP data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMClass GET response)
    
## Delete HRMClassP [DELETE /s/api/v1/hrmclassp/{hrmclassp_ident}]
To delete all HRMClassP data.
+ Parameters
    + hrmclassp_ident: `11` (string) - HRMClassP Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMClassP [POST]
To create new  HRMClassP.

+ Request (application/json)
    + Attributes (HRMClass CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMClassP [PUT]
Updating HRMClassP.
+ Request (application/json)
    + Attributes (HRMClass UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMTitleCodes-Nazivi [/s/api/v1/hrmtitlecodes{?page}{?per}]
HRMTitleCodes API. 
**This Api Documentation is work in progress !**.

## Get HRMTitleCodes [GET /s/api/v1/hrmtitlecodes/{hrmclasspl_ident}]
To receive specific HRMTitleCodes data with HRMTitleCodes Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMTitleCodes GET ONE response)


##HRMTitleCodes Collection [GET]
To receive HRMTitleCodes data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMTitleCodes GET response)
    
## Delete HRMTitleCodes [DELETE /s/api/v1/hrmtitlecodes/{hrmclasspl_ident}]
To delete all HRMTitleCodes data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMTitleCodes Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMTitleCodes [POST]
To create new  HRMTitleCodes.

+ Request (application/json)
    + Attributes (HRMTitleCodes CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMTitleCodes [PUT]
Updating HRMTitleCodes.
+ Request (application/json)
    + Attributes (HRMTitleCodes UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMHabilitationCodeArea-Področja izvolitve [/s/api/v1/hrmhabilitationcodearea{?page}{?per}]
HRMHabilitationCodeArea API. 
**This Api Documentation is work in progress !**.

## Get HRMHabilitationCodeArea [GET /s/api/v1/hrmhabilitationcodearea/{hrmclasspl_ident}]
To receive specific HRMHabilitationCodeArea data with HRMHabilitationCodeArea Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMHabilitationCodeArea GET ONE response)


##HRMHabilitationCodeArea Collection [GET]
To receive HRMHabilitationCodeArea data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMHabilitationCodeArea GET response)
    
## Delete HRMHabilitationCodeArea [DELETE /s/api/v1/hrmhabilitationcodearea/{hrmclasspl_ident}]
To delete all HRMHabilitationCodeArea data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMHabilitationCodeArea Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMHabilitationCodeArea [POST]
To create new  HRMHabilitationCodeArea.

+ Request (application/json)
    + Attributes (HRMHabilitationCodeArea CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMHabilitationCodeArea [PUT]
Updating HRMHabilitationCodeArea.
+ Request (application/json)
    + Attributes (HRMHabilitationCodeArea UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMEducationLocation- Lokacije izobraževanj [/s/api/v1/hrmeducationlocation{?page}{?per}]
HRMEducationLocation API. 
**This Api Documentation is work in progress !**.

## Get HRMEducationLocation [GET /s/api/v1/hrmeducationlocation/{hrmclasspl_ident}]
To receive specific HRMEducationLocation data with HRMEducationLocation Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMEducationLocation GET ONE response)


##HRMEducationLocation Collection [GET]
To receive HRMEducationLocation data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationLocation GET response)
    
## Delete HRMEducationLocation [DELETE /s/api/v1/hrmeducationlocation/{hrmclasspl_ident}]
To delete all HRMEducationLocation data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMEducationLocation Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationLocation [POST]
To create new  HRMEducationLocation.

+ Request (application/json)
    + Attributes (HRMEducationLocation CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationLocation [PUT]
Updating HRMEducationLocation.
+ Request (application/json)
    + Attributes (HRMEducationLocation UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMCatalogTraining - Katalog usposabljanj [/s/api/v1/hrmcatalogtraining{?page}{?per}]
HRMCatalogTraining API. 
**This Api Documentation is work in progress !**.

## Get HRMCatalogTraining [GET /s/api/v1/hrmcatalogtraining/{hrmclasspl_ident}]
To receive specific HRMCatalogTraining data with HRMCatalogTraining Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMCatalogTraining GET ONE response)


##HRMCatalogTraining Collection [GET]
To receive HRMCatalogTraining data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMCatalogTraining GET response)
    
## Delete HRMCatalogTraining [DELETE /s/api/v1/hrmcatalogtraining/{hrmclasspl_ident}]
To delete all HRMCatalogTraining data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMCatalogTraining Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMCatalogTraining [POST]
To create new  HRMCatalogTraining.

+ Request (application/json)
    + Attributes (HRMCatalogTraining CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMCatalogTraining [PUT]
Updating HRMCatalogTraining.
+ Request (application/json)
    + Attributes (HRMCatalogTraining UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMTraining - Usposabljanje [/s/api/v1/hrmtraining{?page}{?per}]
HRMTraining API. 
**This Api Documentation is work in progress !**.

## Get HRMTraining [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMTraining data with HRMTraining Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMTraining GET ONE response)


##HRMTraining Collection [GET]
To receive HRMTraining data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMTraining GET response)
    
## Delete HRMTraining [DELETE /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To delete all HRMTraining data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMTraining Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMTraining [POST]
To create new  HRMTraining.

+ Request (application/json)
    + Attributes (HRMTraining CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMTraining [PUT]
Updating HRMTraining.
+ Request (application/json)
    + Attributes (HRMTraining UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMInstructor - Predavatelj usposabljanja [/s/api/v1/hrminstructor{?page}{?per}]
HRMInstructor API. 
**This Api Documentation is work in progress !**.

## Get HRMInstructor [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMInstructor data with HRMInstructor Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMInstructor GET ONE response)


##HRMInstructor Collection [GET]
To receive HRMInstructor data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMInstructor GET response)
    
## Delete HRMInstructor [DELETE /s/api/v1/hrminstructor/{hrmclasspl_ident}]
To delete all HRMInstructor data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMInstructor Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMInstructor [POST]
To create new  HRMInstructor.

+ Request (application/json)
    + Attributes (HRMInstructor CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMInstructor [PUT]
Updating HRMInstructor.
+ Request (application/json)
    + Attributes (HRMInstructor UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerInsurance - Zavarovanje [/s/api/v1/hrmworkerinsurance{?page}{?per}]
HRMInstructor API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerInsurance [GET /s/api/v1/hrmworkerinsurance/{hrmclasspl_ident}]
To receive specific HRMWorkerInsurance data with HRMWorkerInsurance Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerInsurance GET ONE response)


##HRMWorkerInsurance Collection [GET]
To receive HRMWorkerInsurance data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerInsurance GET response)
    
## Delete HRMWorkerInsurance [DELETE /s/api/v1/hrmworkerinsurance/{hrmclasspl_ident}]
To delete all HRMWorkerInsurance data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMWorkerInsurance Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerInsurance [POST]
To create new  HRMWorkerInsurance.

+ Request (application/json)
    + Attributes (HRMWorkerInsurance CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerInsurance [PUT]
Updating HRMWorkerInsurance.
+ Request (application/json)
    + Attributes (HRMWorkerInsurance UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMYearlyReview - Letne ocene [/s/api/v1/hrmyearlyreview{?page}{?per}]
HRMInstructor API. 
**This Api Documentation is work in progress !**.

## Get HRMYearlyReview [GET /s/api/v1/hrmyearlyreview/{hrmclasspl_ident}]
To receive specific HRMYearlyReview data with HRMYearlyReview Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMYearlyReview GET ONE response)


##HRMYearlyReview Collection [GET]
To receive HRMYearlyReview data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMYearlyReview GET response)
    
## Delete HRMYearlyReview [DELETE /s/api/v1/hrmyearlyreview/{hrmclasspl_ident}]
To delete all HRMYearlyReview data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMYearlyReview Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMYearlyReview [POST]
To create new  HRMYearlyReview.

+ Request (application/json)
    + Attributes (HRMYearlyReview CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMYearlyReview [PUT]
Updating HRMYearlyReview.
+ Request (application/json)
    + Attributes (HRMYearlyReview UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMTrainingCosts - Stroški usposabljanj [/s/api/v1/hrmtrainingcosts{?page}{?per}]
HRMTrainingCosts API. 
**This Api Documentation is work in progress !**.

## Get HRMTrainingCosts [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMTrainingCosts data with HRMTrainingCosts Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMTrainingCosts GET ONE response)


##HRMTrainingCosts Collection [GET]
To receive HRMTrainingCosts data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMTrainingCosts GET response)
    
## Delete HRMTrainingCosts [DELETE /s/api/v1/hrmtrainingcosts/{hrmclasspl_ident}]
To delete all HRMTrainingCosts data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMTrainingCosts Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMTrainingCosts [POST]
To create new  HRMTrainingCosts.

+ Request (application/json)
    + Attributes (HRMTrainingCosts CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMTrainingCosts [PUT]
Updating HRMTrainingCosts.
+ Request (application/json)
    + Attributes (HRMTrainingCosts UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMTrainingParticipants - Udeleženci usposabljanj [/s/api/v1/hrmtrainingparticipants{?page}{?per}]
HRMTrainingParticipants API. 
**This Api Documentation is work in progress !**.

## Get HRMTrainingParticipants [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMTrainingParticipants data with HRMTrainingParticipants Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMTrainingParticipants GET ONE response)


##HRMTrainingParticipants Collection [GET]
To receive HRMTrainingParticipants data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMTrainingParticipants GET response)
    
## Delete HRMTrainingParticipants [DELETE /s/api/v1/hrmtrainingparticipants/{hrmclasspl_ident}]
To delete all HRMTrainingParticipants data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMTrainingParticipants Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMTrainingParticipants [POST]
To create new  HRMTrainingParticipants.

+ Request (application/json)
    + Attributes (HRMTrainingParticipants CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMTrainingParticipants [PUT]
Updating HRMTrainingParticipants.
+ Request (application/json)
    + Attributes (HRMTrainingParticipants UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMEducationProgramType - Vrsta usposabljanja [/s/api/v1/hrmeducationprogramtype{?page}{?per}]
HRMTrainingParticipants API. 
**This Api Documentation is work in progress !**.

## Get HRMEducationProgramType [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMEducationProgramType data with HRMEducationProgramType Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMEducationProgramType GET ONE response)


##HRMEducationProgramType Collection [GET]
To receive HRMEducationProgramType data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationProgramType GET response)
    
## Delete HRMEducationProgramType [DELETE /s/api/v1/hrmeducationprogramtype/{hrmclasspl_ident}]
To delete all HRMEducationProgramType data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMEducationProgramType Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationProgramType [POST]
To create new  HRMEducationProgramType.

+ Request (application/json)
    + Attributes (HRMEducationProgramType CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationProgramType [PUT]
Updating HRMEducationProgramType.
+ Request (application/json)
    + Attributes (HRMEducationProgramType UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)



# HRMEducationInstitute - Institucije [/s/api/v1/hrmeducationinstitute{?page}{?per}]
HRMTrainingParticipants API. 
**This Api Documentation is work in progress !**.

## Get HRMEducationInstitute [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMEducationInstitute data with HRMEducationInstitute Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMEducationInstitute GET ONE response)


##HRMEducationInstitute Collection [GET]
To receive HRMEducationInstitute data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationInstitute GET response)
    
## Delete HRMEducationInstitute [DELETE /s/api/v1/hrmeducationinstitute/{hrmclasspl_ident}]
To delete all HRMEducationInstitute data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMEducationInstitute Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationInstitute [POST]
To create new  HRMEducationInstitute.

+ Request (application/json)
    + Attributes (HRMEducationInstitute CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationInstitute [PUT]
Updating HRMEducationInstitute.
+ Request (application/json)
    + Attributes (HRMEducationInstitute UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMWorkerAttribute - Atributi delavca [/s/api/v1/hrmworkerattribute{?page}{?per}]
HRMTrainingParticipants API. 
**This Api Documentation is work in progress !**.

## Get HRMWorkerAttribute [GET /s/api/v1/hrmworkerattribute/{hrmclasspl_ident}]
To receive specific HRMWorkerAttribute data with HRMWorkerAttribute Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMWorkerAttribute GET ONE response)


##HRMWorkerAttribute Collection [GET]
To receive HRMWorkerAttribute data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMWorkerAttribute GET response)
    
## Delete HRMWorkerAttribute [DELETE /s/api/v1/hrmworkerattribute/{hrmclasspl_ident}]
To delete all HRMWorkerAttribute data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMWorkerAttribute Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMWorkerAttribute [POST]
To create new  HRMWorkerAttribute.

+ Request (application/json)
    + Attributes (HRMWorkerAttribute CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMWorkerAttribute [PUT]
Updating HRMWorkerAttribute.
+ Request (application/json)
    + Attributes (HRMWorkerAttribute UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# HRMCodification - Splošni šifrant [/s/api/v1/hrmcodification{?page}{?per}]
HRMTrainingParticipants API. 
**This Api Documentation is work in progress !**.

## Get HRMCodification [GET /s/api/v1/hrmtraining/{hrmclasspl_ident}]
To receive specific HRMCodification data with HRMCodification Ident

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmclasspl_ident: e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID

    
+ Response 200 (application/json)
    + Attributes (HRMCodification GET ONE response)


##HRMCodification Collection [GET]
To receive HRMCodification data. If parameters page and per are not specified it`s default value is 0 and 100.


+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMCodification GET response)
    
## Delete HRMCodification [DELETE /s/api/v1/hrmcodification/{hrmclasspl_ident}]
To delete all HRMCodification data.
+ Parameters
    + hrmclasspl_ident: `11` (string) - HRMCodification Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMCodification [POST]
To create new  HRMCodification.

+ Request (application/json)
    + Attributes (HRMCodification CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMCodification [PUT]
Updating HRMCodification.
+ Request (application/json)
    + Attributes (HRMCodification UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)



# HRMEducationCodeDegree - Stopnja izobrazbe [/s/api/v1/hrmeducationcodedegree{?page}{?per}]
HRMEducationCodeDegree API.

## Get HRMEducationCodeDegree [GET /s/api/v1/hrmeducationcodedegree/{hrmeducationcodedegree_ident}]
To receive specific HRMEducationCodeDegree data with hrmeducationcodedegree Identification number

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmeducationcodedegree_ident: `III.` - HRMEducationCodeDegree Identification number
 
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeDegree GET ONE response)

##HRMEducationCodeDegree Collection [GET]
To receive HRMEducationCodeDegree data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeDegree GET response)
    
## Delete HRMEducationCodeDegree [DELETE /s/api/v1/hrmeducationcodedegree/{hrmeducationcodedegree_ident}]
To delete all HRMEducationCodeDegree data by Identification number.
+ Parameters
    + hrmeducationcodedegree_ident: `III.` - HRMEducationCodeDegree Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationCodeDegree [POST]
To create new  HRMEducationCodeDegree.

+ Request (application/json)
    + Attributes (HRMEducationCodeDegree CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationCodeDegree [PUT]
Updating HRMEducationCodeDegree.
+ Request (application/json)
    + Attributes (HRMEducationCodeDegree UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMEducationCode - Poklicna in strokovna izobrazba [/s/api/v1/hrmeducationcode{?page}{?per}]
HRMEducationCode API.

## Get HRMEducationCode [GET /s/api/v1/hrmeducationcode/{hrmeducationcode_ident}]
To receive specific HRMEducationCode data with hrmeducationcode Identification number

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmeducationcode_ident: `III.` - HRMEducationCode Identification number
 
+ Response 200 (application/json)
    + Attributes (HRMEducationCode GET ONE response)

##HRMEducationCode Collection [GET]
To receive HRMEducationCode data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationCode GET response)
    
## Delete HRMEducationCode [DELETE /s/api/v1/hrmeducationcode/{hrmeducationcode_ident}]
To delete all HRMEducationCode data by Identification number.
+ Parameters
    + hrmeducationcode_ident: `III.` - HRMEducationCode Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationCode [POST]
To create new  HRMEducationCode.

+ Request (application/json)
    + Attributes (HRMEducationCode CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationCode [PUT]
Updating HRMEducationCode.
+ Request (application/json)
    + Attributes (HRMEducationCode UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMEducationCodeSKP - Poklic po SKP [/s/api/v1/hrmeducationcodeskp{?page}{?per}]
HRMEducationCodeSKP API.

## Get HRMEducationCodeSKP [GET /s/api/v1/hrmeducationcodeskp/{hrmeducationcodeskp_ident}]
To receive specific HRMEducationCodeSKP data with hrmeducationcodeskp Identification number

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmeducationcodeskp_ident: `III.` - HRMEducationCodSKP Identification number
 
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeSKP GET ONE response)

##HRMEducationCodeSKP Collection [GET]
To receive HRMEducationCodeSKP data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationCode GET response)
    
## Delete HRMEducationCodeSKP [DELETE /s/api/v1/hrmeducationcodeskp/{hrmeducationcodeskp_ident}]
To delete all HRMEducationCodeSKP data by Identification number.
+ Parameters
    + hrmeducationcodeskp_ident: `III.` - HRMEducationCodSKP Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationCodeSKP [POST]
To create new  HRMEducationCodeSKP.

+ Request (application/json)
    + Attributes (HRMEducationCodeSKP CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationCodeSKP [PUT]
Updating HRMEducationCodeSKP.
+ Request (application/json)
    + Attributes (HRMEducationCodeSKP UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMEducationCodeArea - Področja izobrazbe [/s/api/v1/hrmeducationcodearea{?page}{?per}]
HRMEducationCodeArea API.

## Get HRMEducationCodeArea [GET /s/api/v1/hrmeducationcodearea/{hrmeducationcodearea_ident}]
To receive specific HRMEducationCodeArea data with hrmeducationcodearea Identification number

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmeducationcodearea_ident: `III.` - HRMEducationCodeArea Identification number
 
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeArea GET ONE response)

##HRMEducationCodeArea Collection [GET]
To receive HRMEducationCodeArea data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeArea GET response)
    
## Delete HRMEducationCodeArea [DELETE /s/api/v1/hrmeducationcodearea/{hrmeducationcodearea_ident}]
To delete all HRMEducationCodeArea data by Identification number.
+ Parameters
    + hrmeducationcodearea_ident: `III.` - HRMEducationCodeArea Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationCodeArea [POST]
To create new  HRMEducationCodeArea.

+ Request (application/json)
    + Attributes (HRMEducationCodeArea CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationCodeArea [PUT]
Updating HRMEducationCodeArea.
+ Request (application/json)
    + Attributes (HRMEducationCodeArea UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)

# HRMEducationCodeType - Vrsta izobrazbe [/s/api/v1/hrmeducationcodetype{?page}{?per}]
HRMEducationCodeArea API.

## Get HRMEducationCodeType [GET /s/api/v1/hrmeducationcodetype/{hrmeducationcodetype_ident}]
To receive specific HRMEducationCodeType data with hrmeducationcodetype Identification number

+ Request
    + Headers
    
            Authenticate: Bearer token_string
            
+ Parameters
    + hrmeducationcodetype_ident: `III.` - HRMEducationCodeType Identification number
 
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeType GET ONE response)

##HRMEducationCodeType Collection [GET]
To receive HRMEducationCodeType data. If parameters page and per are not specified it`s default value is 0 and 100.

+ Parameters
    + page (optional, number) ... Maximum number of pages
    + per (optional, number) ... Maximum number of data objects per page
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 
            
+ Response 200 (application/json)
    + Attributes (HRMEducationCodeType GET response)
    
## Delete HRMEducationCodeType [DELETE /s/api/v1/hrmeducationcodetype/{hrmeducationcodetype_ident}]
To delete all HRMEducationCodeType data by Identification number.
+ Parameters
    + hrmeducationcodetype_ident: `III.` - HRMEducationCodeType Identification number
    
+ Request
    + Headers
    
            Authenticate: Bearer token_string 

+ Response 200 (application/json)
    + Attributes (CB RESPONSE DELETE VALID)
    
## Create  HRMEducationCodeType [POST]
To create new  HRMEducationCodeType.

+ Request (application/json)
    + Attributes (HRMEducationCodeType CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)
    
## Update HRMEducationCodeType [PUT]
Updating HRMEducationCodeType.
+ Request (application/json)
    + Attributes (HRMEducationCodeType UPDATE request)
    
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

+ Response 200 (application/json)
    + Attributes (CB RESPONSE INVALID)


# Group DocumentSystem 

# Document  [/s/api/v1/dsdocument]
Document system API. 
**This Api Documentation is work in progress !**.

## Create Document[POST]
To create new document for interchange. Typically generates document from xml + pdf pair of files. However it is allowed to supply more than just these two files.

+ Request (application/json)
    + Attributes (DSDocument CREATE request)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)
            
# Group MailBook

# MailBook documents
API for get mailbook documents.
**This Api Documentation is work in progress !**.

## Get Documents [GET /s/api/v1/mbmail?dateFrom=YYYY-MM-DD&dateTo=YYYY-MM-DD]
Get all documents for given period, returns list of all document.

+ Request (application/json)
    + Headers
    
            Authenticate: Bearer token_string

+ Parameters
    + dateFrom (date) - 2016-01-01 ISO date, period limiter from
    + dateTo (date) - 2016-01-01 ISO date, period limiter to

+ Response 200 (application/json)
    + Attributes (MBMail PUT data)

# Group Finances

# Bookings
API for get/create bookings.
**This Api Documentation is work in progress !**.

## Get Bookings [GET /s/api/v1/fibookings?dateFrom=YYYY-MM-DD&dateTo=YYYY-MM-DD]
Get all bookings for given period, returns list of all bookings.

+ Request (application/json)
    + Headers
    
            Authenticate: Bearer token_string

+ Parameters
    + dateFrom (date) - 2016-01-01 ISO date, period limiter from
    + dateTo (date) - 2016-01-01 ISO date, period limiter to

+ Response 200 (application/json)
    + Attributes (Bookings PUT data)

## Create Bookings [POST /s/api/v1/fibookings]
Save list of bookings to financial module. It is allowed to save one financial statement at a time.

+ Request (application/json)
    + Attributes (Bookings PUT data)
    + Headers
    
            Authenticate: Bearer token_string
            
+ Response 200 (application/json)
    + Attributes (CB RESPONSE VALID)

# Group VAT

# Documents
API for issued/received documents.
**This Api Documentation is work in progress !**.

## Create Issued document [POST /s/api/v1/vatissueddocument]
Save list of documents and their bookings to financial module.

+ Request (application/json)
    + Attributes (VATIssued PUT data)
    + Headers
    
            Authenticate: Bearer token_string

## Get Received document [GET /s/api/v1/vatreceiveddocument?dateFrom=YYYY-MM-DD&dateTo=YYYY-MM-DD]
Get all received documents for given period, returns list of all received documenst.

+ Request (application/json)
    + Headers
    
            Authenticate: Bearer token_string

+ Parameters
    + dateFrom (date) - 2016-01-01 ISO date, period limiter from
    + dateTo (date) - 2016-01-01 ISO date, period limiter to

+ Response 200 (application/json)
    + Attributes (VATReceived PUT data)

## Create Received document [POST /s/api/v1/vatreceiveddocument]
Save list of documents and their bookings to financial module.

+ Request (application/json)
    + Attributes (VATReceived PUT data)
    + Headers
    
            Authenticate: Bearer token_string

## Data Structures

### Create CRMSalesData (array)
+ (object)
    + IdPartner: 0009 (string, required) - Partner Ident
    + Document: FA20160001 (string, required) - Document name
    + Product: 0002 (string, required) - Product Ident
    + Quantity: 15.50 (number) - Quantity of the product
    + Price: 10.00 (number) - Price of the product
    + SumValue: 155.00 (number) - Sum for position

### Delete Base (object)
+ result: true (boolean, required) - True if it was successfully deleted or false if wasn`t 
+ Primary_key: 1231231231231 (string) - contact unique Id Primary key in DB

### Get Full Contacts (object)
+ Birthday: 2016-09-08T07:48:33+00:00 - Persons birthday
+ ContactCityName: 294D2F08-6207-4482-BEDB-436249AF3606 (string) - Contact city name
+ ContactCountryCode: D28CF5EE-EC48-4247-A3CE-A283B37DF158 (string) - Contact country code
+ ContactGuardianIdent: 3948df3e-2850-4acf-b801-af2c0c0c18af (string) - Contact guardian unique Ident
+ ContactPostOfficeCode: 5A876DE5-1DEA-46D6-A1BE-4BB126CB5E04 (string) - Postal code
+ ContactStreet: ContactStreet (string) - Contact street name
+ ContactWorkplaceCode: 00ac638d-9d55-4750-8807-f2ce062b096b (string) - Contact workplace unique code
+ ContactWorkplaceDepartmentTitle: 2256069b-5986-4f5e-bf78-c5e3a099d03b (string) - Contact workplace department
+ Email: test@email.com (string) - Contact email
+ Fax: 564564654 (string) - Contacts fax
+ FirstName: TTTEST (string) - Person first name
+ IdPartner: 000D25D2-A7A7-47EF-8C41-D5D8A5CA9C42 (string) - Partner`s unique Id
+ IdPerson: 714b1e66-642b-486f-b2f9-bf01f59ec961 (string)- Person unique Id
+ LastName: Polanec (string) - Person`s last name
+ Mobile: 65445654654 (string) - Contact mobile phone
+ MsnAddress: msn (string) - Contacts Msn adress
+ PartnerIdCompanyNum: 1673947 (string) - Partner unique company number Id
+ PartnerName: DIAGCENTER D.O.O. (string) - Partner`s name
+ PartnerTaxNumber: 47910984 (string) - Partner`s tax number
+ PersonCityName: 294D2F08-6207-4482-BEDB-436249AF3606 (string) - Person City name
+ PersonCountryCode: D28CF5EE-EC48-4247-A3CE-A283B37DF158 (string) - Person international country code
+ PersonPostOfficeCode: 5A876DE5-1DEA-46D6-A1BE-4BB126CB5E04 (string) - Person postal code
+ PersonStreet: OPerson street (string) - Person street name
+ Phone: 0415642336 (string)- Contacts phone number
+ ShowAs: ostroznik test (string) - Show As of Person
+ SkypeAddress: skype (string) - Contacts Skype adress
+ TitleAfterName: null (string) - Person`s title after name
+ TitleBeforeName: mag (string) - Person`s title before name
+ WebSite: website (string) - Contacts web site adress
+ WorkArea: IT (string) - Contacts work area

### Get Full Accounts (object)
+ Model: ModelModel2 (string) - Bank Account model
+ AccountDateClosed: null - Bank account closed date
+ DateOpened: 2015-10-28T00:00:00+00:00 - Bank accounr date opened
+ AccountNumber: 666666666 (string) - Account number
+ RawAccount: 5641455 (string) - Raw account number
+ AccountDateBlocked: null - Account date blocked
+ Exposition: null (string) - Bank account exposition
+ Type: 41220651 (string) - Bank account type
+ Bank: Banka Celeeeee (string) - Bank name
+ Swift: LongName2 (string) - Swift number
+ AccountBlocked: 0 (number) - Account blocked
+ DataRole: DataRoleDataRole (string) - Data role
+ OutstandingLiabilities: null (string) - Bank account outstanding liabilities
+ Notes: textnotes (string) - Bank account notes
+ IdentPartner: 77766 (string) - Partner unique identification number(Ident)
+ PrimaryAccount: 1 (number) - Primary account

### Get ONE Reminder (object)
+ Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  Reminder unique Id
+ Code: code (string, required) - Number for identification
+ Notes:  notes, (string, required) - Reminder notes
+ Title: Title (string, required) - Reminder title

### Get Full Reminders (object)
+ data(array)
    + (Get ONE Reminder)
+ meta (Get Meta)

### Get ONE IOP (object)
+ Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) - IOP unique Id
+ Code: code (string, required) - Number for identification
+ Notes:  notes, (string, required) - IOP notes
+ Title: Title (string, required) - IOP title

### Get Full IOP (object)
+ data(array)
    + (Get ONE IOP)
+ meta (Get Meta)

### PRODUCT GET ONE response (object)
+ AKTIVEN: D (string) 
+ DOBAVITELJ: TUŠMOBIL D.O.O. (string) - Dobavitelj short name
+ DOBAVIT_ID: `8373F55A-C9B2-4833-A776-7E85725AA877`(string) - Dobavitelj unique Id
+ DOBAVIT_IM: TUŠMOBIL D.O.O., PODJETJE ZA MOBILNE KOMUNIKACIJE (string) - Dobavitelj Long name
+ EAN: test  (string) 
+ GRUPA: A (string)
+ IDG: 00001 (string) - Artikel unique Id 
+ ID_ART: 00001 (string) - Number for identification
+ KALK_CENA: 0 (string)
+ KLASIF: 20 (string) - Clasification of Artikel
+ NAZIV: PRO.4 FAKTURIRANJE STORITEV (string) - Artikel title
+ OPIS: opis (string) - Artikel description 1
+ OPIS2: opis2 (string) - Artikel description 2
+ POREKLO:SI  (string) - Artikel origin
+ PROIZVAJALEC: 9574 (string) - Artikel manufacturer
+ V_ZALOGE: N (string) - Is Artikel In Stock or not

### PRODUCT GET response (object)
+ data (array)
    + (PRODUCT GET ONE response)
+ meta (Get Meta)

### Get Meta (object)
+ page: 1 (required, number) - Number of pages
+ page_size: 2 (required, number) - Number of Partner`s per page
+ total_count: 1032 (required, number) - Number of all Partners received

### Contacts Collection (object)
+ data (Get Full Contacts) - An array of full data objects
+ meta (Get Meta, required)

### Create/Update (object)
+ Id: ed2fb8d2-6125-41b7-b154-a07e3b12042e (string, optional)
+ IdPartner: 34244 (string)
+ IdVatNumber: SI92308763 (string)
+ TaxNumber: SI92308763 (string)
+ TaxPayer: 0 (string)
+ IdCompanyNumber: 234234 (string)
+ PersonalNumber: 34234234 (string)
+ Address: RUDOLFSPLATZ 9999A (string)
+ CountryCode: SI (string)
+ PostalCode: 3210 (string)
+ Phone: 051223554 (string)
+ Fax: 0133255 (string)
+ Mobile: 041220651 (string)
+ Email: test@test.si (string)
+ WebSite: www.test_website.si (string)
+ Sector: S.14 (string)
+ LongName2: second very long nameeee (string)
+ Town: TownName (string)
+ PartnerRegion: 14 (string)
+ Driver: John Snow (string)
+ PartnerType: OP (string)
+ OurShare: 20 (string)
+ PartnerShare: 9 (string)
+ TemporaryLongName: Temporary very long name (string)
+ TemporaryAddress: RUDOLFSPLATZ 2312312313B (string)
+ TemporaryPostalCode: 5000 (string)
+ Payer: 00000114 (string)
+ Rebate: 11 (string)
+ SuperRebate: 1 (string)
+ SuperRebateType: + (string)
+ StatementType: FKD (string)
+ PriceType: PC (string)
+ ShippingType: 1 (string)
+ BusinessType: 1 (string)
+ Parity: 1 (string)
+ ParityLocation: RUDOLFSPLATZ 2b (string)
+ PaymentIBAN: 1515158484 (string)
+ ExtensionNumber: 1 (string)
+ PaymentDays: 3 (string)
+ SupplierPaymentDays: 2 (string)
+ PaymentDateByReceivedDate: 1 (string)

### Create/Update Contacts (object)
+ TitleBeforeName: mag (string) - Person`s title before name
+ FirstName: TTTEST (string) - Person first name
+ LastName: Polanec (string) - Person`s last name 
+ TitleAfterName: null (string) - Person`s title after name
+ ShowAs: ostroznik test (string) - Show As of Person
+ Birthday: 2016-09-07 07:48:33 (string) - Person birthday
+ PersonStreet: OPerson street (string) - Person street name
+ PersonPostOfficeCode : 3215 (string) - Person postal code
+ PersonCityName: SLOVENSKE KONJICE (string) - Person City name
+ PersonCountryCode : SI (string) - Person international country code
+ IdPartner: 1383 (string) - Partner`s unique Id
+ ContactStreet : ContactStreet (string) - Contact street name
+ ContactPostOfficeCode : 3215 (string) - Postal code
+ ContactCityName:SLOVENSKE KONJICE (string) - Contact city name
+ ContactCountryCode: SI (string)  - Contact country code
+ ContactWorkplaceCode: J035028 (string)- Contact workplace unique code
+ ContactWorkplaceDepartmentTitle: Informatika (string) - Contact workplace department
+ WorkArea: IT (string) - Contacts work area
+ Phone: 0415642336 (string) - Contacts phone number
+ Fax: 564564654 (string) - Contacts fax
+ Mobile: 65445654654 (string) - Contact mobile phone
+ Email: test@email.com (string) - Contact email
+ MsnAddress: msn (string) - Contacts Msn adress
+ SkypeAddress: skype (string) - Contacts Skype adress
+ WebSite: website (string) - Contacts web site adress
+ ContactGuardianIdent : 0086 (string) - Contacts guardian unique Ident

### Create/Update Reminders (object)
+ Code: Code (string, required) - Number for identification
+ Notes: Notes (string, required) - Reminder notes
+ Title: Title (string, required) - Reminder title

### Create/Update IOP (object)
+ Code: Code (string, required) - Number for identification
+ Notes: Notes (string) - IOP notes
+ Title: Title (string, required) - IOP title

### Create Few (array)
+ (Create/Update)

### Create Contacts Few (array)
+ (Create/Update Contacts)

### Create Reminders Few (array)
+ (Create/Update Reminders)

### Create IOP Few (array)
+ (Create/Update IOP)

### Update Single (object)
+ id_partner: 34244 (string)
+ data (Create/Update)

### Update Few (array)
+ (Update Single)

### Create Err Empty (array)
+ (object)

### Create Err Full (array)
+ (object)
    + errors (array)
        + Missing field ShortName
        + Missing field LongName
    + id_partner: 34244 (string)
 
### Create Err Contacts Full (array)
+ (object)
    + errors (array)
        + Missing field LastName
        + Missing field FirstName
    + id: 34244 (string)
    
### Update Contacts Single (object)
+ Id: 34244 (string, required)
+ data (Create/Update Contacts)

### Update Contacts Few (array)
+ (Update Contacts Single)

### Create Full Response (object)
+ errors (Create Err Empty)
+ success (array)
    + (object)
        + IdPartner: 34244 (string)
        + ShortName: test (string)
 
### Create Full Contacts Response (object)
+ errors (Create Err Empty)
+ success (array)
    + (object)
        + ContactId: 34244 (string)
        + Notes: test (string)
    + (object)
        + PersonId: 34244 (string)
        + ShowAs: test (string) 
      
### Update Full Contacts Response (object)
+ errors (Create Err Contacts Full)
+ success (array)
    + (object)

### Update Full Response (object)
+ errors (Create Err Full)
+ success (array)
    + (object)
    
### Product CREATE request (array) 
+ (object)
    + AKTIVEN: D (string) 
    + DOBAVITEL: 1357 (string) - Dobavitelj unique ID
    + EAN: test  (string, required) 
    + GRUPA: A (string)
    + IDG: 00001 (string) - Artikel unique Id 
    + ID_ART: 00001 (string) - Number for identification
    + KALK_CENA: 0 (number)
    + KLASIF: 20 (string) - Clasification of Artikel
    + NAZIV: PRO.4 FAKTURIRANJE STORITEV (string, required) - Artikel title
    + OPIS: opis (string) - Artikel description 1
    + OPIS2: opis2 (string) - Artikel description 2
    + POREKLO:SI  (string) - Artikel origin
    + PROIZVAJALEC: 9574 (string) - Artikel manufacturer
    + V_ZALOGE: N (string) - Is Artikel In Stock or not
    + EM: METER (string) - Measurement unit`s title
    
### PRODUCT UPDATE request (array)
+ (object)
    + IDG: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required)
    + data (object) 
        + AKTIVEN: D (string) 
        + DOBAVITEL: TUŠMOBIL D.O.O. (string) - Dobavitelj short name
        + EAN: test  (string) 
        + GRUPA: A (string)
        + IDG: 00001 (string) - Artikel unique Id 
        + ID_ART: 00001 (string) - Number for identification
        + KALK_CENA: 0 (string)
        + KLASIF: 20 (string) - Clasification of Artikel
        + NAZIV: PRO.4 FAKTURIRANJE STORITEV (string) - Artikel title
        + OPIS: opis (string) - Artikel description 1
        + OPIS2: opis2 (string) - Artikel description 2
        + POREKLO:SI  (string) - Artikel origin
        + PROIZVAJALEC: 9574 (string) - Artikel manufacturer
        + V_ZALOGE: N (string) - Is Artikel In Stock or not
        + EM: KILOGRAM (string) - Measurement unit`s title

### CostCenter GET ONE response (object)
+ Address: Ulica test 12 (string) - Cost Center`s address
+ BusinessUnitRegNo: 152 (string)
+ Country: SI (string) - International code for countries
+ Ident: 001 (string) - Number for identification
+ Name: CostCenter_001 (string) - Cost Center`s Title
+ PostOffice: 3210 (string) - Postal code
+ ManagerWorker: 0001 (string) - Manager worker ident
+ DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
+ RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident
+ Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string) - Cost center`s unique Id
 
### CostCenter GET response (object)
+ data (array)
    + (CostCenter GET ONE response)
+ meta (Get Meta)
        
### CostCenter CREATE request (array) 
+ (object)
    + Address: Ulica test 12 (string) - Cost Center`s address
    + BusinessUnitRegNo: 152 (string)
    + Country: SI (string) - International code for countries
    + Ident: 001 (string) - Number for identification
    + Name: CostCenter_001 (string, required) - Cost Center`s Title
    + PostOffice: 3210 (string) - Postal code
    + ManagerWorker: 0001 (string) - Manager worker ident
    + DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
    + RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident


### IOP UPDATE request (array)
+ (object)
    + Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required)
    + data (object) 
        + Code: Ulica test 2 (string, optional)
        + Notes: 3432 (string, optional)
        + Title: SI (string, optional

### CostCenter UPDATE request (array)
+ (object)
    + Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required)
    + data (object) 
        + Address: Ulica test 2 (string) - Cost Center`s address
        + BusinessUnitRegNo: 3432 (string)
        + Country: SI (string) - International code for countries
        + Ident: 001a (string) - Number for identification
        + Name: CostCenter_001a (string) - Cost Center`s Title
        + PostOffice: 3211 (string) - Postal code
        + ManagerWorker: 0001 (string) - Manager worker ident
        + DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
        + RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident

### CostOrganisationUnit GET ONE response (object)
+ Address: Ulica test 12 (string) - Cost Center`s address
+ BusinessUnitRegNo: 152 (string)
+ Country: SI (string) - International code for countries
+ Ident: 001 (string) - Number for identification
+ Name: CostCenter_001 (string) - Cost Center`s Title
+ PostOffice: 3210 (string) - Postal code
+ ManagerWorker: 0001 (string) - Manager worker ident
+ DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
+ RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident
+ Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string) - Cost center`s unique Id
 
### CostOrganisationUnit GET response (object)
+ data (array)
    + (CostOrganisationUnit GET ONE response)
+ meta (Get Meta)
        
### CostOrganisationUnit CREATE request (array) 
+ (object)
    + Address: Ulica test 12 (string) - Cost Center`s address
    + BusinessUnitRegNo: 152 (string)
    + Country: SI (string) - International code for countries
    + Ident: 001 (string) - Number for identification
    + Name: CostCenter_001 (string, required) - Cost Center`s Title
    + PostOffice: 3210 (string) - Postal code
    + ManagerWorker: 0001 (string) - Manager worker ident
    + DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
    + RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident


### CostOrganisationUnit UPDATE request (array)
+ (object)
    + Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required)
    + data (object) 
        + Address: Ulica test 2 (string) - Cost Center`s address
        + BusinessUnitRegNo: 3432 (string)
        + Country: SI (string) - International code for countries
        + Ident: 001a (string) - Number for identification
        + Name: CostCenter_001a (string) - Cost Center`s Title
        + PostOffice: 3211 (string) - Postal code
        + ManagerWorker: 0001 (string) - Manager worker ident
        + DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
        + RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident
        
### CostCarrier GET ONE response (object)
+ Code: 1 (string) - Number for identification
+ CodificationType: CostCarrier (string) - Type of codification
+ Description: SN description (string) - Cost carrier`s description
+ Id: `1259c101-c4b9-4f36-a7b4-4046d9acad22` (string) - Cost center`s unique Id
+ Title: SN - prvi (string) - Cost center`s title

### CostCarrier GET response (object)
+ data (array)
    + (CostCarrier GET ONE response)
+ meta (Get Meta)
        
### CostCarrier CREATE request (array) 
+ (object)
    + Code: 001 (string, required) - Number for identification
    + Description: It`s costcarrier (string) - Cost carrier`s description
    + Title: CostCarrier no1 (string, required) - Cost carrier`s title
    
### CostCarrier UPDATE request (array)
+ (object)
    + Id: `5b0071d0-237b-4d29-9d42-ebfd8d6bbaf9` (string, required) - Cost center`s unique Id
    + data (object)  - object with data that we want to update
        + Code: 004 (string) - Number for identification
        + Description: It`s costcarrier4 (string) - Cost carrier`s description
        + Title: CostCarrier no4 (string) - Cost carrier`s title
        
### Workplace GET response (object)
+ data (array)
    + (Workplace GET ONE response)
+ meta (Get Meta)

### Workplace GET ONE response (object)
+ Id: `092DB435-7686-4DCF-BB9A-C6E259BDDE36` (string) - Workplace`s unique Id
+ Ident: 0001 (string) - Number for identification
+ Name: Direktor (string) - Name of workplace

### Workplace CREATE request (array) 
+ (object)
    + Ident: 9111 (string) - Number for identification
    + Name: Test Workplace (string, required) - Title of workplace

### Workplace UPDATE request (array)
+ (object) - Object with id and data we want to update, there could be passed in more objects at once
    + Id: `8bf7263b-7480-4e07-8afb-8420ac3ca642` (string, required) - Workplace`s unique Id
    + data (object) 
        + Ident: 9111b (string) - Number for identification
        + Name: Test Workplaceb (string) - Title of workplace

### Bookingtype GET response (object)
+ data (array)
    + (Bookingtype GET ONE response)
+ meta (Get Meta)

### Bookingtype GET ONE response (object)
+ Id: `150875f9-3368-4a0d-a67f-b7bdb7c5b88d` (string) - Booking type`s unique Id
+ Ident: Z (string) - Number for identification
+ IsDebit: true (boolean)
+ Name: KUPCI - ZADRŽANA SREDSTVA (string) - Title of booking type

### Bookingtype CREATE request (object) 
+ (object)
    + Ident: Z (string, required) - Number for identification
    + IsDebit: 1 (number, required)
    + Name: Booking type examle (string, required) - Title of booking type

### Bookingtype UPDATE request (array)
+ (object)
    + Id: `7ef743ec-0917-4d83-a8bc-6db7f7839fee` (string, required) - Workplace`s unique Id
    + data (object) 
        + Ident: U (string) - Number for identification
        + IsDebit: 0 (number)
        + Name: Booking type examle_edit (string) - Title of booking type

### Account GET response (object)
+ data (array)
    + (Account GET ONE response)
+ meta (Get Meta)

### Account GET ONE response (object)
+ AttributeCostCarrierRequired: true (boolean) - true if Cost Carrier is required and false otherwise
+ AttributeCostCenterRequired: true (boolean) -  true if Cost Center is required and false otherwise
+ Bookable: false (boolean) - true if Account is bookable and false otherwise
+ Description: Stroški transportnih storitev (string) - Account`s description
+ ForeignDescription: Description in some foreign language (string) - Account`s description in foreign language
+ Id: `0225dafe-5351-4baa-91f6-17c383470fc1` (string) - Account`s unique Id
+ Ident: 411 (string) - Number for identification
+ Name: Stroški transportnih storitev (string) - Account`s Title
+ NameForeignName: name (string) -  Account`s Title in foreign language
+ PartnerRequired: false (boolean) - true if Partner is required and false otherwise
+ Status: status (string)
+ TransitionalAccount: 95485 (string) - Account`s Ident for transitions
+ TypeOfDocument: A (string)

### Account CREATE request (array) 
+ (object)
    + AttributeCostCarrierRequired: 1 (number) - 1 if Cost Carrier is required and 0 otherwise
    + AttributeCostCenterRequired: 1 (number) - 1 if Cost Center is required and 0 otherwise
    + Bookable: 0 (number) - 1 if Account is bookable and 0 otherwise
    + Description: Test first description (string) - Account`s description
    + FinancialInstrument: F.79 (string)
    + ForeignDescription: Test in foreign description (string) - Description in foreign language
    + Ident: 411 (string) - Number for identification
    + Name: Test first (string) - Account`s title
    + NameForeignName: Test in foreign language (string) - Account`s title in foreign language
    + PartnerRequired: 0 (number) - 1 if Partner is required and 0 otherwise
    + Sector: S.15000 (string) - Identification code for Sector
    + TransitionalAccount: 757000 (string) - Account`s Ident for transitions
    + TypeOfDocument: Z (string)

### Account UPDATE request (array)
+ (object)
    + Id: `fb13e588-d81f-4651-8b94-e69fca45731d` (string, required)
    + data (object) 
        + AttributeCostCarrierRequired: 1 (number) - 1 if Cost Carrier is required and 0 otherwise
        + AttributeCostCenterRequired: 1 (number) - 1 if Cost Center is required and 0 otherwise
        + Bookable: 0 (number) - 1 if Account is bookable and 0 otherwise
        + Description: Test first description2 (string) - Account`s description
        + FinancialInstrument: F.792 (string)
        + ForeignDescription: Test in foreign description2 (string) - Description in foreign language
        + Ident: 41122 (string) - Number for identification
        + Name: Test first2 (string) - Account`s title
        + NameForeignName: Test in foreign language2 (string) - Account`s title in foreign language
        + PartnerRequired: 1 (number) - 1 if Partner is required and 0 otherwise
        + Sector: S.150002 (string) - Identification code for Sector
        + TransitionalAccount: 7570001 (string) - Account`s Ident for transitions
        + TypeOfDocument: U (string)
        
### ProductType GET ONE response (object)
+ IDG: `dccde67e-cc40-4d44-a89f-b302c4f60cd1` (string) - Product type`s unique IDG
+ KONTO: 0890890 (string)
+ KONTO_KONS: 34234 (string)
+ NAZIV: IZDELEK (string) - Product type`s title
+ STATUS: IZD (string)
+ TIP_ART: IZD (string) - Short identification code for product type
      
### ProductType GET response (object)
+ data (array)
    + (ProductType GET ONE response)
+ meta (Get Meta)
        
### ProductType CREATE request (array) 
+ (object)
      + KONTO: 0890890
      + KONTO_KONS: 34234 (string)
      + NAZIV: IZDELEK (string, required) - Product type`s title
      + STATUS: IZD (string)
      + TIP_ART: IZD (string, required) - Short identification code for product type
    
### ProductType UPDATE request (array)
+ (object)
    + Id: `dccde67e-cc40-4d44-a89f-b302c4f60cd1` (string, required)
    + data (object) 
        + KONTO: 089111 (string)
        + KONTO_KONS: 11 (string)
        + NAZIV: Material_edit (string) - Product type`s title
        + STATUS: MAT (string)
        + TIP_ART: MAT (string) - Short identification code for product type
        
        
### CB RESPONSE DELETE VALID (object)
+ Status: true (boolean)
+ Primary_key: 000000 (string)

### Department GET ONE response (object)
+ Address: Ulica test 12 (string) - Cost Center`s address
+ BusinessUnitRegNo: 152 (string)
+ Country: SI (string) - International code for countries
+ Ident: 001 (string) - Number for identification
+ Name: CostCenter_001 (string) - Cost Center`s Title
+ PostOffice: 3210 (string) - Postal code
+ ManagerWorker: 0001 (string) - Manager worker ident
+ DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
+ RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident
+ Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string) - Cost center`s unique Id
 
### Department GET response (object)
+ data (array)
    + (Department GET ONE response)
+ meta (Get Meta)
        
### Department CREATE request (array) 
+ (object)
    + Address: Ulica test 12 (string) - Cost Center`s address
    + BusinessUnitRegNo: 152 (string)
    + Country: SI (string) - International code for countries
    + Ident: 001 (string) - Number for identification
    + Name: CostCenter_001 (string, required) - Cost Center`s Title
    + PostOffice: 3210 (string) - Postal code
    + ManagerWorker: 0001 (string) - Manager worker ident
    + DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
    + RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident

### Reminder UPDATE request (array)
+ (object)
    + Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required) - Reminder unique Id
    + data (object) 
        + Code: Ulica test 2 (string, optional)
        + Notes: 3432 (string, optional)
        + Title: SI (string, optional


### Department UPDATE request (array)
+ (object)
    + Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required)
    + data (object) 
        + Address: Ulica test 2 (string) - Cost Center`s address
        + BusinessUnitRegNo: 3432 (string)
        + Country: SI (string) - International code for countries
        + Ident: 001a (string) - Number for identification
        + Name: CostCenter_001a (string) - Cost Center`s Title
        + PostOffice: 3211 (string) - Postal code
        + ManagerWorker: 0001 (string) - Manager worker ident
        + DepartmentManagerWorker: 001 (string) - DepartmentManager worker ident
        + RegionalManagerWorker: 0001 (string) - DepartmentManager worker ident
        
### PayoutPlace GET ONE response (object)
+ Id:`28336700-753e-4775-b608-205dc2d26d2c` (string)  - Payout place`s unique Id
+ Ident: 1 (string) - Number for identification
+ Name: Test payout place (string) - Department`s Title
      
### PayoutPlace GET response (object)
+ data (array)
    + (PayoutPlace GET ONE response)
+ meta (Get Meta)
        
### PayoutPlace CREATE request (array) 
+ (object)
    + Ident: 1  (string) - Number for identification
    + Name: Test payout place  (string) - Payout place`s Title
    
### PayoutPlace UPDATE request (array)
+ (object)
    + Id: `28336700-753e-4775-b608-205dc2d26d2c` (string, required) - Payout place`s unique Id
    + data (object) 
        + Ident: 1_b (string) - Number for identification
        + Name: Test payout place 1_edited (string)  - Payout place`s Title
        
### CRMPartner GET response (object)
+ data (array)
    + (CRMPartner GET ONE response)
+ meta (Get Meta)


### CRMPartnerBankAccount GET response (object)
+ data (array)
    + (CRMPartnerBankAccount GET ONE response)
+ meta (Get Meta)

### CRMPartnerBankAccount GET ONE response (object)
+ Bank: null  (string) - Bank name
+ Model: null (string) - Bank Account model
+ AccountBlocked: 0 (number) - Account blocked
+ DataRole: null (string) - Data role
+ Swift: Test12 (string) - Swift number
+ DateOpened: 2015-10-28T00:00:00+00:00 - Bank account date opened
+ AccountNumber:  666666666 (string) - Account number
+ RawAccount:  666666666 (string) - Raw account number
+ OutstandingLiabilities: null (string) - Bank account outstanding liabilities
+ AccountDateBlocked: null - Account date blocked
+ Exposition: null (string) - Bank account exposition
+ Notes: null string) - Bank account notes
+ AccountDateClosed: null - Bank account closed date
+ Type: null (string) - Bank account type
+ PrimaryAccount: 0 (number) - Primary account
+ IdentPartner: 77766 (string) - Partner unique identification number(Ident)


### CRMPartner GET ONE response (object)
+ Address: RUDOLFSPLATZ 9999A (string) - Partner`s address
+ BusinessType: 1 (string)
+ CityName: Slovenske Konjice (string) - City`s unique Id
+ Country: SLOVENIJA (string) - Partner`s country name
+ CountryCode: SI (string) - Country`s identification number
+ Driver: John Snow (string) - Partner`s driver
+ Email: john@snow.no(string) - Partner`s email
+ ExtensionNumber: 1 (string) 
+ Fax: 0133255 (string) - Partner`s fax
+ Id: `b8ff5788-714f-47d6-af9b-4cdb5f512d73` (string) - Partner`s unique Id
+ IdCompanyNumber: 234234 (string)
+ IdPartner: 9192 (string) - Partner`s code for identification
+ IdVatNumber: SI92308763 (string)
+ LongName: SnowMobile (string) - Partner`s second long name
+ LongName2: LongName2 - Partner`s second long name
+ Mobile: 041220651 - Partner`s mobile number
+ OurShare: 20 (number)
+ Parity: 1 (string)
+ ParityLocation: RUDOLFSPLATZ 2b (string)
+ PartnerRegion: 14 (number)
+ PartnerShare: 9 (number)
+ Payer: 00000114 (string)
+ PaymentDays: 3 (number)
+ PaymentIBAN: 1515158484 (string)
+ PersonalNumber: 34234234 (string)
+ Phone: 051223554 (string)
+ PostalCode: 3210 (string) - Partner`s post office code for identification
+ PriceType: PC (string)
+ Rebate: 11 (number)
+ Sector: S.14 (string)
+ ShippingType: 1 (string)
+ ShortName: Snowmobile (string) - Partner`s short name
+ StatementType: FKD (string)
+ SuperRebate: 1 (number)
+ SuperRebateType: + (string)
+ SupplierPaymentDays: 2 (number)
+ TaxNumber: SI92308763 (string)
+ TaxPayer: 0 (number) - 1 if Partner is paying taxes and 0 otherwise
+ Town: TownName (string) - Partner`s town
+ WebSite: www.test_website.si (string) - Partner`s website
+ PersonResponsible: 0188 (string) - Worker`s unique Ident

### CRMPartnerBankAccount CREATE request (array) 
+ (object)
    + Bank: null  (string) - Bank name
    + Model: null (string) - Bank Account model
    + AccountBlocked: 0 (number) - Account blocked
    + DataRole: null (string) - Data role
    + Swift: Test12 (string) - Swift number
    + DateOpened: 2015-10-28T00:00:00+00:00 - Bank account date opened
    + AccountNumber:  666666666 (string) - Account number
    + RawAccount:  666666666 (string) - Raw account number
    + OutstandingLiabilities: null (string) - Bank account outstanding liabilities
    + AccountDateBlocked: null - Account date blocked
    + Exposition: null (string) - Bank account exposition
    + Notes: null string) - Bank account notes
    + AccountDateClosed: null - Bank account closed date
    + Type: null (string) - Bank account type
    + PrimaryAccount: 0 (number) - Primary account
    + IdentPartner: 1545 (string) - Partner unique identification number(Ident)
 
### CRMPartnerBankAccount UPDATE request (array)
+ (object)
    + AccountNumber: `66763207` (string, required) - Account number unique Id in DB
    + data (object) 
        + Bank: null  (string) - Bank name
        + Model: null (string) - Bank Account model
        + AccountBlocked: 0 (number) - Account blocked
        + DataRole: null (string) - Data role
        + Swift: Test12 (string) - Swift number
        + DateOpened: 2015-10-28T00:00:00+00:00 - Bank account date opened
        + AccountNumber:  666666666 (string) - Account number
        + RawAccount:  666666666 (string) - Raw account number
        + OutstandingLiabilities: null (string) - Bank account outstanding liabilities
        + AccountDateBlocked: null - Account date blocked
        + Exposition: null (string) - Bank account exposition
        + Notes: null string) - Bank account notes
        + AccountDateClosed: null - Bank account closed date
        + Type: null (string) - Bank account type
        + PrimaryAccount: 0 (number) - Primary account
        + IdentPartner: 77766 (string) - Partner unique identification number(Ident)
            
            
### CRMPartner CREATE request (array) 
+ (object)
    + Id: ed2fb8d2-6125-41b7-b154-a07e3b12042e (string, optional - if you leave this blank, it will automatically generate uuid for you) - Partner`s id
    + Address: RUDOLFSPLATZ 9999A (string) - Partner`s address
    + BusinessType: 1 (string)
    + CityName: Slovenske Konjice (string) - City`s identification code
    + CountryCode: SI (string) - Country`s identification code
    + Driver: John Snow (string) - Partner`s driver name
    + Email: john@snow.no(string) - Partner`s email
    + ExtensionNumber: 1 (string) 
    + Fax: 0133255 (string) - Partner`s fax number
    + IdCompanyNumber: 234234 (string)
    + IdPartner: 9192 (string, required) - Partner`s code for identification
    + IdVatNumber: SI92308763 (string)
    + LongName: SnowMobile (string, required) - Partner`s second long name
    + LongName2: LongName2(string) - Partner`s second long name
    + Mobile: 041220651(number) - Partner`s mobile number
    + OurShare: 20 (number)
    + Parity: 1 (string)
    + ParityLocation: RUDOLFSPLATZ 2b (string)
    + PartnerRegion: 14 (number)
    + PartnerShare: 9 (number)
    + Payer: 00000114 (string)
    + PaymentDays: 3 (number)
    + PaymentIBAN: 1515158484 (string)
    + PersonalNumber: 34234234 (string)
    + Phone: 051223554 (string)
    + PostalCode: 3210 (string) - Post office`s identification number - Ident
    + PriceType: PC (string) - Type of price
    + Rebate: 11 (number)
    + Sector: S.14 (string)
    + ShippingType: 1 (string)
    + ShortName: Snowmobile (string, required) - Partner`s short name
    + StatementType: FKD (string)
    + SuperRebate: 1 (number)
    + SuperRebateType: + (string)
    + SupplierPaymentDays: 2 (number)
    + TaxNumber: SI92308763 (string)
    + TaxPayer: 0 (string) - 1 if Partner is paying taxes and 0 otherwise
    + Town: TownName (string) - Partner`s town
    + WebSite: www.test_website.si (string) - Partner`s website
    + PersonResponsible: 0188 (string) - Worker`s unique Ident
    
### CRMPartner UPDATE request (array)
+ (object)
    + Id: `66763207` (string, required) - Partner`s identification code- in DB as Id
    + data (object) 
        + Address: RUDOLFSPLATZ 9999A (string) - Partner`s address
        + BusinessType: 1 (string)
        + CityName: Slovenske Konjice (string) - City`s identification code
        + CountryCode: SI (string) - Country`s identification code
        + Driver: John Snow (string) - Partner`s driver
        + Email: john@snow.no - Partner`s email
        + ExtensionNumber: 1 (string) 
        + Fax: 0133255 (string) - Partner`s fax
        + IdCompanyNumber: 234234 (string)
        + IdPartner: 9192 (string, required) - Partner`s code for identification
        + IdVatNumber: SI92308763 (string)
        + LongName: SnowMobile (string, required) - Partner`s second long name
        + LongName2: LongName2 - Partner`s second long name
        + Mobile: 041220651 - Partner`s mobile number
        + OurShare: 20 (number)
        + Parity: 1 (string)
        + ParityLocation: RUDOLFSPLATZ 2b (string)
        + PartnerRegion: 14 (number)
        + PartnerShare: 9 (number)
        + Payer: 00000114 (string)
        + PaymentDays: 3 (number)
        + PaymentIBAN: 1515158484 (string)
        + PersonalNumber: 34234234 (string)
        + Phone: 051223554 (string)
        + PostalCode: 3210 (string) - Post office`s identification number - Ident
        + PriceType: PC (string)
        + Rebate: 11 (number)
        + Sector: S.14 (string)
        + ShippingType: 1 (string)
        + ShortName: Snowmobile (string, required) - Partner`s short name
        + StatementType: FKD (string)
        + SuperRebate: 1 (number)
        + SuperRebateType: + (string)
        + SupplierPaymentDays: 2 (number)
        + TaxNumber: SI92308763 (string)
        + TaxPayer: 0 (string) - 1 if Partner is paying taxes and 0 otherwise
        + Town: TownName (string) - Partner`s town
        + WebSite: www.test_website.si (string) - Partner`s website
        + PersonResponsible: 0188 (string) - Worker`s unique Ident

### CB RESPONSE VALID (object)
+ Errors (array)
+ Success (array)
    + (object)
        + Object num: 1(number) - Number of data object to specify which are successful or not
        + Primary_key: 123456 (string) - Unique identification number which can be used in GET api
        + Status: true (boolean) - true if success and false if not
        
### CB RESPONSE INVALID (object)
+ Status: false (boolean)
+ message (array)
    + (object)
        + Object num: 1(number) - Number of data object to specify which are successful or not
        + error (array) - List of errors
            + description (string) - Description of error
            
### Get ONE Email (object)
+ Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16` (string, required) - Email`s unique Id
+ Code: code (string, required) - Number for identification
+ Notes:  notes, (string, required) - Notes
+ Title: Title (string, required) - Title
           
            
### Get Full Email (object)
+ data(array)
    + (Get ONE Email)
+ meta (Get Meta)

### EMAIL UPDATE request (array)
+ (object)
    + Id: `05f2a560-c9a3-45b6-8e99-f5ec18e49fdd` (string, required) - Email`s unique Id
    + data (object) 
        + Code: Ulica test 2 (string, optional) - Number for identification
        + Notes: 3432 (string, optional) - Notes
        + Title: SI (string, optional) - Title
        
### Create EMAIL Few (array)
+ (Create/Update EMAIL)

### Create/Update EMAIL (object)
+ Code: Code (string, required) - Number for identification
+ Notes: Notes (string) - Notes
+ Title: Title (string, required) - Title

### HRMClass GET ONE response (object)
+ Description: test (string) - HRM Class description
+ Id: `98ffe32a-b2f1-413a-99a1-51d28e0c11f0` (string) - HRM Class unique Id
+ Ident: 22 (string) - Number for identification
+ Name: asdasdd (string) - HRM Class Name
+ NumberOfPointsAmount: 2 (string)
+ ValidFrom: `2015-09-30T22:00:00+00:00` (string) - Valid from date
+ ValidTo: `2016-09-30T22:00:00+00:00` - Valid to date

### HRMClass GET response (object)
+ data (array)
    + (HRMClass GET ONE response)
+ meta (Get Meta)

### HRMClass CREATE request (array) 
+ (object)
    + Description: Description test (string) - HRM Class description
    + Ident: 11 (string) - Number for identification
    + Name: test-11 (string, required) - HRM Class Name
    + NumberOfPointsAmount: 31.11 (number)
    + ValidFrom: `2015-09-30T22:00:00+00:00`  (string) - Valid from date
    + ValidTo: `2016-09-30T22:00:00+00:00` (string) - Valid to date
        
### HRMClass UPDATE request (array)
+ (object)
    + Ident: `11`(string) - HRM Class identification number
    + data (object)
        + Description: Description test (string) - HRM Class description
        + Ident: 11 (string) - Number for identification
        + Name: test-11 (string, required) - HRM Class Name
        + NumberOfPointsAmount: 31.11 (number)
        + ValidFrom: `2015-09-30T22:00:00+00:00`  (string) - Valid from date
        + ValidTo: `2016-09-30T22:00:00+00:00` (string) - Valid to date
        

### HRMCBWorker UPDATE request (array)
+ (object)
    + Ident: `0001`(string, required) - CB Worker`s unique Ident
    + data (object) 
        + TaxCode: `12345678`(string, required) - CB Worker`s TaxCode
        + Birthday: `2016-08-31T22:00:00+00:00` (string) - Worker birthday date
        + CellPhoneNumber: 031123123 (string) - Workers cell phone number
        + Citizenship: 0001 (string) - Citizenship
        + City: Celje (string) - Worker city
        + CostCenter: 001 (string)
        + CostCenterOrganizationalUnit: 001 (string)
        + Country: SI (string) - Worker country code
        + CountryOfBirth: SI (string) - Worker country of birth
        + Department: 001 (string) - Department
        + Email: `primoz.znidar@pro-bit.si` (string) - Worker e-mail
        + Email2: `primoz.znidar@pro-bit.si` (string) - Worker e-mail
        + EmployerType: G (string) - Worker employer type
        + ExternalRegisterCode: 001 (string)
        + FaxNumber: 031123123 (string) - Fax number
        + Firstname: Primož (string) - First name
        + Gender: M (string) - Worker gender
        + Lastname: Žnidar (string) - Last name
        + MaidenName: Lubocič (string) - Maiden name
        + MaritalStatus: 001 (string) - Worker marital status
        + Municipality: 001 (string) - Worker municipality
        + PayoutPlace: 001 (string) 
        + PersonsGroupType: 001 (string)
        + PersonsSubGroupType: 001 (string)
        + PhoneNumber: 031123123 (string) - Worker phone number
        + PlaceOfBirth: Celje (string) - Worker place of birth
        + PostOffice: 3214 (string) - Post office
        + Prefix: gdc (string) - Worker prefix
        + RegistrationNumber: 4562133654 (string)
        + ResidentStatus: 001 (string)
        + SingleParent: 1 (number) - Worker single parent status
        + Street: null (string) - Worker address street
        + User: primozz@pb5 (string) - Worker username
        + Bank1: 0001 (string) - Worker bank 1 ident
        + Bank2: 0001 (string) - Worker bank 2 ident
        + Bank3: 0001 (string) - Worker bank 3 ident
        + IBAN1: 4322345676543 (string) - Worker IBAN 1
        + IBAN2: 4322345676543 (string) - Worker IBAN 2
        + IBAN3: 4322345676543 (string) - Worker IBAN 3
        + Bank1Precent: 100 (number) - Worker bank1 percent
        + Bank2Precent: 100 (number) - Worker bank2 percent
        + Bank3Precent: 100 (number) - Worker bank3 percent
        + TypeOfPayment: 01 (string) - Worker type of payment(gross,net,hours,paygrade)
        + CountryTemporary: SI (string) - Worker temporary country code
        + MunicipalityTemporary: 001 (string) - Worker temporary municipality code
        + PostOfficeTemporary: 3000 (string) - Worker temporary postoffice code
        + CityTemporary: 0001 (string) - Worker temporary city code
        + StreetTemporary: Ulica (string) - Worker temporary street 
        + YearOfRefund: 2015 (string) - Worker year of refund
        + LastYearOfWorkForRefund: 10.45 (number) - Worker last year of refund
        + LastMonthForWorkFund: 12.55 (number) - Worker last month of refund
        + PaymentValue: 1200.98 (number) - Worker salary
        + DocumentPass: 1234 (string) - Password for documents
        + ActiveRecord: 1 (string) - Worker ActiveRecord, values(1,0)
        + DegreeOfPhysicalImpairment: '001' (string) - DegreeOfPhysicalImpairment
        + PhysicalImpairment: 1 (number) - PhysicalImpairment(1 or 0)

### HRMCBWorker CREATE request (array) 
+ (object)
    + Ident: `0001`(string, required) - CB Worker`s Ident
    + TaxCode: `12345678`(string, required) - CB Worker`s TaxCode
    + Birthday: `2016-08-31T22:00:00+00:00` (string) - Worker birthday date
    + CellPhoneNumber: 031123123 (string) - Workers cell phone number
    + Citizenship: 0001 (string) - Citizenship
    + City: Celje (string) - Worker city
    + CostCenter: 001 (string)
    + CostCenterOrganizationalUnit: 001 (string)
    + Country: SI (string) - Worker country code
    + CountryOfBirth: SI (string) - Worker country of birth
    + Department: 001 (string) - Department
    + Email: `primoz.znidar@pro-bit.si` (string) - Worker e-mail
    + Email2: `primoz.znidar@pro-bit.si` (string) - Worker e-mail
    + EmployerType: G (string) - Worker employer type
    + ExternalRegisterCode: 001 (string)
    + FaxNumber: 031123123 (string) - Fax number
    + Firstname: Primož (string) - First name
    + Gender: M (string) - Worker gender
    + Lastname: Žnidar (string) - Last name
    + MaidenName: Lubocič (string) - Maiden name
    + MaritalStatus: 001 (string) - Worker marital status
    + Municipality: 001 (string) - Worker municipality
    + PayoutPlace: 001 (string) 
    + PersonsGroupType: 001 (string)
    + PersonsSubGroupType: 001 (string)
    + PhoneNumber: 031123123 (string) - Worker phone number
    + PlaceOfBirth: Celje (string) - Worker place of birth
    + PostOffice: 3214 (string) - Post office
    + Prefix: gdc (string) - Worker prefix
    + RegistrationNumber: 4562133654 (string)
    + ResidentStatus: 001 (string)
    + SingleParent: 1 (number) - Worker single parent status
    + Street: null (string) - Worker address street
    + User: primozz@pb5 (string) - Worker username
    + Bank1: 0001 (string) - Worker bank 1 ident
    + Bank2: 0001 (string) - Worker bank 2 ident
    + Bank3: 0001 (string) - Worker bank 3 ident
    + IBAN1: 4322345676543 (string) - Worker IBAN 1
    + IBAN2: 4322345676543 (string) - Worker IBAN 2
    + IBAN3: 4322345676543 (string) - Worker IBAN 3
    + Bank1Precent: 100 (number) - Worker bank1 percent
    + Bank2Precent: 100 (number) - Worker bank2 percent
    + Bank3Precent: 100 (number) - Worker bank3 percent
    + TypeOfPayment: 01 (string) - Worker type of payment(gross,net,hours,paygrade)
    + CountryTemporary: SI (string) - Worker temporary country code
    + MunicipalityTemporary: 001 (string) - Worker temporary municipality code
    + PostOfficeTemporary: 3000 (string) - Worker temporary postoffice code
    + CityTemporary: 0001 (string) - Worker temporary city code
    + StreetTemporary: Ulica (string) - Worker temporary street 
    + YearOfRefund: 2015 (string) - Worker year of refund
    + LastYearOfWorkForRefund: 10.45 (number) - Worker last year of refund
    + LastMonthForWorkFund: 12.55 (number) - Worker last month of refund
    + PaymentValue: 1200.98 (number) - Worker salary
    + DocumentPass: 1234 (string) - Password for documents
    + ActiveRecord: 1 (string) - Worker ActiveRecord, values(1,0)
    + DegreeOfPhysicalImpairment: '001' (string) - DegreeOfPhysicalImpairment
    + PhysicalImpairment: 1 (number) - PhysicalImpairment(1 or 0)
    
### HRMCBWorker GET ONE response (object)
+ Ident: `0001`(string, required) - CB Worker`s Ident
+ TaxCode: `12345678`(string, required) - CB Worker`s TaxCode
+ Birthday: `2016-08-31T22:00:00+00:00` (string) - Worker birthday date
+ CellPhoneNumber: 031123123 (string) - Workers cell phone number
+ Citizenship: 0001 (string) - Citizenship
+ City: Celje (string) - Worker city
+ CostCenter: 001 (string)
+ CostCenterOrganizationalUnit: 001 (string)
+ Country: SI (string) - Worker country code
+ CountryOfBirth: SI (string) - Worker country of birth
+ Department: 001 (string) - Department
+ Email: `primoz.znidar@pro-bit.si` (string) - Worker e-mail
+ Email2: `primoz.znidar@pro-bit.si` (string) - Worker e-mail
+ EmployerType: G (string) - Worker employer type
+ ExternalRegisterCode: 001 (string)
+ FaxNumber: 031123123 (string) - Fax number
+ Firstname: Primož (string) - First name
+ Gender: M (string) - Worker gender
+ Lastname: Žnidar (string) - Last name
+ MaidenName: Lubocič (string) - Maiden name
+ MaritalStatus: 001 (string) - Worker marital status
+ Municipality: 001 (string) - Worker municipality
+ PayoutPlace: 001 (string) 
+ PersonsGroupType: 001 (string)
+ PersonsSubGroupType: 001 (string)
+ PhoneNumber: 031123123 (string) - Worker phone number
+ PlaceOfBirth: Celje (string) - Worker place of birth
+ PostOffice: 3214 (string) - Post office
+ Prefix: gdc (string) - Worker prefix
+ RegistrationNumber: 4562133654 (string)
+ ResidentStatus: 001 (string)
+ SingleParent: 1 (number) - Worker single parent status
+ Street: null (string) - Worker address street
+ User: primozz@pb5 (string) - Worker username
+ Bank1: 0001 (string) - Worker bank 1 ident
+ Bank2: 0001 (string) - Worker bank 2 ident
+ Bank3: 0001 (string) - Worker bank 3 ident
+ IBAN1: 4322345676543 (string) - Worker IBAN 1
+ IBAN2: 4322345676543 (string) - Worker IBAN 2
+ IBAN3: 4322345676543 (string) - Worker IBAN 3
+ Bank1Precent: 100 (number) - Worker bank1 percent
+ Bank2Precent: 100 (number) - Worker bank2 percent
+ Bank3Precent: 100 (number) - Worker bank3 percent
+ TypeOfPayment: 01 (string) - Worker type of payment(gross,net,hours,paygrade)
+ CountryTemporary: SI (string) - Worker temporary country code
+ MunicipalityTemporary: 001 (string) - Worker temporary municipality code
+ PostOfficeTemporary: 3000 (string) - Worker temporary postoffice code
+ CityTemporary: 0001 (string) - Worker temporary city code
+ StreetTemporary: Ulica (string) - Worker temporary street 
+ YearOfRefund: 2015 (string) - Worker year of refund
+ LastYearOfWorkForRefund: 10.45 (number) - Worker last year of refund
+ LastMonthForWorkFund: 12.55 (number) - Worker last month of refund
+ PaymentValue: 1200.98 (number) - Worker salary
+ DocumentPass: 1234 (string) - Password for documents
+ ActiveRecord: 1 (string) - Worker ActiveRecord, values(1,0)
+ DegreeOfPhysicalImpairment: '001' (string) - DegreeOfPhysicalImpairment
+ PhysicalImpairment: 1 (number) - PhysicalImpairment(1 or 0)

### HRMCBWorker GET response (object)
+ data (array)
    + (HRMCBWorker GET ONE response)
+ meta (Get Meta)


### HRMWorkerEmployment UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) - Id
    + data (object) 
        + StartWorking: `2016-08-31T22:00:00+00:00` (string) - Worker start working date
        + DateOfEvent: `2016-08-31T22:00:00+00:00` (string) - Worker date of event date -usually same as startworking
        + DateOfTerminationOfEmployment: `2016-08-31T22:00:00+00:00` (string) - Date of termination employment
        + HoursPerWeek: 40 (number) - Hours per week
        + NumberOfWorkingDays: 5 (number) - Number of working days
        + WorkWeekTime: 8 (number) - Hours per day
        + OtherEmployerName: Testno podjetje (string) - Other employer name
        + OtherEmployerHours: 40 (number) - Other employer hours
        + EmployedAfter1242013: 1 (number) - employed after 12.4.2013 1 or 0
        + Worker: 0001 (string) - Worker ident
        + TypeOfEmployment: 001 (string) - Type of employment code
        + TypeOfContract: 001 (string) - Type of contract code
        + WorkPlace1: 001 (string) - Work place ident
        + OtherEmployer: G (string) - Type of other employer
        + Worker: 0001 (string, required) - Workers ident
        + EndDateOfEvent: `2016-08-31T22:00:00+00:00` (string) - End date of event
        + DateChangedHoursPerWeekYearsOfService: `2016-08-31T22:00:00+00:00` (string) - Date Changed Hours Per Week YearsOfService
        + ParenthoodFrom: `2016-08-31T22:00:00+00:00` (string) - ParenthoodFrom
        + ParenthoodTo: `2016-08-31T22:00:00+00:00` (string) - ParenthoodTo
        + DisabilityFrom: `2016-08-31T22:00:00+00:00` (string) - DisabilityFrom
        + DisabilityTo: `2016-08-31T22:00:00+00:00` (string) - DisabilityTo
        + TryoutPeriodFrom: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodFrom
        + TryoutPeriodTo: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodTo
        + TryoutPeriodExamDate: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodExamDate
        + DateOfTerminationOfEmploymentSuggestion: `2016-08-31T22:00:00+00:00` (string) - DateOfTerminationOfEmploymentSuggestion
        + DescriptionOfEvent: `Event description` (string) - Event description
        + StaffPlan: 1 (string) - StaffPlan
        + FullYearsOfService: 1 (number) - FullYearsOfService
        + CompetitionClause: 1 (number) - CompetitionClause
        + OtherEmployerPublicSector: 1 (number) - OtherEmployerPublicSector
        + OtherEmployer2PublicSector: 1 (number) - OtherEmployer2PublicSector
        + Parenthood: 1 (number) - Parenthood
        + Disability: 1 (number) - Disability
        + Benefits: 1 (number) - Benefits
        + Trainee: 1 (number) - Trainee
        + TryoutPeriodExamPass: 1 (number) - TryoutPeriodExamPass
        + OtherEmployerName2: `Firm` (string) - OtherEmployerName2
        + BenefitsPolicy: `Some text` (string) - BenefitsPolicy
        + ReasonForLeavingDescription: `Some text` (string) - ReasonForLeavingDescription
        + HoursPerWeekForYearsOfService: 40 (number) - HoursPerWeekForYearsOfService
        + OtherEmployerHours2: 40 (number) - OtherEmployerHours2
        + InsuranceBase: 001 (string) - InsuranceBase
        + ReasonForEmployment: 001 (string) - ReasonForEmployment
        + TypeOfWorkingTime: 001 (string) - TypeOfWorkingTime
        + ShiftWork: 1 (string) - ShiftWork
        + FailureTime: 001 (string) - FailureTime
        + BenefitsDuration: 001 (string) - BenefitsDuration
        + DurationOfTraineeship: 001 (string) - DurationOfTraineeship
        + ModesOfTerminationOfEmployment: 001 (string) - ModesOfTerminationOfEmployment
        + ZZZSCancellation: 01 (string) - ZZZSCancellation
        + WorkPlace2: 001 (string) - WorkPlace2
        + WorkPlace3: 001 (string) - WorkPlace3
        + WorkPlace4: 001 (string) - WorkPlace4
        + WorkPlace1Grade: 001 (string) - WorkPlace1Grade
        + WorkPlace2Grade: 001 (string) - WorkPlace2Grade
        + WorkPlace3Grade: 001 (string) - WorkPlace3Grade
        + WorkPlace4Grade: 001 (string) - WorkPlace4Grade
        + TypeOfEmployment2: 001 (string) - TypeOfEmployment2
        + TypeOfEmployment3: 001 (string) - TypeOfEmployment3
        + TypeOfEmployment4: 001 (string) - TypeOfEmployment4
        + Workplace1TypeOfReallocation: 001 (string) - Workplace1TypeOfReallocation
        + Workplace2TypeOfReallocation: 001 (string) - Workplace2TypeOfReallocation
        + Workplace3TypeOfReallocation: 001 (string) - Workplace3TypeOfReallocation
        + Workplace4TypeOfReallocation: 001 (string) - Workplace4TypeOfReallocation
        + WorkPlace1Percent: 100 (number) - WorkPlace1Percent
        + WorkPlace2Percent: 100 (number) - WorkPlace2Percent
        + WorkPlace3Percent: 100 (number) - WorkPlace3Percent
        + WorkPlace4Percent: 100 (number) - WorkPlace4Percent
        + WorkPlace1ContractNumber: 100 (string) - WorkPlace1ContractNumber
        + WorkPlace2ContractNumber: 100 (string) - WorkPlace2ContractNumber
        + WorkPlace3ContractNumber: 100 (string) - WorkPlace3ContractNumber
        + WorkPlace4ContractNumber: 100 (string) - WorkPlace4ContractNumber
        + WorkPlace1FactorAdd: 1 (number) - WorkPlace1FactorAdd
        + WorkPlace2FactorAdd: 1 (number) - WorkPlace2FactorAdd
        + WorkPlace3FactorAdd: 1 (number) - WorkPlace3FactorAdd
        + WorkPlace4FactorAdd: 1 (number) - WorkPlace4FactorAdd
        + WorkPlace1AdditionalTasks: Some text (string) - WorkPlace1AdditionalTasks
        + WorkPlace2AdditionalTasks: Some text (string) - WorkPlace2AdditionalTasks
        + WorkPlace3AdditionalTasks: Some text (string) - WorkPlace3AdditionalTasks
        + WorkPlace4AdditionalTasks: Some text (string) - WorkPlace4AdditionalTasks
        + EmployedAfter12420132: 1 (number) - EmployedAfter12420132
        + EmployedAfter12420133: 1 (number) - EmployedAfter12420133
        + EmployedAfter12420134: 1 (number) - EmployedAfter12420134
        + WorkPlace1DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateFrom
        + WorkPlace2DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateFrom
        + WorkPlace3DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateFrom
        + WorkPlace4DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateFrom
        + WorkPlace1DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateTo
        + WorkPlace2DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateTo
        + WorkPlace3DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateTo
        + WorkPlace4DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateTo
        + WorkPlace1DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateOfPossiblePromotion
        + WorkPlace2DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateOfPossiblePromotion
        + WorkPlace3DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateOfPossiblePromotion
        + WorkPlace4DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateOfPossiblePromotion
        + Workplace1DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace1DateofPromotion
        + Workplace2DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace2DateofPromotion
        + Workplace3DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace3DateofPromotion
        + Workplace4DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace4DateofPromotion
        + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
        + DateFrom2: `2016-08-31T22:00:00+00:00` (string) - DateFrom2
        + DateFrom3: `2016-08-31T22:00:00+00:00` (string) - DateFrom3
        + DateFrom4: `2016-08-31T22:00:00+00:00` (string) - DateFrom4
        + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
        + DateTo2: `2016-08-31T22:00:00+00:00` (string) - DateTo2
        + DateTo3: `2016-08-31T22:00:00+00:00` (string) - DateTo3
        + DateTo4: `2016-08-31T22:00:00+00:00` (string) - DateTo4
        + WorkPlace1DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateOfContract
        + WorkPlace2DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateOfContract
        + WorkPlace3DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateOfContract
        + WorkPlace4DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateOfContract
        + TypeOfEvent: 001 (string) - TypeOfEvent
        + ActiveRecord: 1 (number) - Employment ActiveRecord, values(1,0)
        + Active: 1 (number) - Employment Active, values(1,0)


### HRMWorkerEmployment CREATE request (array) 
+ (object)
    + StartWorking: `2016-08-31T22:00:00+00:00` (string) - Worker start working date
    + DateOfEvent: `2016-08-31T22:00:00+00:00` (string) - Worker date of event date -usually same as startworking
    + DateOfTerminationOfEmployment: `2016-08-31T22:00:00+00:00` (string) - Date of termination employment
    + HoursPerWeek: 40 (number) - Hours per week
    + NumberOfWorkingDays: 5 (number) - Number of working days
    + WorkWeekTime: 8 (number) - Hours per day
    + OtherEmployerName: Testno podjetje (string) - Other employer name
    + OtherEmployerHours: 40 (number) - Other employer hours
    + EmployedAfter1242013: 1 (number) - employed after 12.4.2013 1 or 0
    + Worker: 0001 (string) - Worker ident
    + TypeOfEmployment: 001 (string) - Type of employment code
    + TypeOfContract: 001 (string) - Type of contract code
    + WorkPlace1: 001 (string) - Work place ident
    + OtherEmployer: G (string) - Type of other employer
    + Worker: 0001 (string, required) - Workers ident
    + EndDateOfEvent: `2016-08-31T22:00:00+00:00` (string) - End date of event
    + DateChangedHoursPerWeekYearsOfService: `2016-08-31T22:00:00+00:00` (string) - Date Changed Hours Per Week YearsOfService
    + ParenthoodFrom: `2016-08-31T22:00:00+00:00` (string) - ParenthoodFrom
    + ParenthoodTo: `2016-08-31T22:00:00+00:00` (string) - ParenthoodTo
    + DisabilityFrom: `2016-08-31T22:00:00+00:00` (string) - DisabilityFrom
    + DisabilityTo: `2016-08-31T22:00:00+00:00` (string) - DisabilityTo
    + TryoutPeriodFrom: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodFrom
    + TryoutPeriodTo: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodTo
    + TryoutPeriodExamDate: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodExamDate
    + DateOfTerminationOfEmploymentSuggestion: `2016-08-31T22:00:00+00:00` (string) - DateOfTerminationOfEmploymentSuggestion
    + DescriptionOfEvent: `Event description` (string) - Event description
    + StaffPlan: 1 (string) - StaffPlan
    + FullYearsOfService: 1 (number) - FullYearsOfService
    + CompetitionClause: 1 (number) - CompetitionClause
    + OtherEmployerPublicSector: 1 (number) - OtherEmployerPublicSector
    + OtherEmployer2PublicSector: 1 (number) - OtherEmployer2PublicSector
    + Parenthood: 1 (number) - Parenthood
    + Disability: 1 (number) - Disability
    + Benefits: 1 (number) - Benefits
    + Trainee: 1 (number) - Trainee
    + TryoutPeriodExamPass: 1 (number) - TryoutPeriodExamPass
    + OtherEmployerName2: `Firm` (string) - OtherEmployerName2
    + BenefitsPolicy: `Some text` (string) - BenefitsPolicy
    + ReasonForLeavingDescription: `Some text` (string) - ReasonForLeavingDescription
    + HoursPerWeekForYearsOfService: 40 (number) - HoursPerWeekForYearsOfService
    + OtherEmployerHours2: 40 (number) - OtherEmployerHours2
    + InsuranceBase: 001 (string) - InsuranceBase
    + ReasonForEmployment: 001 (string) - ReasonForEmployment
    + TypeOfWorkingTime: 001 (string) - TypeOfWorkingTime
    + ShiftWork: 1 (string) - ShiftWork
    + FailureTime: 001 (string) - FailureTime
    + BenefitsDuration: 001 (string) - BenefitsDuration
    + DurationOfTraineeship: 001 (string) - DurationOfTraineeship
    + ModesOfTerminationOfEmployment: 001 (string) - ModesOfTerminationOfEmployment
    + ZZZSCancellation: 01 (string) - ZZZSCancellation
    + WorkPlace2: 001 (string) - WorkPlace2
    + WorkPlace3: 001 (string) - WorkPlace3
    + WorkPlace4: 001 (string) - WorkPlace4
    + WorkPlace1Grade: 001 (string) - WorkPlace1Grade
    + WorkPlace2Grade: 001 (string) - WorkPlace2Grade
    + WorkPlace3Grade: 001 (string) - WorkPlace3Grade
    + WorkPlace4Grade: 001 (string) - WorkPlace4Grade
    + TypeOfEmployment2: 001 (string) - TypeOfEmployment2
    + TypeOfEmployment3: 001 (string) - TypeOfEmployment3
    + TypeOfEmployment4: 001 (string) - TypeOfEmployment4
    + Workplace1TypeOfReallocation: 001 (string) - Workplace1TypeOfReallocation
    + Workplace2TypeOfReallocation: 001 (string) - Workplace2TypeOfReallocation
    + Workplace3TypeOfReallocation: 001 (string) - Workplace3TypeOfReallocation
    + Workplace4TypeOfReallocation: 001 (string) - Workplace4TypeOfReallocation
    + WorkPlace1Percent: 100 (number) - WorkPlace1Percent
    + WorkPlace2Percent: 100 (number) - WorkPlace2Percent
    + WorkPlace3Percent: 100 (number) - WorkPlace3Percent
    + WorkPlace4Percent: 100 (number) - WorkPlace4Percent
    + WorkPlace1ContractNumber: 100 (string) - WorkPlace1ContractNumber
    + WorkPlace2ContractNumber: 100 (string) - WorkPlace2ContractNumber
    + WorkPlace3ContractNumber: 100 (string) - WorkPlace3ContractNumber
    + WorkPlace4ContractNumber: 100 (string) - WorkPlace4ContractNumber
    + WorkPlace1FactorAdd: 1 (number) - WorkPlace1FactorAdd
    + WorkPlace2FactorAdd: 1 (number) - WorkPlace2FactorAdd
    + WorkPlace3FactorAdd: 1 (number) - WorkPlace3FactorAdd
    + WorkPlace4FactorAdd: 1 (number) - WorkPlace4FactorAdd
    + WorkPlace1AdditionalTasks: Some text (string) - WorkPlace1AdditionalTasks
    + WorkPlace2AdditionalTasks: Some text (string) - WorkPlace2AdditionalTasks
    + WorkPlace3AdditionalTasks: Some text (string) - WorkPlace3AdditionalTasks
    + WorkPlace4AdditionalTasks: Some text (string) - WorkPlace4AdditionalTasks
    + EmployedAfter12420132: 1 (number) - EmployedAfter12420132
    + EmployedAfter12420133: 1 (number) - EmployedAfter12420133
    + EmployedAfter12420134: 1 (number) - EmployedAfter12420134
    + WorkPlace1DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateFrom
    + WorkPlace2DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateFrom
    + WorkPlace3DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateFrom
    + WorkPlace4DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateFrom
    + WorkPlace1DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateTo
    + WorkPlace2DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateTo
    + WorkPlace3DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateTo
    + WorkPlace4DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateTo
    + WorkPlace1DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateOfPossiblePromotion
    + WorkPlace2DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateOfPossiblePromotion
    + WorkPlace3DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateOfPossiblePromotion
    + WorkPlace4DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateOfPossiblePromotion
    + Workplace1DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace1DateofPromotion
    + Workplace2DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace2DateofPromotion
    + Workplace3DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace3DateofPromotion
    + Workplace4DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace4DateofPromotion
    + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
    + DateFrom2: `2016-08-31T22:00:00+00:00` (string) - DateFrom2
    + DateFrom3: `2016-08-31T22:00:00+00:00` (string) - DateFrom3
    + DateFrom4: `2016-08-31T22:00:00+00:00` (string) - DateFrom4
    + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
    + DateTo2: `2016-08-31T22:00:00+00:00` (string) - DateTo2
    + DateTo3: `2016-08-31T22:00:00+00:00` (string) - DateTo3
    + DateTo4: `2016-08-31T22:00:00+00:00` (string) - DateTo4
    + WorkPlace1DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateOfContract
    + WorkPlace2DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateOfContract
    + WorkPlace3DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateOfContract
    + WorkPlace4DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateOfContract
    + TypeOfEvent: 001 (string) - TypeOfEvent
    + ActiveRecord: 1 (number) - Employment ActiveRecord, values(1,0)
    + Active: 1 (number) - Employment Active, values(1,0)

### HRMWorkerEmployment GET ONE response (object)
+ StartWorking: `2016-08-31T22:00:00+00:00` (string) - Worker start working date
+ DateOfEvent: `2016-08-31T22:00:00+00:00` (string) - Worker date of event date -usually same as startworking
+ DateOfTerminationOfEmployment: `2016-08-31T22:00:00+00:00` (string) - Date of termination employment
+ HoursPerWeek: 40 (number) - Hours per week
+ NumberOfWorkingDays: 5 (number) - Number of working days
+ WorkWeekTime: 8 (number) - Hours per day
+ OtherEmployerName: Testno podjetje (string) - Other employer name
+ OtherEmployerHours: 40 (number) - Other employer hours
+ EmployedAfter1242013: 1 (number) - employed after 12.4.2013 1 or 0
+ Worker: 0001 (string) - Worker ident
+ TypeOfEmployment: 001 (string) - Type of employment code
+ TypeOfContract: 001 (string) - Type of contract code
+ WorkPlace1: 001 (string) - Work place ident
+ OtherEmployer: G (string) - Type of other employer
+ Worker: 0001 (string, required) - Workers ident
+ EndDateOfEvent: `2016-08-31T22:00:00+00:00` (string) - End date of event
+ DateChangedHoursPerWeekYearsOfService: `2016-08-31T22:00:00+00:00` (string) - Date Changed Hours Per Week YearsOfService
+ ParenthoodFrom: `2016-08-31T22:00:00+00:00` (string) - ParenthoodFrom
+ ParenthoodTo: `2016-08-31T22:00:00+00:00` (string) - ParenthoodTo
+ DisabilityFrom: `2016-08-31T22:00:00+00:00` (string) - DisabilityFrom
+ DisabilityTo: `2016-08-31T22:00:00+00:00` (string) - DisabilityTo
+ TryoutPeriodFrom: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodFrom
+ TryoutPeriodTo: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodTo
+ TryoutPeriodExamDate: `2016-08-31T22:00:00+00:00` (string) - TryoutPeriodExamDate
+ DateOfTerminationOfEmploymentSuggestion: `2016-08-31T22:00:00+00:00` (string) - DateOfTerminationOfEmploymentSuggestion
+ DescriptionOfEvent: `Event description` (string) - Event description
+ StaffPlan: 1 (string) - StaffPlan
+ FullYearsOfService: 1 (number) - FullYearsOfService
+ CompetitionClause: 1 (number) - CompetitionClause
+ OtherEmployerPublicSector: 1 (number) - OtherEmployerPublicSector
+ OtherEmployer2PublicSector: 1 (number) - OtherEmployer2PublicSector
+ Parenthood: 1 (number) - Parenthood
+ Disability: 1 (number) - Disability
+ Benefits: 1 (number) - Benefits
+ Trainee: 1 (number) - Trainee
+ TryoutPeriodExamPass: 1 (number) - TryoutPeriodExamPass
+ OtherEmployerName2: `Firm` (string) - OtherEmployerName2
+ BenefitsPolicy: `Some text` (string) - BenefitsPolicy
+ ReasonForLeavingDescription: `Some text` (string) - ReasonForLeavingDescription
+ HoursPerWeekForYearsOfService: 40 (number) - HoursPerWeekForYearsOfService
+ OtherEmployerHours2: 40 (number) - OtherEmployerHours2
+ InsuranceBase: 001 (string) - InsuranceBase
+ ReasonForEmployment: 001 (string) - ReasonForEmployment
+ TypeOfWorkingTime: 001 (string) - TypeOfWorkingTime
+ ShiftWork: 1 (string) - ShiftWork
+ FailureTime: 001 (string) - FailureTime
+ BenefitsDuration: 001 (string) - BenefitsDuration
+ DurationOfTraineeship: 001 (string) - DurationOfTraineeship
+ ModesOfTerminationOfEmployment: 001 (string) - ModesOfTerminationOfEmployment
+ ZZZSCancellation: 01 (string) - ZZZSCancellation
+ WorkPlace2: 001 (string) - WorkPlace2
+ WorkPlace3: 001 (string) - WorkPlace3
+ WorkPlace4: 001 (string) - WorkPlace4
+ WorkPlace1Grade: 001 (string) - WorkPlace1Grade
+ WorkPlace2Grade: 001 (string) - WorkPlace2Grade
+ WorkPlace3Grade: 001 (string) - WorkPlace3Grade
+ WorkPlace4Grade: 001 (string) - WorkPlace4Grade
+ TypeOfEmployment2: 001 (string) - TypeOfEmployment2
+ TypeOfEmployment3: 001 (string) - TypeOfEmployment3
+ TypeOfEmployment4: 001 (string) - TypeOfEmployment4
+ Workplace1TypeOfReallocation: 001 (string) - Workplace1TypeOfReallocation
+ Workplace2TypeOfReallocation: 001 (string) - Workplace2TypeOfReallocation
+ Workplace3TypeOfReallocation: 001 (string) - Workplace3TypeOfReallocation
+ Workplace4TypeOfReallocation: 001 (string) - Workplace4TypeOfReallocation
+ WorkPlace1Percent: 100 (number) - WorkPlace1Percent
+ WorkPlace2Percent: 100 (number) - WorkPlace2Percent
+ WorkPlace3Percent: 100 (number) - WorkPlace3Percent
+ WorkPlace4Percent: 100 (number) - WorkPlace4Percent
+ WorkPlace1ContractNumber: 100 (string) - WorkPlace1ContractNumber
+ WorkPlace2ContractNumber: 100 (string) - WorkPlace2ContractNumber
+ WorkPlace3ContractNumber: 100 (string) - WorkPlace3ContractNumber
+ WorkPlace4ContractNumber: 100 (string) - WorkPlace4ContractNumber
+ WorkPlace1FactorAdd: 1 (number) - WorkPlace1FactorAdd
+ WorkPlace2FactorAdd: 1 (number) - WorkPlace2FactorAdd
+ WorkPlace3FactorAdd: 1 (number) - WorkPlace3FactorAdd
+ WorkPlace4FactorAdd: 1 (number) - WorkPlace4FactorAdd
+ WorkPlace1AdditionalTasks: "Some text" (string) - WorkPlace1AdditionalTasks
+ WorkPlace2AdditionalTasks: "Some text" (string) - WorkPlace2AdditionalTasks
+ WorkPlace3AdditionalTasks: "Some text" (string) - WorkPlace3AdditionalTasks
+ WorkPlace4AdditionalTasks: "Some text" (string) - WorkPlace4AdditionalTasks
+ EmployedAfter12420132: 1 (number) - EmployedAfter12420132
+ EmployedAfter12420133: 1 (number) - EmployedAfter12420133
+ EmployedAfter12420134: 1 (number) - EmployedAfter12420134
+ WorkPlace1DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateFrom
+ WorkPlace2DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateFrom
+ WorkPlace3DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateFrom
+ WorkPlace4DateFrom: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateFrom
+ WorkPlace1DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateTo
+ WorkPlace2DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateTo
+ WorkPlace3DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateTo
+ WorkPlace4DateTo: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateTo
+ WorkPlace1DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateOfPossiblePromotion
+ WorkPlace2DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateOfPossiblePromotion
+ WorkPlace3DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateOfPossiblePromotion
+ WorkPlace4DateOfPossiblePromotion: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateOfPossiblePromotion
+ Workplace1DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace1DateofPromotion
+ Workplace2DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace2DateofPromotion
+ Workplace3DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace3DateofPromotion
+ Workplace4DateofPromotion: `2016-08-31T22:00:00+00:00` (string) - Workplace4DateofPromotion
+ DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
+ DateFrom2: `2016-08-31T22:00:00+00:00` (string) - DateFrom2
+ DateFrom3: `2016-08-31T22:00:00+00:00` (string) - DateFrom3
+ DateFrom4: `2016-08-31T22:00:00+00:00` (string) - DateFrom4
+ DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
+ DateTo2: `2016-08-31T22:00:00+00:00` (string) - DateTo2
+ DateTo3: `2016-08-31T22:00:00+00:00` (string) - DateTo3
+ DateTo4: `2016-08-31T22:00:00+00:00` (string) - DateTo4
+ TypeOfEvent: 001 (string) - TypeOfEvent
+ ActiveRecord: 1 (number) - Employment ActiveRecord, values(1,0)
+ Active: 1 (number) - Employment Active, values(1,0)
+ WorkPlace1DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace1DateOfContract
+ WorkPlace2DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace2DateOfContract
+ WorkPlace3DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace3DateOfContract
+ WorkPlace4DateOfContract: `2016-08-31T22:00:00+00:00` (string) - WorkPlace4DateOfContract

### HRMWorkerEmployment GET response (object)
+ data (array)
    + (HRMWorkerEmployment GET ONE response)
+ meta (Get Meta)



### HRMWorkerVacation UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) - Id
    + data (object) 
        + VacationSum: 10 (number) - Worker vacation left - this and last year
        + VacationLeft: 10 (number) - Worker vacation left this year
        + VacationUsed: 10 (number) - Worker vacation used this year
        + VacationOldLeft: 10 (number) - Worker vacation old left
        + VacationOld: 10 (number) - VacationOld
        + Vacation: 10 (number) - Vacation
        + VacationUsedAnotherEmployer: 10 (number) - VacationUsedAnotherEmployer
        + VacationProportionDays: 10 (number) - VacationProportionDays
        + VacationProportionMonths: 10 (number) - VacationProportionMonths
        + VacationProportion: 10 (number) - VacationProportion
        + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
        + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
        + Worker: 0001 (string, required) - Workers ident



### HRMWorkerVacation CREATE request (array) 
+ (object)
    + VacationSum: 10 (number) - Worker vacation left - this and last year
    + VacationLeft: 10 (number) - Worker vacation left this year
    + VacationUsed: 10 (number) - Worker vacation used this year
    + VacationOldLeft: 10 (number) - Worker vacation old left
    + VacationOld: 10 (number) - VacationOld
    + Vacation: 10 (number) - Vacation
    + VacationUsedAnotherEmployer: 10 (number) - VacationUsedAnotherEmployer
    + VacationProportionDays: 10 (number) - VacationProportionDays
    + VacationProportionMonths: 10 (number) - VacationProportionMonths
    + VacationProportion: 10 (number) - VacationProportion
    + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
    + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
    + Worker: 0001 (string, required) - Workers ident

### HRMWorkerVacation GET ONE response (object)
+ VacationSum: 10 (number) - Worker vacation left - this and last year
+ VacationLeft: 10 (number) - Worker vacation left this year
+ VacationUsed: 10 (number) - Worker vacation used this year
+ VacationOldLeft: 10 (number) - Worker vacation old left
+ VacationOld: 10 (number) - VacationOld
+ Vacation: 10 (number) - Vacation
+ VacationUsedAnotherEmployer: 10 (number) - VacationUsedAnotherEmployer
+ VacationProportionDays: 10 (number) - VacationProportionDays
+ VacationProportionMonths: 10 (number) - VacationProportionMonths
+ VacationProportion: 10 (number) - VacationProportion
+ DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
+ DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
+ Worker: 0001 (string, required) - Workers ident

### HRMWorkerVacation GET response (object)
+ data (array)
    + (HRMWorkerVacation GET ONE response)
+ meta (Get Meta)



### HRMWorkerCalculatedEmployment UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) -  Id
    + data (object) 
        + TotalActualYearsOfServiceOnDate: 10 (number)
        + TotalActualMonthsOfServiceOnDate: 10 (number)
        + TotalActualDaysOfServiceOnDate: 10 (number)
        + TotalActualYearsEmploymentInFirmOnDate: 10 (number)
        + TotalActualMonthsEmploymentInFirmOnDate: 10 (number)
        + TotalActualDaysEmploymentInFirmOnDate: 10 (number)
        + TotalActualYearsOfPastEmployment: 10 (number)
        + TotalActualMonthsOfPastEmployment: 10 (number)
        + TotalActualDaysOfPastEmployment: 10 (number)
        + ActualYearsOfPastEmploymentInFirm: 10 (number)
        + ActualMonthsOfPastEmploymentInFirm: 10 (number)
        + ActualDaysOfPastEmploymentInFirm: 10 (number)
        + PensionYearsOfPastEmploymentInFirm: 10 (number)
        + PensionMonthsOfPastEmploymentInFirm: 10 (number)
        + PensionDaysOfPastEmploymentInFirm: 10 (number)
        + ActualYearsOfPastEmploymentPublicSector: 10 (number)
        + ActualMonthsOfPastEmploymentPublicSector: 10 (number)
        + ActualDaysOfPastEmploymentPublicSector: 10 (number)
        + PensionYearsOfPastEmploymentPublicSector: 10 (number)
        + PensionMonthsOfPastEmploymentPublicSector: 10 (number)
        + PensionDaysOfPastEmploymentPublicSector: 10 (number)
        + TotalPensionYearsOfPastEmployment: 10 (number)
        + TotalPensionMonthsOfPastEmployment: 10 (number)
        + TotalPensionDaysOfPastEmployment: 10 (number)
        + TotalActualYearsOfPastEmploymentFull: 10 (number)
        + TotalActualMonthsOfPastEmploymentFull: 10 (number)
        + TotalActualDaysOfPastEmploymentFull: 10 (number)
        + TotalPensionYearsOfPastEmploymentFull: 10 (number)
        + TotalPensionMonthsOfPastEmploymentFull: 10 (number)
        + TotalPensionDaysOfPastEmploymentFull: 10 (number)
        + PensionYearsOfOtherEmployment: 10 (number)
        + PensionMonthsOfOtherEmployment: 10 (number)
        + PensionDaysOfOtherEmployment: 10 (number)
        + TotalActualYearsEmploymentInFirmOnDateFull: 10 (number)
        + TotalActualMonthsEmploymentInFirmOnDateFull: 10 (number)
        + TotalActualDaysEmploymentInFirmOnDateFull: 10 (number)
        + TotalActualYearsOfPastEmploymentPublicSector: 10 (number)
        + TotalActualMonthsOfPastEmploymentPublicSector: 10 (number)
        + TotalActualDaysOfPastEmploymentPublicSector: 10 (number)
        + TotalPensionYearsOfServiceOnDate: 10 (number)
        + TotalPensionMonthsOfServiceOnDate: 10 (number)
        + TotalPensionDaysOfServiceOnDate: 10 (number)
        + TotalActualYearsOfServiceOnEndOfYear: 10 (number)
        + TotalActualMonthsOfServiceOnEndOfYear: 10 (number)
        + TotalActualDaysOfServiceOnEndOfYear: 10 (number)
        + TotalPensionYearsOfServiceOnEndOfYear: 10 (number)
        + TotalPensionMonthsOfServiceOnEndOfYear: 10 (number)
        + TotalPensionDaysOfServiceOnEndOfYear: 10 (number)
        + TotalActualYearsOfServiceOnDateFull: 10 (number)
        + TotalActualMonthsOfServiceOnDateFull: 10 (number)
        + TotalActualDaysOfServiceOnDateFull: 10 (number)
        + Worker: 0001 (string, required) - Workers ident



### HRMWorkerCalculatedEmployment CREATE request (array) 
+ (object)
    + TotalActualYearsOfServiceOnDate: 10 (number)
    + TotalActualMonthsOfServiceOnDate: 10 (number)
    + TotalActualDaysOfServiceOnDate: 10 (number)
    + TotalActualYearsEmploymentInFirmOnDate: 10 (number)
    + TotalActualMonthsEmploymentInFirmOnDate: 10 (number)
    + TotalActualDaysEmploymentInFirmOnDate: 10 (number)
    + TotalActualYearsOfPastEmployment: 10 (number)
    + TotalActualMonthsOfPastEmployment: 10 (number)
    + TotalActualDaysOfPastEmployment: 10 (number)
    + ActualYearsOfPastEmploymentInFirm: 10 (number)
    + ActualMonthsOfPastEmploymentInFirm: 10 (number)
    + ActualDaysOfPastEmploymentInFirm: 10 (number)
    + PensionYearsOfPastEmploymentInFirm: 10 (number)
    + PensionMonthsOfPastEmploymentInFirm: 10 (number)
    + PensionDaysOfPastEmploymentInFirm: 10 (number)
    + ActualYearsOfPastEmploymentPublicSector: 10 (number)
    + ActualMonthsOfPastEmploymentPublicSector: 10 (number)
    + ActualDaysOfPastEmploymentPublicSector: 10 (number)
    + PensionYearsOfPastEmploymentPublicSector: 10 (number)
    + PensionMonthsOfPastEmploymentPublicSector: 10 (number)
    + PensionDaysOfPastEmploymentPublicSector: 10 (number)
    + TotalPensionYearsOfPastEmployment: 10 (number)
    + TotalPensionMonthsOfPastEmployment: 10 (number)
    + TotalPensionDaysOfPastEmployment: 10 (number)
    + TotalActualYearsOfPastEmploymentFull: 10 (number)
    + TotalActualMonthsOfPastEmploymentFull: 10 (number)
    + TotalActualDaysOfPastEmploymentFull: 10 (number)
    + TotalPensionYearsOfPastEmploymentFull: 10 (number)
    + TotalPensionMonthsOfPastEmploymentFull: 10 (number)
    + TotalPensionDaysOfPastEmploymentFull: 10 (number)
    + PensionYearsOfOtherEmployment: 10 (number)
    + PensionMonthsOfOtherEmployment: 10 (number)
    + PensionDaysOfOtherEmployment: 10 (number)
    + TotalActualYearsEmploymentInFirmOnDateFull: 10 (number)
    + TotalActualMonthsEmploymentInFirmOnDateFull: 10 (number)
    + TotalActualDaysEmploymentInFirmOnDateFull: 10 (number)
    + TotalActualYearsOfPastEmploymentPublicSector: 10 (number)
    + TotalActualMonthsOfPastEmploymentPublicSector: 10 (number)
    + TotalActualDaysOfPastEmploymentPublicSector: 10 (number)
    + TotalPensionYearsOfServiceOnDate: 10 (number)
    + TotalPensionMonthsOfServiceOnDate: 10 (number)
    + TotalPensionDaysOfServiceOnDate: 10 (number)
    + TotalActualYearsOfServiceOnEndOfYear: 10 (number)
    + TotalActualMonthsOfServiceOnEndOfYear: 10 (number)
    + TotalActualDaysOfServiceOnEndOfYear: 10 (number)
    + TotalPensionYearsOfServiceOnEndOfYear: 10 (number)
    + TotalPensionMonthsOfServiceOnEndOfYear: 10 (number)
    + TotalPensionDaysOfServiceOnEndOfYear: 10 (number)
    + TotalActualYearsOfServiceOnDateFull: 10 (number)
    + TotalActualMonthsOfServiceOnDateFull: 10 (number)
    + TotalActualDaysOfServiceOnDateFull: 10 (number)
    + Worker: 0001 (string, required) - Workers ident

    
### HRMWorkerCalculatedEmployment GET ONE response (object)
+ TotalActualYearsOfServiceOnDate: 10 (number)
+ TotalActualMonthsOfServiceOnDate: 10 (number)
+ TotalActualDaysOfServiceOnDate: 10 (number)
+ TotalActualYearsEmploymentInFirmOnDate: 10 (number)
+ TotalActualMonthsEmploymentInFirmOnDate: 10 (number)
+ TotalActualDaysEmploymentInFirmOnDate: 10 (number)
+ TotalActualYearsOfPastEmployment: 10 (number)
+ TotalActualMonthsOfPastEmployment: 10 (number)
+ TotalActualDaysOfPastEmployment: 10 (number)
+ ActualYearsOfPastEmploymentInFirm: 10 (number)
+ ActualMonthsOfPastEmploymentInFirm: 10 (number)
+ ActualDaysOfPastEmploymentInFirm: 10 (number)
+ PensionYearsOfPastEmploymentInFirm: 10 (number)
+ PensionMonthsOfPastEmploymentInFirm: 10 (number)
+ PensionDaysOfPastEmploymentInFirm: 10 (number)
+ ActualYearsOfPastEmploymentPublicSector: 10 (number)
+ ActualMonthsOfPastEmploymentPublicSector: 10 (number)
+ ActualDaysOfPastEmploymentPublicSector: 10 (number)
+ PensionYearsOfPastEmploymentPublicSector: 10 (number)
+ PensionMonthsOfPastEmploymentPublicSector: 10 (number)
+ PensionDaysOfPastEmploymentPublicSector: 10 (number)
+ TotalPensionYearsOfPastEmployment: 10 (number)
+ TotalPensionMonthsOfPastEmployment: 10 (number)
+ TotalPensionDaysOfPastEmployment: 10 (number)
+ TotalActualYearsOfPastEmploymentFull: 10 (number)
+ TotalActualMonthsOfPastEmploymentFull: 10 (number)
+ TotalActualDaysOfPastEmploymentFull: 10 (number)
+ TotalPensionYearsOfPastEmploymentFull: 10 (number)
+ TotalPensionMonthsOfPastEmploymentFull: 10 (number)
+ TotalPensionDaysOfPastEmploymentFull: 10 (number)
+ PensionYearsOfOtherEmployment: 10 (number)
+ PensionMonthsOfOtherEmployment: 10 (number)
+ PensionDaysOfOtherEmployment: 10 (number)
+ TotalActualYearsEmploymentInFirmOnDateFull: 10 (number)
+ TotalActualMonthsEmploymentInFirmOnDateFull: 10 (number)
+ TotalActualDaysEmploymentInFirmOnDateFull: 10 (number)
+ TotalActualYearsOfPastEmploymentPublicSector: 10 (number)
+ TotalActualMonthsOfPastEmploymentPublicSector: 10 (number)
+ TotalActualDaysOfPastEmploymentPublicSector: 10 (number)
+ TotalPensionYearsOfServiceOnDate: 10 (number)
+ TotalPensionMonthsOfServiceOnDate: 10 (number)
+ TotalPensionDaysOfServiceOnDate: 10 (number)
+ TotalActualYearsOfServiceOnEndOfYear: 10 (number)
+ TotalActualMonthsOfServiceOnEndOfYear: 10 (number)
+ TotalActualDaysOfServiceOnEndOfYear: 10 (number)
+ TotalPensionYearsOfServiceOnEndOfYear: 10 (number)
+ TotalPensionMonthsOfServiceOnEndOfYear: 10 (number)
+ TotalPensionDaysOfServiceOnEndOfYear: 10 (number)
+ TotalActualYearsOfServiceOnDateFull: 10 (number)
+ TotalActualMonthsOfServiceOnDateFull: 10 (number)
+ TotalActualDaysOfServiceOnDateFull: 10 (number)
+ Worker: 0001 (string, required) - Workers ident


### HRMWorkerCalculatedEmployment GET response (object)
+ data (array)
    + (HRMWorkerCalculatedEmployment GET ONE response)
+ meta (Get Meta)


### HRMWorkerFamilyMember UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) -  Id
    + data (object) 
        + Firstname: Janez (string, required) - Family member firstname
        + Lastname: Novak (string, required) - Family member lastname
        + DateOfBirth: `2016-08-31T22:00:00+00:00` (string, required) - Family member birthday
        + TaxCode: 895626587 (string, required) - Family member taxcode
        + DependentFrom: `2016-08-31T22:00:00+00:00` (string, required) - Family member dapendent from date
        + DependentTo: `2016-08-31T22:00:00+00:00` (string, required) - Family member dependent to date
        + Dependent: 1 (number, required) - Family member dependet true or false
        + DependentCode: A1 (string, required) - Family member dependent code
        + RegistrationNumber: 1234323456543 (string) - RegistrationNumber
        + PlaceOfBirth: Celje (string) - PlaceOfBirth
        + CountryOfBirth: SI (string) - CountryOfBirth
        + Gender: M (string) - Gender
        + CareForHandicapped: 1 (number) - CareForHandicapped
        + Citizenship: SI (string) - Citizenship
        + Street: T.Ulica 2 (string) - Street
        + StreetTemporary: T.Ulica 2 (string) - Street
        + CertifcateStudyTo: `2016-08-31T22:00:00+00:00` (string) - CertifcateStudyTo
        + ResidentalVisaTo: `2016-08-31T22:00:00+00:00` (string) - ResidentalVisaTo
        + Notes: Some notes (string) - Notes
        + PhoneNumberTemporary: Some notes (string) - PhoneNumberTemporary
        + PhoneNumber: Some notes (string) - PhoneNumber
        + City: Celje (string) - City
        + CityTemporary: Celje (string) - CityTemporary
        + PostOffice: 2000 (string) - PostOffice
        + PostOfficeTemporary: 2000 (string) - PostOfficeTemporary
        + Municipality: 001 (string) - Municipality
        + MunicipalityTemporary: 001 (string) - MunicipalityTemporary
        + Country: SI (string) - Country
        + CountryTemporary: SI (string) - CountryTemporary
        + InsuranceBase: 001 (string) - InsuranceBase
        + Worker: 0001 (string, required) - Workers ident
        + RelationshipToEmployee: 2 (string, required) - Relationship code



### HRMWorkerFamilyMember CREATE request (array) 
+ (object)
    + Firstname: Janez (string, required) - Family member firstname
    + Lastname: Novak (string, required) - Family member lastname
    + DateOfBirth: `2016-08-31T22:00:00+00:00` (string, required) - Family member birthday
    + TaxCode: 895626587 (string, required) - Family member taxcode
    + DependentFrom: `2016-08-31T22:00:00+00:00` (string, required) - Family member dapendent from date
    + DependentTo: `2016-08-31T22:00:00+00:00` (string, required) - Family member dependent to date
    + Dependent: 1 (number, required) - Family member dependet true or false
    + DependentCode: A1 (string, required) - Family member dependent code
    + RegistrationNumber: 1234323456543 (string) - RegistrationNumber
    + PlaceOfBirth: Celje (string) - PlaceOfBirth
    + CountryOfBirth: SI (string) - CountryOfBirth
    + Gender: M (string) - Gender
    + CareForHandicapped: 1 (number) - CareForHandicapped
    + Citizenship: SI (string) - Citizenship
    + Street: T.Ulica 2 (string) - Street
    + StreetTemporary: T.Ulica 2 (string) - Street
    + CertifcateStudyTo: `2016-08-31T22:00:00+00:00` (string) - CertifcateStudyTo
    + ResidentalVisaTo: `2016-08-31T22:00:00+00:00` (string) - ResidentalVisaTo
    + Notes: Some notes (string) - Notes
    + PhoneNumberTemporary: Some notes (string) - PhoneNumberTemporary
    + PhoneNumber: Some notes (string) - PhoneNumber
    + City: Celje (string) - City
    + CityTemporary: Celje (string) - CityTemporary
    + PostOffice: 2000 (string) - PostOffice
    + PostOfficeTemporary: 2000 (string) - PostOfficeTemporary
    + Municipality: 001 (string) - Municipality
    + MunicipalityTemporary: 001 (string) - MunicipalityTemporary
    + Country: SI (string) - Country
    + CountryTemporary: SI (string) - CountryTemporary
    + InsuranceBase: 001 (string) - InsuranceBase
    + Worker: 0001 (string, required) - Workers ident
    + RelationshipToEmployee: 2 (string, required) - Relationship code


### HRMWorkerFamilyMember GET ONE response (object)
    + Firstname: Janez (string, required) - Family member firstname
    + Lastname: Novak (string, required) - Family member lastname
    + DateOfBirth: `2016-08-31T22:00:00+00:00` (string, required) - Family member birthday
    + TaxCode: 895626587 (string, required) - Family member taxcode
    + DependentFrom: `2016-08-31T22:00:00+00:00` (string, required) - Family member dapendent from date
    + DependentTo: `2016-08-31T22:00:00+00:00` (string, required) - Family member dependent to date
    + Dependent: 1 (number, required) - Family member dependet true or false
    + DependentCode: A1 (string, required) - Family member dependent code
    + RegistrationNumber: 1234323456543 (string) - RegistrationNumber
    + PlaceOfBirth: Celje (string) - PlaceOfBirth
    + CountryOfBirth: SI (string) - CountryOfBirth
    + Gender: M (string) - Gender
    + CareForHandicapped: 1 (number) - CareForHandicapped
    + Citizenship: SI (string) - Citizenship
    + Street: T.Ulica 2 (string) - Street
    + StreetTemporary: T.Ulica 2 (string) - Street
    + CertifcateStudyTo: `2016-08-31T22:00:00+00:00` (string) - CertifcateStudyTo
    + ResidentalVisaTo: `2016-08-31T22:00:00+00:00` (string) - ResidentalVisaTo
    + Notes: Some notes (string) - Notes
    + PhoneNumberTemporary: Some notes (string) - PhoneNumberTemporary
    + PhoneNumber: Some notes (string) - PhoneNumber
    + City: Celje (string) - City
    + CityTemporary: Celje (string) - CityTemporary
    + PostOffice: 2000 (string) - PostOffice
    + PostOfficeTemporary: 2000 (string) - PostOfficeTemporary
    + Municipality: 001 (string) - Municipality
    + MunicipalityTemporary: 001 (string) - MunicipalityTemporary
    + Country: SI (string) - Country
    + CountryTemporary: SI (string) - CountryTemporary
    + InsuranceBase: 001 (string) - InsuranceBase
    + Worker: 0001 (string, required) - Workers ident
    + RelationshipToEmployee: 2 (string, required) - Relationship code


### HRMWorkerFamilyMember GET response (object)
+ data (array)
    + (HRMWorkerFamilyMember GET ONE response)
+ meta (Get Meta)


### HRMWorkerEducation UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) -  Id
    + data (object) 
        + DateObtained: `2016-09-08T07:48:33+00:00` (string) - DateObtained
        + Worker: 001 (string) - Worker ident
        + VocationalTechnicalEducation1: 78068 (string) - VocationalTechnicalEducation1
        + VocationalTechnicalEducation2: 78068 (string) - VocationalTechnicalEducation2
        + EducationDegree: V. (string) - EducationDegree
        + FieldOfEducation: 851 (string) - FieldOfEducation
        + KindOfEducation: 16202 (string) - KindOfEducation
        + StandardProfessionClass: 4415 (string) - StandardProfessionClass
        + WayOfObtaining: 001 (string) - WayOfObtaining
        + Active: 1 (number) - 1
        + ActiveRecord: 1 (number) - 1


### HRMWorkerEducation CREATE request (array) 
+ (object)
    + DateObtained: `2016-09-08T07:48:33+00:00` (string) - DateObtained
    + Worker: 001 (string) - Worker ident
    + VocationalTechnicalEducation1: 78068 (string) - VocationalTechnicalEducation1
    + VocationalTechnicalEducation2: 78068 (string) - VocationalTechnicalEducation2
    + EducationDegree: V. (string) - EducationDegree
    + FieldOfEducation: 851 (string) - FieldOfEducation
    + KindOfEducation: 16202 (string) - KindOfEducation
    + StandardProfessionClass: 4415 (string) - StandardProfessionClass
    + WayOfObtaining: 001 (string) - WayOfObtaining
    + Active: 1 (number) - 1
    + ActiveRecord: 1 (number) - 1

### HRMWorkerEducation GET ONE response (object)
    + DateObtained: `2016-09-08T07:48:33+00:00` (string) - DateObtained
    + Worker: 001 (string) - Worker ident
    + VocationalTechnicalEducation1: 78068 (string) - VocationalTechnicalEducation1
    + VocationalTechnicalEducation2: 78068 (string) - VocationalTechnicalEducation2
    + EducationDegree: V. (string) - EducationDegree
    + FieldOfEducation: 851 (string) - FieldOfEducation
    + KindOfEducation: 16202 (string) - KindOfEducation
    + StandardProfessionClass: 4415 (string) - StandardProfessionClass
    + WayOfObtaining: 001 (string) - WayOfObtaining
    + Active: 1 (number) - 1
    + ActiveRecord: 1 (number) - 1

### HRMWorkerEducation GET response (object)
+ data (array)
    + (HRMWorkerEducation GET ONE response)
+ meta (Get Meta)


### HRMWorkerHabilitation UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) -  Id
    + data (object) 
        + Ident: 001 (string) - Ident
        + Worker: 001 (string) - Worker ident
        + TitleCodes: 001 (string) - TitleCodes
        + EducationArea: 001 (string) - EducationArea
        + EducationLocation: 001 (string) - EducationLocation
        + NumberOfRenewal: 10 (number) - NumberOfRenewal
        + DateOfSubmission: `2016-09-08T07:48:33+00:00` (string) - DateOfSubmission
        + DateOfElection: `2016-09-08T07:48:33+00:00` (string) - DateOfElection
        + DateOfExpiration: `2016-09-08T07:48:33+00:00` (string) - DateOfExpiration


### HRMWorkerHabilitation CREATE request (array) 
+ (object)
    + Ident: 001 (string) - Ident
    + Worker: 001 (string) - Worker ident
    + TitleCodes: 001 (string) - TitleCodes
    + EducationArea: 001 (string) - EducationArea
    + EducationLocation: 001 (string) - EducationLocation
    + NumberOfRenewal: 10 (number) - NumberOfRenewal
    + DateOfSubmission: `2016-09-08T07:48:33+00:00` (string) - DateOfSubmission
    + DateOfElection: `2016-09-08T07:48:33+00:00` (string) - DateOfElection
    + DateOfExpiration: `2016-09-08T07:48:33+00:00` (string) - DateOfExpiration
    
### HRMWorkerHabilitation GET ONE response (object)
    + Ident: 001 (string) - Ident
    + Worker: 001 (string) - Worker ident
    + TitleCodes: 001 (string) - TitleCodes
    + EducationArea: 001 (string) - EducationArea
    + EducationLocation: 001 (string) - EducationLocation
    + NumberOfRenewal: 10 (number) - NumberOfRenewal
    + DateOfSubmission: `2016-09-08T07:48:33+00:00` (string) - DateOfSubmission
    + DateOfElection: `2016-09-08T07:48:33+00:00` (string) - DateOfElection
    + DateOfExpiration: `2016-09-08T07:48:33+00:00` (string) - DateOfExpiration

### HRMWorkerHabilitation GET response (object)
+ data (array)
    + (HRMWorkerHabilitation GET ONE response)
+ meta (Get Meta)

### HRMWorkerDisability UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) - Id
    + data (object) 
        + DateFrom: `2016-09-08T07:48:33+00:00` (string, required) - Disability date from
        + DateTo: `2016-09-08T07:48:33+00:00` (string, required) - Disability date to
        + QuotaOfDisabled: 002 (string, required) - Disability code
        + TypeOfDisability: 002 (string) - TypeOfDisability
        + CauseOfDisability: 002 (string) - CauseOfDisability
        + CodeM3: 002 (string) - CodeM3
        + WorkHoursPerWeek: 40 (number) - WorkHoursPerWeek
        + Worker: 0001 (string, required) - Workers ident
        + Description: Disability description (string) - Description
        + DecisionIssuer: Osebni zdravnik (string) - DecisionIssuer
        + DecisionNumber: 012345A DecisionIssuer (string) - DecisionNumber
        + DisabilityPending: 1 (number) - DisabilityPending
        + PartialDisabilityPension: 1 (number) - PartialDisabilityPension
        + NumberOfWorkingHoursPerDay: 4 (number) - NumberOfWorkingHoursPerDay
        + NumberOfWorkingDaysPerWeek: 20 (number) - NumberOfWorkingDaysPerWeek
        + RestrictionsAtWork: 001 (string) - RestrictionsAtWork
        + CategoryOfDisability: 001 (string) - CategoryOfDisability



### HRMWorkerDisability CREATE request (array) 
+ (object)
    + DateFrom: `2016-09-08T07:48:33+00:00` (string, required) - Disability date from
    + DateTo: `2016-09-08T07:48:33+00:00` (string, required) - Disability date to
    + DateOfDisability: `2016-09-08T07:48:33+00:00` (string) - DateOfDisability
    + DateOfReEvaluationOfDisability: `2016-09-08T07:48:33+00:00` (string) - DateOfReEvaluationOfDisability
    + QuotaOfDisabled: 002 (string, required) - Disability code
    + TypeOfDisability: 002 (string) - TypeOfDisability
    + CauseOfDisability: 002 (string) - CauseOfDisability
    + CodeM3: 002 (string) - CodeM3
    + WorkHoursPerWeek: 40 (number) - WorkHoursPerWeek
    + Worker: 0001 (string, required) - Workers ident
    + Description: Disability description (string) - Description
    + DecisionIssuer: Osebni zdravnik (string) - DecisionIssuer
    + DecisionNumber: 012345A DecisionIssuer (string) - DecisionNumber
    + DisabilityPending: 1 (number) - DisabilityPending
    + PartialDisabilityPension: 1 (number) - PartialDisabilityPension
    + NumberOfWorkingHoursPerDay: 4 (number) - NumberOfWorkingHoursPerDay
    + NumberOfWorkingDaysPerWeek: 20 (number) - NumberOfWorkingDaysPerWeek
    + RestrictionsAtWork: 001 (string) - RestrictionsAtWork
    + CategoryOfDisability: 001 (string) - CategoryOfDisability

    
### HRMWorkerDisability GET ONE response (object)
+ DateFrom: `2016-09-08T07:48:33+00:00` (string, required) - Disability date from
+ DateTo: `2016-09-08T07:48:33+00:00` (string, required) - Disability date to
+ QuotaOfDisabled: 002 (string, required) - Disability code
+ TypeOfDisability: 002 (string) - TypeOfDisability
+ CauseOfDisability: 002 (string) - CauseOfDisability
+ CodeM3: 002 (string) - CodeM3
+ WorkHoursPerWeek: 40 (number) - WorkHoursPerWeek
+ Worker: 0001 (string, required) - Workers ident
+ Description: Disability description (string) - Description
+ DecisionIssuer: Osebni zdravnik (string) - DecisionIssuer
+ DecisionNumber: 012345A DecisionIssuer (string) - DecisionNumber
+ DisabilityPending: 1 (number) - DisabilityPending
+ PartialDisabilityPension: 1 (number) - PartialDisabilityPension
+ NumberOfWorkingHoursPerDay: 4 (number) - NumberOfWorkingHoursPerDay
+ NumberOfWorkingDaysPerWeek: 20 (number) - NumberOfWorkingDaysPerWeek
+ RestrictionsAtWork: 001 (string) - RestrictionsAtWork
+ CategoryOfDisability: 001 (string) - CategoryOfDisability

### HRMWorkerDisability GET response (object)
+ data (array)
    + (HRMWorkerDisability GET ONE response)
+ meta (Get Meta)

### HRMWorkerMedicalExamination UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) - Id
    + data (object) 
        + ExaminationDate: `2016-09-08T07:48:33+00:00` (string) - ExaminationDate
        + ExaminationDateNext: `2016-09-08T07:48:33+00:00` (string) - ExaminationDateNext
        + ExaminationPeriod: 6 (number) - ExaminationPeriod
        + Description: Some description (string) - Description
        + ConclusionsDesc: Some conclusion description (string) - ConclusionsDesc
        + MeasuresDesc: Some measure description (string) - MeasuresDesc
        + TypeOfExamination: 001 (string) - TypeOfExamination
        + RestrictionsAtWork: 001 (string) - RestrictionsAtWork
        + Conclusions: 001 (string) - Conclusions
        + Worker: 0001 (string, required) - Workers ident


### HRMWorkerMedicalExamination CREATE request (array) 
+ (object)
    + ExaminationDate: `2016-09-08T07:48:33+00:00` (string) - ExaminationDate
    + ExaminationDateNext: `2016-09-08T07:48:33+00:00` (string) - ExaminationDateNext
    + ExaminationPeriod: 6 (number) - ExaminationPeriod
    + Description: Some description (string) - Description
    + ConclusionsDesc: Some conclusion description (string) - ConclusionsDesc
    + MeasuresDesc: Some measure description (string) - MeasuresDesc
    + TypeOfExamination: 001 (string) - TypeOfExamination
    + RestrictionsAtWork: 001 (string) - RestrictionsAtWork
    + Conclusions: 001 (string) - Conclusions
    + Worker: 0001 (string, required) - Workers ident

    
### HRMWorkerMedicalExamination GET ONE response (object)
+ ExaminationDate: `2016-09-08T07:48:33+00:00` (string) - ExaminationDate
+ ExaminationDateNext: `2016-09-08T07:48:33+00:00` (string) - ExaminationDateNext
+ ExaminationPeriod: 6 (number) - ExaminationPeriod
+ Description: Some description (string) - Description
+ ConclusionsDesc: Some conclusion description (string) - ConclusionsDesc
+ MeasuresDesc: Some measure description (string) - MeasuresDesc
+ TypeOfExamination: 001 (string) - TypeOfExamination
+ RestrictionsAtWork: 001 (string) - RestrictionsAtWork
+ Conclusions: 001 (string) - Conclusions
+ Worker: 0001 (string, required) - Workers ident

### HRMWorkerMedicalExamination GET response (object)
+ data (array)
    + (HRMWorkerMedicalExamination GET ONE response)
+ meta (Get Meta)


### HRMWorkerAbsence UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) - Id
    + data (object) 
        + DateFrom: `2016-09-08T07:48:33+00:00` (string) - DateFrom
        + DateTo: `2016-09-08T07:48:33+00:00` (string) - DateTo
        + Description: Some description (string) - Description
        + HoursPerWeek: 40 (number) - HoursPerWeek
        + TypeOfAbsence: 001 (string) - TypeOfAbsence
        + Worker: 0001 (string, required) - Workers ident
        + Substitution: 0001 (string, required) - Substitution ident


### HRMWorkerAbsence CREATE request (array) 
+ (object)
    + DateFrom: `2016-09-08T07:48:33+00:00` (string) - DateFrom
    + DateTo: `2016-09-08T07:48:33+00:00` (string) - DateTo
    + Description: Some description (string) - Description
    + HoursPerWeek: 40 (number) - HoursPerWeek
    + TypeOfAbsence: 001 (string) - TypeOfAbsence
    + Worker: 0001 (string, required) - Workers ident
    + Substitution: 0001 (string, required) - Substitution ident

    
### HRMWorkerAbsence GET ONE response (object)
+ DateFrom: `2016-09-08T07:48:33+00:00` (string) - DateFrom
+ DateTo: `2016-09-08T07:48:33+00:00` (string) - DateTo
+ Description: Some description (string) - Description
+ HoursPerWeek: 40 (number) - HoursPerWeek
+ TypeOfAbsence: 001 (string) - TypeOfAbsence
+ Worker: 0001 (string, required) - Workers ident
+ Substitution: 0001 (string, required) - Substitution ident

### HRMWorkerAbsence GET response (object)
+ data (array)
    + (HRMWorkerAbsence GET ONE response)
+ meta (Get Meta)


### HRMWorkerPastEmployment UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string, required) - Id
    + data (object) 
        + DateFrom: `2016-09-08T07:48:33+00:00` (string) - DateFrom
        + DateTo: `2016-09-08T07:48:33+00:00` (string) - DateTo
        + Employer: Company name (string) - Company name
        + BenefitsDuration: 001 (string) - Type of benefits furation(15/12,18/12...)
        + HoursPerWeek: 40 (number) - HoursPerWeek
        + YearsOfService: 10 (number) - YearsOfService
        + MonthsOfService: 10 (number) - MonthsOfService
        + DaysOfService: 10 (number) - DaysOfService
        + YearsOfServiceFull: 10 (number) - YearsOfServiceFull
        + MonthsOfServiceFull: 10 (number) - MonthsOfServiceFull
        + DaysOfServiceFull: 10 (number) - DaysOfServiceFull
        + YearsOfServiceBenefits: 10 (number) - YearsOfServiceBenefits
        + MonthsOfServiceBenefits: 10 (number) - MonthsOfServiceBenefits
        + DaysOfServiceBenefits: 10 (number) - DaysOfServiceBenefits
        + FullYearsOfService: 1 (number) - Boolean if full years of service or not
        + EmploymentPublicSector: 1 (number) - Boolean if employment in public sector
        + Benefits: 1 (number) - Boolean if benefits or not
        + Worker: 0001 (string, required) - Workers ident
        + TypeOfEmployment: 0001 (string) - Type of employer(this firm,another employer...)


### HRMWorkerPastEmployment CREATE request (array) 
+ (object)
    + DateFrom: `2016-09-08T07:48:33+00:00` (string) - DateFrom
    + DateTo: `2016-09-08T07:48:33+00:00` (string) - DateTo
    + Employer: Company name (string) - Company name
    + BenefitsDuration: 001 (string) - Type of benefits furation(15/12,18/12...)
    + HoursPerWeek: 40 (number) - HoursPerWeek
    + YearsOfService: 10 (number) - YearsOfService
    + MonthsOfService: 10 (number) - MonthsOfService
    + DaysOfService: 10 (number) - DaysOfService
    + YearsOfServiceFull: 10 (number) - YearsOfServiceFull
    + MonthsOfServiceFull: 10 (number) - MonthsOfServiceFull
    + DaysOfServiceFull: 10 (number) - DaysOfServiceFull
    + YearsOfServiceBenefits: 10 (number) - YearsOfServiceBenefits
    + MonthsOfServiceBenefits: 10 (number) - MonthsOfServiceBenefits
    + DaysOfServiceBenefits: 10 (number) - DaysOfServiceBenefits
    + FullYearsOfService: 1 (number) - Boolean if full years of service or not
    + EmploymentPublicSector: 1 (number) - Boolean if employment in public sector
    + Benefits: 1 (number) - Boolean if benefits or not
    + Worker: 0001 (string, required) - Workers ident
    + TypeOfEmployment: 0001 (string) - Type of employer(this firm,another employer...)

    
### HRMWorkerPastEmployment GET ONE response (object)
+ DateFrom: `2016-09-08T07:48:33+00:00` (string) - DateFrom
+ DateTo: `2016-09-08T07:48:33+00:00` (string) - DateTo
+ Employer: Company name (string) - Company name
+ BenefitsDuration: 001 (string) - Type of benefits furation(15/12,18/12...)
+ HoursPerWeek: 40 (number) - HoursPerWeek
+ YearsOfService: 10 (number) - YearsOfService
+ MonthsOfService: 10 (number) - MonthsOfService
+ DaysOfService: 10 (number) - DaysOfService
+ YearsOfServiceFull: 10 (number) - YearsOfServiceFull
+ MonthsOfServiceFull: 10 (number) - MonthsOfServiceFull
+ DaysOfServiceFull: 10 (number) - DaysOfServiceFull
+ YearsOfServiceBenefits: 10 (number) - YearsOfServiceBenefits
+ MonthsOfServiceBenefits: 10 (number) - MonthsOfServiceBenefits
+ DaysOfServiceBenefits: 10 (number) - DaysOfServiceBenefits
+ FullYearsOfService: 1 (number) - Boolean if full years of service or not
+ EmploymentPublicSector: 1 (number) - Boolean if employment in public sector
+ Benefits: 1 (number) - Boolean if benefits or not
+ Worker: 0001 (string, required) - Workers ident
+ TypeOfEmployment: 0001 (string) - Type of employer(this firm,another employer...)

### HRMWorkerPastEmployment GET response (object)
+ data (array)
    + (HRMWorkerPastEmployment GET ONE response)
+ meta (Get Meta)


### HrmWorkplace GET response (object)
+ data (array)
    + (HrmWorkplace GET ONE response)
+ meta (Get Meta)

### HrmWorkplace GET ONE response (object)
+ Ident: 0001 (string) - Ident for identification
+ IdentZspjs: 0001 (string) - IdentZspjs for identification
+ Name: Direktor (string) - Workplace name
+ Title: Direktor (string) - Workplace Title
+ PositionExtra: 0 (number) -  Work place title-0,1,2,3...
+ RequieredWorkExperience: 60 (string) - In Months
+ TryoutPeriod: 5 (number)- TryoutPeriod
+ ResponsibilityDescription: Workplace description (string)- Description of work place
+ ValidFrom: `2016-08-31T22:00:00+00:00` (string)- Work place valid date from
+ VacationDays: 2 (number)- Work place vacation days
+ AllowedWorkers: 10 (number)- Allowed workers
+ PromotionsNumber: 5 (number)- PromotionsNumber
+ CompetitionClause: 1 (number)- CompetitionClause 1 for true, 0 for false
+ NightWork: 0 (number)- NightWork 1 for true, 0 for false
+ PsychophysicalStress: 0 (number)- PsychophysicalStress 1 for true, 0 for false
+ PhysicalStress: 0 (number)- PhysicalStress 1 for true, 0 for false
+ WorkWithMentallyDisturbingPeople: 0 (number)- WorkWithMentallyDisturbingPeople 1 for true, 0 for false
+ SocialType: 0 (number)- SocialType 1 for true, 0 for false
+ TehnicalType: 0 (number)- TehnicalType 1 for true, 0 for false
+ IdPositioningSupplement: 2 (string)- IdPositioningSupplement 
+ WorkWithMentallyDisturbingPeoplePercent: 2 (number)- WorkWithMentallyDisturbingPeoplePercent 
+ WorkWithMentallyDisturbingPeopleHoursPerDay: 2 (number)- WorkWithMentallyDisturbingPeopleHoursPerDay 
+ PeriodicalMedicalExam: 1 (number)- PeriodicalMedicalExam  1 for true, 0 for false
+ PeriodicalMedicalExam1: 0 (number)- PeriodicalMedicalExam1  1 for true, 0 for false
+ PeriodicalMedicalExam2: 0 (number)- PeriodicalMedicalExam2 1 for true, 0 for false
+ MedicalExamPeriod: 12 (number)- MedicalExamPeriod
+ MedicalExamPeriod1: 12 (number)- MedicalExamPeriod1
+ MedicalExamPeriod2: 12 (number)- MedicalExamPeriod2
+ PayGrade: 79 (string)- PayGrade
+ ParentWorkplace: 0001 (string)- Work place ident for parent workplace
+ TariffClass: V. (string)- TariffClass
+ PublicliclyRecognizedQualifications1: 78068 (string)- PublicliclyRecognizedQualifications1
+ PublicliclyRecognizedQualifications2: 78068 (string)- PublicliclyRecognizedQualifications2
+ PublicliclyRecognizedQualifications3: 78068 (string)- PublicliclyRecognizedQualifications3
+ RequieredEducationDegree1: III. (string)- RequieredEducationDegree1
+ RequieredEducationDegree2: III. (string)- RequieredEducationDegree2
+ FailureTime: 001 (string)- FailureTime
+ WorkShifts: 1 (string)- WorkShifts
+ MedicalExamType: 001 (string)- MedicalExamType
+ MedicalExamType1: 001 (string)- MedicalExamType1
+ MedicalExamType2: 001 (string)- MedicalExamType2
+ CostCenter: 001 (string)- CostCenter

### HRM Workplace CREATE request (array) 
+ (object)
    + Ident: 0001 (string) - Ident for identification
    + IdentZspjs: 0001 (string) - IdentZspjs for identification
    + Name: Direktor (string) - Workplace name
    + Title: Direktor (string) - Workplace Title
    + PositionExtra: 0 (number) -  Work place title-0,1,2,3...
    + RequieredWorkExperience: 60 (string) - In Months
    + TryoutPeriod: 5 (number)- TryoutPeriod
    + ResponsibilityDescription: Workplace description (string)- Description of work place
    + ValidFrom: `2016-08-31T22:00:00+00:00` (string)- Work place valid date from
    + VacationDays: 2 (number)- Work place vacation days
    + AllowedWorkers: 10 (number)- Allowed workers
    + PromotionsNumber: 5 (number)- PromotionsNumber
    + CompetitionClause: 1 (number)- CompetitionClause 1 for true, 0 for false
    + NightWork: 0 (number)- NightWork 1 for true, 0 for false
    + PsychophysicalStress: 0 (number)- PsychophysicalStress 1 for true, 0 for false
    + PhysicalStress: 0 (number)- PhysicalStress 1 for true, 0 for false
    + WorkWithMentallyDisturbingPeople: 0 (number)- WorkWithMentallyDisturbingPeople 1 for true, 0 for false
    + SocialType: 0 (number)- SocialType 1 for true, 0 for false
    + TehnicalType: 0 (number)- TehnicalType 1 for true, 0 for false
    + IdPositioningSupplement: 2 (string)- IdPositioningSupplement 
    + WorkWithMentallyDisturbingPeoplePercent: 2 (number)- WorkWithMentallyDisturbingPeoplePercent 
    + WorkWithMentallyDisturbingPeopleHoursPerDay: 2 (number)- WorkWithMentallyDisturbingPeopleHoursPerDay 
    + PeriodicalMedicalExam: 1 (number)- PeriodicalMedicalExam  1 for true, 0 for false
    + PeriodicalMedicalExam1: 0 (number)- PeriodicalMedicalExam1  1 for true, 0 for false
    + PeriodicalMedicalExam2: 0 (number)- PeriodicalMedicalExam2 1 for true, 0 for false
    + MedicalExamPeriod: 12 (number)- MedicalExamPeriod
    + MedicalExamPeriod1: 12 (number)- MedicalExamPeriod1
    + MedicalExamPeriod2: 12 (number)- MedicalExamPeriod2
    + PayGrade: 79 (string)- PayGrade
    + ParentWorkplace: 0001 (string)- Work place ident for parent workplace
    + TariffClass: V. (string)- TariffClass
    + PublicliclyRecognizedQualifications1: 78068 (string)- PublicliclyRecognizedQualifications1
    + PublicliclyRecognizedQualifications2: 78068 (string)- PublicliclyRecognizedQualifications2
    + PublicliclyRecognizedQualifications3: 78068 (string)- PublicliclyRecognizedQualifications3
    + RequieredEducationDegree1: III. (string)- RequieredEducationDegree1
    + RequieredEducationDegree2: III. (string)- RequieredEducationDegree2
    + FailureTime: 001 (string)- FailureTime
    + WorkShifts: 1 (string)- WorkShifts
    + MedicalExamType: 001 (string)- MedicalExamType
    + MedicalExamType1: 001 (string)- MedicalExamType1
    + MedicalExamType2: 001 (string)- MedicalExamType2
    + CostCenter: 001 (string)- CostCenter

###  HRM Workplace UPDATE request (array)
+ (object)
    + Id: `4d407470-e228-4b52-8dc1-79ab07ea2a17`  (string, required) - Workplace unique Id
    + data (object) 
        + Ident: 0001 (string) - Ident for identification
        + IdentZspjs: 0001 (string) - IdentZspjs for identification
        + Name: Direktor (string) - Workplace name
        + Title: Direktor (string) - Workplace Title
        + PositionExtra: 0 (number) -  Work place title-0,1,2,3...
        + RequieredWorkExperience: 60 (string) - In Months
        + TryoutPeriod: 5 (number)- TryoutPeriod
        + ResponsibilityDescription: Workplace description (string)- Description of work place
        + ValidFrom: `2016-08-31T22:00:00+00:00` (string)- Work place valid date from
        + VacationDays: 2 (number)- Work place vacation days
        + AllowedWorkers: 10 (number)- Allowed workers
        + PromotionsNumber: 5 (number)- PromotionsNumber
        + CompetitionClause: 1 (number)- CompetitionClause 1 for true, 0 for false
        + NightWork: 0 (number)- NightWork 1 for true, 0 for false
        + PsychophysicalStress: 0 (number)- PsychophysicalStress 1 for true, 0 for false
        + PhysicalStress: 0 (number)- PhysicalStress 1 for true, 0 for false
        + WorkWithMentallyDisturbingPeople: 0 (number)- WorkWithMentallyDisturbingPeople 1 for true, 0 for false
        + SocialType: 0 (number)- SocialType 1 for true, 0 for false
        + TehnicalType: 0 (number)- TehnicalType 1 for true, 0 for false
        + IdPositioningSupplement: 2 (string)- IdPositioningSupplement 
        + WorkWithMentallyDisturbingPeoplePercent: 2 (number)- WorkWithMentallyDisturbingPeoplePercent 
        + WorkWithMentallyDisturbingPeopleHoursPerDay: 2 (number)- WorkWithMentallyDisturbingPeopleHoursPerDay 
        + PeriodicalMedicalExam: 1 (number)- PeriodicalMedicalExam  1 for true, 0 for false
        + PeriodicalMedicalExam1: 0 (number)- PeriodicalMedicalExam1  1 for true, 0 for false
        + PeriodicalMedicalExam2: 0 (number)- PeriodicalMedicalExam2 1 for true, 0 for false
        + MedicalExamPeriod: 12 (number)- MedicalExamPeriod
        + MedicalExamPeriod1: 12 (number)- MedicalExamPeriod1
        + MedicalExamPeriod2: 12 (number)- MedicalExamPeriod2
        + PayGrade: 79 (string)- PayGrade
        + ParentWorkplace: 0001 (string)- Work place ident for parent workplace
        + TariffClass: V. (string)- TariffClass
        + PublicliclyRecognizedQualifications1: 78068 (string)- PublicliclyRecognizedQualifications1
        + PublicliclyRecognizedQualifications2: 78068 (string)- PublicliclyRecognizedQualifications2
        + PublicliclyRecognizedQualifications3: 78068 (string)- PublicliclyRecognizedQualifications3
        + RequieredEducationDegree1: III. (string)- RequieredEducationDegree1
        + RequieredEducationDegree2: III. (string)- RequieredEducationDegree2
        + FailureTime: 001 (string)- FailureTime
        + WorkShifts: 1 (string)- WorkShifts
        + MedicalExamType: 001 (string)- MedicalExamType
        + MedicalExamType1: 001 (string)- MedicalExamType1
        + MedicalExamType2: 001 (string)- MedicalExamType2
        + CostCenter: 001 (string)- CostCenter

### DSDocument CREATE request (object) 
+ (object)
    + taxNumber: 12345678 (string) - Recipient partner tax number
    + fileList: (array) - list of files
        + :(object) - item of list of files
            + ext: xml (string) - File extension (xml, pdf)
            + content: base64content (string) - base64 encoded content of the xml file
        + :(object) - item of list of files
            + ext: pdf (string) - File extension (xml, pdf)
            + content: base64content (string) - base64 encoded content of the pdf file

### Bookings GET ONE response (object)    
+ Account: 0500 (string) - Account number
+ AccountName: POPRAVEK VREDNOSTI OPREME IN N (string) - Name of account
+ AttributeOne: Text (string) - Code of the attribute one
+ AttributeOneName: Text (string) - Name of the attribute one
+ AttributeThree: Text (string) - Code of the attribute three
+ AttributeThreeName: Text (string) - Name of the attribute three
+ AttributeTwo: Text (string) - Code of the attribute two
+ AttributeTwoName: Text (string) - Name of the attribute two
+ CostCarrier: Text (string) - Code of the cost carrier
+ CostCarrierName: Name (string) - Name of the cost carrier
+ CostCenter: 103 (string) - Code of the cost center
+ CostCenterName: 103 STM ZA TESTIRANJE (string) - Name of the cost center
+ CreditForeign: 0 (number) - Credit amount in foreign currency
+ CreditHome: 2553 (number) - Credit amount in home currency
+ Date: 30.09.2016 (string) - Date of the booking position (DD.MM.YYYY)
+ DebitHome: 0 (number) - Debit amount in home currency
+ DebitForeign: 0 (number) - Debit amount in foreign currency
+ DeliveryServiceDate: 23.10.2016 (string) - Date of the delivery or service (DD.MM.YYYY) - only for partner bookings
+ Description: 0009220 EL.HIDR.PREŠA S ČELJUSTMI (string) - Description of booking position
+ DocumentDate: Text (string) - Date of the document (DD.MM.YYYY) - only for partner bookings
+ DocumentNumber: 0009220  (string) - Number of the document (eg. invoice)
+ DocumentReference: vendorDoc  (string) - Reference number of document (eg. vendor document number)
+ EntryType: 00 (string) - Entry type of the booking position
+ IdentCurrency: Text (string) - Ident of the foreign currency
+ Partner: Text (string) - Code of the partner
+ PartnerName: Text (string) - Name of the partner
+ Project: Text (string) - Code of the project
+ ProjectName: Text (string) - Name of the project
+ Reference: SI0022223 (string) - Payment reference
+ SourceOfFinance: Text (string) - Code of the source of finance attribute
+ SourceOfFinanceName: Text (string) - Name of the source of finance attribute
+ StatementIdent: TE1600058 (string) - Code of the finacial statement
+ ValueDate: Text (string) - Value date (DD.MM.YYYY) - only for partner bookings

### Bookings GET data (array) 
+ (object)
    + (Bookings GET ONE response)

### Bookings PUT data (object)
+ data (array)
    + (Bookings GET ONE response)

### MBMail GET ONE response (object)    
+ ReceivedDate: 04.02.2018 (string) - receive date of the document (DD.MM.YYYY)
+ DocumentDate: 31.01.2018 (string) - date of the original document (DD.MM.YYYY)
+ DocumentTypeShowAs: 02 Prejeti računi (string) - ident and name of the document type
+ DocumentValue: 100.23 (number) - total amount on the document
+ EventDate: 31.01.2018 (string) - date of the event on ther original document - supply or service date (DD.MM.YYYY)
+ Ident: 1800002 (string) - ident of the mailbook document
+ IdentPartner: 0001 (string) - ident of the partner
+ PartnerAddress: Tovarniška cesta 8a (string) - address of the partner
+ PartnerCountry: SI (string) - country of the partner
+ PartnerIdVatNumber: SI63745178 (string) - vat number of the partner
+ PartnerPostalOffice: 3210, Slovenske Konjice (string) - postal code and city of the partner
+ PartnerShortName: TOVARNA d.o.o. (string) - name of the partner
+ PartnerTaxNumber: 63745178 (string) - tax number of the partner
+ SupplierDocumentNumber: FA1134/2018 (string) - original (supplier) number of the document
+ ValueDate: 15.02.2018 (string) - due date (DD.MM.YYYY)
+ WfBusinessAreaName: Likvidatura (string) - name of the work area

### MBMail PUT data (object)
+ data (array)
    + (MBMail GET ONE response)

### VATIssued GET ONE response (object)    
+ Article76Amount: 0 (number) - Amount for services by article 76
+ Article76ForeignAmount: 0 (number) - Amount in foreign currency for services by article 76
+ Article76GoodsAmount: 0 (number) - Amount for goods by article 76
+ Article76GoodsForeignAmount: 0 (number) - Amount in foreign currency for goods by article 76
+ CPAmount: 0 (number) - Amount for CP
+ CPForeignAmount: 0 (number) - Amount in foreign currency for CP
+ AttributeOne: Text (string) - Code of the attribute one
+ AttributeOneName: Text (string) - Name of the attribute one
+ AttributeThree: Text (string) - Code of the attribute three
+ AttributeThreeName: Text (string) - Name of the attribute three
+ AttributeTwo: Text (string) - Code of the attribute two
+ AttributeTwoName: Text (string) - Name of the attribute two
+ CostCarrier: Text (string) - Code of the cost carrier
+ CostCarrierName:Name (string) - Name of the cost carrier
+ CostCenter: 103 (string) - Code of the cost center
+ CostCenterName: 103 STM ZA TESTIRANJE (string) - Name of the cost center
+ DeliveryServiceDate: 23.10.2016 (string) - Date of the delivery or service (DD.MM.YYYY)
+ DocumentIndicator: R (string) - Document indicator (R=invoice, A=advance)
+ DocumentInputType: 001 (string) - Document input type (depending on the invoice type; 001, 002, ...)
+ DocumentNumber: 0009220  (string) - Number of the document-invoice
+ DocumentTotalAmount: 1220 (number) - Total amount of the document
+ DocumentTotalForeignAmount: 0 (number) - Total amount of the document in foreign currency 
+ DocumentType: IF (string) - Document subtype - used for booking models
+ ExemptSupplyAmount: 0 (number) - Amount for exempt supplies
+ ExemptSupplyAmount: 0 (number) - Amount for exempt supplies in foreign currency
+ ForeignCurrency: USD (string) - Ident of foreign currency (eg. USD)
+ GoodsExportAmount: 0 (number) - Amount for goods export
+ GoodsExportForeignAmount: 0 (number) - Amount for goods export
+ HomeTaxAmountForeignHigh: 0 (number) - Home tax on normal tax rate in foreign currency
+ HomeTaxAmountForeignLow: 0 (number) - Home tax on low tax rate in foreign currency
+ HomeTaxAmountHigh: 220 (number) - Home tax on normal tax rate
+ HomeTaxAmountLow: 0 (number) - Home tax on low tax rate
+ HomeTaxBaseAmountForeignHigh: 0 (number) - Home base for normal tax rate in foreign currency
+ HomeTaxBaseAmountForeignLow: 0 (number) - Home base for low tax rate in foreign currency
+ HomeTaxBaseAmountHigh: 1000 (number) - Home base for normal tax rate
+ HomeTaxBaseAmountLow: 0 (number) - Home base for low tax rate
+ IdentPartner: 000003  (string) - Ident of partner
+ InstallationAmount: 0 (number) - Amount for installations
+ InstallationForeignAmount: 0 (number) - Amount for installations in foreign currency
+ InvoiceDate: 23.10.2016 (string) - Date of the invoice (DD.MM.YYYY)
+ NoTaxAmount: 0 (number) - Amount for non taxable transactions
+ NoTaxAmountForeign: 0 (number) - Amount for non taxable transactions in foreign currency
+ NoVIESAmount: 0 (number) - Amount for non VIES transactions
+ NoVIESForeignAmount: 0 (number) - Amount for non VIES transactions in foreign currency
+ OtherAmount: 0 (number) - Other amount
+ OtherAmountForeign: 0 (number) - Other amount in foreign currency
+ PaymentReference: SI00133354 (string) - Reference for payment
+ RemoteSalesAmount: 0 (number) - Amount for remote sales
+ RemoteSalesForeignAmount: 0 (number) - Amount for remote sales in foreign currency
+ TaxDate: 23.10.2016 (string) - Date for tax (DD.MM.YYYY)
+ ThreePartyAmount: 0 (number) - Amount for three party sales
+ ThreePartyForeignAmount: 0 (number) - Amount for three party sales in foreign currency
+ VATSubject: 1 (number) - Is subject to VAT calculation (1/0)
+ VATStatement: 1 (number) - Use bookings for finances (1/0)
+ VATUseModel: 0 (number) - Create bookings for finances based on pre-defined models (1/0)
+ ValueDate: 30.10.2016 (string) - Date for paymentt (DD.MM.YYYY)
+ ValueDays: 8 (number) - Days for calculating value date
+ WithoutTaxAmount: 0 (number) - Amount without tax
+ WithoutTaxAmountForeign: 0 (number) - Amount without tax in foreign currency

### VATIssued PUT data (object)
+ data (array)
    + (VATIssued GET ONE response)
        + Bookings (array)
            + (Bookings GET ONE response)

### VATReceived GET ONE response (object)    
+ WithoutTaxAmount: 0 (number) - Amount without tax
+ WithoutTaxAmount: 0 (number) - Amount without tax in foreign currency
+ NoTaxAmount: 0 (number) - Amount that is not for vat purposes
+ ExemptSupplyAmount: 0 (number) - Amount of exempt supplies
+ ExemptSupplyAmountForeign: 0 (number) - Amount of exempt supplies in foreign currency
+ ThreePartyAmount: 0 (number) - Amount for three party supplies
+ AttributeOne: Text (string) - Code of the attribute one
+ AttributeOneName: Text (string) - Name of the attribute one
+ AttributeThree: Text (string) - Code of the attribute three
+ AttributeThreeName: Text (string) - Name of the attribute three
+ AttributeTwo: Text (string) - Code of the attribute two
+ AttributeTwoName: Text (string) - Name of the attribute two
+ CostCarrier: Text (string) - Code of the cost carrier
+ CostCarrierName:Name (string) - Name of the cost carrier
+ CostCenter: 103 (string) - Code of the cost center
+ CostCenterName: 103 STM ZA TESTIRANJE (string) - Name of the cost center
+ DeliveryServiceDate: 23.10.2016 (string) - Date of the delivery or service (DD.MM.YYYY)
+ ReceivedDate: 23.10.2016 (string) - Received date of the invoice (DD.MM.YYYY)
+ DocumentIndicator: R (string) - Document indicator (R=invoice, A=advance)
+ DocumentInputType: 001 (string) - Document input type (depending on the invoice type; 001, 002, ...)
+ DocumentNumber: 0009220  (string) - Number of the document-invoice (internal numbering)
+ VendorDocumentNumber: FA16234  (string) - Number of the original document-invoice (supplier numbering)
+ DocumentTotalAmount: 1220 (number) - Total amount of the document
+ DocumentTotalForeignAmount: 0 (number) - Total amount of the document in foreign currency 
+ DocumentType: DF (string) - Document subtype - used for booking models
+ FixedAssetAmount: 0 (number) - Amount for fixed assets supply
+ RealEstateAmount: 0 (number) - Amount for real estate supply
+ ForeignCurrency: USD (string) - Ident of foreign currency (eg. USD)
+ HomeTaxAmountForeignHigh: 0 (number) - Home tax on normal tax rate in foreign currency
+ HomeTaxAmountForeignLow: 0 (number) - Home tax on low tax rate in foreign currency
+ HomeTaxAmountHigh: 220 (number) - Home tax on normal tax rate
+ HomeTaxAmountLow: 0 (number) - Home tax on low tax rate
+ HomeTaxAmountSpecial: 0 (number) - Home tax on special tax rate
+ HomeTaxAmountForeignSpecial: 0 (number) - Home tax on special tax rate in foreign currency
+ HomeTaxBaseAmountForeignHigh: 0 (number) - Home base for normal tax rate in foreign currency
+ HomeTaxBaseAmountForeignLow: 0 (number) - Home base for low tax rate in foreign currency
+ HomeTaxBaseAmountForeignSpecial: 0 (number) - Home base for special tax rate in foreign currency
+ HomeTaxBaseAmountHigh: 1000 (number) - Home base for normal tax rate
+ HomeTaxBaseAmountLow: 0 (number) - Home base for low tax rate
+ HomeTaxBaseAmountSpecial: 0 (number) - Home base for special tax rate
+ IdentPartner: 000003  (string) - Ident of partner
+ InvoiceDate: 23.10.2016 (string) - Date of the invoice (DD.MM.YYYY)
+ IBAN: SI56 xxxx (string) - IBAN number
+ PaymentReference: SI00133354 (string) - Reference for payment
+ TaxDate: 23.10.2016 (string) - Date for tax (DD.MM.YYYY)
+ VATSubject: 1 (number) - Is subject to VAT calculation (1/0)
+ VATStatement: 1 (number) - Use bookings for finances (1/0)
+ VATUseModel: 0 (number) - Create bookings for finances based on pre-defined models (1/0)
+ ValueDate: 30.10.2016 (string) - Date for paymentt (DD.MM.YYYY)
+ ValueDays: 8 (number) - Days for calculating value date
+ DSFile: 2234 (string) - ID of document from external DMS

### VATReceived PUT data (object)
+ data (array)
    + (VATReceived GET ONE response)
        + Bookings (array)
            + (Bookings GET ONE response)

### HRMEducationCodeDegree GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ IdTypeOfEducation: `B336A7BC-DA9F-4094-8EFE-BE861881A94B` (string) - Type of education unique ID
+ Ident: `III.` (string) - Identification code
+ Name: `nižje poklicno izobraževanje (2 letno)` (string) - Eduation`s title
+ TypeOfEducation: 002 (string) - Identification number for education type
+ Vacation: 0 (number) - Number of vacation

### HRMEducationCodeDegree GET response (object)
+ data (array)
    + (HRMEducationCodeDegree GET ONE response)
+ meta (Get Meta)

### HRMEducationCodeDegree CREATE request (array) 
+ (object)
     + Ident: `III.` (string, required) - Identification code
     + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
     + Vacation: 0 (number) - Number of vacation

###  HRMEducationCodeDegree UPDATE request (array)
+ (object)
    + Ident: `III.` (string) - Education code degree Identification code
    + data (object) 
        + Ident: `III.` (string) - Identification code
        + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
        + Vacation: 0 (number) - Number of vacation

### HRMEducationCode GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ IdTypeOfEducation: `B336A7BC-DA9F-4094-8EFE-BE861881A94B` (string) - Type of education unique ID
+ Ident: `III.` (string) - Identification code
+ Name: `nižje poklicno izobraževanje (2 letno)` (string) - Eduation`s title
+ TypeOfEducation: 002 (string) - Identification number for education type
+ Vacation: 0 (number) - Number of vacation

### HRMEducationCode GET response (object)
+ data (array)
    + (HRMEducationCode GET ONE response)
+ meta (Get Meta)

### HRMEducationCode CREATE request (array) 
+ (object)
     + Ident: `III.` (string, required) - Identification code
     + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
     + Vacation: 0 (number) - Number of vacation

###  HRMEducationCode UPDATE request (array)
+ (object)
    + Ident: `III.` (string) - Education code Identification code
    + data (object) 
        + Ident: `III.` (string) - Identification code
        + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
        + Vacation: 0 (number) - Number of vacation

### HRMEducationCodeSKP GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ IdTypeOfEducation: `B336A7BC-DA9F-4094-8EFE-BE861881A94B` (string) - Type of education unique ID
+ Ident: `III.` (string) - Identification code
+ Name: `nižje poklicno izobraževanje (2 letno)` (string) - Eduation`s title
+ TypeOfEducation: 002 (string) - Identification number for education type
+ Vacation: 0 (number) - Number of vacation

### HRMEducationCodeSKP GET response (object)
+ data (array)
    + (HRMEducationCodeSKP GET ONE response)
+ meta (Get Meta)

### HRMEducationCodeSKP CREATE request (array) 
+ (object)
     + Ident: `III.` (string, required) - Identification code
     + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
     + Vacation: 0 (number) - Number of vacation

###  HRMEducationCodeSKP UPDATE request (array)
+ (object)
    + Ident: `III.` (string) - Education code skp Identification code
    + data (object) 
        + Ident: `III.` (string) - Identification code
        + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
        + Vacation: 0 (number) - Number of vacation

### HRMEducationCodeArea GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ IdTypeOfEducation: `B336A7BC-DA9F-4094-8EFE-BE861881A94B` (string) - Type of education code area unique ID
+ Ident: `III.` (string) - Identification code
+ Name: `nižje poklicno izobraževanje (2 letno)` (string) - Eduation`s title
+ TypeOfEducation: 002 (string) - Identification number for education type
+ Vacation: 0 (number) - Number of vacation

### HRMEducationCodeArea GET response (object)
+ data (array)
    + (HRMEducationCodeArea GET ONE response)
+ meta (Get Meta)

### HRMEducationCodeArea CREATE request (array) 
+ (object)
     + Ident: `III.` (string, required) - Identification code
     + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
     + Vacation: 0 (number) - Number of vacation

###  HRMEducationCodeArea UPDATE request (array)
+ (object)
    + Ident: `III.` (string) - Education code area Identification code
    + data (object) 
        + Ident: `III.` (string) - Identification code
        + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
        + Vacation: 0 (number) - Number of vacation

### HRMEducationCodeType GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ IdTypeOfEducation: `B336A7BC-DA9F-4094-8EFE-BE861881A94B` (string) - Type of education code type unique ID
+ Ident: `III.` (string) - Identification code
+ Name: `nižje poklicno izobraževanje (2 letno)` (string) - Eduation`s title
+ TypeOfEducation: 002 (string) - Identification number for education type
+ Vacation: 0 (number) - Number of vacation

### HRMEducationCodeType GET response (object)
+ data (array)
    + (HRMEducationCodeType GET ONE response)
+ meta (Get Meta)

### HRMEducationCodeType CREATE request (array) 
+ (object)
     + Ident: `III.` (string, required) - Identification code
     + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
     + Vacation: 0 (number) - Number of vacation

###  HRMEducationCodeType UPDATE request (array)
+ (object)
    + Ident: `III.` (string) - Education code type Identification code
    + data (object) 
        + Ident: `III.` (string) - Identification code
        + Name: `nižje poklicno izobraževanje (2 letno)` (string, required) - Eduation`s title
        + Vacation: 0 (number) - Number of vacation

### HRMTitleCodes GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Ident: `001` (string) - Identification code
+ Name: `Naziv` (string) - Name
+ ValidMonths: 6 (number) - ValidMonths


### HRMTitleCodes GET response (object)
+ data (array)
    + (HRMEducationCodeType GET ONE response)
+ meta (Get Meta)

### HRMTitleCodes CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Identification code
    + Name: `Naziv` (string) - Name
    + ValidMonths: 6 (number) - ValidMonths

###  HRMTitleCodes UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID` (string) - Education code type Identification code
    + data (object) 
        + Ident: `001` (string) - Identification code
        + Name: `Naziv` (string) - Name
        + ValidMonths: 6 (number) - ValidMonths

### HRMHabilitationCodeArea GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Ident: `001` (string) - Identification code
+ Name: `CodeArea` (string) - Name


### HRMHabilitationCodeArea GET response (object)
+ data (array)
    + (HRMEducationCodeType GET ONE response)
+ meta (Get Meta)

### HRMHabilitationCodeArea CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Identification code
    + Name: `Code area` (string) - Name

###  HRMHabilitationCodeArea UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID` (string) - Education code type Identification code
    + data (object) 
        + Ident: `001` (string) - Identification code
        + Name: `Code area` (string) - Name

### HRMEducationLocation GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Ident: `001` (string) - Identification code
+ Name: `CodeArea` (string) - Name
+ Street: `Ulica na roglo` (string) - Street
+ City: `Celje` (string) - City
+ PostOffice: `3214` (string) - PostOffice


### HRMEducationLocation GET response (object)
+ data (array)
    + (HRMEducationCodeType GET ONE response)
+ meta (Get Meta)

### HRMEducationLocation CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Identification code
    + Name: `Code area` (string) - Name
    + Street: `Ulica na roglo` (string) - Street
    + City: `Celje` (string) - City
    + PostOffice: `3214` (string) - PostOffice

###  HRMEducationLocation UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID` (string) - Education code type Identification code
    + data (object) 
        + Ident: `001` (string) - Identification code
        + Name: `Code area` (string) - Name
        + Street: `Ulica na roglo` (string) - Street
        + City: `Celje` (string) - City
        + PostOffice: `3214` (string) - PostOffice


### HRMCatalogTraining GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Name: `Varstvo pri delu` (string) - Name
+ Ident: `001` (string) - Ident
+ ValidMonths: 12 (number) - ValidMonths
+ NumberOfPoints: 100 (number) - NumberOfPointsty
+ TypeOfTraining: `001` (string) - TypeOfTraining
+ GroupOfTraining: `001` (string) - GroupOfTraining
+ FieldOfTraining: `851` (string) - FieldOfTraining
+ ProfessionalExamination: 1 (number) - ProfessionalExamination
+ VisibleOnWorkPlace: 1 (number) - VisibleOnWorkPlace


### HRMCatalogTraining GET response (object)
+ data (array)
    + (HRMCatalogTraining GET ONE response)
+ meta (Get Meta)

### HRMCatalogTraining CREATE request (array) 
+ (object)
    + Name: `Varstvo pri delu` (string) - Name
    + Ident: `001` (string) - Ident
    + ValidMonths: 12 (number) - ValidMonths
    + NumberOfPoints: 100 (number) - NumberOfPointsty
    + TypeOfTraining: `001` (string) - TypeOfTraining
    + GroupOfTraining: `001` (string) - GroupOfTraining
    + FieldOfTraining: `851` (string) - FieldOfTraining
    + ProfessionalExamination: 1 (number) - ProfessionalExamination
    + VisibleOnWorkPlace: 1 (number) - VisibleOnWorkPlace

###  HRMCatalogTraining UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Name: `Varstvo pri delu` (string) - Name
        + Ident: `001` (string) - Ident
        + ValidMonths: 12 (number) - ValidMonths
        + NumberOfPoints: 100 (number) - NumberOfPointsty
        + TypeOfTraining: `001` (string) - TypeOfTraining
        + GroupOfTraining: `001` (string) - GroupOfTraining
        + FieldOfTraining: `851` (string) - FieldOfTraining
        + ProfessionalExamination: 1 (number) - ProfessionalExamination
        + VisibleOnWorkPlace: 1 (number) - VisibleOnWorkPlace



### HRMTraining GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Description: `Varstvo pri delu` (string) - Name
+ Ident: `001` (string) - Ident
+ ValidMonths: 12 (number) - ValidMonths
+ IdWayOfTraining: `Interno` (string) - Interno or Externo
+ DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
+ DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
+ ValidDate: `2016-08-31T22:00:00+00:00` (string) - ValidDate
+ IncreaseDateFrom: `2016-08-31T22:00:00+00:00` (string) - IncreaseDateFrom
+ IncreaseDateTo: `2016-08-31T22:00:00+00:00` (string) - IncreaseDateTo
+ CatalogTraining: `Varstvo pri delu` (string) - CatalogTraining
+ TypeOfTraining: `Obvezno izobraževanje` (string) - TypeOfTraining
+ CodeArea: `851` (string) - CodeArea
+ EducationLocation: `001` (string) - EducationLocation
+ Country: `001` (string) - Country
+ Instructor: `001` (string) - Instructor
+ StateStatus: `001` (string) - StateStatus
+ KnowledgeTest: 0 (number) - KnowledgeTest, 1 or 0
+ Abroad: 0 (number) - Abroad, 1 or 0
+ ContractualObligation: 0 (number) - ContractualObligation, 1 or 0
+ DurationInsideWorkTime: 5 (number) - DurationInsideWorkTime
+ DurationOutsideWorkTime: 5 (number) - DurationOutsideWorkTime
+ DurationHours: 5 (number) - DurationHours
+ DurationDays: 5 (number) - DurationDays
+ NumberOfPoints: 5 (number) - NumberOfPoints
+ Costs: 5 (number) - Costs


### HRMTraining GET response (object)
+ data (array)
    + (HRMTraining GET ONE response)
+ meta (Get Meta)

### HRMTraining CREATE request (array) 
+ (object)
    + Description: `Varstvo pri delu` (string) - Name
    + Ident: `001` (string) - Ident
    + ValidMonths: 12 (number) - ValidMonths
    + IdWayOfTraining: `Interno` (string) - Interno or Externo
    + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
    + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
    + ValidDate: `2016-08-31T22:00:00+00:00` (string) - ValidDate
    + IncreaseDateFrom: `2016-08-31T22:00:00+00:00` (string) - IncreaseDateFrom
    + IncreaseDateTo: `2016-08-31T22:00:00+00:00` (string) - IncreaseDateTo
    + CatalogTraining: `Varstvo pri delu` (string) - CatalogTraining
    + TypeOfTraining: `Obvezno izobraževanje` (string) - TypeOfTraining
    + CodeArea: `851` (string) - CodeArea
    + EducationLocation: `001` (string) - EducationLocation
    + Country: `001` (string) - Country
    + Instructor: `001` (string) - Instructor
    + StateStatus: `001` (string) - StateStatus
    + KnowledgeTest: 0 (number) - KnowledgeTest, 1 or 0
    + Abroad: 0 (number) - Abroad, 1 or 0
    + ContractualObligation: 0 (number) - ContractualObligation, 1 or 0
    + DurationInsideWorkTime: 5 (number) - DurationInsideWorkTime
    + DurationOutsideWorkTime: 5 (number) - DurationOutsideWorkTime
    + DurationHours: 5 (number) - DurationHours
    + DurationDays: 5 (number) - DurationDays
    + NumberOfPoints: 5 (number) - NumberOfPoints
    + Costs: 5 (number) - Costs

###  HRMTraining UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string) -  ID` (string)
    + data (object) 
        + Description: `Varstvo pri delu` (string) - Name
        + Ident: `001` (string) - Ident
        + ValidMonths: 12 (number) - ValidMonths
        + IdWayOfTraining: `Interno` (string) - Interno or Externo
        + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
        + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
        + ValidDate: `2016-08-31T22:00:00+00:00` (string) - ValidDate
        + IncreaseDateFrom: `2016-08-31T22:00:00+00:00` (string) - IncreaseDateFrom
        + IncreaseDateTo: `2016-08-31T22:00:00+00:00` (string) - IncreaseDateTo
        + CatalogTraining: `Varstvo pri delu` (string) - CatalogTraining
        + TypeOfTraining: `Obvezno izobraževanje` (string) - TypeOfTraining
        + CodeArea: `851` (string) - CodeArea
        + EducationLocation: `001` (string) - EducationLocation
        + Country: `001` (string) - Country
        + Instructor: `001` (string) - Instructor
        + StateStatus: `001` (string) - StateStatus
        + KnowledgeTest: 0 (number) - KnowledgeTest, 1 or 0
        + Abroad: 0 (number) - Abroad, 1 or 0
        + ContractualObligation: 0 (number) - ContractualObligation, 1 or 0
        + DurationInsideWorkTime: 5 (number) - DurationInsideWorkTime
        + DurationOutsideWorkTime: 5 (number) - DurationOutsideWorkTime
        + DurationHours: 5 (number) - DurationHours
        + DurationDays: 5 (number) - DurationDays
        + NumberOfPoints: 5 (number) - NumberOfPoints
        + Costs: 5 (number) - Costs



### HRMInstructor GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Ident: `001` (string) - Ident
+ Worker: `001` (string) - Worker -send or worker or crmpartner, if "notranji" then worker else CrmPartner
+ CrmPartner: `001` (string) - CrmPartner
+ Amount: 100 (number) - Amount
+ IdTypeOfInstructor: `Notranji` (string) - IdTypeOfInstructor, Notranji or zunanji
+ Training: `001` (string) - Training Ident
+ Instructor: `001` (string) - Instructor Ident
+ Firstname: `Janez` (string) - Firstname Ident
+ Lastname: `Novak` (string) - Lastname Ident
+ RegistrationNumber: `1234567894566` (string) - RegistrationNumber Ident
+ TaxCode: `78945612` (string) - TaxCode Ident
+ Street: `78945612` (string) - Street Ident
+ Phone: `78945612` (string) - Phone Ident
+ GSM: `78945612` (string) - GSM Ident
+ IBAN: `78945612` (string) - IBAN Ident
+ PostOffice: `3210` (string) - PostOffice Ident

### HRMInstructor GET response (object)
+ data (array)
    + (HRMInstructor GET ONE response)
+ meta (Get Meta)

### HRMInstructor CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Ident
    + Worker: `001` (string) - Worker -send or worker or crmpartner, if "notranji" then worker else CrmPartner
    + CrmPartner: `001` (string) - CrmPartner
    + Amount: 100 (number) - Amount
    + IdTypeOfInstructor: `Notranji` (string) - IdTypeOfInstructor, Notranji or zunanji
    + Training: `001` (string) - Training Ident
    + Instructor: `001` (string) - Instructor Ident
    + Firstname: `Janez` (string) - Firstname Ident
    + Lastname: `Novak` (string) - Lastname Ident
    + RegistrationNumber: `1234567894566` (string) - RegistrationNumber Ident
    + TaxCode: `78945612` (string) - TaxCode Ident
    + Street: `78945612` (string) - Street Ident
    + Phone: `78945612` (string) - Phone Ident
    + GSM: `78945612` (string) - GSM Ident
    + IBAN: `78945612` (string) - IBAN Ident
    + PostOffice: `3210` (string) - PostOffice Ident



###  HRMInstructor UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Ident: `001` (string) - Ident
        + Worker: `001` (string) - Worker -send or worker or crmpartner, if "notranji" then worker else CrmPartner
        + CrmPartner: `001` (string) - CrmPartner
        + Amount: 100 (number) - Amount
        + IdTypeOfInstructor: `Notranji` (string) - IdTypeOfInstructor, Notranji or zunanji
        + Training: `001` (string) - Training Ident
        + Instructor: `001` (string) - Instructor Ident
        + Firstname: `Janez` (string) - Firstname Ident
        + Lastname: `Novak` (string) - Lastname Ident
        + RegistrationNumber: `1234567894566` (string) - RegistrationNumber Ident
        + TaxCode: `78945612` (string) - TaxCode Ident
        + Street: `78945612` (string) - Street Ident
        + Phone: `78945612` (string) - Phone Ident
        + GSM: `78945612` (string) - GSM Ident
        + IBAN: `78945612` (string) - IBAN Ident
        + PostOffice: `3210` (string) - PostOffice Ident


### HRMTrainingCosts GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Ident: `001` (string) - Ident
+ Worker: `001` (string) - Worker
+ TypeOfCost: `001` (string) - TypeOfCost
+ CostName: `Strošek` (string) - CostName
+ WorkerCost: 1 (number) - WorkerCost
+ Amount: 100 (number) - Amount
+ AmountPart: 10 (number) - AmountPart
+ AmountPartNum: 10 (number) - AmountPartNum
+ AmountPaid: 20 (number) - AmountPaid
+ Training: `001` (string) - Training Ident


### HRMTrainingCosts GET response (object)
+ data (array)
    + (HRMTrainingCosts GET ONE response)
+ meta (Get Meta)

### HRMTrainingCosts CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Ident
    + Worker: `001` (string) - Worker
    + TypeOfCost: `001` (string) - TypeOfCost
    + CostName: `Strošek` (string) - CostName
    + WorkerCost: 1 (number) - WorkerCost
    + Amount: 100 (number) - Amount
    + AmountPart: 10 (number) - AmountPart
    + AmountPartNum: 10 (number) - AmountPartNum
    + AmountPaid: 20 (number) - AmountPaid
    + Training: `001` (string) - Training Ident


###  HRMTrainingCosts UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Ident: `001` (string) - Ident
        + Worker: `001` (string) - Worker
        + TypeOfCost: `001` (string) - TypeOfCost
        + CostName: `Strošek` (string) - CostName
        + WorkerCost: 1 (number) - WorkerCost
        + Amount: 100 (number) - Amount
        + AmountPart: 10 (number) - AmountPart
        + AmountPartNum: 10 (number) - AmountPartNum
        + AmountPaid: 20 (number) - AmountPaid
        + Training: `001` (string) - Training Ident

### HRMTrainingParticipants GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Ident: `001` (string) - Ident
+ Worker: `001` (string) - Worker
+ CostCenter: `001` (string) - CostCenter
+ AcquiredDate: `2016-08-31T22:00:00+00:00` (string) - AcquiredDate
+ ContractualObligationDateTo: `2016-08-31T22:00:00+00:00` (string) - ContractualObligationDateTo
+ CertificateOfCompetence: `Da` (string) - CertificateOfCompetence
+ Description: `Da` (string) - Description
+ CertificateOfCompetence: `Da` (string) - CertificateOfCompetence
+ ContractNumber: `123423` (string) - ContractNumber
+ ContractDescription: `Opis pogodbe` (string) - ContractDescription
+ ContractualObligation: 0 (number) - ContractualObligation, 1 or zero
+ AcquiredKnowledge: 0 (number) - AcquiredKnowledge, 1 or zero
+ Training: `001` (string) - Training Ident



### HRMTrainingParticipants GET response (object)
+ data (array)
    + (HRMTrainingParticipants GET ONE response)
+ meta (Get Meta)

### HRMTrainingParticipants CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Ident
    + Worker: `001` (string) - Worker
    + CostCenter: `001` (string) - CostCenter
    + AcquiredDate: `2016-08-31T22:00:00+00:00` (string) - AcquiredDate
    + ContractualObligationDateTo: `2016-08-31T22:00:00+00:00` (string) - ContractualObligationDateTo
    + CertificateOfCompetence: `Da` (string) - CertificateOfCompetence
    + Description: `Da` (string) - Description
    + CertificateOfCompetence: `Da` (string) - CertificateOfCompetence
    + ContractNumber: `123423` (string) - ContractNumber
    + ContractDescription: `Opis pogodbe` (string) - ContractDescription
    + ContractualObligation: 0 (number) - ContractualObligation, 1 or zero
    + AcquiredKnowledge: 0 (number) - AcquiredKnowledge, 1 or zero
    + Training: `001` (string) - Training Ident


###  HRMTrainingParticipants UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Ident: `001` (string) - Ident
        + Worker: `001` (string) - Worker
        + CostCenter: `001` (string) - CostCenter
        + AcquiredDate: `2016-08-31T22:00:00+00:00` (string) - AcquiredDate
        + ContractualObligationDateTo: `2016-08-31T22:00:00+00:00` (string) - ContractualObligationDateTo
        + CertificateOfCompetence: `Da` (string) - CertificateOfCompetence
        + Description: `Da` (string) - Description
        + CertificateOfCompetence: `Da` (string) - CertificateOfCompetence
        + ContractNumber: `123423` (string) - ContractNumber
        + ContractDescription: `Opis pogodbe` (string) - ContractDescription
        + ContractualObligation: 0 (number) - ContractualObligation, 1 or zero
        + AcquiredKnowledge: 0 (number) - AcquiredKnowledge, 1 or zero
        + AmountPaid: 20 (number) - AmountPaid
        + Training: `001` (string) - Training Ident

### HRMEducationProgramType GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Name: `001` (string) - Name
+ Ident: `001` (string) - Ident

### HRMEducationProgramType GET response (object)
+ data (array)
    + (HRMEducationProgramType GET ONE response)
+ meta (Get Meta)

### HRMEducationProgramType CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Ident
    + Name: `001` (string) - Name


###  HRMEducationProgramType UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Name: `001` (string) - Name
        + Ident: `001` (string) - Ident




### HRMWorkerInsurance GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
+ DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
+ InsuranceAmount: 10.54 (number) - InsuranceAmount
+ InsurancePolicy: `1234567` (string) - InsurancePolicy
+ Worker: `001` (string) - Worker
+ TypeOfInsurance: `001` (string) - TypeOfInsurance
+ InterruptionReason: `001` (string) - InterruptionReason
+ FondsCodes: `001` (string) - FondsCodes
+ InsuranceCompany: `001` (string) - InsuranceCompany
+ PremiumClass: `001` (string) - PremiumClass


### HRMWorkerInsurance GET response (object)
+ data (array)
    + (HRMWorkerInsurance GET ONE response)
+ meta (Get Meta)

### HRMWorkerInsurance CREATE request (array) 
+ (object)
    + Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
    + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
    + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
    + InsuranceAmount: 10.54 (number) - InsuranceAmount
    + InsurancePolicy: `1234567` (string) - InsurancePolicy
    + Worker: `001` (string) - Worker
    + TypeOfInsurance: `001` (string) - TypeOfInsurance
    + InterruptionReason: `001` (string) - InterruptionReason
    + FondsCodes: `001` (string) - FondsCodes
    + InsuranceCompany: `001` (string) - InsuranceCompany
    + PremiumClass: `001` (string) - PremiumClass

###  HRMWorkerInsurance UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
        + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
        + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
        + InsuranceAmount: 10.54 (number) - InsuranceAmount
        + InsurancePolicy: `1234567` (string) - InsurancePolicy
        + Worker: `001` (string) - Worker
        + TypeOfInsurance: `001` (string) - TypeOfInsurance
        + InterruptionReason: `001` (string) - InterruptionReason
        + FondsCodes: `001` (string) - FondsCodes
        + InsuranceCompany: `001` (string) - InsuranceCompany
        + PremiumClass: `001` (string) - PremiumClass


### HRMYearlyReview GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ YearOfReview: 2015 (number) - YearOfReview
+ ComplainDate: `2016-08-31T22:00:00+00:00` (string) - ComplainDate
+ Date: `2016-08-31T22:00:00+00:00` (string) - Date
+ Worker: `001` (string) - Worker
+ Assessor: `001` (string) - Assessor
+ Description: `Yearly review` (string) - Description
+ ComplainDescription: `Some text` (string) - ComplainDescription
+ WorkResultExpertise: 3 (number) - WorkResultExpertise
+ WorkResultScopeOfWork: 3 (number) - WorkResultScopeOfWork
+ WorkResultTimely: 3 (number) - WorkResultTimely
+ Autonomy: 3 (number) - Autonomy
+ AutonomyCreativity: 3 (number) - AutonomyCreativity
+ AutonomyAccuracy: 3 (number) - AutonomyAccuracy
+ Reliability: 3 (number) - Reliability
+ ReliabilityCooperation: 3 (number) - ReliabilityCooperation
+ ReliabilityLabourOrganisation: 3 (number) - ReliabilityLabourOrganisation
+ OtherSkillsInterdisciplinarity: 3 (number) - OtherSkillsInterdisciplinarity
+ OtherSkillsAttitudeTowardsUsers: 3 (number) - OtherSkillsAttitudeTowardsUsers
+ OtherSkillsCommunication: 3 (number) - OtherSkillsCommunication
+ OtherSkillsOther: 3 (number) - OtherSkillsOther
+ AverageGrade: 3 (number) - AverageGrade
+ WorkResultAverage: 3 (number) - WorkResultAverage
+ AutonomyAverage: 3 (number) - AutonomyAverage
+ ReliabilityAverage: 3 (number) - ReliabilityAverage
+ QualityAverage: 3.4 (number) - QualityAverage
+ OtherSkillsAverage: 3.2 (number) - OtherSkillsAverage
+ Complain: 1 (number) - Complain 1 or 0



### HRMYearlyReview GET response (object)
+ data (array)
    + (HRMYearlyReview GET ONE response)
+ meta (Get Meta)

### HRMYearlyReview CREATE request (array) 
+ (object)
    + Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
    + YearOfReview: 2015 (number) - YearOfReview
    + ComplainDate: `2016-08-31T22:00:00+00:00` (string) - ComplainDate
    + Date: `2016-08-31T22:00:00+00:00` (string) - Date
    + Worker: `001` (string) - Worker
    + Assessor: `001` (string) - Assessor
    + Description: `Yearly review` (string) - Description
    + ComplainDescription: `Some text` (string) - ComplainDescription
    + WorkResultExpertise: 3 (number) - WorkResultExpertise
    + WorkResultScopeOfWork: 3 (number) - WorkResultScopeOfWork
    + WorkResultTimely: 3 (number) - WorkResultTimely
    + Autonomy: 3 (number) - Autonomy
    + AutonomyCreativity: 3 (number) - AutonomyCreativity
    + AutonomyAccuracy: 3 (number) - AutonomyAccuracy
    + Reliability: 3 (number) - Reliability
    + ReliabilityCooperation: 3 (number) - ReliabilityCooperation
    + ReliabilityLabourOrganisation: 3 (number) - ReliabilityLabourOrganisation
    + OtherSkillsInterdisciplinarity: 3 (number) - OtherSkillsInterdisciplinarity
    + OtherSkillsAttitudeTowardsUsers: 3 (number) - OtherSkillsAttitudeTowardsUsers
    + OtherSkillsCommunication: 3 (number) - OtherSkillsCommunication
    + OtherSkillsOther: 3 (number) - OtherSkillsOther
    + AverageGrade: 3 (number) - AverageGrade
    + WorkResultAverage: 3 (number) - WorkResultAverage
    + AutonomyAverage: 3 (number) - AutonomyAverage
    + ReliabilityAverage: 3 (number) - ReliabilityAverage
    + QualityAverage: 3.4 (number) - QualityAverage
    + OtherSkillsAverage: 3.2 (number) - OtherSkillsAverage
    + Complain: 1 (number) - Complain 1 or 0



###  HRMYearlyReview UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
        + YearOfReview: 2015 (number) - YearOfReview
        + ComplainDate: `2016-08-31T22:00:00+00:00` (string) - ComplainDate
        + Date: `2016-08-31T22:00:00+00:00` (string) - Date
        + Worker: `001` (string) - Worker
        + Assessor: `001` (string) - Assessor
        + Description: `Yearly review` (string) - Description
        + ComplainDescription: `Some text` (string) - ComplainDescription
        + WorkResultExpertise: 3 (number) - WorkResultExpertise
        + WorkResultScopeOfWork: 3 (number) - WorkResultScopeOfWork
        + WorkResultTimely: 3 (number) - WorkResultTimely
        + Autonomy: 3 (number) - Autonomy
        + AutonomyCreativity: 3 (number) - AutonomyCreativity
        + AutonomyAccuracy: 3 (number) - AutonomyAccuracy
        + Reliability: 3 (number) - Reliability
        + ReliabilityCooperation: 3 (number) - ReliabilityCooperation
        + ReliabilityLabourOrganisation: 3 (number) - ReliabilityLabourOrganisation
        + OtherSkillsInterdisciplinarity: 3 (number) - OtherSkillsInterdisciplinarity
        + OtherSkillsAttitudeTowardsUsers: 3 (number) - OtherSkillsAttitudeTowardsUsers
        + OtherSkillsCommunication: 3 (number) - OtherSkillsCommunication
        + OtherSkillsOther: 3 (number) - OtherSkillsOther
        + AverageGrade: 3 (number) - AverageGrade
        + WorkResultAverage: 3 (number) - WorkResultAverage
        + AutonomyAverage: 3 (number) - AutonomyAverage
        + ReliabilityAverage: 3 (number) - ReliabilityAverage
        + QualityAverage: 3.4 (number) - QualityAverage
        + OtherSkillsAverage: 3.2 (number) - OtherSkillsAverage
        + Complain: 1 (number) - Complain 1 or 0


### HRMCodification GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Title: `Redno zaposleni` (string) - Title
+ Description: `Redno zaposleni` (string) - Description
+ Code: `001` (string) - Code
+ CodificationType: `PersonsGroup` (string) - CodificationType

### HRMCodification GET response (object)
+ data (array)
    + (HRMCodification GET ONE response)
+ meta (Get Meta)

### HRMCodification CREATE request (array) 
+ (object)
    + Title: `Redno zaposleni` (string) - Title
    + Description: `Redno zaposleni` (string) - Description
    + Code: `001` (string) - Code
    + CodificationType: `PersonsGroup` (string) - CodificationType


###  HRMCodification UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Title: `Redno zaposleni` (string) - Title
        + Description: `Redno zaposleni` (string) - Description
        + Code: `001` (string) - Code
        + CodificationType: `PersonsGroup` (string) - CodificationType


### HRMEducationInstitute GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ Name: `001` (string) - Name
+ Ident: `001` (string) - Ident

### HRMEducationInstitute GET response (object)
+ data (array)
    + (HRMEducationInstitute GET ONE response)
+ meta (Get Meta)

### HRMEducationInstitute CREATE request (array) 
+ (object)
    + Ident: `001` (string) - Ident
    + Name: `001` (string) - Name


###  HRMEducationInstitute UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + Name: `001` (string) - Name
        + Ident: `001` (string) - Ident


### HRMWorkerAttribute GET ONE response (object)    
+ Id: `06589E2C-71B2-4E3A-9D33-11A15C696E9E` (string) - Unique ID
+ DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
+ DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
+ Worker: `001` (string) - Worker
+ OrganizationalUnit: `001` (string) - OrganizationalUnit
+ Department: `001` (string) - Department
+ CostCenter: `001` (string) - CostCenter
+ AttributeOne: `001` (string) - CBCostCarrier
+ WorkAreaIdent: `001` (string) - WorkAreaIdent
+ WorkOrder: `001` (string) - WorkOrder
+ WorkPlace: `DM1` (string) - WorkPlace
+ AttributePercent: 100 (number) (string) - WorkPlace
+ HomeCostCenter: 1 (number) - HomeCostCenter

### HRMWorkerAttribute GET response (object)
+ data (array)
    + (HRMWorkerAttribute GET ONE response)
+ meta (Get Meta)

### HRMWorkerAttribute CREATE request (array) 
+ (object)
    + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
    + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
    + Worker: `001` (string) - Worker
    + OrganizationalUnit: `001` (string) - OrganizationalUnit
    + Department: `001` (string) - Department
    + CostCenter: `001` (string) - CostCenter
    + AttributeOne: `001` (string) - CBCostCarrier
    + WorkAreaIdent: `001` (string) - WorkAreaIdent
    + WorkOrder: `001` (string) - WorkOrder
    + WorkPlace: `DM1` (string) - WorkPlace
    + AttributePercent: 100 (number) - WorkPlace
    + HomeCostCenter: 1 (number) - HomeCostCenter


###  HRMWorkerAttribute UPDATE request (array)
+ (object)
    + Id: `e5a8c44e-d172-4bc9-aaf8-4b79503dee16`(string)
    + data (object) 
        + DateFrom: `2016-08-31T22:00:00+00:00` (string) - DateFrom
        + DateTo: `2016-08-31T22:00:00+00:00` (string) - DateTo
        + Worker: `001` (string) - Worker
        + OrganizationalUnit: `001` (string) - OrganizationalUnit
        + Department: `001` (string) - Department
        + CostCenter: `001` (string) - CostCenter
        + AttributeOne: `001` (string) - CBCostCarrier
        + WorkAreaIdent: `001` (string) - WorkAreaIdent
        + WorkOrder: `001` (string) - WorkOrder
        + WorkPlace: `DM1` (string) - WorkPlace
        + AttributePercent: 100 (number) - WorkPlace
        + HomeCostCenter: 1 (number) - HomeCostCenter