# indexer/domain
This documentation provides detailed descriptions of various blockchain-related classes inside indexer/domain, each modeling specific aspects of blockchain transactions, token transfers, contract interactions, and balances. 

## Comprehensive Guide on Blockchain Classes and Their Usage

### 1. Token Transfer Classes

#### TokenTransfer
This class is a generic model for a token transfer event, which is later specialized into specific token types (e.g., ERC20, ERC721, ERC1155). It includes common transfer information such as the transaction hash, token addresses, and the value transferred.

**Attributes**:
- `transaction_hash`: The hash of the transaction.
- `log_index`: The index of the log entry within the block.
- `from_address`: The address that initiated the transfer.
- `to_address`: The recipient of the transfer.
- `token_id`: The ID of the token (optional for ERC20).
- `value`: The amount transferred (in tokens).
- `token_type`: The type of token (ERC20, ERC721, ERC1155).
- `token_address`: The address of the token contract.
- `block_number`: The block number in which the transfer occurred.
- `block_hash`: The hash of the block.
- `block_timestamp`: The timestamp when the block was mined.

**Usage**:
- Use when dealing with any token transfer that is not specific to ERC20, ERC721, or ERC1155.
- It acts as a generic representation of a token transfer event and can be further specialized.

---

#### ERC20TokenTransfer
This class models ERC20 token transfers, which are standard fungible tokens.

**Attributes**:
- Inherits all attributes from `TokenTransfer`.
- `value`: The amount of ERC20 tokens transferred (must be a positive integer).

**Usage**:
- Use this class when handling **ERC20 token transfers**.
- Typically used in functions that handle ERC20 transfers, where the `token_type` is set to `"ERC20"`.

---

#### ERC721TokenTransfer
This class models ERC721 token transfers, which are used for **non-fungible tokens (NFTs)**.

**Attributes**:
- Inherits all attributes from `TokenTransfer`.
- `token_id`: The unique identifier for the transferred NFT.
- `value`: Not used as ERC721 tokens are non-fungible. The `value` attribute will often be `1` since each token is unique.

**Usage**:
- Use this class when handling **ERC721 token transfers**.
- Suitable for NFTs, as it requires the `token_id` to specify which unique token is being transferred.

---

#### ERC1155TokenTransfer
This class models ERC1155 token transfers, which are used for **multi-token standard** (both fungible and non-fungible tokens).

**Attributes**:
- Inherits all attributes from `TokenTransfer`.
- `token_id`: The ID of the transferred token.
- `value`: The amount transferred for this specific `token_id`. Can be greater than `1` for fungible tokens.

**Usage**:
- Use this class for **ERC1155 token transfers**, as it supports batch transfers.
- Suitable when working with both fungible and non-fungible tokens (since ERC1155 can represent both).

---

### 2. Blockchain Classes

#### Trace
A trace represents an internal transaction within a smart contract call, tracking detailed information about the execution of a contract.

**Attributes**:
- `trace_id`: A unique identifier for the trace.
- `from_address`: The address that initiated the trace.
- `to_address`: The address that received the trace.
- `value`: The value transferred in the trace.
- `input`: The input data for the trace.
- `output`: The output data after execution.
- `trace_type`: The type of trace (e.g., call, delegatecall).
- `call_type`: The type of call (e.g., call, create).
- `gas`: The gas used in the trace.
- `gas_used`: The actual gas used in the trace.
- `subtraces`: The number of subtraces within the trace.
- `error`: Any error message if the trace fails.
- `status`: The status of the trace (successful or failed).
- `block_number`: The block number in which the trace was created.
- `block_hash`: The block hash.
- `block_timestamp`: The block timestamp.
- `transaction_index`: The index of the transaction.
- `transaction_hash`: The hash of the transaction.
- `trace_index`: The index of the trace in the transaction.
- `trace_address`: A list of addresses indicating the path of the trace.

**Usage**:
- Use when tracking **internal contract transactions** and execution flow, especially when tracing contract interactions like calls and delegatecalls.
- Differentiates from normal transactions in that it is focused on the execution path within a contract, not the transaction itself.

---

#### Transaction
Models a general blockchain transaction, including details about its execution and associated state changes.

**Attributes**:
- `hash`: The hash of the transaction.
- `nonce`: The transaction’s nonce (sequence number).
- `transaction_index`: The position of the transaction in the block.
- `from_address`: The address initiating the transaction.
- `to_address`: The address receiving the transaction.
- `value`: The amount of cryptocurrency transferred.
- `gas_price`: The price of gas for the transaction.
- `gas`: The amount of gas allowed for the transaction.
- `transaction_type`: The type of the transaction (e.g., 0 for regular, 2 for EIP-1559).
- `input`: The input data for the transaction.
- `block_number`: The block number in which the transaction was included.
- `block_timestamp`: The block timestamp.
- `block_hash`: The block hash.
- `blob_versioned_hashes`: List of any versioned hashes.
- `max_fee_per_gas`: Maximum fee per gas for EIP-1559 transactions.
- `max_priority_fee_per_gas`: Maximum priority fee per gas.
- `receipt`: Associated receipt for the transaction (e.g., gas used, contract address).
- `exist_error`: Whether there is an error with the transaction.
- `error`: The error message if the transaction failed.
- `revert_reason`: Reason for the transaction's failure.

