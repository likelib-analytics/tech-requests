# tech-requests
Bug reports and feature requests for LikeLib team

# Bugs

## 1. Corrupted docs / wrong method name

Method `get_account_info` [described in docs](https://github.com/heshu-by-lab/likelib-utonhack-2020) is not available. Method `get_account` should be used instead.

## 2. Bugged address

```
.client/get_account_info --address "3MoV75RVds2D534XcgU6gnrTahSs"

{'method': 'get_account',
 'result': {'address': '3MoV75RVds2D534XcgU6gnrTahSs',
  'balance': '13119',
  'nonce': 2,
  'transaction_hashes': ['SVXvZYm7/gJ3K8CoSBeVBOfVBmgt6OuEOcxGtpqjDYM=',
   'SVXvZYm7/gJ3K8CoSBeVBOfVBmgt6OuEOcxGtpqjDYM='],
  'type': 'Client'},
 'status': 'ok'}
```

There are 2 equal transaction hashes but `/get_transaction` gives only one transaction with this hash. Either `get_account_info` returns a duplicate or `get_transaction` doesnt return all available data.

# Feature requests

## 1. There's no way to get hash of the block.

`get_block --number` doesn't return hash of the block. <br>
It will causes issues for analytical apps that querying the node for new blocks.

## 2. There's no direct way to get transaction hashes in a particular block.

`get_block` returns list of transactions with no transaction hash. <br>
The only way to get transaction hash is query address info, iterate over all transactions in order to find transactions with timestamp corresponding to block's timestamp.

## 3. Any miners' data is missing.

There's no way to get any data about miners, in particular:

* miner's address (the address which mined a block)
* uncles (of a block)
* difficulty (totalDifficulty)
* reward (fees -if any and block reward)
* etc

## 4. [nice to have] Get top block number/hash.

We'd like to be able to get top block number or hash with a single query. Currently there's no way to do that.

## 5. [nice to have] Network state snapshots.

We'd like to get the data about network's state. In particular:

    * POW hashrate. 
    * Nodes in the network
    * Transactions in memory pool (list of hashes)
    * etc
