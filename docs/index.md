**O~2~**

**Interface Specification**

**37229 Product Offering Qualification API**

Version 1.3

Definitions and abbreviations
=============================

Definitions
-----------

  ---------- ---------------------------------
  **Term**   **Definition**
  ReST       Representational state transfer
  JSON       JavaScript Object Notation
  ---------- ---------------------------------

Introduction
============

Overview
--------

This Product Offering Qualification API documented here define and
describe the functionality related to the product offerings of the PAYM
consumer subscriber. This API supports following capabilities.

-   Retrieve the valid productofferings available for the subscriber

-   Validate if the product offering can be added to customer’s account

-   Retrieve the valid Tariff offerings available for the subscriber

-   Validate if the subscriber’s tariff change is allowed

-   Determine the subscriber’s current tariff Bolton products that are
    compatible to the new tariff.

Resources Summary
=================

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Resource Purpose**                     **Resource URI**
  ---------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------
                                           

  Get Valid Product Offerings              GET /api/productOfferingQualificationManagement/v1/productOffering/{msisdn}

  Get Product Offering Business Policies   Get
                                           
                                           /*api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/businessPolicies*

  Get Valid Tariff Offerings               *GET *
                                           
                                           */api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/tariffOfferings*

  Get Tariff Offering Business Policies    *GET /api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/tariff/businessPolicies*

  Get Tariff Compatible Products           *GET*
                                           
                                           */api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/tariff/compatibleProducts?newTariffOfferId={newTariffOfferId}*
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

HTTP Request Headers 
---------------------

Each service operation accepts O2 standard HTTP headers. Refer to
‘***API Management Gateway - Consumer Application Connectivity Guide***’
for the full list of headers to be sent.

Resource Definition
===================

Get Valid Product Offerings
---------------------------

  ------------------------------------------------------------------------------------------------------------------
  **Resource URI**   GET
                     
                     /api/productOfferingQualificationManagement/v1/productOffering/{msisdn}
  ------------------ -----------------------------------------------------------------------------------------------
  **Description**    This function returns the list of product offerings that the customer can add to its account.

  **Content Type**   application/json
  ------------------------------------------------------------------------------------------------------------------

### Input () and Output () parameters

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**                       **Is Mandatory**   **Type**   **Description**
  -------------------- ----------------------------------- ------------------ ---------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   msisdn             String                              Yes                Path       Mobile phone number for which the product offerings will be returned. It should be international format.
                                                                                         
                                                                                         E.g. 447720342101

  tariffOfferId       String                              No                 Query      Id of the target tariff offer. This field should be passed only when compatible products for the new tariff offer is required.

  returnConflicts     String                              No                 Query      Flag to request the conflict offerings in SOA response. If this flag is not sent, SOA will filter out the offerings which has conflicts with customer’s existing products.
                                                                                         
                                                                                         Allowed value is:
                                                                                         
                                                                                         “Y”

  myOfferings         [offeringType](#offeringtype)\[\]   No                 Body       This is an array of product offerings. Refer to [Appendix A](#appendix_a__1) for offering details returned.
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Success and Fault Definitions

  **HTTP Status Code**   **Error Code**                              **Description**                                                                          **Category**
  ---------------------- ------------------------------------------- ---------------------------------------------------------------------------------------- --------------
  200                    N/A                                         N/A                                                                                      Success
  200                    productofferingqualification-37229-3602-E   Subscriber is not active.                                                                Business
  400                    productofferingqualification-37229-4501-V   Invalid Request. Please check the input and resubmit.                                    Validation
  400                    productofferingqualification-37229-4000-V   The requested application or channel is either not recognised or invalid.                Validation
  408                    productofferingqualification-37229-2502-F   Backend service call timed out. Please try again later.                                  Technical
  503                    productofferingqualification-37229-2501-F   One or more back end services are not available at the moment. Please try again later.   Technical
  404                    productofferingqualification-37229-3601-E   Subscriber is either not recognised or cannot be found.                                  Business
  500                    productofferingqualification-37229-3612-E   Internal service error has occurred.                                                     Technical

### Sample Request and Responses

#### Success scenario

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342101*

**Request**

  ------------------
  No request body.
  ------------------

**Response**

**HTTP/1.1**: 200 OK

  ----------------------------------------------
  {
  
  "myOfferings":\[
  
  {
  
  "offerId":"20000019",
  
  "offerCode":"3GBBOLTON:1",
  
  "externalId":"3GBBOLTON",
  
  "name":"3GB Data Bolt On",
  
  "description":"3GB Snacking Data Bolt On ",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"200"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155212058013161778",
  
  "offeringGroupName":"Data Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"Data",
  
  "value":"3221225472"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"22000002",
  
  "offerCode":"100MMS:1",
  
  "externalId":"100MMS",
  
  "name":"100 MMS",
  
  "description":"100 MMS",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"100"
  
  }
  
  > \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490440913240014",
  
  "offeringGroupName":"MMS Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"MMS",
  
  "value":"100"
  
  }
  
  \]
  
  }
  
  \]
  
  }
  ----------------------------------------------

