-------------------------
API Jam Demo Guide readme
-------------------------

---
FAQ
----
Q. How do I get started?

A. See steps below:
  *Register on Dev Console
  *Create an Project App
  *Enable services on the App
  *Copy Client ID & Secret Key
  *Read API documentation (URL for each here)
  *Start Coding



Q. How do I create Interswitch Security?

A. See documentation [here](https://confluence.interswitch.com/confluence/api/interswitch-services-authentication-specification). See sample code [here](https://github.com/techquest/java-isw-api-utility-sample)


	
Q. How do I create Interswitch secure data

A. See documentation here. See sample code here



Q. How do I create Interswitch auth data

A. See documentation here. See sample code here.



Q. What APIs are available?

A.	*eWallet
	*Loyalty
	*Paycode
	*Payment Gateway
	*QuickTeller

	
Q. What is a Payment Instrument?

A. A Payment Instrument is used to make a payment e.g. Card Number (PAN), Account Number, etc.


Q. What is an eWallet API

A. eWallet API give developers to customer's Payment Instruments (Card Number, Account Number etc). It makes life easier so their customer doesnt have to enter their card number everytime they need to do transaction. The API fetches all Payment instruments for a customer. Developer can then display and Customer can select whichever they want to use for transaction


What else is available in the eWallet API box	
	Developers can generate an OTP which can be used on any Interswitch Gateway (Webpay) powered website
	Developers can Generate Paycode
What is a Paycode
	A Paycode is a one time token generated for making payment, or getting cash at the ATM. The use case can be limitless. It can be generated becuase Customer forgot or lost his/her wallet. The Customer can generate Paycode from his mobile phone and use it to get cash at the ATM. He can also decide to use same Paycode to make payment at a merchant location. There is also an option of generating bulk Paycodes in order to use it for disbursing payment to a large number of people.
What is Reward/Loyalty API	
	It allows customers to see merchant locations where they can use their cards and get discounts. Customers can also see what offers they can enjoy.
What is an Access Token and why do I need it?
	An Access Token contains validated & signed credentials of the identity of the developer. In some cases, the access token contains customer's (user's) validated identity and it can be used to access some customer's resources. It is also used to determine the resources a developer can have access to and the access level.

How do I use the eWallet API?

How do I use the Payment Gateway API?
	See steps below:
		Decide what VAS service you want to provide to the customer
		Get an Access Token from Interswitch
		Collect Payment Instrument (Card details) from customer
		Package your request (See documentation here)
		Send your request to Interswitch Payment Gateway
		Process the response from Interswitch Payment Gateway
How do I use the QuickTeller API?
	QuickTeller API will allow you to Pay for Bills, Transfer Funds to Account all from your Payment Instrument. See steps below:
		Get Quickteller Bills Category (See "get category" documentation here)
		Select a catory and get all the billers under the category (See "get biller by category" documentation here)
		Select the biller, and request for customer details (e.g. if DSTV request for SmartCard Number, if PHCN request for Meter Number)
		Request for amount the customer will like to pay
		Validate customer details to ensure they are valid (See "bill inquiry" documentation here)
		Package your request to QuickTeller
		Send your request (See "send transaction" documentation here)
		Process the response from QuickTeller
How do I use the Paycode API?
	See steps below:
		Request customer to sign in to QuickTeller by reqirecting to Interswitch Passport
		Get Access Token returned by Interswitch Passport
		Use Access Token to get Customer's Payment Instrument (Cards)
		Generate Paycode (See "Generate Paycode" documentation here)
		Process response
	Make a call to get payment methods, select one of the payment methods, Enter Payment method details (PIN, CVV, Expiry Date if required), generate Paycode using the selected payment method. See documentation here.
How do I use the Loyalty API?
What is the URL of Interswitch Developer Console
	https://developer.interswitchng.com
	
