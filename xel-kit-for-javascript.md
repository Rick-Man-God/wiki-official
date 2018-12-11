<!-- TITLE: Xel Kit For Javascript -->

# XELKit for Javascript
Javascript development framework for XEL. Create transactions with Javascript, get the most used XEL functions.

# Why?

The XELKit is a light version of the full NRS which was developed to work with the XEL API and JavaScript in the XEL Wallet.
Setup the server in nrs.js (default localhost) to use your XEL node, any transaction that will go through the wrapper will be signed with Javascript and then submitted to the XEL API.

No passphrase will leave your JavaSscript, check NRS.sendRequest

# Installation

### Public Node

Find a public node with open API and cors enabled

Insert this into server variable of js/nrs.js

Hallmarked nodes provide an extra layer of security.

### Localhost

Extraced from NRS Version 3.1.3 https://github.com/xel-software/xel-lite-wallet/releases
Please install XEL locally and open cors in the configuration as explained here:

	# Enable Cross Origin Filter for the API server.
	nxt.apiServerCORS=true
	​
	# Enable Cross Origin Filter for NRS user interface server.
	nxt.uiServerCORS=true

restart XEL



## XEL Api

When XEL is running go to:

http://localhost:17876/test

API documentation:

-  <a href="xel-api">XEL API</a>

# Use NRS functions

use NRS functions, to submit XEL requests.

## Examples

	 NRS.sendRequest("getBlockchainStatus", {

	}, function(response, input) {
		if (!response.errorCode) {
			console.log(response);
			console.log(input);

			$("#blockchainStatus").html('Current Block: '+response.numberOfBlocks+' - Current XEL Time '+response.time);

		} else {
			console.log('Could not connect to XEL. Please enable cors like explained on https://github.com/GTnode/XELKit');
		}
	});

# Benefits

Using the NRS.sendRequest will be a secure wrapper for your XEL transactions. When you POST a transaction with passphrase, it will

1) create the transaction with JavaScript

2) Sign the transaction with passphrase

3) broadcast transaction to local /public XEL API

# Documentation

## Variables

https://github.com/GTnode/XELKit/blob/master/js/nrs.js

//Modify to set your XEL Node

NRS.server = "http://localhost:17876";

NRS.database = null;

NRS.databaseSupport = false;


## Functions

Use NRS functions, so you have not to write your own for:

https://github.com/GTnode/XELKit/blob/master/js/nrs.sever.js

NRS.setServerPassword = function (password)

NRS.sendOutsideRequest = function (url, data, callback, async)

NRS.sendRequest = function (requestType, data, callback, isAsync)

NRS.processAjaxRequest = function (requestType, data, callback, isAsync)

NRS.verifyAndSignTransactionBytes = function (transactionBytes, signature, requestType, data, callback, response, extra)

NRS.verifyTransactionBytes = function (byteArray, requestType, data, attachment)

NRS.verifyTransactionTypes = function (byteArray, transaction, requestType, data, pos, attachment)

NRS.broadcastTransactionBytes = function (transactionData, callback, originalResponse, originalData)

https://github.com/GTnode/XELKit/blob/master/js/nrs.util.js

NRS.fromEpochTime = function (epochTime)

NRS.toEpochTime = function (currentTime)

NRS.formatTimestamp = function (timestamp, date_only, isAbsoluteTime)

NRS.isPrivateIP = function (ip)

NRS.convertToHex16 = function (str)

NRS.convertFromHex16 = function (hex)

NRS.convertFromHex8 = function (hex)

NRS.convertToHex8 = function (str)

NRS.convertNumericToRSAccountFormat = function (account)

NRS.getAccountTitle = function (object, acc)

NRS.formatStyledAmount = function (strAmount, round)

NRS.getUnconfirmedTransactionsFromCache = function (type, subtype, fields, single)

NRS.completeUnconfirmedTransactionDetails = function (unconfirmedTransaction)

NRS.hasTransactionUpdates = function (transactions)

NRS.setCookie = function (name, value, days)

NRS.getCookie = function (name)

NRS.deleteCookie = function (name)

NRS.validateDecimals = function (maxFractionLength, charCode, val, e)

NRS.getUrlParameter = function (sParam)

NRS.getUtf8Bytes = function (str)

NRS.getTransactionStatusIcon = function (phasedEntity)

NRS.phasingControlObjectToPhasingParams = function(controlObj)

NRS.strToUTF8Arr = function(str)

function byteArrayToBigInteger(byteArray)

NRS.generateToken = function(message, secretPhrase)

### Links

Link to JS files https://github.com/GTnode/XELKit/tree/master/js

<a href="https://github.com/GTnode/XELKit/blob/master/LICENSE" title=""><img src="http://img.shields.io/:license-mit-blue.svg" alt="license"></a>