**Usage**:
- Use this class when tracking general **blockchain transactions** and their details.
- It provides more comprehensive information compared to `Trace`, including the overall status of the transaction and its gas usage.

---

#### Log
Represents logs (event logs) emitted during transaction execution, typically in response to contract events.

**Attributes**:
- `log_index`: The index of the log in the block.
- `address`: The address of the contract that emitted the log.
- `data`: The event data stored in the log.
- `transaction_hash`: The transaction hash associated with the log.
- `transaction_index`: The transaction index.
- `block_timestamp`: The timestamp of the block that included the log.
- `block_number`: The block number.
- `block_hash`: The hash of the block.
- `topic0, topic1, topic2, topic3`: The topics associated with the log (usually for filtering events).

**Usage**:
- Use for tracking **logs emitted by contracts**.
- Logs are emitted during transaction execution and contain event-related data.

---

#### Receipt
Models the **transaction receipt**, providing important details like whether the transaction was successful, its gas usage, and any emitted logs.

**Attributes**:
- `transaction_hash`: The hash of the transaction.
- `transaction_index`: The transaction index within the block.
- `contract_address`: The address of the deployed contract (if applicable).
- `status`: The transaction's status (e.g., successful, failed).
- `logs`: A list of logs associated with the transaction.
- `root`: The root of the state changes.
- `cumulative_gas_used`: Total gas used up to the transaction.
- `gas_used`: Gas used by the specific transaction.
- `effective_gas_price`: The price of gas after any adjustments.
- `l1_fee`, `l1_fee_scalar`, `l1_gas_used`, `l1_gas_price`: Layer 1 fees and related values (if applicable).
- `blob_gas_used`, `blob_gas_price`: For blob transactions in EIP-4844.

**Usage**:
- Use when working with **transaction receipts** to get details on the outcome of a transaction, its gas usage, and any logs.

---

### 3. Token and Contract-Related Classes

#### Token
Models a blockchain token with general information about the token.

**Attributes**:
- `address`: The token contract address.
- `token_type`: The type of token (ERC20, ERC721, etc.).
- `name`: The name of the token.
- `symbol`: The token's symbol.
- `decimals`: The number of decimals the token supports.
- `block_number`: The block number where the token was tracked.
- `total_supply`: The total supply of the token.

**Usage**:
- Use when working with **token contracts** and their details.
- Ideal for handling general token properties.

---

#### Contract
Models a blockchain contract and provides its attributes.

**Attributes**:
- `address`: The contract address.
- `name`: The name of the contract.
- `contract_creator`: The creator of the contract.
- `creation_code`: The creation code of the contract.
- `deployed_code`: The deployed code of the contract.
- `block_number`: The block number.
- `block_hash`: The block hash.
- `block_timestamp`: The timestamp of the block.
- `transaction_index`: The index of the transaction that deployed the contract.
- `transaction_hash`: The transaction hash of the deployment.
- `transaction_from_address`: The address from which the contract was deployed.

**Usage**:
- Use when dealing with **contract deployment details**.
- Specifically designed for tracking contract creation and associated transactions.

---

#### Block
Models a blockchain block with key attributes, including the block number, hash, gas usage, and miner details.

**Attributes**:
- `number`: The block number.
- `timestamp`: The block timestamp.
- `hash`: The hash of the block.
- `parent_hash`: The hash of the parent block.
- `nonce`: The nonce of the block.
- `gas_limit`: The gas limit of the block.
- `gas_used`: The gas used by the block.
- `base_fee_per_gas`: The base fee for gas in the block.
- `blob_gas_used`: The blob gas used in the block.
- `excess_blob_gas`: Any excess blob gas used.
- `difficulty`: The difficulty of the block.
- `total_difficulty`: The total difficulty up to this block.
- `size`: The size of the block.
- `miner`: The miner of the block.
- `sha3_uncles`: The hash for the block.
- `transactions_root`: The root hash of the transactions in the block.
- `state_root`: The root hash of the state of the block.
- `receipts_root`: The root hash of the receipts for the block.
- `transactions`: List of transactions in the block.
- `extra_data`: Any extra data stored in the block.
- `withdrawals_root`: The root hash of the withdrawals for the block.

**Usage**:
- Use when tracking **block details** in a blockchain system.

---

