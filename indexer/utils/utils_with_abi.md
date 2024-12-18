# token_fetcher.py

## TokenFetcher:
The TokenFetcher class is designed for efficient token data retrieval on Ethereum-like blockchains using the Multicall mechanism, Web3, and JSON-RPC. Here's how you might use it in various scenarios:

   ### Initializing TokenFetcher: 
   ```
    token_fetcher = TokenFetcher(web3, kwargs=config)
   ```
   ### Fetching Token Balances: 
Use this to retrieve token balances for a list of addresses and tokens.
```
token_fetcher = TokenFetcher(web3, kwargs=config)
```
#### Params:
tokens (list[dict]): A list of token records with required fields like address, token_address, token_type, token_id, and block_number.
#### Returns:
A list of token balance records.

### Fetching Token Metadata:
Retrieve token ownership, URIs, and supply details.
```
metadata = token_fetcher.fetch_token_ids_info(token_info_items)
```
 #### Params:
token_info_items (list[dict]): Details of tokens to query, including contract addresses, token IDs, and query flags.
#### Returns:
A list of metadata records.

### Handling Multicall Requests:
Handles concurrent Multicall requests for token data retrieval.

```
results = token_fetcher.fetch_result(chunks)
```
#### Params:
chunks (list): Batches of Multicall requests.
#### Returns:
The results of these Multicall queries.
### Decoding Multicall Results:
Decodes results from Multicall responses.
```
fallback_data = token_fetcher.fetch_to_execute_batch_calls(func, to_execute_batch_calls)
```
#### Params:
func (callable): The function to perform JSON-RPC requests.
to_execute_batch_calls (list): Tokens needing direct JSON-RPC queries.
#### Returns:
A dictionary of token results.

# abi_setting.py
We are defining the ABI for both events and functions using classes like Event and Function. When interacting with a smart contract, you need the correct ABI for the functions and events that the contract exposes.Here are the abi defined :-

## Event abi

#### WETH_DEPOSIT_EVENT: 
Event for deposits to the WETH (Wrapped ETH) contract, logging dst (destination address) and wad (amount deposited).
#### WETH_WITHDRAW_EVENT: 
Event for withdrawals from the WETH contract, logging src (source address) and wad (amount withdrawn).
#### ERC20_TRANSFER_EVENT: 
Event for ERC20 token transfers, logging from, to (addresses), and value (amount transferred).
#### ERC721_TRANSFER_EVENT: 
Event for ERC721 token transfers (NFT transfers), logging from, to (addresses), and tokenId (the specific NFT transferred).
#### ERC1155_SINGLE_TRANSFER_EVENT: 
Event for ERC1155 token transfers (with multiple token types), logging operator (who initiated the transfer), from, to, id (token type), and value (amount transferred).
#### ERC1155_BATCH_TRANSFER_EVENT:
Similar to the single transfer event, but for batch transfers of ERC1155 tokens.

## Function abi

#### TOKEN_NAME_FUNCTION: 
Function to retrieve the name of an ERC20 token.
#### TOKEN_SYMBOL_FUNCTION: 
Function to retrieve the symbol (ticker) of an ERC20 token.
#### TOKEN_DECIMALS_FUNCTION: 
Function to retrieve the number of decimals used by the ERC20 token.
#### TOKEN_TOTAL_SUPPLY_FUNCTION: 
Function to get the total supply of an ERC20 token.
#### TOKEN_TOTAL_SUPPLY_WITH_ID_FUNCTION: 
A variant of the total supply function for ERC1155 tokens, where it requires a token ID to get the supply of that specific token.
#### ERC721_OWNER_OF_FUNCTION: 
Function to get the owner of an ERC721 token by its tokenId.
#### ERC721_TOKEN_URI_FUNCTION: 
Function to retrieve the URI (Uniform Resource Identifier) of an ERC721 token, usually pointing to metadata.
#### ERC1155_MULTIPLE_TOKEN_URI_FUNCTION: 
Function to retrieve the URI for a specific ERC1155 token by its tokenId.
#### ERC20_BALANCE_OF_FUNCTION: 
Function to retrieve the balance of ERC20 tokens for a specific address.
#### ERC1155_TOKEN_ID_BALANCE_OF_FUNCTION: 
Function to retrieve the balance of an ERC1155 token (identified by id) for a specific address.