#### Success scenario – where conflicts offerId’s are returned

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342101?returnConflicts=’Y’*

**Request**

  ------------------
  No request body.
  ------------------

**Response**

**HTTP/1.1**: 200 OK

  --------------------------------------------------
  {
  
  "myOfferings":\[
  
  {
  
  "offerId":"20000019",
  
  "offerCode":"3GBBOLTON:1",
  
  "externalId":"3GBBOLTON",
  
  "name":"3GB Data Bolt On",
  
  "description":"3GB Snacking Data Bolt On ",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"200"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155212058013161778",
  
  "offeringGroupName":"Data Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"Data",
  
  "value":"3221225472"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"22000002",
  
  "offerCode":"100MMS:1",
  
  "externalId":"100MMS",
  
  "name":"100 MMS",
  
  "description":"100 MMS",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"100"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490440913240014",
  
  "offeringGroupName":"MMS Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"MMS",
  
  "value":"100"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"90081021",
  
  "offerCode":"O2TRAVEL:1",
  
  "externalId":"O2TRAVEL",
  
  "name":"O2 Travel",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"MRC",
  
  "value":"0"
  
  }
  
  \],
  
  "conflicts":\[
  
  {
  
  "offerId":"20000030"
  
  },
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490460613240017",
  
  "offeringGroupName":"Roaming Recurrent Bolt Ons"
  
  }
  
  }
  
  \]
  
  }
  --------------------------------------------------

#### Success scenario – with Perk Product and mandatory characteristic

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342101*

**Request**

  ------------------
  No request body.
  ------------------

**Response**

**HTTP/1.1**: 200 OK

  ----------------------------------------------
  {
  
  "myOfferings":\[
  
  {
  
  "offerId":"20000019",
  
  "offerCode":"3GBBOLTON:1",
  
  "externalId":"3GBBOLTON",
  
  "name":"3GB Data Bolt On",
  
  "description":"3GB Snacking Data Bolt On ",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"200"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155212058013161778",
  
  "offeringGroupName":"Data Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"Data",
  
  "value":"3221225472"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"22000002",
  
  "offerCode":"100MMS:1",
  
  "externalId":"100MMS",
  
  "name":"100 MMS",
  
  "description":"100 MMS",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"100"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490440913240014",
  
  "offeringGroupName":"MMS Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"MMS",
  
  "value":"100"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"26000005",
  
  "offerCode":"CAFYN:1",
  
  "externalId":"CAFYN",
  
  "name":"Cafeyn",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"MRC",
  
  "value":"300"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9158073895513816860",
  
  "offeringGroupName":"Books & Magazines"
  
  },
  
  "chars":
  
  {
  
  "name":"Extra Type",
  
  "value":\[
  
  "Free Only"
  
  \],
  
  "mandatory":"true"
  
  }
  
  },
  
  {
  
  "offerId":"26000008",
  
  "offerCode":"MCAFMSS:1",
  
  "externalId":"MCAFMSS",
  
  "name":"McAfee",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"MRC",
  
  "value":"500"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9158073896513816860",
  
  "offeringGroupName":"Digital Productivity"
  
  },
  
  "chars":
  
  {
  
  "name":"Extra Type",
  
  "value":\[
  
  "Paid Only"
  
  \],
  
  "mandatory":"true"
  
  }
  
  }
  
  \]
  
  }
  ----------------------------------------------

#### Fault scenario – MSISDN Not Found

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342107*

**Request**

  -----------------
  No request body
  -----------------

**Response:**

**HTTP/1.1**: 404 Not Found

  -----------------------------------------------------------------------
  {
  
  "error": {
  
  "code": "productofferingqualification-37229-3601-E",
  
  "message": "Subscriber is either not recognised or cannot be found.”,
  
  "faultTrace": \[
  
  {
  
  "faultCode": "404",
  
  "faultDescription": "Not Found"
  
  }
  
  \]
  
  }
  
  }
  -----------------------------------------------------------------------

