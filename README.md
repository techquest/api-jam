-------------------------
API Jam Demo Guide readme
-------------------------

##How do I get started?
- Register on Interswitch Developer Console [here] (https://developer.interswitchng.com)
- Create a new Project App. (Please use REST/SOAP Client). See documentation [here] (https://confluence.interswitch.com/confluence/api/developer-console-guide/create-a-new-app)
- Enable services on the App. See documentation [here] (https://confluence.interswitch.com/confluence/api/developer-console-guide/create-a-new-app)
- Copy Client ID & Secret Key on Developer Console for re-use during development
- Read API documentation for how to integrate to each. Please see each API usage in this FAQ.
- Start Coding

##I want to accept payment with Interswitch Payment Gateway, how do I get started?
- Register on the Payment Gateway portal [here] (https://www.interswitchgroup.com/paymentgateway). If you have an existing profile on Developer Console, use the same email address to register.
- Click the Developer Console link on the Payment Gateway portal after successful log in
- Copy Client ID & Secret Key on Developer Console for re-use during development
- Read API documentation for how to integrate to Payment Gateway below in this FAQ (How do I use the Payment Gateway API?).
- Start Coding

##What is the URL of Interswitch Developer Console
https://developer.interswitchng.com
	
##What APIs are available?
* eWallet
* Loyalty
* Paycode
* Payment Gateway
* QuickTeller

##How do I access these APIs?
Each API call requires authentication. Interswitch uses **_OAuth 2.0_** standards for access to the APIs, therefore each call requires an Access Token.

##How do I get Access Token?
Interswitch has provided libraries (SDK) that helps generate Client Access Token. There is also a Javascript library to generate a User Access Token. The SDKs generate the Access Token and use it to call the APIs. However, if the API requires a User Access Token, developer are advised to use any OAuth2 library they are familiar with. Access Tokens are requested from an Interswitch Authorization Server (IAS) called Interswitch Passport. See the URL to call when developer wants a redirect to get a User Access Token:

**Sandbox Authorization Server**
```
https://sandbox.interswitchng.com/passport/oauth/authorize?response_type=token&client_id={clientId}&redirect_uri={redirectUri} 
```
**Production Authorization Server**
```
https://saturn.interswitchng.com/passport/oauth/authorize?response_type=token&client_id={clientId}&redirect_uri={redirectUri}
```

##What is the difference between User Access Token and Client Access Token?
A User Access Token is a signed authorization token that grants Developer (Client) access to their customer's resources (e.g. Customer's Payment Instruments). The resources are owned by the user but stored by the service provider (Interswitch). Client Access Token on the other hand is a signed authorization token that grants Developer access to service provider's resources (e.g. Payment Gateway, QuickTeller VAS API etc).

##What SDKs do I need?
The interswitch SDK is available in github and quite a number of programming languages are supported: 
* [JavaScript] (https://github.com/techquest/interswitch_javascript)
* [PHP] (https://github.com/techquest/interswitch_php)
* [Ruby] (https://github.com/techquest/interswitch_ruby)
* [Java] (https://github.com/techquest/interswitch_java)
* [C#] (https://github.com/techquest/interswitch_csharp)

##How do I use the SDKs?
* Initialize
  * Interswitch interswitch = new Interswitch(String clientId, String secretkey, Interswitch.ENV_SANDBOX);
* Send request. The send function can be used. The send function is overloaded. Additional parameters can be send depending on the requirement of the API. Please see API documentation.
  * HashMap response = interswitch.send(String uri, String httpMethod, String data). See API documentation for the URI of each service e.g. api/v1/quickteller/categories

##What is a Payment Instrument?
A Payment Instrument is used to make a payment e.g. Card Number or Card PAN, Account Number, etc.

##What is an eWallet API?
eWallet API give developers to customer's Payment Instruments (Card Number, Account Number etc). It makes life easier so their customer doesnt have to enter their card number everytime they need to do transaction. The API fetches all Payment instruments for a customer. Developer can then display and Customer can select whichever they want to use for transaction

##What else is available in the eWallet API box?
* Developers can generate an OTP which can be used on any Interswitch Gateway (Webpay) powered website
* Developers can Generate Paycode
	
##What is a Paycode?
A Paycode is a one time token generated for making payment, or getting cash at the ATM. The use case can be limitless. It can be generated becuase Customer forgot or lost his/her wallet. The Customer can generate Paycode from his mobile phone and use it to get cash at the ATM. He can also decide to use same Paycode to make payment at a merchant location. There is also an option of generating bulk Paycodes in order to use it for disbursing payment to a large number of people.
	
##What is Reward/Loyalty API?
It allows customers to see merchant locations where they can use their cards and get discounts. Customers can also see what offers they can enjoy.
	
##What is an Access Token and why do I need it?
An Access Token contains validated & signed credentials of the identity of the developer. In some cases, the access token contains customer's (user's) validated identity and it can be used to access some customer's resources. It is also used to determine the resources a developer can have access to and the access level.

##How do I use the eWallet API?
Typically you will want to use eWallet API to get your custoemr's payment instruments. The payment instruments can be used to generate OTP, generate Paycode, Get Balance.
* Redirect your app to Interswitch Passport Page
* Customer will enter their Interswitch (QuickTeller) Passport username & password
* An Access Token is returned to the developer
* Developer uses Access Token to fetch Customer's payment instruments
* Payment Instruments can be used to generate OTP, Paycode, Get Balance etc

##How do I use the Paycode API?
Paycode API enables customer to generate a one time code and use for payment or cash withdrawal at the ATM. See steps below:
* Request customer to sign in to QuickTeller by reqirecting to Interswitch Passport
* Get Access Token returned by Interswitch Passport. (See documentation here)
* Use Access Token to get Customer's Payment Instrument (Cards)
* Request customer to enter Payment instrument details (Card Expiry date, CVV, PIN)
* Generate Paycode (See **Generate Paycode** documentation [here] (https://confluence.interswitch.com/confluence/api/paycode-api/generate-token))
* Process response

##How do I use the Loyalty API?
Loyalty API enables customer to know merchant locations where rewards can be eanred and what type of rewards they can earn. See steps below:
* Get Merchant Locations. See documentation here
* Get Reward Offers available. See documentation here

##How do I use the Payment Gateway API?
Payment Gateway enables merchants to accept payment from their customers. See the steps below:
* Decide what VAS service you want to provide to the customer
* Get an Access Token from Interswitch (See documentation [here] (https://confluence.interswitch.com/confluence/api/payment-api-security/request))
* Collect Payment Instrument (Card details) from customer
* Package your request (See documentation [here] (https://confluence.interswitch.com/confluence/api/payment-api-security/request-authentication))
* Send your request to Interswitch Payment Gateway
* Process the response from Interswitch Payment Gateway

##How do I use the QuickTeller API?
QuickTeller API will allow you to Pay for Bills, Transfer Funds to Account all from your Payment Instrument. See steps below:
* Get Quickteller Bills Category (See **Get Category** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/getbillercategories))
* Select a catory and get all the billers under the category (See **Get Biller by Category** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/getbillers-by-category))
* Select the biller, and request for customer details (e.g. if DSTV request for SmartCard Number, if PHCN request for Meter Number)
* Request for amount the customer will like to pay
* Validate customer details to ensure they are valid (See **Bill Inquiry** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/bill-payment-inquiry))
* Package your request to QuickTeller
* Send your request (See **Send Transaction** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/send-bill-payment-transaction))
* Process the response from QuickTeller



##What does User Access Token (Redirect) SDK do?
Developer calls SDK to get User Access Token. The SDK redirects to **Interswitch Passport** portal where customer signs in with their **QuickTeller** login credentials. The SDK returns an Access Token to the developer. Note that this SDK will redirect your App to a new web page.

##What does Client Access Token SDK do?
Developer calls SDK to get Client Access Token. SDK makes an API call to **Interswitch Passport** and returns an Access Token to the developer. Note, there is no redirect required. This is the default Access Token used when the Interswitch.send() function is called in the SDK.

##How are sensitive data (Payment Instrument e.g Card PAN, Card PIN, CVV, Expiry Date) sent in the API?
In cases where Customer sensitive data are required to compelte transactons, Interswitch has secure ways to send these data over the wire. Please see **_Ho do I create Interswitch Secure Data_** and **_How do I create Interswitch Auth Data_** for more info.

##When do I use Secure Data and Auth Data?
The documentation for each API specifies which to use.

##How do I create Interswitch Secure Data?
Some Interswitch API requires sensitive data to be encrypted in a certain way. Interswitch Secure Data SDK will do this for you. See documentation here. See sample code [here] (https://github.com/techquest/java-isw-api-utility-sample).

##How do I create Interswitch Auth Data?
Some Interswitch API requires sensitive data to be encrypted in a certain way. Interswitch Auth Data SDK will do this for you. See documentation [here] (https://confluence.interswitch.com/confluence/api/payment-api-security/authdata). See sample code [here] (https://github.com/techquest/java-isw-api-utility-sample).

##How do I create Interswitch Security?
In order to access Interswitch API, developers will have to send a couple of HTTP headers along with their request. These headers are used for client authentication. See documentation [here] (https://confluence.interswitch.com/confluence/api/interswitch-services-authentication-specification). See sample code [here] (https://github.com/techquest/java-isw-api-utility-sample).
