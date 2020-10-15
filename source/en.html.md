---
title: GonWeb - GON JavaScript SDK

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

search: true

code_clipboard: true
---

# What is GonWeb

GonWeb is a JavaScript library that calls GonGrid API to get Gon blockchain data. It can be used independently or as a plug-in for GonWeb.

# GonWeb

## GonWeb Object

Create an instance of the GonWeb javascript library. In addition to utility functions, it also includes all related modules.

### Request parameter

| Field Name | Is it necessary | description |
| ---------- | -------- | ------------- |
| fullNode   | Y        | Node API address |
| privateKey | N        | privateKey          |

> Example:

```javascript
const GonWeb = require('tronweb')
const fullNode = 'http://api.testnet.gaiaopen.network/api/v1/';
const  privateKey = "11d1b79653eda8f697f316dfc2d7e6db468252c57b7092c8dfa19cdf44e627fd";
const gonWeb = new GonWeb(fullNode,privateKey);

> gonWeb.node
> gonWeb.transactionBuilder
> gonWeb.utils

```

</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>
</br>

### privateKey

privateKey is not a required parameter, if you only want to call the method in the SDK, you can only pass the fullNode parameter

> Example:

```javascript
const gonWeb = new GonWeb(fullNode);
```

## setPrivateKey

Set the private key of the GonWeb instance, which is used to sign transactions.

<aside class="warning">
Do not use this for user-facing gonweb instances, this will result in the disclosure of private keys.
</aside>

### Usage

`gonWeb.setPrivateKey()`

### Request parameter

String

### Return value

No return value

> Example:

```javascript
gonWeb.setPrivateKey(
  "9ecf9e348738e9462e7c9fa2f40d26d3644717d127669323e3feecdd2b7caffe"
);
//return: undefined

gonWeb.defaultPrivateKey;
//return: '9ecf9e348738e9462e7c9fa2f40d26d3644717d127669323e3feecdd2b7caffe'
```

## createAccount

A new private key + public key combination will be generated. The account has not been activated on the blockchain.

<aside class="warning">
The private key created by this method. Do not use it in any unsafe environment.
</aside>

### Usage

`gonWeb.createAccount()`

### Request parameter

No

### Return value

Json

> Example:

```javascript
gonWeb.createAccount();

/*
return:
{
    privateKey: "9ecf9e348738e9462e7c9fa2f40d26d3644717d127669323e3feecdd2b7caffe",
    publicKey: "0420502d1eea08bbd0decb4e49fa93db289175495a9b098750f03b03913e9c431dceaa3569374788782a53d0111c6dcb076f1150dd546c43f93f306bdcea9cb166"
}
*/
```

## toHex

Convert any value to HEX

### Usage

`gonWeb.toHex()`

### Request parameter

String|Number|Object|Array|BigNumber - Need to be converted into HEX value.  
If it is an object or array type, it will first be converted into a string using JSON.stringify. 
If BigNumber is passed in, the HEX of the corresponding Number will be obtained.

### Return value

String

> Example:

```javascript
gonWeb.toHex("abcABC");
//return: "0x616263414243"
gonWeb.toHex({ abc: "ABC" });
//return: "0x7b22616263223a22414243227d"
```

## fromUtf8

An auxiliary function to convert data in UTF8 format to HEX format.

### Usage

`gonWeb.fromUtf8()`

### Request parameter

String

### Return value

hexString - Hexadecimal string.

> Example:

```javascript
gonWeb.fromUtf8("test");
//return: "0x74657374"
```

## toUtf8

Auxiliary function to convert HEX format to Utf8 format.

### Usage

`gonWeb.toUtf8()`

### Request parameter

hexString - Hexadecimal string.

### Return value

String - The ASCII code value corresponding to the given hexadecimal string.

> Example:

```javascript
gonWeb.toUtf8("0x74657374");
//return: "test"
```

## fromAscii

Auxiliary function to convert ASCII to HEX

### Usage

`gonWeb.fromAscii()`

### Request parameter

String

### Return value

hexString - Hexadecimal string.

> Example:

```javascript
gonWeb.fromAscii("test");
//return: "0x74657374"
```

## toAscii

Auxiliary function to convert HEX string to ASCII string.

### Usage

`gonWeb.toAscii()`

### Request parameter

hexString - Hexadecimal string.

### Return value

String - The ASCII code value corresponding to the given hexadecimal string.

> Example:

```javascript
gonWeb.toAscii("0x74657374");
//return: "test"
```

## fromDecimal

Convert a number or a number in the form of a string to a hexadecimal string.

### Usage

`gonWeb.fromDecimal()`

### Request parameter

Number|String - Number

### Return value

hexString - Hexadecimal string.

> Example:

```javascript
gonWeb.fromDecimal("100");
//return: "0x64"
```

## toDecimal

Convert a hexadecimal number to a decimal number.

### Usage

`gonWeb.toDecimal()`

### Request parameter

hexString - Hexadecimal string.

### Return value

Number - Number

> Example:

```javascript
gonWeb.toDecimal("0x64");
//return: 100
```

## toBigNumber

Convert the given number or hexadecimal string to BigNumber.

### Usage

`gonWeb.toBigNumber()`

### Request parameter

Number|hexString - Number or number in hexadecimal format.

### Return value

BigNumber - An instance of BigNumber.

> Example:

```javascript
var value = gonWeb.toBigNumber("200000000000000000000001");
console.log(value.toNumber());
//return: 2.0000000000000002e+23
console.log(value.toString(10));
//return: 200000000000000000000001
```

## sha3

Use the keccak-256 hash algorithm to calculate the hash value of a given string.

### Usage

`gonWeb.sha3()`

### Request parameter

1.String - The incoming string needs to be hashed using Keccak-256 SHA3 algorithm.
2.Object - Optional settings. If you want to parse a hexadecimal string in hex format. Need to set encoding to hex. Because 0x is ignored by default in JS.

### Return value

String - The result of hashing using Keccak-256 SHA3 algorithm.

> Example:

```javascript
var hash = tronWeb.sha3("Welcome to gonweb");
console.log(hash);
//return: 0x99e0379d8df310323f8f7d745e7aa3b63158a28c555b80a75eefe4da20580ca0
var hashOfHash = tronWeb.sha3(hash, { encoding: "hex" });
console.log(hashOfHash);
//return: 0x728ddc61a2bec551eb37f18851c74d75e658fd92f4f5805f15edb123db09764a
var hash1 = tronWeb.sha3("Welcome to gonweb", { encoding: "hex" });
console.log(hash1);
//return: 0x99e0379d8df310323f8f7d745e7aa3b63158a28c555b80a75eefe4da20580ca0
```

