# JSON HTTP API

* [Getting Started](#getting-started)
  * [Introduction](#introduction)
  * [API Summary](#api-summary)
* [API Key Rate Limit & Errors](#api-key-rate-limit-&-errors)
  * [API Call](#api-call)
* [Node](#node)  
  * [nodeStatus](#nodestatus) 
  * [getProtocolVersion](#getprotocolversion) 
* [Block](#block)  
  * [getBlock](#getblock) 
  * [getBlcokCount](#getblockcount) 
  * [getBlcokTransactions](#getblocktransaction) 
* [Wallet](#wallet)  
  * [newWallet](#newwallet) 
  * [getWalletInfo](#getwalletinfo) 
* [Transaction](#transaction)  
  * [sendTo](#sendto) 
  * [getPendingTransaction](#getpendingtransaction) 
  * [findWalletTransaction](#findwallettransaction) 
  * [getFee](#getfee) 
* [Contract](#contract)  
  * [createContract](#createcontract) 
  * [sendContract](#sendcontract) 
  * [adminContract](#admincontract) 
  * [infoContract](#infocontract) 
  * [holderContract](#holdercontract) 
  
## Getting Started

### Introduction
```
The SUWORLD Developer APIs are provided as a service and without warranty, so please use what you need and no more. We support POST requests and there is a rate limit of 5 calls per sec/IP.
```
### API Summary
```
* To use the API service please create a Api-Key Token from within the Register API area which you can then use with all your api requests.
* Kindly refer API Key Rate Limit & Errors for expected returns. Please contact us if you would like to upgrade your API Plan.
```

## API Key Rate Limit & Errors:

### API Call
```
During the enforcement of the API key requirement, developers will expect the return errors listed, where an API key is not in use or exceeding the rate limit.
* The 5 calls per sec/IP rate limit is exceeded
* An API request with a blank API Key or the default "ApiKey"
* An API request with Invalid API Key
* API requests with Invalid API Key exceeding limit
```


## Node

### nodeStatus
```
Returns node status
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none | none | no | none |

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
ready      | Boolean |  Must be true, otherwise Node is not ready to execute transactions |
timestamp      | NumberString |  Timestamp of the Node |
blocks      | NumberString |  	Blockchain blocks |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"nodeStatus"}'


Response:
{"result":"S0001","data":{"ready":true,"timestamp":1587027784,"blocks":11336}}
```
### getProtocolVersion
```
Returns node protocol version
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none | none | no | none |

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
ver      | Integer |  	Net protocol version |
ver_a      | Integer |  Net protocol available |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getProtocolVersion"}'


Response:
{"result":"S0001","data":{"netprotocol":{"ver":1,"ver_a":1}}}
```



## Block

### getBlock
```
Get block information
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
block | NumberString | yes | Block number (0..blocks count-1)|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
block      | NumberString |  Block number |
ver      | Intger |  Net protocol version |
ver_a      | Intger |  Net protocol available |
timestamp      | NumberString |  Timestamp of the Node |
createwallet      | Intger |  Created wallet number of block |
nopsp      | Intger |  Action value of block |
niopsp      | Intger |  InAction value of block |
reward      | NumberString |  Mined reward of block |
blocksize      | Intger |  Size of block |
hash      | String |  Hash of block |
trx_fee      | NumberString |  Transaction Fee of block |
operations      | Intger |  Transaction count of block |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getBlock","params":{"block":8888}


Response:
{"result":4153118,"id":100,"jsonrpc":"2.0"}
```
### getBlcokCount
```
Get chain high in this node
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none | none | no | none |

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
data      | NumberString |  Returns an Integer with blockcount of node |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getBlcokCount"}'


Response:
{"result":"S0001","data":4153118}
```
### getBlcokTransactions
```
Get operations of specified block
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
block | NumberString | yes | Block number (0..blocks count-1)|
max | Integer | no | Maximum number of transactions|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
block      | NumberString |  Block number |
opblock      | Intger |  Transaction (0..transactions-1) of this block |
optype      | Intger |  Transaction type |
nopsp      | Intger |  Action value |
niopsp      | Intger |  InAction value |
oprice      | NumberString |  Action Price |
iopprice      | NumberString |  InAction Price |
signer_account      | Intger |  Will return the account that signed (and payed fee) for this transaction |
n_operation      | Intger |  Transactions made by this account |
amount      | NumberString |  	Amount of coins transferred from senders_account to receivers_account |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getBlcokTransactions","params":{"block":8888,"max":300}}'


Response:
{"result":"S0001","data": [{"block":8888,"opblock":0,"optype":1,"nopsp":20,"niopsp":0,"oprice":25,"iopprice":0,"signer_account":43905,"n_operation":5,"amount":100,"senders":[{"account":43905,"payload":"asd","payload_type":0}],"receivers":[{"account":43906}]}]}
```



## Wallet

### newWallet
```
Adds a new key to the Wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
passphrase | String | yes | Wallet password|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
wallet      | String |  Wallet Address |
version      | Intger |  Wallet version |
pkey      | String |  	Walelt PrivateKey |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"newWallet","params":{"passphrase":"password"}}'


Response:
{"result":"S0001","data":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","version":1,"pkey":"WalletPrivateKey"}}
```
### getWalletInfo
```
Get infomation of specified wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes | Wallet Address|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
account      | Integer |  Wallet Number |
updated_active      | NumberString |  Wallet active Block |
updated_passive      | NumberString |  Wallet passive Block |
n_operation      | Integer |  	Transactions made by this account |
balance      | NumberString |  Wallet SUC quantity |
wallet      | String |  Wallet Address |
state      | String |  Wallet Status |
state_code      | String |  Wallet Status Code |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getWalletInfo","params":{"wallet":"SWZNDY8AeRH6G75HDmgyLRo9ghXsTSQxAvmSFH93pGMyp45a"}}'


Response:
{"result":"S0001","data":{"account":102,"updated_active":2926,"updated_passive":2926,"n_operation":1,"balance":"100000000000000000","wallet":"SWZNDY8AeRH6G75HDmgyLRo9ghXsTSQxAvmSFH93pGMyp45a","state":"normal wallet",state_code":1}}
```



## Transaction

### sendTo
```
Executes a transaction
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
sender | String | yes | Sender Wallet address|
receiver | String | yes | Receiver Wallet address|
amount | String | yes | Amount of coins transferred from sender to receiver|
passphrase | String | yes | Sender wallet password|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
sender      | String |  Sender Wallet address |
receiver      | String |  Receiver Wallet address |
amount      | NumberString |  Amount of coins transferred from sender to receiver |
fee      | NumberString |  Transaction Fee |
balance      | NumberString |  Remaining balance |
ophash      | String |  Transaction hash |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"sendTo","params":{"sender":"SWHgyqvvaiShRfvKbTw5jD5Kz7M1G6dQbnvoUxVKFvDnZtwi","receiver":"SWEk7bHfhZFg5GoZgftb18J8SKkDQbBpPA7g36dbPSambfAY","amount":1000,"passphrase":"password"}}'


Response:
{"result":"S0001","data": {"time":1476363846,"sender":"SWovpcsg6ijJhwMDf1UKyNT7AhTEEpSFeaxZbhk2BYfknU2Q","receiver":"SWiMyhPLdF377H4YPHW8Z5RKVNE5nK2RKcgn3NXqyw7dovUT","amount":1000, "fee":0.0001,"balance":150605.9999,"ophash":"000000006C8D0100010000003536463332393641383335344236323945464536"}}
```
### getPendingTransaction
```
Get pendings transaction to be included in the chain
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
max | Integer | yes | Get transaction count|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
optype      | Intger |  Transaction type |
nopsp      | Intger |  Action value |
niopsp      | Intger |  InAction value |
oprice      | NumberString |  Action Price |
iopprice      | NumberString |  InAction Price |
signer_account      | Intger |  Will return the account that signed (and payed fee) for this transaction |
n_operation      | Intger |  Transactions made by this account |
amount      | NumberString |  	Amount of coins transferred from senders_account to receivers_account |



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getPendingTransaction","params":{"max":100}}'


Response:
{"result":"S0001","data": [{"optype":1,"nopsp":20,"niopsp":0,"oprice":25,"iopprice":0,"signer_account":43905,"n_operation":5,"amount":0,"senders":[{"account":43905,"payload":"asd","payload_type":0}],"receivers":[{"account":43906}]}]}
```
### findWalletTransaction
```
Get transactions made to an wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet |String | yes|	Walelt Address|
start |NumberString | yes|	Start at position(Max Blockcount is 0) |	
max |Integer | yes|	Get transaction count |	

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
block | NumberString |	Block number (0..blocks count-1)|
opblock | Integer |	Transaction (0..transactions-1) of this block|
optype | Integer |	Transaction type|
nopsp | Integer |	Action value |
niopsp | Integer |	InAction value |
oprice | NumberString |	Action Price |
iopprice | NumberString |	InAction Price |
signer_account | Integer |	Will return the account that signed (and payed fee) for this transaction|
n_operation | Integer |	Transactions made by this account |
amount | NumberString |	Amount of coins transferred from senders_account to receivers_account|

```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"findWalletTransaction","params":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","start":8888,"max":100}}'

Response:
{"result":"S0001","data": [{"block":8888,"opblock":0,"optype":1,"nopsp":20,"niopsp":0,"oprice":25,"iopprice":0,"signer_account":43905,"n_operation":5,"amount":100,"senders":[{"account":43905,"payload":"asd","payload_type":0}],"receivers":[{"account":43906}],}]}
```
### getFee
```
Transaction fee calculated by chain
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none| none | no | none | 


Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
oprice | 	NumberString |	Action Price |	
iopprice | 	NumberString |	InAction Price |	

```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"getFee"}'

Response:
{"result":"S0001","data": {"oprice":25,"iopprice":0}}
```



## Contract

### createContract
```
Executes create contract over an wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes | 	Issuer walelt Address |
passphrase | String | yes | 		Walelt password |
business | 	Boolean | yes | 	Business or Normal Contract |
name | String | yes | 	Contract Name |
symbol | String | yes | 	Contract Symbol |
totalAmount | String | yes | 		Issue Amount |
decimal | String | yes | 	Token decimal|
summary | String | yes | 	Contract Description |

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
cwallet      | 	String |  Contract walelt Address	|
block      | 	NumberString |  Contract walelt Address	|
opblock      | 	Integer |  Transaction (0..transactions-1) of this block	|
optype      | 	Integer |  Transaction type	|
nopsp      | 	Integer |  Action value	|
oprice     | 	NumberString |  Action Price	|
signer_account     | 	Integer |  Will return the account that signed (and payed fee) for this transaction	|
n_operation      | 	Integer |  Transactions made by this account	|
ophash      | 	String | Transaction hash	|
optxt     | 	String |  Contract Description	|
name     | 	String |  Contract Name	|
symbol    | 	String |  Contract Symbol	|



```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"createContract","params":{"wallet":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","passphrase":"password","business":"true","name":"TESTCOIN","symbol":"TCN","totalAmount":"100000","decimal":"18","summary":"TEST COIN IS TEST"}}'


Response:
{"result":"S0001","data":{"cwallet":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz","block":0,"time":1596431621,"opblock":0,"maturation":null,"optype":6,"nopsp":369748,"oprice":"","signer_account":2,"n_operation":7,"optxt":"Create Business Contract Name:'TESTCOIN',Symbol:'TCN'","ophash":"00000000020000000700000004F3BE23CB0C58C16F37074663339EC4F3627E44"}}
```
### sendContract
```
Executes a contract transaction
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
sender | String | yes | Sender walelt Address|	
receiver | String | yes | Receiver walelt Address|
amount | NumberString | yes |	Amount of coins transferred from sender to receiver	|
contract | String | yes | Contract walelt Address	|
passphrase | String | yes |	Sender walelt password|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
sender | String | Sender walelt Address|
receiver | String |	Receiver walelt Address|
amount | NumberString |	Amount of coins transferred from sender to receiver	|
fee | NumberString | Transaction Fee |
balance | NumberString | Remaining balance	|
ophash | String | Transaction hash	|


```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"sendContract","params":{"sender":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","receiver":"SWogTJtxnqQD3emG57S759CzAKnxDTGwgeSGoUbfqRsKaYQL","amount":"100","contract":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz","passphrase":"password","payload":"hi"}}'

Response:
{"result":"S0001","data":{"block":0,"time":1596438644,"opblock":0,"maturation":null,"optype":7,"subtype":0,"nopsp":168,"niopsp":0,"oprice":"3076923076230769","ioprice":"3076923076230769","signer_account":2,"n_operation":8,"contract_account":18,"amount":"100000000000000000000","senders":[{"account":2,"payload":"6869","payload_type":0}],"receivers":[{"account":4}],"optxt":"Contract Transfer 100000000000000000000 ","ophash":"0000000002000000080000001FB863D37A8AFD1DDBF857FBE833DD5DD20D1161"}}
```
### adminContract
```
Executes a contract admin transaction
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
sender | String | yes |	Sender walelt Address |	
passphrase | String | yes |	Sender walelt password |
receiver | String | yes | Applied walelt Address |
contract | String | yes |	Contract walelt Address |
method | String | yes |	function method(transferEnabled,transferWalletEnabled,lockWalletVolume,burnWalletVolume,mintWalletVolume,ownershipWallet)|
amount | NumberString | yes |	function Amount(lockWalletVolume,burnWalletVolume,mintWalletVolume)|
select | Boolean | yes |	True or False(transferEnabled,transferWalletEnabled) |	

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
sender | String | Sender walelt Address|
receiver | String |	Receiver walelt Address|
amount | NumberString |	Amount of coins transferred from sender to receiver	|
fee | NumberString | Transaction Fee|	
balance | NumberString | Remaining balance|	
ophash | String | Transaction hash	|


```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"adminContract","params":{"sender":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","passphrase":"eoqkrskwktjdrhd","contract":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz","method":"transferEnabled","select":"false"}}'

Response:
{"result":"S0001","data":{"block":0,"time":1596438809,"opblock":0,"maturation":null,"optype":8,"subtype":0,"nopsp":300,"niopsp":0,"oprice":"3076923076230769","ioprice":"3076923076230769","signer_account":2,"n_operation":9,"contract_account":18,"amount":"0","senders":[{"account":2,"payload":"51808102000000000000000000000000000000000000000000000000000000000000000000000000000000000000","payload_type":1}],"receivers":[{"account":0}],"optxt":"Contract Function  ","ophash":"00000000020000000900000003EEBAEDAAD0705FD863CD112B536577F88CF32D"}}
```
### infoContract
```
Returns creation contract infomation
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes |	Contract walelt Address	|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
totalHolder | Integer |	Contract Holder Count |	
business | Boolean |	Business or Normal Contract	|
symbol | String |	Contract Symbol	|
name | String |	Contract Name	|
summary | String |	Contract Description|
issuer | String |	Issuer walelt Address|
owner | String |	Owner walelt Address|
totalAmount | String |	Issue Amount|
decimal | String |	Token decimal|

```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"infoContract","params":{"wallet":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz"}}'

Response:
{"result":"S0001","data":{"totalHolder":1,"business":true,"symbol":"'TCN'","name":"'TESTCOIN'","summary":"'TEST COIN IS TEST'","issuer":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","owner":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","decimal":18,"totalAmount":"100000.0"}}
```
### holderContract
```
Returns contract holder infomation
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes |	Contract walelt Address	|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | String |  Success(S0001) or Error(ER001 etc..) |
transfer | Boolean |	Contract transfer enabled |
business | Boolean |	Business or Normal Contract	|
totalHolder | Integer |	Contract Holder Count |
holder | Json array | Contract Holder detail |	

```
Request:
curl --request POST \
--url https://devapi.suworld.net \
--header 'content-type: application/json' \
--data '{"api":"YourApiKey","method":"holderContract","params":{"wallet":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz"}}'

Response:
{"result":"S0001","data":{"transfer":true,"bussiness":true,"totalHolder":1,"holder":[{"btransfer":true,"balance":"100000000000000000000000","wallet":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","volumeLock":"0","volumeTimeLock":"0"}]}}
```
