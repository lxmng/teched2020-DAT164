SAP Analytics Cloud Push Demo
========================================
#### Description

This example graph shows how data can be pushed to a dataset in SAP Analytics Cloud. The graph is configured to create an SAP Analytics Cloud dataset, but can easily be reconfigured to append to an existing dataset using the SAP Analytics Cloud Formatter operator.

The graph is composed of the following components:

* Read File Operator: Used to read files from local storage or major cloud filestores.
* Table Decoder: Parses raw bytes provided by Read File into a CSV-style message.table format, which the next operator reads.
* SAP Analytics Cloud Formatter: Parses the input message and configuration details, and then produces an output format that is accepted in SAP Analytics Cloud.
* SAP Analytics Cloud Producer: Handles HTTP requests to the SAP Analytics Cloud application. It also provides a response to SAP Analytics Cloud Formatter, if necessary.
* Wiretaps: Allows insight to data passed between operators.

#### Prerequisites

*  For this graph to run you will need the following:
    * **An existing SAP Analytics Cloud tenant**
        * The dataset API must be enabled for your SAP Analytics Cloud application tenant. (Contact your SAP Analytics Cloud application administrator.
    * **A CSV File**
    * **A fully configured OAuth client in the SAP Analytics Cloud application**
        * **oauthClientId** (type string): Client ID used for the OAuth2 authentication.
        * **oauthClientSecret** (type string): Client Secret used for the OAuth2 authentication.
        * **oauthTokenUrl** (type string): URL for the address where the OAuth2 authentication is performed.
        * **oauth2AuthUrl** (type string): The authorization URL used by “oauth2” security scheme when the flow is set to “accessCode”.

        ```Note: ``` The SAP Analytics Cloud API requires OAuth2 Authorization Code Flow for data transfer. It is recommended that you set the refresh token lifetime longer than the expected graph runtime, so the Modeler application is authorized only once per graph run. The token is reused between graphs when the refresh token lifetime is of sufficient length.  For some SAP Cloud Analytics tenants, you may need to use wildcards for the redirect URI generated by Data Intelligence. (ex. https://My_DataIntelligence_host/**)

## Configure and Run the Graph

1. Configure the Read File operator to point to the desired file and connection.
2. Configure the SAP Analytics Cloud Formatter operator by completing the Dataset Name and Description options.
3. Configure the SAP Analytics Cloud Producer operator by completing the hostname and oauth parameters provided by the SAP Analytics Cloud application.
4. Save and run the graph. 
5. On the first run, authorize the Modeler application by opening the SAP Analytics Cloud Producer operator and following the operator instructions. After the authorization is complete, restart the graph to use your new token.
6. Use the Wiretap operator to view messages returned from the SAP Analytics Cloud application. If your data is not showing up in the SAP Analytics Cloud application, check the Wiretap operator for trace files and error messages.

<br>
<div class="footer">
   &copy; 2020 SAP SE or an SAP affiliate company. All rights reserved.
</div>