# GonWeb.node

## Query transaction information

> Example:

```javascript
var result = gonWeb.node.getTransactionInfoByHash('0x3823383e6232d77016f1451a5b6955a977a1f254f73f9e5bdd4ba8c408a96a58')
console.log(result);
>
Promise { <pending> }
{
    "data":{
        "blockHash":"0x55a58ff4ba4b649479fdb26c5cc34109d7c65f0465e8394bb44b137dcfcbcfab",
        "blockNumber":268305,
        "txHash":"0x3823383e6232d77016f1451a5b6955a977a1f254f73f9e5bdd4ba8c408a96a58",
        "transactionIndex":0,
        "actions":[
            {
                "actionType":256,
                "nonce":2,
                "fromAccount":"prefsabi@homes",
                "toAccount":"account@gon",
                "assetId":0,
                "gasLimit":500000,
                "amount":49,
                "remark":"hello",
                "payload":"0xf85188743140686f6d657380b841047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd83313131",
                "actionHash":"0x7593b62625852c7109633c269abb3bef92f72ab3032ea716f09ff09c9e1063bd",
                "actionIndex":0,
                "signIndex":[
                    0
                ]
            }
        ],
        "gasAssetId":0,
        "gasPrice":1000,
        "gasCost":500000000
    },
    "errorCode":0,
    "errorMsg":""
}
```

### Usage

`gonWeb.node.getTransactionInfoByHash(hash)`

### Request parameter

| Field Name | Is it necessary | description |
| -------- | -------- | --------- |
| hash     | Y       | Transaction hash |

### Return value

Object

## Check transaction status

> Example:

```javascript
var result = gonWeb.node.getTransactionReceipt('0x3823383e6232d77016f1451a5b6955a977a1f254f73f9e5bdd4ba8c408a96a58')
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "blockHash": "0x55a58ff4ba4b649479fdb26c5cc34109d7c65f0465e8394bb44b137dcfcbcfab",
        "blockNumber": 268305,
        "txHash": "0x3823383e6232d77016f1451a5b6955a977a1f254f73f9e5bdd4ba8c408a96a58",
        "transactionIndex": 0,
        "postState": "0x36b1879eba50bba87bafb2efeaee84c152643ccc7606b86530baff943dcd81af",
        "actionResults": [
            {
                "gasAllot": [
                    {
                        "name": "spongebob117",
                        "gasLimit": 100000,
                        "typeId": 0
                    },
                    {
                        "name": "founder@gon",
                        "gasLimit": 400000,
                        "typeId": 1
                    }
                ],
                "authors": [
                    {
                        "index": 0,
                        "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                        "weight": 1
                    }
                ],
                "actionType": 256,
                "status": 0,
                "index": 0,
                "gasUsed": 500000,
                "parentIndex": 0,
                "permitType": 0,
                "permitThreshold": 1
            }
        ],
        "cumulativeGasUsed": 500000,
        "totalGasUsed": 500000,
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "logs": null
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Usage

`gonWeb.node.getTransactionReceipt(hash)`

### Request parameter

| Field Name | Is it necessary | description |
| -------- | -------- | --------- |
| hash     | Y       | Transaction hash |

### Return value

Object

## Get chain configuration

### Usage

`gonWeb.node.getChainConfig()`

> Example:

```javascript
var result = gonWeb.node.getChainConfig()
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "bootnodes": [
            "gnode://0469430d2d237a97f932e3aa62eca2d396458f8c41814f860c1afd5b4bed8b7c1e2fd4bba8277d016eb410994a2fe44812fc3edbe61dfb5ec275c7c375d10c2339@boot1.testnet.gaiaopen.network:30000",
            "gnode://04e24a53e2885fa60a9d6ecfc9e582bf11db0bea0881949268edafa5c4d35f9cbcfbaf7513a445f1dfb26ba465d752944078bfd21e22f263bb8bdc53d28248a727@boot2.testnet.gaiaopen.network:30000",
            "gnode://046f82c6136f72dbc56f3ff78048d9becc03e65d086c94ca426ceffee9bea637654924669d8c969c95f52aa2ffeb85a75337f9d6c37f4eb321b1064d6abe0d242d@boot3.testnet.gaiaopen.network:30000"
        ],
        "chainId": 1,
        "chainName": "gon",
        "chainUrl": "https://www.gaiaopen.network",
        "accountParams": {
            "level": 2
        },
        "assetParams": {
            "level": 2
        },
        "chargeParams": {
            "assetRatio": 80,
            "contractRatio": 80
        },
        "upgradeParams": {
            "blockCnt": 10000,
            "upgradeRatio": 80
        },
        "dposParams": {
            "maxURLLen": 512,
            "unitStake": 1,
            "candidateMinQuantity": 100000,
            "voterMinQuantity": 1,
            "activatedMinQuantity": 600000,
            "blockInterval": 3000,
            "blockFrequency": 6,
            "candidateScheduleSize": 6,
            "backupScheduleSize": 4,
            "extraBlockReward": 0,
            "blockReward": 0
        },
        "systemName": "founder@gon",
        "accountName": "account@gon",
        "assetName": "asset@gon",
        "dposName": "dpos@gon",
        "snapshotInterval": 3600000,
        "feeName": "fee@gon",
        "systemToken": "gcoin",
        "sysTokenDecimal": 9,
        "referenceTime": 1598284800000000000
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

No

### Return value

Object

## Get the gas price

### Usage

`gonWeb.node.getGasPrice()`

> Example:

```javascript
var result = gonWeb.node.getGasPrice()
console.log(result);
>
Promise { <pending> }
{
    "data": 1000,
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

No

### Return value

Object

## Query currency information based on asset ID

### Usage

`gonWeb.node.getAssetInfoById(assetId)`

> Example:

```javascript
var result = gonWeb.node.getAssetInfoById(0)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "assetId": 0,
        "assetName": "gcoin",
        "symbol": "gcoin",
        "amount": 1000000000000000000,
        "decimals": 9,
        "founder": "owner@gon",
        "owner": "owner@gon",
        "addIssue": 1000000000000000000,
        "upperLimit": 0,
        "contract": "",
        "createdAt": 1598284800,
        "destructionNum": 0,
        "description": "GCoin",
        "logo": ""
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| assetId | Y | Asset ID |

