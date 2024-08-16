# ETH-Avax-inter4
The DegenToken contract is an ERC20 token with features for item redemption. It includes functions for minting, burning, transferring tokens, and redeeming items. Users can redeem predefined items by burning tokens, with the contract tracking each user’s redeemed items. The contract also provides a function to view available items and their redemption costs.

#Car nft Marketplace along with their price:
    1. Item1:  Biglight ,price: 1000
    2. Item2: Anywhere Door, price: 3000
    3. Item3: Bamboo Copter, price: 1500
    4. Item4: Time Machine, price: 5000
    
# Interact with the Contract
Mint Tokens: Only the contract owner can mint new tokens by calling the mint function with the recipient's address and the amount.
Transfer Tokens: Users can transfer their tokens to others using the transfer function.
Redeem Tokens: Users can redeem their tokens for items in the in-game store using the redeem function by specifying the item ID and quantity.
Check Token Balance: Use the balanceOf function to check the token balance of any address.
Burn Tokens: Users can burn (destroy) their own tokens using the burn function.
Check Redeemed Items: Use the getRedeemedItems function to see the items a user has redeemed.
