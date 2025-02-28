# craftstacks 

## Overview  
craftstacks is a smart contract built on the Stacks blockchain using Clarity. It enables artisans to register, list their crafted items, and sell them to buyers in a decentralized manner. The contract also includes a platform fee mechanism and owner-controlled verification for artisans.

## Features  
- **Artisan Registration**: Users can register as artisans with a name and description.
- **Verification System**: The contract owner can verify artisans.
- **Craft Item Listing**: Artisans can list, update, or remove crafted items.
- **Purchasing System**: Buyers can purchase items, with funds automatically transferred to the artisan after deducting a platform fee.
- **Platform Fee Management**: The contract owner can modify the platform fee.
- **Fund Withdrawal**: Artisans can withdraw their balance after sales.

## Smart Contract Functions  

### Artisan Management  
- **`(register-artisan (name (string-utf8 100)) (description (string-utf8 500)))`**  
  Registers an artisan with a name and description.  

- **`(update-artisan-info (name (string-utf8 100)) (description (string-utf8 500)))`**  
  Updates an artisan's profile.  

- **`(verify-artisan (artisan principal))`**  
  Allows the contract owner to verify an artisan.  

- **`(get-artisan (wallet principal)) -> (optional (tuple ...))`**  
  Returns artisan data if available.  

### Craft Item Management  
- **`(list-craft-item (name (string-utf8 100)) (description (string-utf8 500)) (price uint) (image-url (string-utf8 500))) -> (response uint uint)`**  
  Lists a new craft item with its details and assigns a unique item ID.  

- **`(update-craft-item (item-id uint) (name (string-utf8 100)) (description (string-utf8 500)) (price uint) (image-url (string-utf8 500))) -> (response bool uint)`**  
  Updates an existing craft item if not sold.  

- **`(delist-craft-item (item-id uint)) -> (response bool uint)`**  
  Removes an unsold craft item from the marketplace.  

- **`(get-craft-item (item-id uint)) -> (optional (tuple ...))`**  
  Returns data of a specific craft item.  

### Purchasing & Transactions  
- **`(purchase-craft-item (item-id uint)) -> (response bool uint)`**  
  Transfers STX from the buyer to the artisan, deducting a platform fee.  

- **`(withdraw-funds (amount uint)) -> (response bool uint)`**  
  Allows an artisan to withdraw their funds after sales.  

### Platform Fee Management  
- **`(get-platform-fee) -> uint`**  
  Returns the current platform fee percentage.  

- **`(change-platform-fee (new-fee uint)) -> (response bool uint)`**  
  Allows the contract owner to adjust the platform fee (max 100%).  

## Error Codes  
| Code  | Description |
|-------|------------|
| `100` | Not the contract owner |
| `101` | Artisan already registered |
| `102` | Artisan not registered |
| `103` | Item not found |
| `104` | Item already sold |
| `105` | Insufficient funds |
| `404` | Not found |
| `500` | Item already sold |
| `600` | Invalid input |
| `601` | Fee too high |
| `602` | Zero price not allowed |

## Installation & Deployment  
To deploy the contract on the Stacks blockchain, use:  
```sh
clarity-cli check craftstacks.clar
clarity-cli launch craftstacks.clar