### Return value

Object

## Obtain currency information based on the full name of the currency

### Usage

`gonWeb.node.getAssetInfoByName(assetName)`

> Example:

```javascript
var result = gonWeb.node.getAssetInfoByName('gcoin')
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "assetId": 0,
        "assetName": "gcoin",
        "symbol": "gcoin",
        "amount": 1000000000000000000,
        "decimals": 9,
        "founder": "owner@gon",
        "owner": "owner@gon",
        "addIssue": 1000000000000000000,
        "upperLimit": 0,
        "contract": "",
        "createdAt": 1598284800,
        "destructionNum": 0,
        "description": "GCoin",
        "logo": ""
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| assetName | Y | Full name of assets |

### Return value

Object

## Get contract information

### Usage

`gonWeb.node.getContract(contractName)`

> Example:

```javascript
var result = gonWeb.node.getContract('prefsabi@homes')
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "abi": "[{\"constant\":false,\"inputs\":[],\"name\":\"unpause\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"pause\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_minAmount\",\"type\":\"uint256\"}],\"name\":\"setMinAmount\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[],\"name\":\"getBaseInfo\",\"outputs\":[{\"name\":\"_originalAssetId\",\"type\":\"uint256\"},{\"name\":\"_lockAssetId\",\"type\":\"uint256\"},{\"name\":\"_minLockAmount\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"applyUnLock\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"cancleApply\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"unLock\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"lock\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"inputs\":[{\"name\":\"_originalAssetId\",\"type\":\"uint256\"},{\"name\":\"_lockAssetId\",\"type\":\"uint256\"},{\"name\":\"_minLockAmount\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
        "accountName": "prefsabi@homes",
        "founder": "@homes",
        "accountId": 4341,
        "accountType": 4,
        "number": 153574,
        "code": "608060405234801561001057600080fd5b5033600260006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff1602179055506110fb806100616000396000f30060806040526004361061006d576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680632b29c0fa146100725780632efb374e146100c557806339e899ee146101305780633e10510b14610173578063605e5ee11461023f575b600080fd5b34801561007e57600080fd5b506100c3600480360381019080803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390505050610282565b005b3480156100d157600080fd5b5061012e600480360381019080803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390505050610400565b005b34801561013c57600080fd5b50610171600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291905050506106f2565b005b34801561017f57600080fd5b506101c4600480360381019080803590602001908201803590602001919091929391929390803590602001908201803590602001919091929391929390505050610843565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156102045780820151818401526020810190506101e9565b50505050905090810190601f1680156102315780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561024b57600080fd5b50610280600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190505050610b0b565b005b606060008090506102c486868080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050610c54565b8092508193505050801515610341576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600f8152602001807f4b657920697320696c6c6567616c2e000000000000000000000000000000000081525060200191505060405180910390fd5b83836000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020846040518082805190602001908083835b6020831015156103b75780518252602082019150602081019050602083039250610392565b6001836020036101000a038019825116818451168082178552505050505050905001915050908152602001604051809103902091906103f792919061102a565b50505050505050565b600060606000600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff1615156001151514806104b25750600260009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16145b15156104bd57600080fd5b88888080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050805190602001c95050925060008314151515610574576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260148152602001807f6163636f756e74206973206e6f7420657869737400000000000000000000000081525060200191505060405180910390fd5b600090506105b387878080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050610c54565b8092508193505050801515610630576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600f8152602001807f4b657920697320696c6c6567616c2e000000000000000000000000000000000081525060200191505060405180910390fd5b84846000808673ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020846040518082805190602001908083835b6020831015156106a65780518252602082019150602081019050602083039250610681565b6001836020036101000a038019825116818451168082178552505050505050905001915050908152602001604051809103902091906106e692919061102a565b50505050505050505050565b600260009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff1614151561074e57600080fd5b600073ffffffffffffffffffffffffffffffffffffffff168173ffffffffffffffffffffffffffffffffffffffff161415151561078a57600080fd5b600160008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff161515600015151415156107e957600080fd5b60018060008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff02191690831515021790555050565b606060006060600087878080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050805190602001c95050925060008314151515610902576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004018080602001828103825260148152602001807f6163636f756e74206973206e6f7420657869737400000000000000000000000081525060200191505060405180910390fd5b6000905061094186868080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050610c54565b80925081935050508015156109be576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040180806020018281038252600f8152602001807f4b657920697320696c6c6567616c2e000000000000000000000000000000000081525060200191505060405180910390fd5b6000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020826040518082805190602001908083835b602083101515610a325780518252602082019150602081019050602083039250610a0d565b6001836020036101000a03801982511681845116808217855250505050505090500191505090815260200160405180910390208054600181600116156101000203166002900480601f016020809104026020016040519081016040528092919081815260200182805460018160011615610100020316600290048015610af95780601f10610ace57610100808354040283529160200191610af9565b820191906000526020600020905b815481529060010190602001808311610adc57829003601f168201915b50505050509350505050949350505050565b600260009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff16141515610b6757600080fd5b600073ffffffffffffffffffffffffffffffffffffffff168173ffffffffffffffffffffffffffffffffffffffff1614151515610ba357600080fd5b600160008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16151560011515141515610c0257600080fd5b600160008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81549060ff021916905550565b6060600060606000849150600082511415610c755781600093509350611023565b600090505b815181101561101b5760217f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610cb557fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191610158015610dcd5750607e7f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610d5d57fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191611155b1515610ddf5781600093509350611023565b60417f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610e1157fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191610158015610f295750605a7f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610eb957fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff191611155b1561100e5760208282815181101515610f3e57fe5b9060200101517f010000000000000000000000000000000000000000000000000000000000000090047f0100000000000000000000000000000000000000000000000000000000000000027f01000000000000000000000000000000000000000000000000000000000000009004017f0100000000000000000000000000000000000000000000000000000000000000028282815181101515610fdd57fe5b9060200101907effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff1916908160001a9053505b8080600101915050610c7a565b816001935093505b5050915091565b828054600181600116156101000203166002900490600052602060002090601f016020900481019282601f1061106b57803560ff1916838001178555611099565b82800160010185558215611099579182015b8281111561109857823582559160200191906001019061107d565b5b5090506110a691906110aa565b5090565b6110cc91905b808211156110c85760008160009055506001016110b0565b5090565b905600a165627a7a723058207ea610b86f39c314579e8ddde548904675a8b106112d6322255bf98848038bdb0029",
        "codeHash": "0x759bce2c71d45d28095345775510379fb180af521b35f9c03e197196c71cbe47",
        "threshold": 1,
        "updateAuthorThreshold": 1,
        "balances": [
            {
                "assetId": 0,
                "balance": 9360999999
            }
        ],
        "authors": [
            {
                "authorType": "pubKey",
                "author": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                "weight": 1,
                "index": 0
            }
        ],
        "description": ""
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| contractName | Y | Contract name |

