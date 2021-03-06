-------------------------
API Jam Demo Guide readme
-------------------------

##How do I get started?
- Register on Interswitch Developer Console <a href="https://developer.interswitchng.com" target="_blank">here</a>
- Create a new Project App. (Please use REST/SOAP Client). See documentation <a href="https://confluence.interswitch.com/confluence/api/developer-console-guide" target="_blank">here</a>
- Enable services on the App. See documentation <a href="https://confluence.interswitch.com/confluence/api/developer-console-guide" target="_blank">here</a>
- Copy Client ID & Secret Key on Developer Console for re-use during development
- Read API documentation for how to integrate to each. Please see each API usage in this FAQ.
- Start Coding

##I want to accept payment with Interswitch Payment Gateway, how do I get started?
- Register on the Payment Gateway portal: <a href="https://sandbox.interswitchng.com/paymentgateway/" target="_blank">Sandbox here </a>, <a href="https://www.interswitchgroup.com/paymentgateway" target="_blank">Production here.</a> If you have an existing profile on Developer Console, use the same email address to register.
- Click the Developer Console link on the Payment Gateway portal after successful log in
- Copy Client ID & Secret Key on Developer Console for re-use during development
- Read API documentation for how to integrate to Payment Gateway below in this FAQ (How do I use the Payment Gateway API?).
- Start Coding

##What is the URL of Interswitch Developer Console
<a href="https://developer.interswitchng.com" target="_blank">https://developer.interswitchng.com</a>
	
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

