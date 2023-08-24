**O~2~**

**Interface Specification**

**37229 Product Offering Qualification API**

Version 1.3

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}**DOCUMENT INFORMATION**


 ** -------------------------- ----------------------------
  **Document Author:**       Dolly Khurana
  **Owner while current:**   <SOAServiceFactory@o2.com>
  **Retention period:**      3 years
  **-------------------------- ----------------------------**

[[[[[[[[[[]{#_Toc6395708 .anchor}]{#_Toc159915942
.anchor}]{#_Toc156645504 .anchor}]{#_Toc153600110
.anchor}]{#_Toc153595980 .anchor}]{#_Toc6395709 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}CHANGE HISTORY

  **------------- ------------ ---------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Version**   **Date**     **Changed by**   **Changes**

  0.1           28-07-2020   Dolly Khurana    Initial version
  0.2           14/08/2020   Dolly Khurana    Internal review complete
  0.3           20/08/2020   Pronisa Baruah   Updated to Introduce a new function “Get Bolton Business Policies” for Bolton’s
                                              Correct the error codes for the Get Valid Bolton offerings function in section 4.1.2
  0.4           27/08/2020   Pronisa Baruah   Error response structure added.
  0.5           01/09/2020   Pronisa Baruah   To introduce new functions
                                              Get Valid Tariff Offerings
                                              Get Tariff Business Policies and
                                              Get Tariff Compatible Products
                                              The error code typo ‘s’ removed in “Get Valid Bolton Offerings” & “Get Bolton Business Policies” functions
  0.6           17/09/2020   Pronisa Baruah   To add offerCode and externalId fields in the offeringType.
                                              Get Tariff & Bolton business policy messages updated
  0.7           30/09/2020   Pronisa Baruah   To add customer in treatment check for Get Bolton business policies.
  0.8           03-11-2020   Apoorva          Resource definition and method names updated for the below API’s.
                                              Get Valid Bolton Offerings
                                              Get Bolton Business Policies
                                              Get Tariff Business Policies
                                              Get Valid Tariff Offerings
                                              Get Tariff Compatible Products
  0.9           12-11-2020   Dolly Khurana    Updated the Get Valid Product Offerings API to include new elements as part of 34.8 IMI Textback service changes
  1.0           14-12-2020   Dolly Khurana    Updated the offering chars field in Get Valid Product Offerings API as part of 34.8 IMI Textback service changes
                             Rajesh Kota      Baseline and signed off version for R3.1
  1.1           22-01-2021   Dolly Khurana    Updated Get Valid Product Offerings sample for mandatory chars
  1.2           20-04-2021   Dolly Khurana    Updated Get Valid Product Offerings sample to remove chars array
  1.3           01-06-2022   Dolly Khurana    Added an optional request element “returnConflicts” in Get Valid Product Offerings API in order to query all the offers including the conflicts with the existing products.
  **------------- ------------ ---------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------**
  
  RELATED DOCUMENTS

 ** -------- -------------------------------------------------------------------------------- ------------- -----------------------------------------------**
  **ID**   **Name**                                                                         **Version**   **Description**
  1        R3 - 163.1 HTK IVR 62.1 HTK SIM Swap Interface Agreement v1.7                    1.7           HTK IVR & SIM Swap Interface Agreement
  2        R3 - IF34.8 IMI PAYM & PAYG Tariffs & Bolt Ons to BSS Interface Agreement v0.7   o.7           IMI PAYM & PAYG & Boltons Interface Agreement
  3        NC.O2.INT Telecom Business API Specification                                     0.28          Netcracker TB API specification
  **-------- -------------------------------------------------------------------------------- ------------- -----------------------------------------------**

[[[[[[]{#_Toc143240779 .anchor}]{#_Toc237660664 .anchor}]{#_Toc159915944
.anchor}]{#_Toc156645506 .anchor}]{#_Toc153600112
.anchor}]{#_Toc153595982 .anchor}DESIGN LEAD SIGN-OFF

  **--------------- ------------------------------------- ----------- ------------
  **Name:**       Rajesh Kota
  **Role:**       SOA Architect
  **APPROVED:**   YES
  **--------------- ------------------------------------- ----------- ------------**

[[[[[[]{#_Toc143240780 .anchor}]{#_Toc237660665 .anchor}]{#_Toc159915945
.anchor}]{#_Toc156645507 .anchor}]{#_Toc153600113
.anchor}]{#_Toc153595983 .anchor}DESIGN GOVERNANCE SIGN-OFF

  **--------------- ------------------------------------- ----------- ------------**
  **Name:**       Rajesh Kota
  **Role:**       SOA Architect
  **APPROVED:**   YES
  **--------------- ------------------------------------- ----------- ------------**

[[[[[[]{#_Toc143240781 .anchor}]{#_Toc237660666 .anchor}]{#_Toc159915946
.anchor}]{#_Toc156645508 .anchor}]{#_Toc153600114
.anchor}]{#_Toc153595984 .anchor}ADDITIONAL APPROVAL SIGNATORIES

 