### Return value

Object

## View contract results

### Usage

`gonWeb.node.getContractResult(options)`

> Example:

```javascript
var options = {
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"setEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"setWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"}],\"name\":\"get\",\"outputs\":[{\"name\":\"_value\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"delWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
    "accountName":"@homes",
    "toAccountName":"prefsabi@homes",
    "function":"get",
    "parameters":["1","2"]
}
var result = gonWeb.node.getContractResult(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "result": "0x08c379a0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000146163636f756e74206973206e6f74206578697374000000000000000000000000",
        "parameter": {
            "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"set\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"},{\"name\":\"_value\",\"type\":\"bytes\"}],\"name\":\"setEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"setWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"_accountName\",\"type\":\"string\"},{\"name\":\"_key\",\"type\":\"string\"}],\"name\":\"get\",\"outputs\":[{\"name\":\"_value\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"view\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"_account\",\"type\":\"address\"}],\"name\":\"delWhiteList\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"constructor\"}]",
            "accountName": "@homes",
            "toAccountName": "prefsabi@homes",
            "function": "get",
            "parameters": [
                "1",
                "2"
            ]
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| abi | Y | ABI file content |
| accountName | Y | account name |
| toAccountName | Y | Called contract name |
| function | Y | Method name |
| parameters | N | parameters |

### Return value

Object


## Get account information

### Usage

`gonWeb.node.getAccount(name)`

> Example:

```javascript
var result = gonWeb.node.getAccount('11@homes')
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "accountName": "11@homes",
        "founder": "11@homes",
        "accountId": 4346,
        "accountType": 4,
        "number": 443909,
        "code": "",
        "codeHash": "0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
        "threshold": 1,
        "updateAuthorThreshold": 1,
        "balances": [
            {
                "assetId": 0,
                "balance": 10000000000
            }
        ],
        "authors": [
            {
                "authorType": "pubKey",
                "author": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                "weight": 1,
                "index": 0
            }
        ],
        "description": "11是11"
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |

### Return value

Object

## Get the Nonce of the account

### Usage

`gonWeb.node.getNonce(name)`

> Example:

