# abi.py
## Working with Smart Contract Events & Functions:
### ```event_log_abi_to_topic(event_abi)```
Contracts log events when something important happens, like a money transfer. This function helps convert an event description into a unique code (called a "topic") that’s easy for the blockchain to recognize.

### ```function_abi_to_4byte_selector_str(function_abi)```
Similar to dialing a phone number, this function generates a unique 4-digit code for calling a specific function in a smart contract.

## Understanding Data Types:

### ```get_types_from_abi_type_list(abi_type_list)```
Contracts use different data types like text, numbers, and lists. This function lists the types of data a contract expects.

### ```generate_type_str(component)```
If the data type is something complex like a list of items, this function figures out how to describe it properly.

## Converting Ethereum Data:
### ```abi_string_to_text(type_str, data)```

If a contract returns text in a computer format, this function makes it readable.
### ```abi_bytes_to_bytes(type_str, data)```

Converts byte-like data (small chunks of raw info) into something the computer understands better.

### ```abi_address_to_hex(type_str, data)```
Ethereum addresses (like bank account numbers) must be formatted in a specific way. This function ensures addresses are correctly formatted.

## Special Utilities:
### ```uint256_to_bytes(value)```
Converts large numbers into a 32-byte format that Ethereum uses. Think of it as putting a big number into a box that always holds exactly 32 pieces.

### ```pad_address(address)```
Ethereum sometimes requires addresses padded with extra zeros. This function adds zeros where needed to make the address the correct length.