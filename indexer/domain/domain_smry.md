# indexer/domain
This documentation provides detailed descriptions of various blockchain-related classes inside indexer/domain, each modeling specific aspects of blockchain transactions, token transfers, contract interactions, and balances. 

## :- block_ts_mapper.py
### BlockTsMapper class maps form mapper arg into named attributes:
   ```block_number, timestamp```

## :- block.py
### Block class models and gives the blockchain key attributes:
   ```number, timestamp, hash, parent_hash, nonce, gas_limit, gas_used, base_fee_per_gas, blob_gas_used, excess_blob_gas, difficulty, total_difficulty, size, miner, sha3_uncles, transactions_root, state_root, receipts_root, transactions, extra_data, withdrawals_root```

### UpdateBlockInternalCount class tracks updates to internal transaction counts:
   ```number, hash, traces_count, internal_transactions_count```

## :- coin_balance.py
### CoinBalance class models and gives the balance of a cryptocurrency address:
   ```address, balance, block_number, block_timestamp```

## :- contract_internal_transaction.py
### ContractInternalTransaction class models and gives an internal transaction in a blockchain contract:
   ```trace_id, from_address, to_address, value, trace_type, call_type, gas, gas_used, trace_address, error, status, block_number, block_hash, block_timestamp, transaction_index, transaction_hash, trace_index, input, output```

## :- contract.py
### Contract class models a blockchain contract with key attributes:
   ```address, name, contract_creator, creation_code, deployed_code, block_number, block_hash, block_timestamp, transaction_index, transaction_hash, transaction_from_address```

## :- current_token_balance.py
### CurrentTokenBalance class models the balance of a specific token for a given address:
   ```address, token_id, token_type, token_address, balance, block_number, block_timestamp```

## :- log.py
### Log class models a log entry from the blockchain, capturing event details:
   ```log_index, address, data, transaction_hash, transaction_index, block_timestamp, block_number, block_hash, topic0, topic1, topic2, topic3```

## :- receipt.py
### Receipt class models a blockchain transaction receipt, capturing key details such as transaction status, gas usage, and logs:
   ```transaction_hash, transaction_index, contract_address, status, logs, root, cumulative_gas_used, gas_used, effective_gas_price, l1_fee, l1_fee_scalar, l1_gas_used, l1_gas_price, blob_gas_used, blob_gas_price```

## :- token_balance.py
### TokenBalance class gives the balance of a specific token for a given address:
   ```address, token_id, token_type, token_address, balance, block_number, block_timestamp```

## :- token_id_infos.py
### ERC721TokenIdChange class models changes in the owner of an ERC721 token:
   ```token_address, token_id, token_owner, block_number, block_timestamp```

### ERC721TokenIdDetail class models track the details of an ERC721 token, including its URI:
   ```token_address, token_id, token_uri, block_number, block_timestamp, token_uri_info```

### UpdateERC721TokenIdDetail class tracks updates to ERC721 token details, including changes to ownership:
   ```token_address, token_id, token_owner, block_number, block_timestamp```

### ERC1155TokenIdDetail class models give the details of an ERC1155 token, including its URI:
   ```token_address, token_id, token_uri, block_number, block_timestamp, token_uri_info```

### UpdateERC1155TokenIdDetail class tracks updates to ERC1155 token details, including the supply of tokens:
   ```token_address, token_id, token_supply, block_number, block_timestamp```

## :- token.py
### Token class models a blockchain token with key attributes:
   ```address, token_type, name, symbol, decimals, block_number, total_supply```

### UpdateToken class tracks updates to a blockchain token's details:
   ```address, block_number, total_supply```

## :- transaction.py
### Transaction class models a blockchain transaction with key attributes:
   ```hash, nonce, transaction_index, from_address, to_address, value, gas_price, gas, transaction_type, input, block_number, block_timestamp, block_hash, blob_versioned_hashes, max_fee_per_gas, max_priority_fee_per_gas, receipt, exist_error, error, revert_reason```

## :- trace.py
### Trace class models a blockchain transaction trace with key attributes:
   ```trace_id, from_address, to_address, value, input, output, trace_type, call_type, gas, gas_used, subtraces, error, status, block_number, block_hash, block_timestamp, transaction_index, transaction_hash, trace_index, trace_address```

## :- token_transfer.py
### TokenTransfer, Models a generic token transfer with key attributes:
```transaction_hash, log_index, from_address, to_address, token_id, value, token_type, token_address, block_number, block_hash, block_timestamp```

### ERC20TokenTransfer, Models an ERC20 token transfer with key attributes:
```transaction_hash, log_index, from_address, to_address, value, token_type, token_address, block_number, block_hash, block_timestamp```

### ERC721TokenTransfer, Models an ERC721 token transfer with key attributes::
```transaction_hash, log_index, from_address, to_address, token_id, token_type, token_address, block_number, block_hash, block_timestamp```

### ERC1155TokenTransfer, Models an ERC1155 token transfer with key attributes::
```transaction_hash, log_index, from_address, to_address, token_id, value, token_type, token_address, block_number, block_hash, block_timestamp```