```javascript
var result = gonWeb.node.getNonce('prefsabi@homes')
console.log(result);
>
Promise { <pending> }
{
    "data": 5,
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |

### Return value

Object

## Get account balance

### Usage

`gonWeb.node.getAccountBalance(name, assetId)`

> Example:

```javascript
var result = gonWeb.node.getAccountBalance('prefsabi@homes', 0)
console.log(result);
>
Promise { <pending> }
{
    "data": 9360999999,
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |
| assetId | Y | Asset ID |

### Return value

Object

## Whether the account exists

### Usage

`gonWeb.node.accountExist(name)`

> Example:

```javascript
var result = gonWeb.node.accountExist('prefsabi@homes')
console.log(result);
>
Promise { <pending> }
{
    "data": true,
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| name | Y | account name |

### Return value

Object

## Get account transfer records

### Usage

`gonWeb.node.accountTransfers(options)`

> Example:

```javascript
var options = {
    "accountName":"@homes",
    "onlyConfirmed":true,
    "limit":10,
    "fingerPrint":"",
    "orderBy":"height#asc",
    "searchInternal":true,
    "assetId":0
}
var result = gonWeb.node.accountTransfers(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "meta": {
            "limit": 10,
            "nextFingerPrint": "54N1U9F897wEKcIUAiW1Ng"
        },
        "content": [
            {
                "txHash": "0x24d9ec4da570ca20bc6237078037823c94a9f9a893f8e0252bbb212ab6b382ff",
                "blockTime": 1599020193,
                "height": 2155,
                "fromAccount": "account@gon",
                "toAccount": "@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "assetId": 0,
                "amount": 100000000000000,
                "transactionType": "internal",
                "payload": "",
                "state": 1,
                "errorMsg": ""
            },
            {
                "txHash": "0x51aed6ecbb64ad91211b4f1e2ec2d718ffc5770d2737472b077201e055b892bd",
                "blockTime": 1599105669,
                "height": 30611,
                "fromAccount": "@homes",
                "toAccount": "aq@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "assetId": 0,
                "amount": 0,
                "transactionType": "general",
                "payload": "",
                "state": 1,
                "errorMsg": ""
            },
            {
                "txHash": "0x3863597565cf842efbbac7f458cf37c7a68947d837f63b667239b1c7397f9d4e",
                "blockTime": 1599105759,
                "height": 30641,
                "fromAccount": "@homes",
                "toAccount": "aq@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "assetId": 0,
                "amount": 10,
                "transactionType": "general",
                "payload": "",
                "state": 1,
                "errorMsg": ""
            },
            {
                "txHash": "0x9572665f4b487604be6853a4af0487d8e49e355cbaeef7997afba934de68c0dc",
                "blockTime": 1599105888,
                "height": 30684,
                "fromAccount": "aq@homes",
                "toAccount": "@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "assetId": 0,
                "amount": 10,
                "transactionType": "general",
                "payload": "",
                "state": 1,
                "errorMsg": ""
            },
            {
                "txHash": "0xa6764334eb19dc3a11d85efc73099a3cb08fae376fd6d2309cb816716e05d564",
                "blockTime": 1600347111,
                "height": 444425,
                "fromAccount": "prefsabi@homes",
                "toAccount": "@homes",
                "assetSymbol": "gcoin",
                "assetName": "gcoin",
                "assetId": 0,
                "amount": 1,
                "transactionType": "general",
                "payload": "",
                "state": 1,
                "errorMsg": ""
            }
        ]
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name | 
| onlyConfirmed | N | Whether it has been confirmed, the default is false | 
| limit | N |  Number of queries, 1~40, default 20 | 
| fingerPrint | N |  Query the fingerprint of the next batch of data, and pass it blank for the first time | 
| orderBy | Y | height#asc,height#desc | 
| searchInternal | N | Query internal transactions | 
| assetId | N | Asset ID |

### Return value

Object

## Signature

### Usage

`gonWeb.node.sign(transaction, privateKey)`

> Example:

```javascript
const data = {
    "accountName":"@gopen",
    "assetId":0,
    "amount":100000000000,
    "newAccountName":"test000004@gopen",
    "founder": "test000004@gopen",
    "publicKey":"0x040ff4426cf65838aab439aa3919167405c07eea24cb4c7ee665e25e61f5392914d1ab70d64e7659513a566357ac6651fa80ef1debcd41da2f0f7aa037835608dd",
    "description":"",
    "remark":"hello"
}
const builder = await gonWeb.transactionBuilder.triggerCreatAccount(data);
console.log(builder);
>
{
	"data": {
		"parameter": {
			"requestParameter": {
				"accountName": "@gopen",
				"assetId": 0,
				"remark": "hello",
				"amount": 100000000000,
				"newAccountName": "test000004@gopen",
				"founder": "test000004@gopen",
				"publicKey": "0x040ff4426cf65838aab439aa3919167405c07eea24cb4c7ee665e25e61f5392914d1ab70d64e7659513a566357ac6651fa80ef1debcd41da2f0f7aa037835608dd",
				"description": ""
			},
			"payloadParameter": {
				"accountName": "test000004@gopen",
				"founder": "test000004@gopen",
				"publicKey": "0x040ff4426cf65838aab439aa3919167405c07eea24cb4c7ee665e25e61f5392914d1ab70d64e7659513a566357ac6651fa80ef1debcd41da2f0f7aa037835608dd"
			}
		},
		"result": {
			"chainId": 1,
			"gasAssetId": 0,
			"gasPrice": 1000,
			"action": {
				"accountName": "@gopen",
				"actionType": 256,
				"assetId": 0,
				"toAccountName": "account@gon",
				"gasLimit": 500000,
				"amount": 100000000000,
				"payload": "0xf866907465737430303030303440676f70656e907465737430303030303440676f70656eb841040ff4426cf65838aab439aa3919167405c07eea24cb4c7ee665e25e61f5392914d1ab70d64e7659513a566357ac6651fa80ef1debcd41da2f0f7aa037835608dd80",
				"remark": "hello",
				"nonce": 245
			}
		}
	},
	"errorCode": 0,
	"errorMsg": ""
}
const privateKey = 'Your private key';
const signStr = await gonWeb.node.sign(builder.data.result, privateKey)
console.log(signStr);
>
{
    rawData:"0xf8e7808203e8f8e1f8df82010081f5808640676f70656e8b6163636f756e7440676f6e8307a12085174876e800b868f866907465737430303030303440676f70656e907465737430303030303440676f70656eb841040ff4426cf65838aab439aa3919167405c07eea24cb4c7ee665e25e61f5392914d1ab70d64e7659513a566357ac6651fa80ef1debcd41da2f0f7aa037835608dd808568656c6c6ff84a80f847f84525a01d92a7832651849c6bd5d7eaefb357c3027827fae91c711f4894fc6f5cfbf499a0521eac5bd39d7b8f8e2e65bfee9792934ac847fb12ab70f62259eef1d8585b9ec180"
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| transaction | Y | Transaction body |
| privateKey | N | privateKey |

If the private key has been set when GonWeb is initialized or when gonWeb.setPrivateKey() is called, the privateKey parameter does not need to be filled in, otherwise it is required.

### Return value

Object

## Broadcast transaction

### Usage

`gonWeb.node.sendRawTransaction(rawData)`

> Example:

```javascript
const signStr = {
    rawData:"0xf8e7808203e8f8e1f8df82010081f5808640676f70656e8b6163636f756e7440676f6e8307a12085174876e800b868f866907465737430303030303440676f70656e907465737430303030303440676f70656eb841040ff4426cf65838aab439aa3919167405c07eea24cb4c7ee665e25e61f5392914d1ab70d64e7659513a566357ac6651fa80ef1debcd41da2f0f7aa037835608dd808568656c6c6ff84a80f847f84525a01d92a7832651849c6bd5d7eaefb357c3027827fae91c711f4894fc6f5cfbf499a0521eac5bd39d7b8f8e2e65bfee9792934ac847fb12ab70f62259eef1d8585b9ec180"
}
gonWeb.node.sendRawTransaction(signStr);
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| rawData | Y | signature |

### Return value

N

# GonWeb.transactionBuilder

## Build a structure for creating an account

### Usage

`gonWeb.transactionBuilder.triggerCreatAccount(options)`

> Example:

```javascript
var options = {
    "accountName": "@homes",
    "assetId": 0,
    "amount": 100000000000,
    "newAccountName": "test000003@homes",
    "founder": "test000003@homes",
    "publicKey": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
    "description": "111",
    "remark": "hello"
}
var result = gonWeb.transactionBuilder.triggerCreatAccount(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "@homes",
                "assetId": 0,
                "remark": "hello",
                "amount": 100000000000,
                "newAccountName": "test000003@homes",
                "founder": "test000003@homes",
                "publicKey": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                "description": "111"
            },
            "payloadParameter": {
                "accountName": "test000003@homes",
                "founder": "test000003@homes",
                "publicKey": "0x047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd",
                "description": "111"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "@homes",
                "actionType": 256,
                "assetId": 0,
                "toAccountName": "account@gon",
                "gasLimit": 500000,
                "amount": 100000000000,
                "payload": "0xf869907465737430303030303340686f6d6573907465737430303030303340686f6d6573b841047db227d7094ce215c3a0f57e1bcc732551fe351f94249471934567e0f5dc1bf795962b8cccb87a2eb56b29fbe37d614e2f4c3c45b789ae4f1f51f4cb21972ffd83313131",
                "remark": "hello",
                "nonce": 87
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name | 
| assetId | Y | Asset ID | 
| amount | Y | Number of transfers when creating an account | 
| newAccountName | Y | New account name | 
| founder | Y | founder | 
| publicKey | Y | publicKey | 
| description | N | description | 
| remark | N | remark |

### Return value

Object

## Build a structure for updating account weights

### Usage

`gonWeb.transactionBuilder.triggerUpdateAccountAuthor(options)`

> Example:

```javascript
var options = {
    "accountName": "3@homes",
    "assetId": 0,
    "remark": "hello",
    "publicKeyAuthors": [
        {
            "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
            "weight": 2,
            "authorActionType":1
        }
    ],
    "activeAuthor": 2,
    "ownerAuthor": 2
}
var result = gonWeb.transactionBuilder.triggerUpdateAccountAuthor(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "3@homes",
                "remark": "hello",
                "publicKeyAuthors": [
                    {
                        "authorActionType": 1,
                        "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                        "weight": 2
                    }
                ],
                "activeAuthor": 2,
                "ownerAuthor": 2
            },
            "payloadParameter": {
                "threshold": 2,
                "updateAuthorThreshold": 2,
                "authorActions": [
                    {
                        "actionType": 1,
                        "author": {
                            "owner": "0x04474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c5",
                            "weight": 2
                        }
                    }
                ]
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "3@homes",
                "actionType": 259,
                "assetId": 0,
                "toAccountName": "account@gon",
                "gasLimit": 100000,
                "amount": 0,
                "payload": "0xf84e0202f84af84801f84501b84104474da0e3024d2089888dd60b7cdd79784725c4074f207b09dd7caa63a5b6ceb226b7141f4720c921003b54be581c84a05072c2d4752a1f5fae698684753424c502",
                "remark": "hello",
                "nonce": 4
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| assetId | Y | Asset ID |
| remark | Y | remark |
| activeAuthor | Y | activeAuthor |
| ownerAuthor | Y | ownerAuthor |
| publicKeyAuthors | N | PublicKey list |
| accountAuthors | N | Account list |
| addressAuthors | N | Address list |
| owner | Y | owner |
| weight | Y | weight |
| authorActionType | Y | authorAction type 0-add 1-update 2-delete |

### Return value

Object

## Build a structure that calls smart contracts

### Usage

`gonWeb.transactionBuilder.triggerSmartContract(options)`

> Example:

```javascript
var options = {
    "accountName":"4@homes",
    "toAccountName":"4@homes",
    "assetId":0,
    "amount":10,
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
    "function":"addAss",
    "parameters":[1,4127,2],
    "remark":"hello"
}
var result = gonWeb.transactionBuilder.triggerSmartContract(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "4@homes",
                "assetId": 0,
                "remark": "hello",
                "toAccountName": "4@homes",
                "amount": 10,
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "function": "addAss",
                "parameters": [
                    1,
                    4127,
                    2
                ]
            },
            "payloadParameter": {
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "function": "addAss",
                "parameters": [
                    1,
                    4127,
                    2
                ]
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "4@homes",
                "actionType": 0,
                "assetId": 0,
                "toAccountName": "4@homes",
                "gasLimit": 1000000,
                "amount": 10,
                "payload": "0x124de4710000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000101f0000000000000000000000000000000000000000000000000000000000000002",
                "remark": "hello",
                "nonce": 6
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| toAccountName | Y | Called contract name |
| assetId | Y | Asset ID |
| amount | Y | Quantity |
| abi | Y | ABI file content |
| function | Y | Method name |
| parameters | N | parameters |
| remark | N | remark |

### Return value

Object

## Build a structure for creating a contract

### Usage

`gonWeb.transactionBuilder.triggerCreateContract(options)`

> Example:

```javascript
var options = {
    "accountName":"10@homes",
    "remark":"创建合约",
    "abi":"[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
    "bin":"608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a40029",
    "parameters":[]
}
var result = gonWeb.transactionBuilder.triggerCreateContract(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "10@homes",
                "remark": "创建合约",
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "bin": "608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a40029",
                "parameters": []
            },
            "payloadParameter": {
                "abi": "[{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"addAss\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetName\",\"type\":\"string\"}],\"name\":\"getAssetID\",\"outputs\":[{\"name\":\"\",\"type\":\"int64\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"gettx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"arg\",\"type\":\"uint256\"},{\"name\":\"id\",\"type\":\"uint256\"}],\"name\":\"getEpoch\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"reg\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"amount\",\"type\":\"uint256\"}],\"name\":\"testGas\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":true,\"inputs\":[{\"name\":\"a\",\"type\":\"uint256\"}],\"name\":\"balances\",\"outputs\":[{\"name\":\"balance\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"pure\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"index\",\"type\":\"uint256\"}],\"name\":\"getCandidate\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"desc\",\"type\":\"string\"}],\"name\":\"getacctid\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"transAsset\",\"outputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"t\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"}],\"name\":\"getSnapshotTime\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getBalanceEx\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"to\",\"type\":\"address\"},{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"time\",\"type\":\"uint256\"},{\"name\":\"typeId\",\"type\":\"uint256\"},{\"name\":\"num\",\"type\":\"int64\"}],\"name\":\"getSnapBalance\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"}],\"name\":\"getCandidateNum\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[],\"name\":\"transferable\",\"outputs\":[{\"name\":\"\",\"type\":\"bool\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"value\",\"type\":\"uint256\"}],\"name\":\"setdestroyasset\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"},{\"name\":\"t\",\"type\":\"uint256\"}],\"name\":\"getassetinfo\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"assetId\",\"type\":\"uint256\"}],\"name\":\"getAssetGroup\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"epoch\",\"type\":\"uint256\"},{\"name\":\"voterID\",\"type\":\"uint256\"},{\"name\":\"candidateID\",\"type\":\"uint256\"}],\"name\":\"getVoterStake\",\"outputs\":[],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"sourcecode\",\"type\":\"bytes\"},{\"name\":\"key\",\"type\":\"bytes\"},{\"name\":\"type1\",\"type\":\"uint256\"}],\"name\":\"getcrypto\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accountID\",\"type\":\"uint256\"}],\"name\":\"getAcctTime\",\"outputs\":[{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"constant\":false,\"inputs\":[{\"name\":\"accid\",\"type\":\"uint256\"}],\"name\":\"getaccountattrs\",\"outputs\":[{\"name\":\"\",\"type\":\"bytes32\"},{\"name\":\"\",\"type\":\"uint256\"},{\"name\":\"\",\"type\":\"uint256\"}],\"payable\":false,\"stateMutability\":\"nonpayable\",\"type\":\"function\"},{\"inputs\":[],\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"constructor\"},{\"payable\":true,\"stateMutability\":\"payable\",\"type\":\"fallback\"}]",
                "bin": "608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a40029",
                "parameters": []
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "10@homes",
                "actionType": 1,
                "assetId": 0,
                "toAccountName": "10@homes",
                "gasLimit": 10000000,
                "amount": 0,
                "payload": "0x608060405261107a806100136000396000f300608060405260043610610128576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff168063124de4711461012a57806317d318bc146101815780631b05c0b2146102045780632b25a38b1461021b5780634708293e14610252578063483b80af146102ae5780634903b0d1146102db5780634bd464481461031c5780635ea32db51461035357806368669bc8146103de5780637a727a41146104285780637d3d999b1461045f57806389174bb7146104ac5780638a108c0e1461051a57806392ff0d31146105475780639b0fd02914610576578063b639096a146105c1578063bf2e5de414610678578063c3397814146106b9578063c6bcfa5c146106fa578063d38abe6b1461082c578063e80c2b311461086d575b005b34801561013657600080fd5b5061017f60048036038101908080359060200190929190803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291905050506108c4565b005b34801561018d57600080fd5b506101e8600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506108e4565b604051808260070b60070b815260200191505060405180910390f35b34801561021057600080fd5b506102196108fa565b005b34801561022757600080fd5b506102506004803603810190808035906020019092919080359060200190929190505050610941565b005b6102ac600480360381019080803590602001908201803590602001908080601f01602080910402602001604051908101604052809392919081815260200183838082843782019150505050505091929192905050506109d5565b005b3480156102ba57600080fd5b506102d9600480360381019080803590602001909291905050506109e1565b005b3480156102e757600080fd5b5061030660048036038101908080359060200190929190505050610a2d565b6040518082815260200191505060405180910390f35b34801561032857600080fd5b506103516004803603810190808035906020019092919080359060200190929190505050610a37565b005b34801561035f57600080fd5b506103ba600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290505050610c2c565b60405180848152602001838152602001828152602001935050505060405180910390f35b610426600480360381019080803573ffffffffffffffffffffffffffffffffffffffff1690602001909291908035906020019092919080359060200190929190505050610c46565b005b34801561043457600080fd5b5061045d6004803603810190808035906020019092919080359060200190929190505050610c96565b005b34801561046b57600080fd5b506104aa600480360381019080803573ffffffffffffffffffffffffffffffffffffffff16906020019092919080359060200190929190505050610ce4565b005b3480156104b857600080fd5b50610518600480360381019080803573ffffffffffffffffffffffffffffffffffffffff169060200190929190803590602001909291908035906020019092919080359060200190929190803560070b9060200190929190505050610d42565b005b34801561052657600080fd5b5061054560048036038101908080359060200190929190505050610dcb565b005b34801561055357600080fd5b5061055c610e17565b604051808215151515815260200191505060405180910390f35b34801561058257600080fd5b506105ab6004803603810190808035906020019092919080359060200190929190505050610e20565b6040518082815260200191505060405180910390f35b3480156105cd57600080fd5b506105f66004803603810190808035906020019092919080359060200190929190505050610e2d565b6040518083815260200180602001828103825283818151815260200191508051906020019080838360005b8381101561063c578082015181840152602081019050610621565b50505050905090810190601f1680156106695780820380516001836020036101000a031916815260200191505b50935050505060405180910390f35b34801561068457600080fd5b506106a360048036038101908080359060200190929190505050610f5f565b6040518082815260200191505060405180910390f35b3480156106c557600080fd5b506106f8600480360381019080803590602001909291908035906020019092919080359060200190929190505050610f6f565b005b34801561070657600080fd5b506107b1600480360381019080803590602001908201803590602001908080601f0160208091040260200160405190810160405280939291908181526020018383808284378201915050505050509192919290803590602001908201803590602001908080601f016020809104026020016040519081016040528093929190818152602001838380828437820191505050505050919291929080359060200190929190505050610fbf565b6040518080602001828103825283818151815260200191508051906020019080838360005b838110156107f15780820151818401526020810190506107d6565b50505050905090810190601f16801561081e5780820380516001836020036101000a031916815260200191505b509250505060405180910390f35b34801561083857600080fd5b506108576004803603810190808035906020019092919050505061102f565b6040518082815260200191505060405180910390f35b34801561087957600080fd5b506108986004803603810190808035906020019092919050505061103a565b604051808460001916600019168152602001838152602001828152602001935050505060405180910390f35b828273ffffffffffffffffffffffffffffffffffffffff1682c150505050565b60008082805190602001cf905080915050919050565b6000ca90507f67657474780000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a150565b6000808383d0915091507f67657445706f63680000000000000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657445706f63680000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b80805190602001c05050565b600081cd90507f74657374476173000000000000000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b6000819050919050565b60008060008060008060008888d296509650965096509650965096507f67657443616e64696461746500000000000000000000000000000000000000008760010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008660010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008560010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008460010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008360010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008260010260405180826000191660001916815260200191505060405180910390a17f67657443616e64696461746500000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050505050505050565b600080600083805190602001c99250925092509193909250565b8273ffffffffffffffffffffffffffffffffffffffff166108fc838391821502919060405160006040518083038186868a8ac4945050505050158015610c90573d6000803e3d6000fd5b50505050565b60008282c690507f676574536e617073686f7454696d6500000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a1505050565b7f67657462616c616e6365657800000000000000000000000000000000000000008273ffffffffffffffffffffffffffffffffffffffff1682c360010260405180826000191660001916815260200191505060405180910390a15050565b600080600191505b8260070b82131515610dc2578673ffffffffffffffffffffffffffffffffffffffff16868686c790507f676574536e617042616c616e63650000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a18180600101925050610d4a565b50505050505050565b600081d190507f67657443616e6469646174654e756d00000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a15050565b60006001905090565b60008282c8905092915050565b6000606060006060600080ca93507f64617461310000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a160646040519080825280601f01601f191660200182016040528015610eae5781602001602082028038833980820191505090505b509250878784805190602001c580601f01601f191660405101604052509150ca90507f64617461320000000000000000000000000000000000000000000000000000008460405180826000191660001916815260200191505060405180910390a17f64617461330000000000000000000000000000000000000000000000000000008160405180826000191660001916815260200191505060405180910390a1818395509550505050509250929050565b60008082d6905080915050919050565b6000838383d390507f676574566f7465725374616b65000000000000000000000000000000000000008160010260405180826000191660001916815260200191505060405180910390a150505050565b606080600060146040519080825280601f01601f191660200182016040528015610ff85781602001602082028038833980820191505090505b50915085805190602001868051906020018580519060200189cc80601f01601f191660405101604052905081925050509392505050565b600081cb9050919050565b600080600083c292509250925091939092505600a165627a7a7230582002feaa902ba4a656f8e92bc4dca0e5d7636f039e341a027e3712920f2953c3a400293078",
                "remark": "创建合约",
                "nonce": 2
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| remark | N | remark |
| abi | Y | ABI file content |
| bin | Y | BIN file content |
| parameters | N | parameters |

### Return value

Object

## Build a structure to update the asset agreement

### Usage

`gonWeb.transactionBuilder.triggerUpdateContract(options)`

> Example:

```javascript
var options = {
    "accountName":"@homes",
    "remark":"Update",
    "assetId":2,
    "contract":"contract0002"
}
var result = gonWeb.transactionBuilder.triggerUpdateContract(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "@homes",
                "assetId": 2,
                "contract": "contract0002",
                "remark": "更新"
            },
            "payloadParameter": {
                "assetId": 2,
                "contract": "contract0002"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "@homes",
                "actionType": 516,
                "assetId": 2,
                "toAccountName": "asset@gon",
                "gasLimit": 100000,
                "amount": 0,
                "payload": "0xce028c636f6e747261637430303032",
                "remark": "更新",
                "nonce": 87
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| remark | N | remark |
| assetId | Y | Asset ID |
| contract | Y | Asset Agreement |

### Return value

Object

## Build a structure for issuing assets

### Usage

`gonWeb.transactionBuilder.triggerIssueAsset(options)`

> Example:

```javascript
var options = {
    "accountName": "prefsabi@homes",
    "founder": "prefsabi@homes",
    "owner": "prefsabi@homes",
    "assetId": 0,
    "remark": "hello",
    "assetName": "timmyhahahaha",
    "symbol": "th",
    "assetAmount": 1000,
    "decimals": 1,
    "upperLimit": 2000,
    "contract": "hello world",
    "description": "hello"
}
var result = gonWeb.transactionBuilder.triggerIssueAsset(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "prefsabi@homes",
                "founder": "prefsabi@homes",
                "owner": "prefsabi@homes",
                "remark": "hello",
                "assetName": "timmyhahahaha",
                "symbol": "th",
                "assetAmount": 1000,
                "decimals": 1,
                "upperLimit": 2000,
                "contract": "hello world",
                "description": "hello"
            },
            "payloadParameter": {
                "assetName": "timmyhahahaha",
                "symbol": "th",
                "amount": 1000,
                "decimals": 1,
                "founder": "prefsabi@homes",
                "owner": "prefsabi@homes",
                "upperLimit": 2000,
                "contract": "hello world",
                "description": "hello"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "prefsabi@homes",
                "actionType": 513,
                "assetId": 0,
                "toAccountName": "asset@gon",
                "gasLimit": 10000000,
                "amount": 0,
                "payload": "0xf8488d74696d6d7968616861686168618274688203e8018e707265667361626940686f6d65738e707265667361626940686f6d65738207d08b68656c6c6f20776f726c648568656c6c6f",
                "remark": "hello",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| founder | Y | founder |
| owner | Y | owner (Must be consistent with accountName)|
| remark | N | remark |
| assetName | Y | Full name of assets |
| symbol | Y | Asset abbreviation |
| assetAmount | Y | Number of assets |
| decimals | Y | decimals |
| upperLimit | Y | Asset issuance ceiling |
| contract | Y | Asset Agreement |
| description | N | description |

### Return value

Object

## Build the structure of additional assets

### Usage

`gonWeb.transactionBuilder.triggerIncrementAsset(options)`

> Example:

```javascript
var options = {
    "accountName":"prefsabi@homes",
    "assetId":0,
    "remark":"hello",
    "incrAssetId":1,
    "assetAmount":1000,
    "acceptor":"abc"
}
var result = gonWeb.transactionBuilder.triggerIncrementAsset(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "prefsabi@homes",
                "remark": "hello",
                "incrAssetId": 1,
                "assetAmount": 1000,
                "acceptor": "abc"
            },
            "payloadParameter": {
                "assetId": 1,
                "amount": 1000,
                "acceptor": "abc"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "prefsabi@homes",
                "actionType": 512,
                "assetId": 0,
                "toAccountName": "asset@gon",
                "gasLimit": 100000,
                "amount": 0,
                "payload": "0xc8018203e883616263",
                "remark": "hello",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| remark | N | remark |
| incrAssetId | Y | Additional asset ID |
| assetAmount | Y | Number of additional issuances |
| acceptor | Y | Benefit account |

### Return value

Object

## Build a structure for destroying assets

### Usage

`gonWeb.transactionBuilder.triggerDestroyAsset(options)`

> Example:

```javascript
var options = {
    "accountName": "2@homes",
    "assetId": 2,
    "amount":1,
    "remark": "销毁资产"
}
var result = gonWeb.transactionBuilder.triggerDestroyAsset(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "2@homes",
                "assetId": 2,
                "remark": "销毁资产",
                "amount": 1
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "2@homes",
                "actionType": 514,
                "assetId": 2,
                "toAccountName": "asset@gon",
                "gasLimit": 100000,
                "amount": 1,
                "payload": "",
                "remark": "销毁资产",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| assetId | Y | Asset ID |
| amount | Y | Quantity |
| remark | N | remark |

### Return value

Object

## Build the structure of the transfer

### Usage

`gonWeb.transactionBuilder.triggerTransfer(options)`

> Example:

```javascript
var options = {
    "accountName":"prefsabi@homes",
    "assetId":0,
    "amount":1,
    "remark":"hello",
    "toAccountName":"prefsabi@homes"
}
var result = gonWeb.transactionBuilder.triggerTransfer(options)
console.log(result);
>
Promise { <pending> }
{
    "data": {
        "parameter": {
            "requestParameter": {
                "accountName": "prefsabi@homes",
                "assetId": 0,
                "remark": "hello",
                "amount": 1,
                "toAccountName": "prefsabi@homes"
            }
        },
        "result": {
            "chainId": 1,
            "gasAssetId": 0,
            "gasPrice": 1000,
            "action": {
                "accountName": "prefsabi@homes",
                "actionType": 515,
                "assetId": 0,
                "toAccountName": "prefsabi@homes",
                "gasLimit": 100000,
                "amount": 1,
                "payload": "",
                "remark": "hello",
                "nonce": 5
            }
        }
    },
    "errorCode": 0,
    "errorMsg": ""
}
```

### Request parameter

| Field Name | Is it necessary | description |
| --- | ------|-------------|
| accountName | Y | account name |
| assetId | Y | Asset ID |
| amount | Y | Quantity |
| remark | N | remark |
| toAccountName | Y | Transfer destination account |

### Return value

Object
