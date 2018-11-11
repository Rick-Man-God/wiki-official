<!-- TITLE: Api -->
<!-- SUBTITLE: A quick summary of Api -->

# XEL api





Get Account
-----
Request:

``
http://localhost:17876/nxt?requestType=deleteAccountProperty&recipient=XEL-7A48-47JL-T7LD-D5FS3&property=testkey1&secretPhrase=iWontTellYou&feeNQT=100000000&deadline=60
``

Response:

``
{
  "signatureHash": "4ff58a03d056ee8a3fee89766bf8e4acd008c2147216...",
  "transactionJSON": {
    "senderPublicKey": "373522bcd8904f4707472e590cbb67976d40e7af...",
    "signature": "26ed697fc82f3b15e6d2c972eff5b195445314aa4bacc8...",
    "feeNQT": "100000000",
    "type": 1,
    "fullHash": "33f7edaec1034153f8e28a996b13b2b2665d0d0a3e4a194...",
    "version": 1,
    "phased": false,
    "ecBlockId": "10023643060833833497",
    "signatureHash": "4ff58a03d056ee8a3fee89766bf8e4acd008c21472...",
    "attachment": {
        "property": "940296349549404868",
        "version.AccountPropertyDelete": 1
    },
    "senderRS": "NXEL-7A48-47JL-T7LD-D5FS3",
    "subtype": 11,
    "amountNQT": "0",
    "sender": "12745647715474645062",
    "recipientRS": "XEL-7A48-47JL-T7LD-D5FS3",
    "recipient": "12745647715474645062",
    "ecBlockHeight": 754255,
    "deadline": 60,
    "transaction": "5999080309032613683",
    "timestamp": 80189128,
    "height": 2147483647
  },
  "unsignedTransactionBytes": "011bc896c7043c00373522bcd8904f4707472e590cbb67976d40e7af39650ea11c...",
  "broadcasted": false,
  "requestProcessingTime": 3,
  "transactionBytes": "011bc896c7043c00373522bcd8904f4707472e590cbb67976d40e7af39650ea11cb2be5734...",
  "fullHash": "33f7edaec1034153f8e28a996b13b2b2665d0d0a3e4a1942718aa480c6097cf6",
  "transaction": "5999080309032613683"
}
``
