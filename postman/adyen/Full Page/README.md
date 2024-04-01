## Introduction ##
The Postman Collection enables Adyen to be used to take payments through OPF. 

The integration supports:

* Authorization of Adyen Payments using the OPF "Full Page" UX Pattern
* Deferred Capture support
* Refunds
* Reauthorization of saved payment

In summary: to import the [Adyen Full Page Postman Collection](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Provider_Configuration.json) this page will guide you through the following steps: 

a) Create Your Adyen Test Account.

b) Create a Merchant Account Group in OPF Workbench.

c) Set up Your Adyen Test Account to work with OPF.

d) Prepare the [Postman Environment](https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/adyen/Full%20Page/Adyen%20-%20FULL_PAGE%20-%20PARTIAL_CAPTURE%20-%20OPF_Environment_Configuration.json) file so the collection can be imported with all your OPF Tenant and Adyen Test Account unique values. 

## Create an Adyen Account ##
You can sign up for a free Adyen Test Account at <https://ca-test.adyen.com/ca/ca/login.shtml>.


## Creating the Merchant Account Group 
Ceate a new Account Group in the OPF Workbench.

i) In payment integrations.. click **Create**.
![](images/cybersource-create-button.png)

ii) Add account name (can be anything) and set payment gateway to Adyen.
![](images/cybersource-create-account.png)

iii) Click **configure** on Test column of newly created Account.
![](images/opf-account-group-id.png)

**You must set a merchant ID first.**
You can obtain your merchant ID in the Adyen Dashboard.
![](images/cybersource-get-merchant-id.png)

## Set up Your Adyen Test Account to work with OPF
This includes **Configuring Payment Method**, **Configuring Checkout**, **Configuring Merchant Notifications**, **Configuring a Adyen Hosted Response Page**, and **Activating a Profile**. For detailed instructions, see [Secure Acceptance Hosted Checkout
Integration](https://developer.cybersource.com/library/documentation/dev_guides/Secure_Acceptance_Hosted_Checkout/html/index.html#t=Topics%2FSecurity_Keys.htm%23TOC_Creating_Security_Keysbc-1&rhtocid=_4_2_0).

**TIP** The Notification URL to be used for Merchant Notifcation can be obtained in OPF Workbench at the following location:  
![](images/cybersource-get-notification-url.png)

## Preparing the Postman environment_configuration file

**1. Token**

Get your access token using the auth endpoint https://{{authendpoint}}/oauth2/token and client ID and secret obtained from BTP Cockpit.

Copy the value of the access_token field (it’s a JWT) and set as the ``token`` value in the environment file.

**IMPORTANT**: Ensure the value is prefixed with **Bearer**. e.g. ``Bearer {{token}}``.

**2. Root url**

The ``rootUrl`` is the **BASE URL** of your OPF tenant.

E.g. if your workbench/OPF cockpit url was this …

<https://opf-iss-d0.uis.commerce.stage.context.cloud.sap/opf-workbench>.

The base Url would be

https://opf-iss-d0.uis.commerce.stage.context.cloud.sap.

**3. Account and Account Group**

The ``accountId`` and ``accountGroupId`` values identify the merchant account group can be found in the top left of your merchant configuration.

![](images/cybersource-get-group-id.png)

**4. merchantId** 

You can obtain your merchant ID in the Adyen Dashboard.

![](images/cybersource-get-merchant-id.png)

**5. secretKey** and **accessKey**

The secretKey can be obtained here in the Adyen dashboard. 
For detailed instructions, see [Secure Acceptance Hosted Checkout
Integration](https://developer.cybersource.com/library/documentation/dev_guides/Secure_Acceptance_Hosted_Checkout/html/index.html#t=Topics%2FSecurity_Keys.htm%23TOC_Creating_Security_Keysbc-1&rhtocid=_4_2_0). 

![](images/cybersource-get-access-key.png)


**6.profileId**

In the left navigation panel of Adyen dashboard, choose **Payment Configuration**-> **Secure Acceptance Settings** to create a Hosted Checkout Profile.
Click the created profile name to view the profile details.
![](images/cybersource-get-profile-id.png)

**7.apiKeyId** and **apiKeyValue**

In the left navigation panel, choose **Payment Configuration** -> **Key Management**.

a) Click **Generate Key**.

b) Select **REST Shared Secret**.

c) Copy the generated key to your clipboard by clicking the **clipboard** icon, or click **Download key** to download the shared secret.

d) Under the **Key Management** page, select **REST Shared Secret** from the filter to locate the newly created API Key and copy the Key ID and value.

![](images/cybersource-get-apikey.png)

**Summary**

The envirionment file is now ready for importing into Postman together with the Mapping Configuration Collection file. Ensure you select the correct environment before running the collection.

In summary, you should have edited the following variables: 

- **token** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L6)
- **rootUrl** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L11)
- **accountGroupId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L16)
- **accountId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L21)
- **merchantId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L68)
- **secretKey** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L98)
- **accessKey** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L86)
- **profileId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L80)
- **apiKeyId** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json//#L74)
- **apiKeyValue** (https://github.com/opf-postman/commerce-cloud-open-payment-integration/blob/main/postman/cybersource/iFrame/Cybersource%20-%20iFrame%20-%20CAPTURE_PER_SHIPMENT%20-%20OPF_Environment_Configuration.json#L92)