##What SDKs are available?
* **Integrate with JavaScript**
```
```
Check out the [Javascript source and sample codes on GitHub.] (https://github.com/techquest/interswitch_javascript)

* **Integrate with Node npm**
```
npm install interswitch
```

* **Integrate with PHP Composer**. Add interswitch/interswitch-php to your composer.json file.
```
{
  "require": {
    "interswitch/interswitch-php": "1.*"
  }
}
```
Check out the [PHP source and sample codes on GitHub.] (https://github.com/techquest/interswitch_php)


* **Integrate with Ruby gem** 
```
 gem install interswitch
```
If you use bundler, you can use this. 
```
gem 'interswitch', :git => 'https://github.com/techquest/interswitch_ruby'
```
Check out the [Ruby source and sample codes on GitHub.] (https://github.com/techquest/interswitch_ruby)
  

* **Integrate with Java Maven**
```
<dependency>
  <groupId>com.interswitchng.techquest</groupId>
  <artifactId>interswitch-java</artifactId>
  <version>1.0.0</version>
</dependency>
```
Check out the [Java source and sample codes on GitHub.] (https://github.com/techquest/interswitch_java)

* **Integrate with C# Nuget** 
```
Install-Package Interswitch
```
Check out the [C# source and sample codes on GitHub.] (https://github.com/techquest/interswitch_csharp)


##How do I use the SDKs?
* Initialize
```
Interswitch interswitch = new Interswitch(String clientId, String secretkey, Interswitch.ENV_SANDBOX);
```
* Send request.
```
HashMap response = interswitch.send(String uri, String httpMethod, String data). 
```
The send function is used to send request. The function is overloaded. Additional parameters can be included depending on the requirement of the API. Please see API documentation. See API documentation for the URI of each service e.g. api/v1/quickteller/categories

##What is a Payment Instrument?
A Payment Instrument is used to make a payment e.g. Card Number or Card PAN, Account Number, etc.

##What is an eWallet API?
eWallet API give developers to customer's Payment Instruments (Card Number, Account Number etc). It makes life easier so their customer doesnt have to enter their card number everytime they need to do transaction. The API fetches all Payment instruments for a customer. Developer can then display and Customer can select whichever they want to use for transaction

##What else is available in the eWallet API box?
* Developers can generate an OTP which can be used on any Interswitch Gateway (Webpay) powered website
* Developers can Generate Paycode
	
##What is a Paycode?
A Paycode is a one time token generated for making payment, or getting cash at the ATM. The use case can be limitless. It can be generated becuase Customer forgot or lost his/her wallet. The Customer can generate Paycode from his mobile phone and use it to get cash at the ATM. He can also decide to use same Paycode to make payment at a merchant location. There is also an option of generating bulk Paycodes in order to use it for disbursing payment to a large number of people.

##What is QuickTeller API?
QuickTeller is a VAS platform that enables customer to pay for their bills. Developer can tap into the vast database of billers already registered on the platform and can facilitate transactions while earning a certain part from the transaction fee.

##What is Payment Gateway API?
Interswitch Payment Gateway enables merchant to accept payment into their bank account. You can sell items directly to your customer and ask for payment in all the payment card available, both local and international.

##What is Reward/Loyalty API?
It allows customers to see merchant locations where they can use their cards and get discounts. Customers can also see what offers they can enjoy.

##How do I use the eWallet API?
Typically you will want to use eWallet API to get your custoemr's payment instruments. The payment instruments can be used to generate OTP, generate Paycode, Get Balance.
* Use any OAuth2 SDK of your choice to get the User Access Token to redirect your app to Interswitch Passport page. See How do I get Access Token above.
* Customer will enter their Passport (QuickTeller) username & password and control will be direct to your redirect url
* An Access Token is returned to the developer
* Developer uses Access Token to fetch Customer's payment instruments using the Interswitch libraries in "What SDKs are available?" section of this FAQ
* Payment Instruments can be used to generate OTP, Paycode, Get Balance, Do Recharge using the Interswitch libraries in "What SDKs are available?" section of this FAQ.

##How do I use the Paycode API?
Paycode API enables customer to generate a one time code and use for payment or cash withdrawal at the ATM. See steps below:
* Redirect to Interswitch Passport page (OAuth2)
* Customer will enter Quickteller username & password  on the Passport page.
* Interswitch Passport redirects to Developer's "redirect_url".
* Developer gets Access Token returned by Interswitch Passport.
* Developer uses Access Token to get Customer's Payment Instrument (Cards)
* Package your (Get Customer's Payment Instrument) request. 
* Send your request to eWallet API server. Use "What SDKs are available?" to access API.
* Request customer to enter Payment instrument details (Card Expiry date, CVV, PIN)
* Generate Paycode (See **Generate Paycode** documentation [here] (https://confluence.interswitch.com/confluence/api/paycode-api/generate-token/generate-token-request-sent-from-thirdparty)). Use "What SDKs are available?" to access API.
* Process response

##How do I use the Loyalty API?
Loyalty API enables customer to know merchant locations where rewards can be eanred and what type of rewards they can earn. See steps below:
* Get Merchant Locations. See documentation here
* Get Reward Offers available. See documentation here

##How do I use the Payment Gateway API?
Payment Gateway enables merchants to accept payment from their customers. See the steps below:
* Decide what VAS service you want to provide to your customer
* Collect Payment Instrument (Card details) from customer i.e. ask customer for card number, expiry date, cvv, and pin.
* Package your request. (See documentation [here] (https://confluence.interswitch.com/confluence/api/payment-api-security/request-authentication))
* Send your request to Interswitch Payment Gateway. Use "What SDKs are available?" to access API.
* Process the response from Interswitch Payment Gateway

##How do I use the QuickTeller Bill Payment API?
QuickTeller API will allow you to Pay for Bills, Transfer Funds to Account all from your Payment Instrument. See steps below:
* Get all Bill categories in QuickTeller.
* Package your request to get Bill Categories. (See **Get Category** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/get-biller-categories)).
* Send your request.  Use "What SDKs are available?" to access API.
* Select a category and get all the billers under the category 
* Package your request to get Biller by Category. (See **Get Biller by Category** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/get-billers-by-category))
* Send your request. Use "What SDKs are available?" to access API.
* Select the biller, and request for customer details (e.g. if DSTV request for SmartCard Number, if PHCN request for Meter Number)
* Request for amount the customer will like to pay and do a bill inquiry to validate customer details.
* Package your request to Bill Inquiry. (See **Bill Inquiry** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/bill-payment-inquiry))
* Validate customer details to ensure they are valid. Use "What SDKs are available?" to access API.
* Package your request to Send Transaction. (See **Send Transaction** documentation [here] (https://confluence.interswitch.com/confluence/api/quickteller-service-interface/send-bill-payment-transaction))
* Send your request. Use "What SDKs are available?" to access API.
* Process the response from QuickTeller
