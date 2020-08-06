# JSON RPC API

* [Getting Started](#getting-started)
  * [HOW TO COMPILE SUWORLD](#how-to-compile-suworld)
  * [COMPATIBILITY](#compatibility)
  * [Download and install dependencies](#download-and-install-dependencies)
* [Node](#node)  
  * [addNode](#addnode) 
  * [nodeStatus](#nodestatus) 
  * [getProtocolVersion](#getprotocolversion) 
  * [getAppVersion](#getappversion) 
  * [nodeSearch](#nodesearch) 
* [Block](#block)  
  * [getBlock](#getblock) 
  * [getBlcokCount](#getblockcount) 
  * [getBlcokTransactions](#getblocktransaction) 
  * [getBlocks](#getblocks) 
* [Wallet](#wallet)  
  * [newWallet](#newwallet) 
  * [getWalletInfo](#getwalletinfo) 
  * [lockWallet](#lockwallet) 
  * [unlockWallet](#unlockwallet) 
  * [signMessage](#signmessage) 
  * [verifyMessage](#verifymessage) 
  * [getPrivate](#getprivate) 
  * [inputPrivate](#inputprivate) 
  * [walletRefresh](#walletrefresh) 
  * [newHDWallet](#newhdwallet) 
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

### HOW TO COMPILE SUWORLD
```
This page contains guide to compile SUWORLD for all platforms.
```
### COMPATIBILITY
```
* In Windows, it's tested with XP, Windows 7 and Windows 10.
* In Linux, is tested on Ubuntu 16.04.1, CentOS7, CentOS8 64 bits
* Cross-compatible if using Lazarus, CodeTyphon (Windows + Linux + Mac) (Note: Not tested in Mac, only Windows or Ubuntu or CentOS)
```

## Download and install dependencies

### Download OpenSSL
```
* SUWORLD uses OpenSSL code (cryptographic code maintained by OpenSSL.org)
* Introduced on SUWORLD, only OpenSSL v1.1 is allowed. Usage of OpenSSL v1.0 is deprecated
```
### OpenSSL for Windows
```
If you want to compile for WINDOWS, obtain precompiled OpenSSL DLL's
* libcrypto-1_1.dll <- 32 bits
* libcrypto-1_1-x64.dll <- 64 bits
```
### OpenSSL for Linux
```
If you want to compile for Lazarus, obtain OpenSSL source code from: https://www.openssl.org/source/
* Tested with openssl-1.1.0b.targ.gz (2016-Sep-26)
* libcrypto.so.1.1 <- Library file name for Linux
```


## Node

### addNode
```
Add nodes to connect
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
nodes | string | yes | ontaining 1 or multiple IP:port separated by ";" |

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | Intger |  Returns an integer with nodes added |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"addNode","params":{"nodes":"168.126.63.1:9714;8.8.8.8:9714"},"id":123}'


Response:
{"jsonrpc":"2.0","id":123,"result": 2}
```
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
ready      | Boolean |  Must be true, otherwise Node is not ready to execute transactions |
ready_s      | String |  Human readable information about ready or not |
status_s      | String |  Human readable information about node status. Running, downloading chain, discovering servers. |
port      | Integer |  Server port |
timestamp      | NumberString |  Timestamp of the Node |
version      | String |  Server version |
netprotocol      | JSON Object |  	ver : Integer - Net protocol version, ver_a : Integer - Net protocol available |
blocks      | NumberString |  	Blockchain blocks |
netstats      | JSON Object |  net information |
nodeservers      | JSON Array |  servers candidates |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"nodeStatus","id":123}'


Response:
{"result":{"ready":true,"ready_s":"","status_s":"Discovering servers","port":9714,"timestamp":1587027784,"version":"1.0W32b","netprotocol":{"ver":1,"ver_a":1},"blocks":11336,"netstats":{"active":5,"clients":0,"servers":6,"servers_t":6,"total":9,"tclients":1,"tservers":8,"breceived":491279,"bsend":5306},"nodeservers":[{"ip":"192.168.0.28","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.31","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.87","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.12","port":9714,"lastcon":1587027770,"attempts":0},{"ip":"192.168.0.121","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.123","port":9714,"lastcon":1587027784,"attempts":0}]},"id":123,"jsonrpc":"2.0"}
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
ver      | Integer |  	Net protocol version |
ver_a      | Integer |  Net protocol available |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getProtocolVersion","id":123}'


Response:
{"result":{"netprotocol":{"ver":1,"ver_a":1}},"id":123,"jsonrpc":"2.0"}
```
### getAppVersion
```
Returns application version
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none | none | no | none |

Return field description:

Field | Type | Description |
---------|---------|---------|
version      | String |  	Server version |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getAppVersion","id":123}'


Response:
{"result":{"version":"1.0W32b"},"id":123,"jsonrpc":"2.0"}
```
### nodeSearch
```
Add p2p discovery node connect
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none | none | no | none |

Return field description:

Field | Type | Description |
---------|---------|---------|
ready      | Boolean |  Must be true, otherwise Node is not ready to execute transactions |
ready_s      | String |  Human readable information about ready or not |
status_s      | String |  Human readable information about node status. Running, downloading chain, discovering servers. |
port      | Integer |  Server port |
timestamp      | NumberString |  Timestamp of the Node |
version      | String |  Server version |
netprotocol      | JSON Object |  	ver : Integer - Net protocol version, ver_a : Integer - Net protocol available |
blocks      | NumberString |  	Blockchain blocks |
netstats      | JSON Object |  net information |
nodeservers      | JSON Array |  servers candidates |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"nodeSearch","id":123}'


Response:
{"result":{"ready":true,"ready_s":"","status_s":"Discovering servers","port":9714,"timestamp":1587027784,"version":"1.0W32b","netprotocol":{"ver":1,"ver_a":1},"blocks":11336,"netstats":{"active":5,"clients":0,"servers":6,"servers_t":6,"total":9,"tclients":1,"tservers":8,"breceived":491279,"bsend":5306},"nodeservers":[{"ip":"192.168.0.28","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.31","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.87","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.12","port":9714,"lastcon":1587027770,"attempts":0},{"ip":"192.168.0.121","port":9714,"lastcon":1587027784,"attempts":0},{"ip":"192.168.0.123","port":9714,"lastcon":1587027784,"attempts":0}]},"id":123,"jsonrpc":"2.0"}
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
one_hash      | String |  Hash of block - 1 |
four_hash      | String |  	Hash of block - 4 |
three_hash      | String |  	Hash of block - 3 |
trx_fee      | NumberString |  Transaction Fee of block |
operations      | Intger |  Transaction count of block |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getBlcokCount","id":123}'


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
result      | NumberString |  Returns an Integer with blockcount of node |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getBlock","params":{"block":8888},"id":123}'


Response:
{"result":{"block":8888,"ver":1,"ver_a":1,"timestamp":1592211422,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455336615217638620","blocksize":3261,"hash":"0x017F60AAF6EDDC74C6EB96BDA4F09329AFD50F7755A72F57298D21A8DD69DE79","one_hash":"0xA6E3E878334810F4D240B4BEB2C94856E713AFDD9D4936FCF3A868763116CF76","four_hash":"0x2A0C9B73612D50D6F3ABE287F5CE47B0A5E8B11737E63EA1EA536675A9B67FD2","three_hash":"0x1DA701BCC62280B6CD05D1A19DC7F3A4F648FE877C776D35BD872E7D96AB1F25","trx_fee":"0","operations":13},"id":100,"jsonrpc":"2.0"}
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
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getBlcokTransactions","params":{"block":8888,"max":300},"id":123}'


Response:
{"jsonrpc":"2.0","id":123,"result": [{"block":8888,"opblock":0,"optype":1,"nopsp":20,"niopsp":0,"oprice":25,"iopprice":0,"signer_account":43905,"n_operation":5,"amount":100,"senders":[{"account":43905,"payload":"asd","payload_type":0}],"receivers":[{"account":43906}]}]}
```
### getBlocks
```
Get a list of blocks (last n blocks, or from start to end)
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
start | NumberString | yes | Block number Start block number (0..blocks count-1)|
end | NumberString | yes | End block number (0..blocks count-1)|

Return field description:

Field | Type | Description |
---------|---------|---------|
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
one_hash      | String |  Hash of block - 1 |
four_hash      | String |  	Hash of block - 4 |
three_hash      | String |  	Hash of block - 3 |
trx_fee      | NumberString |  Transaction Fee of block |
operations      | Intger |  Transaction count of block |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"getBlocks","params":{"start":"100","end":"105"}}'


Response:
{"result":[{"block":105,"ver":1,"ver_a":1,"timestamp":1592202629,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455854077893414155","blocksize":2564,"hash":"0xF3B5F7B22C736C34057A25C5AE18513A1D73B6E2784E298DEC597FEB63C13F8B","one_hash":"0xFE90798F7EACF725161463CD316A938DA3BD48B810335A7A7FCAB5773F628C77","four_hash":"0x9F4A2329DBA314291342AB5EB9069B82DE6CFBC530C262F94D8119D554B04542","three_hash":"0xCCC40C0E97EE15797213D07655EA56689D33017586278183305ED0E4A2FFC4AC","trx_fee":"0","operations":10},{"block":104,"ver":1,"ver_a":1,"timestamp":1592202628,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455854136810063120","blocksize":2564,"hash":"0xFE90798F7EACF725161463CD316A938DA3BD48B810335A7A7FCAB5773F628C77","one_hash":"0x170D4D53D868050DBA4E7748E3E3D38509E1AEE302D654E4F3D8D6263F10B9FC","four_hash":"0xB6EA23EAC42D2F4882B83966733EDFD3168946488DA8F48BEED3A58215B6391F","three_hash":"0x9F4A2329DBA314291342AB5EB9069B82DE6CFBC530C262F94D8119D554B04542","trx_fee":"0","operations":10},{"block":103,"ver":1,"ver_a":1,"timestamp":1592202627,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455854195726712144","blocksize":2564,"hash":"0x170D4D53D868050DBA4E7748E3E3D38509E1AEE302D654E4F3D8D6263F10B9FC","one_hash":"0xCCC40C0E97EE15797213D07655EA56689D33017586278183305ED0E4A2FFC4AC","four_hash":"0xDC1C1AC3F40CEE2250B26B1A9EC23137762B6C1F3E0F387D496CA8545D5CD8DE","three_hash":"0xB6EA23EAC42D2F4882B83966733EDFD3168946488DA8F48BEED3A58215B6391F","trx_fee":"0","operations":10},{"block":102,"ver":1,"ver_a":1,"timestamp":1592202626,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455854254643361226","blocksize":2564,"hash":"0xCCC40C0E97EE15797213D07655EA56689D33017586278183305ED0E4A2FFC4AC","one_hash":"0x9F4A2329DBA314291342AB5EB9069B82DE6CFBC530C262F94D8119D554B04542","four_hash":"0x2A1F2574C155430E599BE2BE4079009C25176C7D633B877EAB33A8D8A3429A27","three_hash":"0xDC1C1AC3F40CEE2250B26B1A9EC23137762B6C1F3E0F387D496CA8545D5CD8DE","trx_fee":"0","operations":10},{"block":101,"ver":1,"ver_a":1,"timestamp":1592202625,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455854313560010367","blocksize":2564,"hash":"0x9F4A2329DBA314291342AB5EB9069B82DE6CFBC530C262F94D8119D554B04542","one_hash":"0xB6EA23EAC42D2F4882B83966733EDFD3168946488DA8F48BEED3A58215B6391F","four_hash":"0x10D1B18E357BE53EFE48B6BF6D622D434A14A174F6D75D505086CFE85156907F","three_hash":"0x2A1F2574C155430E599BE2BE4079009C25176C7D633B877EAB33A8D8A3429A27","trx_fee":"0","operations":10},{"block":100,"ver":1,"ver_a":1,"timestamp":1592202624,"createwallet":0,"nopsp":"0","niopsp":"0","reward":"59455854372476659566","blocksize":2563,"hash":"0xB6EA23EAC42D2F4882B83966733EDFD3168946488DA8F48BEED3A58215B6391F","one_hash":"0xDC1C1AC3F40CEE2250B26B1A9EC23137762B6C1F3E0F387D496CA8545D5CD8DE","four_hash":"0x3818512A3F43439A6E63C35709B352DA8C35A61F0E993B4F1CA38FFF0F4FFE0E","three_hash":"0x10D1B18E357BE53EFE48B6BF6D622D434A14A174F6D75D505086CFE85156907F","trx_fee":"0","operations":10}],"id":100,"jsonrpc":"2.0"}
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
wallet      | String |  Wallet Address |
version      | Intger |  Wallet version |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"newWallet","params":{"passphrase":"password"},"id":123}'


Response:
{"result":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","version":1},"id":123,"jsonrpc":"2.0"}
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
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getWalletInfo","params":{"wallet":"SWZNDY8AeRH6G75HDmgyLRo9ghXsTSQxAvmSFH93pGMyp45a"},"id":123}'


Response:
{"result":{"account":102,"updated_active":2926,"updated_passive":2926,"n_operation":1,"balance":"100000000000000000","wallet":"SWZNDY8AeRH6G75HDmgyLRo9ghXsTSQxAvmSFH93pGMyp45a","state":"normal wallet",state_code":1},"id":100,"jsonrpc":"2.0"}
```
### lockWallet
```
Locks the Wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes | Wallet Address|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | Boolean |  True or False |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"lockWallet","params":{"wallet":"SWovpcsg6ijJhwMDf1UKyNT7AhTEEpSFeaxZbhk2BYfknU2Q"},"id":123}'


Response:
{"result":true,"id":123,"jsonrpc":"2.0"}
```
### unlockWallet
```
Unlocks the Wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes | Wallet Address|
passphrase | String | yes | 	Wallet password|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | Boolean |  True or False |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"lockWallet","params":{"wallet":"SWovpcsg6ijJhwMDf1UKyNT7AhTEEpSFeaxZbhk2BYfknU2Q"},"id":123}'


Response:
{"result":true,"id":123,"jsonrpc":"2.0"}
```
### signMessage
```
Signs a message using a public key
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
wallet | String | yes | Wallet Address|
passphrase | String | yes | 	Wallet password|
message | String | yes | 		Message to sign|

Return field description:

Field | Type | Description |
---------|---------|---------|
wallet      | String |  	Wallet Address |
msg      | String |  Origin Message |
enc      | String |  Encrypt public key |
sig      | String |  	Signature |
version      | Integer |  Wallet Version |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"signMessage","params":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","passphrase":"passphrase","message":"msg"},"id":123}'


Response:
{"result":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","msg":"asdasdasd","enc":"CA0220009005E81BE81A3014CA10C6F2BF056E3B4AC9AB875A5127DC96C1F93450658C882000C3A8E3B759BC7901381F8CDE61364FF5D74C9B0DE24B7C495ABE61A1D981638C","sig":"2000776DD80C79077C2568B4C1191DAFEED7DC89CD1E8642C4E0716132955599D8911F002B3D18B2AB773EDFA13A0AADBB6FBBA0B99AC1238B1B2BA928680FD4F9A096","version":1},"id":123,"jsonrpc":"2.0"}
```
### verifyMessage
```
Verify if a digest message is signed by a public key
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
data | String | yes | Signed return JSON|

Return field description:

Field | Type | Description |
---------|---------|---------|
result      | Boolean |  True or False |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"verifyMessage","params":{"data":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","msg":"asdasdasd","enc":"CA0220009005E81BE81A3014CA10C6F2BF056E3B4AC9AB875A5127DC96C1F93450658C882000C3A8E3B759BC7901381F8CDE61364FF5D74C9B0DE24B7C495ABE61A1D981638C","sig":"2000776DD80C79077C2568B4C1191DAFEED7DC89CD1E8642C4E0716132955599D8911F002B3D18B2AB773EDFA13A0AADBB6FBBA0B99AC1238B1B2BA928680FD4F9A096","version":1}},"id":123}'


Response:
{"result":true,"id":123,"jsonrpc":"2.0"}
```
### getPrivate
```
Get private key of specified wallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
passphrase | String | yes | Wallet password|
wallet | String | yes | Wallet Address|

Return field description:

Field | Type | Description |
---------|---------|---------|
status      | Boolean |  True or False |
msg      | String |  Private Key or Error Message |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"getPrivate","params":{"passphrase":"password","wallet":"SW5qktwYPC5A5Hbzz8FZK1NNutZRcRiRx9vBRpYVUYMmqGTn"}}'


Response:
{"result":{"status":true,"msg":"privatekey"},"id":100,"jsonrpc":"2.0"}
```
### inputPrivate
```
Imports the given unencrypted private key into the key store, encrypting it with the passphrase.
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
passphrase | String | yes | Wallet password|
private | String | yes | Private key|

Return field description:

Field | Type | Description |
---------|---------|---------|
status      | Boolean |  True or False |
msg      | String |  Private Key or Error Message |
msg      | String |  Wallet Address or Error Message |
wallet      | String |  Wallet Address |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"inputPrivate","params":{"passphrase":"password","private":"privatekey"}}'


Response:
{"result":{"status":true,"msg":"SW5qktwYPC5A5Hbzz8FZK1NNutZRcRiRx9vBRpYVUYMmqGTn","wallet":"SW5qktwYPC5A5Hbzz8FZK1NNutZRcRiRx9vBRpYVUYMmqGTn"},"id":123,"jsonrpc":"2.0"}
```
### walletRefresh
```
Update the keystore in the keystore directory
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
none | none | no | none |

Return field description:

Field | Type | Description |
---------|---------|---------|
none | none | none |


```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"walletRefresh","id":123}'


Response:
{"id":123,"jsonrpc":"2.0"}
```
### newHDWallet
```
Adds a new key to the HDWallet
```

Request parameters:

Field | Type | Required | Description |
---------|--------|---------|--------|
parent | String | yes | Main Wallet Address|
passphrase | String | yes | Wallet password|

Return field description:

Field | Type | Description |
---------|---------|---------|
parent      | String |  Parent Wallet Address |
wallet      | String |  Wallet Address |
version      | Intger |  Wallet version |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"newHDWallet","params":{"parent":"Main Wallet Address","passphrase":"password"},"id":123}'


Response:
{"result":{"parent":"Parent Wallet Address","wallet":"New HDWallet Address","version":1},"id":123,"jsonrpc":"2.0"}
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
sender      | String |  Sender Wallet address |
receiver      | String |  Receiver Wallet address |
amount      | NumberString |  Amount of coins transferred from sender to receiver |
fee      | NumberString |  Transaction Fee |
balance      | NumberString |  Remaining balance |
ophash      | String |  Transaction hash |



```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"sendTo","params":{"sender":"SWHgyqvvaiShRfvKbTw5jD5Kz7M1G6dQbnvoUxVKFvDnZtwi","receiver":"SWEk7bHfhZFg5GoZgftb18J8SKkDQbBpPA7g36dbPSambfAY","amount":1000,"passphrase":"password"},"id":123}'


Response:
{"jsonrpc":"2.0","id":123,"result": {"time":1476363846,"sender":"SWovpcsg6ijJhwMDf1UKyNT7AhTEEpSFeaxZbhk2BYfknU2Q","receiver":"SWiMyhPLdF377H4YPHW8Z5RKVNE5nK2RKcgn3NXqyw7dovUT","amount":1000, "fee":0.0001,"balance":150605.9999,"ophash":"000000006C8D0100010000003536463332393641383335344236323945464536"}}
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
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getPendingTransaction","params":{"max":100},"id":123}'


Response:
{"jsonrpc":"2.0","id":123,"result": [{"optype":1,"nopsp":20,"niopsp":0,"oprice":25,"iopprice":0,"signer_account":43905,"n_operation":5,"amount":0,"senders":[{"account":43905,"payload":"asd","payload_type":0}],"receivers":[{"account":43906}]}]}
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
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"findWalletTransaction","params":{"wallet":"SWG2LHXBHUr17SYoUpCYCvB9eXzschJbHzM4XPVNnMNvxpj7","start":8888,"max":100},"id":123}'

Response:
{"jsonrpc":"2.0","id":123,"result": [{"block":8888,"opblock":0,"optype":1,"nopsp":20,"niopsp":0,"oprice":25,"iopprice":0,"signer_account":43905,"n_operation":5,"amount":100,"senders":[{"account":43905,"payload":"asd","payload_type":0}],"receivers":[{"account":43906}],}]}
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
oprice | 	NumberString |	Action Price |	
iopprice | 	NumberString |	InAction Price |	

```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","method":"getFee","id":123}'

Response:
{"jsonrpc":"2.0","id":123,"result": {"oprice":25,"iopprice":0}}
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
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"createContract","params":{"wallet":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","passphrase":"password","business":"true","name":"TESTCOIN","symbol":"TCN","totalAmount":"100000","decimal":"18","summary":"TEST COIN IS TEST"}}'


Response:
{"result":{"cwallet":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz","block":0,"time":1596431621,"opblock":0,"maturation":null,"optype":6,"nopsp":369748,"oprice":"","signer_account":2,"n_operation":7,"optxt":"Create Business Contract Name:'TESTCOIN',Symbol:'TCN'","ophash":"00000000020000000700000004F3BE23CB0C58C16F37074663339EC4F3627E44"},"id":100,"jsonrpc":"2.0"}
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
sender | String | Sender walelt Address|
receiver | String |	Receiver walelt Address|
amount | NumberString |	Amount of coins transferred from sender to receiver	|
fee | NumberString | Transaction Fee |
balance | NumberString | Remaining balance	|
ophash | String | Transaction hash	|


```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"sendContract","params":{"sender":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","receiver":"SWogTJtxnqQD3emG57S759CzAKnxDTGwgeSGoUbfqRsKaYQL","amount":"100","contract":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz","passphrase":"password","payload":"hi"}}'

Response:
{"result":{"block":0,"time":1596438644,"opblock":0,"maturation":null,"optype":7,"subtype":0,"nopsp":168,"niopsp":0,"oprice":"3076923076230769","ioprice":"3076923076230769","signer_account":2,"n_operation":8,"contract_account":18,"amount":"100000000000000000000","senders":[{"account":2,"payload":"6869","payload_type":0}],"receivers":[{"account":4}],"optxt":"Contract Transfer 100000000000000000000 ","ophash":"0000000002000000080000001FB863D37A8AFD1DDBF857FBE833DD5DD20D1161"},"id":100,"jsonrpc":"2.0"}
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
sender | String | Sender walelt Address|
receiver | String |	Receiver walelt Address|
amount | NumberString |	Amount of coins transferred from sender to receiver	|
fee | NumberString | Transaction Fee|	
balance | NumberString | Remaining balance|	
ophash | String | Transaction hash	|


```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"adminContract","params":{"sender":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","passphrase":"eoqkrskwktjdrhd","contract":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz","method":"transferEnabled","select":"false"}}'

Response:
{"result":{"block":0,"time":1596438809,"opblock":0,"maturation":null,"optype":8,"subtype":0,"nopsp":300,"niopsp":0,"oprice":"3076923076230769","ioprice":"3076923076230769","signer_account":2,"n_operation":9,"contract_account":18,"amount":"0","senders":[{"account":2,"payload":"51808102000000000000000000000000000000000000000000000000000000000000000000000000000000000000","payload_type":1}],"receivers":[{"account":0}],"optxt":"Contract Function  ","ophash":"00000000020000000900000003EEBAEDAAD0705FD863CD112B536577F88CF32D"},"id":123,"jsonrpc":"2.0"}
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
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"infoContract","params":{"wallet":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz"}}'

Response:
{"result":{"totalHolder":1,"business":true,"symbol":"'TCN'","name":"'TESTCOIN'","summary":"'TEST COIN IS TEST'","issuer":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","owner":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","decimal":18,"totalAmount":"100000.0"},"id":123,"jsonrpc":"2.0"}
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
transfer | Boolean |	Contract transfer enabled |
business | Boolean |	Business or Normal Contract	|
totalHolder | Integer |	Contract Holder Count |
holder | Json array | Contract Holder detail |	

```
Request:
curl --request POST \
--url http://localhost:8121 \
--header 'content-type: application/json' \
--data '{"jsonrpc":"2.0","id":123,"method":"holderContract","params":{"wallet":"SW4R9entgziXv6hLeJBSGLJLLj9o6DwtBxVATui3vNBBuumz"}}'

Response:
{"result":{"transfer":true,"bussiness":true,"totalHolder":1,"holder":[{"btransfer":true,"balance":"100000000000000000000000","wallet":"SWGT2A8gY37RkBedzrX1rwi61H8ZBECSx52r1CmRdeGDjdyS","volumeLock":"0","volumeTimeLock":"0"}]},"id":123,"jsonrpc":"2.0"}
```