[[[[[[[[[[[[[[[[[[[[[[[[[[[[]{#appendix__a .anchor}]{#appendix_b_
.anchor}]{#appendix_c_ .anchor}]{#appendix_cb_ .anchor}]{#appendix_e_-1
.anchor}]{#appendix_e_ .anchor}]{#appendix_f_ .anchor}]{#appendix_gf_
.anchor}]{#appendix_fe_ .anchor}]{#appendix_g_- .anchor}]{#appendix_h_-
.anchor}]{#appendix_hf_- .anchor}]{#appendix_h_ .anchor}]{#appendix_ig_
.anchor}]{#_Appendix__A .anchor}]{#_Appendix_B_–
.anchor}]{#_Appendix_C_– .anchor}]{#_Appendix_CB_–
.anchor}]{#_Appendix_E–_ .anchor}]{#_Appendix_E_–
.anchor}]{#_Appendix_F_– .anchor}]{#_Appendix_GF_–
.anchor}]{#_Appendix_Fe_– .anchor}]{#_Appendix_G_-
.anchor}]{#_Appendix_H_- .anchor}]{#_Appendix_Hf_-
.anchor}]{#_Appendix_H_– .anchor}]{#_Appendix_Ig_– .anchor}

Data Types
----------

### offeringType

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**                             **Is Mandatory**   **Description**
  -------------------- ----------------------------------------- ------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  offerId              String                                    Yes                Id of the offering.

  offerCode            String                                    No                 Unique offering code. This is the unique combination of the offering and price point version.
                                                                                    
                                                                                    E.g. SIMO12\_2019:8182:1

  externalId           String                                    No                 Unique identifier of the offering. This can be used by external systems to identify one or more variants of the given offering.
                                                                                    
                                                                                    E.g. SIMO12\_2018

  name                 String                                    No                 Name of the offering.

  description          String                                    No                 Description of the offering.

  price                [priceType\[\]](#pricetype)               No                 This is an array of different price points returned for the offering i.e. normal price and discounted price if applicable.

  conflicts            [*conflictType\[\]*](#conflicttype)       No                 This is the list of current product offering Id’s present on the customer’s tariff which are conflicting with the given offering.

  offeringGroup        [offeringGroupType](#offeringgrouptype)   No                 This specifies the offering group.

  chars                [offeringCharsType](#offeringcharstype)   No                 This specifies the characteristics of the offering. This is a set of mandatory key-value characteristics applicable for the offering. E.g. Spend Cap variants.

  allowances           [allowancesType](#allowancestype)\[\]     No                 This is an array of different allowances associated with the offering. The allowances are –
                                                                                    
                                                                                    -   Voice
                                                                                    
                                                                                    -   Text
                                                                                    
                                                                                    -   MMS
                                                                                    
                                                                                    -   Data
                                                                                    
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### offeringGroupType

  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ ----------------------------
  offeringGroupId      String          Yes                Id of the offering group
  offeringGroupName    String          Yes                Name of the offering group

### offeringCharsType

  ----------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ --------------------------------------------------------------------
  name                 String          Yes                Characteristic Name

  value                String\[\]      No                 This contains characteristic values

  mandatory            String          Yes                It indicates that characteristic is mandatory when adding an Offer
                                                          
                                                          Valid values: true, false.
  ----------------------------------------------------------------------------------------------------------------------------

### allowancesType

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ ---------------------------------------------------------------------------------------------------------------------------------
  name                 String          Yes                Name of the allowance. The valid values for this field are –
                                                          
                                                          -   Voice
                                                          
                                                          -   Text
                                                          
                                                          -   MMS
                                                          
                                                          -   Data
                                                          

  value                String          Yes                Value of the allowance. The following are the units of each allowance
                                                          
                                                          -   Voice – seconds
                                                          
                                                          -   Text – Number of texts
                                                          
                                                          -   MMS – Number of MMS
                                                          
                                                          -   Data – bytes
                                                          
                                                          For unlimited allowance, the value returned will be “-1”. As of today, there are no product offerings with unlimited allowance.
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### priceType

  ---------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ -------------------------------------------------------------
  category             String          Yes                Price point category. The valid values for this field are –
                                                          
                                                          -   Normal
                                                          
                                                          -   Discounted
                                                          

  type                 String          Yes                Price point type. The valid values for this field are –
                                                          
                                                          -   MRC (Monthly Recurring)
                                                          
                                                          -   NRC (Non-Recurring)
                                                          

  value                String          Yes                Price point value in pence
  ---------------------------------------------------------------------------------------------------------------------

[[[[[[[[]{#businesspoliciestype .anchor}]{#tariffofferingstype
.anchor}]{#producttype_1 .anchor}]{#myproductstype
.anchor}]{#_businessPoliciesType .anchor}]{#_tariffOfferingsType
.anchor}]{#_productType_1 .anchor}]{#_myProductsType .anchor}

### conflictType

  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ -------------------------------------------------------------------------------
  offerId              String          Yes                Offer Id of the existing product which is conflicting with the given offering

Error Response Structure
========================

errorType
---------

  **Name**     **Type**                                **Is Mandatory**   **Description**
  ------------ --------------------------------------- ------------------ ---------------------------------------------------------------------------------------------------------------------
  code         String                                  Yes                Error Code. Refer to Success and Fault definition section of each method to see the HTTP Responses and Error Codes.
  message      String                                  Yes                Error Message. Refer to Success and Fault definition section of each method to see the Error Messages.
  faultTrace   [faultTraceType\[\]](#faulttracetype)   No                 Additional troubleshooting details.

faultTraceType
--------------

  **Name**           **Type**   **Is Mandatory**   **Description**
  ------------------ ---------- ------------------ ----------------------------------------------
  faultCode          String     Yes                Fault code for the internal component
  faultDescription   String     No                 Fault Description for the internal component

**Sample Error Response:**

**HTTP/1.1**: 404 Not Found

  -----------------------------------------------------------------------
  {
  
  "error": {
  
  "code": "productofferingqualification-37229-3601-E",
  
  "message": "Subscriber is either not recognised or cannot be found.”,
  
  "faultTrace": \[
  
  {
  
  "faultCode": "404",
  
  "faultDescription": "Not Found"
  
  }
  
  \]
  
  }
  
  }
  -----------------------------------------------------------------------

[[]{#appendix_a__1 .anchor}]{#_Appendix_A_–_1 .anchor}

Appendix A – OfferingType Mandatory Fields By Method
====================================================

  **Offering Attributes**   **Get Valid Product Offerings**   **Get Valid Tariff Offerings**   **Get Tariff Compatible Products**
  ------------------------- --------------------------------- -------------------------------- ------------------------------------
  offerId                   Y                                 Y                                Y
  offerCode                 Y                                 Y                                Y
  externalId                Y                                 Y                                Y
  name                      Y                                 Y                                N
  description               Y                                 Y                                N
  price                     Y                                 Y                                N
  conflicts                 N                                 N/A                              N/A
  offeringGroup             Y                                 Y                                Y
  chars                     N                                 N                                N
  allowances                N                                 N                                N

[[]{#hlk51333871 .anchor}]{#_Hlk51333871 .anchor}

Appendix B – Business Policy Code and Reason for Product Offering
=================================================================

  **Reason Code**   **Reason Description**
  ----------------- -----------------------------------------------
  5000              Customer current plan is not active.
  5001              Customer current plan is in suspended status.
  5002              A customer has Bankruptcy status.
  5003              A customer has Long Term Illness status.
  5004              A customer has Bereavement status.
  5005              A customer has Financial Difficulty status.
  5006              A customer is in treatment.

Appendix C – Business Policy Code and Reason for Tariff Offering
================================================================

  **Reason Code**   **Reason Description**
  ----------------- ---------------------------------------------------------------------------------
  5000              Customer current plan is not active.
  5001              Customer current plan is in suspended status.
  5002              A customer is in fraud status.
  5003              A customer has deceased status.
  5004              A customer is in treatment.
  5005              A customer has already done the tariff transfer within the last 30 days period.
  5006              A customer has a pending change (e.g. tariff change) on their account.

Appendix D – Product Type Mandatory Fields By Method
====================================================

  **Product Attributes**   **Get Tariff Compatible Products**
  ------------------------ -----------------------------------------------------------------------------------------------------------
  productId                Y
  offer                    Y (Refer to [Appendix A](#appendix-a-offeringtype-mandatory-fields-by-method) for offer details returned)
  productName              Y
  description              Y
  price                    N
  startDate                N
  endDate                  N
  productType              Y
  status                   Y
  chars                    N
  allowances               N
