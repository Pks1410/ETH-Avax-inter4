# Project Title: Degen Token

A Smart Contract for Degen Token (custom ERC 20 Token) deployed on Fuji Network. It has Features like mint, burn , transfer token, Redeem token for NFTs, check token Balance.

## Description
The DegenToken contract is an ERC20 token with features for item redemption. It includes functions for minting, burning, transferring tokens, and redeeming items. Users can redeem predefined items by burning tokens, with the contract tracking each user’s redeemed items. The contract also provides a function to view available items and their redemption costs.

* Marketplace along with their price:
  ```shell
    1. Item1: Biglight ,price: 1000
    2. Item2: Anywhere Door, price: 3000
    3. Item3: Bamboo Copter, price: 1500
    4. Item4: Time Machine, price: 5000
    ```
* functions available to interact with contract:
    * mint() function: Only owner of the contract can mint the function to any address.

    ```shell
    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }
    ```

    * burn() function: any user can burn their token using this function, if their token balance > amount to be burnt

    ```shell
  function burn(uint256 amount) public {
        require(balanceOf(msg.sender) >= amount, "Insufficient balance");
        _burn(msg.sender, amount);
    }
    ```

    * transferToken() function: It allows user to transfer their token to another user/address on the chain, can be done by any user on the network. The function automatically approves sender the amount of val to be transfered. 

    ```shell
    function TransferToken(address _receiver, uint amount) external {
        require(balanceOf(msg.sender) >= amount, "Sorry, Not enough Degen tokens available");
        approve(msg.sender, amount);
        transferFrom(msg.sender, _receiver, amount);
    }
    ```

    * redeem function :Lets users redeem an item by burning the required number of tokens.The user's token balance must be adequate to cover the redemption cost.Updates the user's redemption history.


    ```shell
   function redeem(uint256 item) external payable {
        Item storage selectedItem = items[item];
        require(bytes(selectedItem.name).length > 0, "Invalid redeem item");
        require(balanceOf(msg.sender) >= selectedItem.redeemAmount, "Insufficient balance to redeem");

        _burn(msg.sender, selectedItem.redeemAmount);
        redeemedItems[msg.sender][item] += 1; // Track the redeemed item
    }

    ```

    * showStore() function: Returns a string listing all available items along with the number of tokens required to redeem them.


    ```shell
   function showStore() external pure returns (string memory) {
        return "1.Biglight(1000 tokens) 2.Anywhere Door(3000 tokens) 3.Bamboo Copter(1500 tokens) 4.Time Machine(5000 tokens)";
    }
    ```
    * getRedeemedItems function: Retrieves the count of how many times a specific item has been redeemed by a particular user.
 
   ```shell
   function getRedeemedItems(address user, uint256 item) external view returns (uint256) {
        return redeemedItems[user][item]; // Function to get the count of redeemed items for a user
    }
   ```
### Installing

* User can fork this repository and the clone it to there local system. 
* User is required to install Node.js prior before executing the program.


### Executing program

1. After cloning the Repository, open first terminal and enter the commands: 

```shell
npm i
```
```shell
npm install @openzeppelin/contracts
```
```shell
npm install dotenv
```
```shell
npm install --save-dev hardhat
```

2. create a ".env " file in root directory and write the following in this:
```shell
WALLET_PRIVATE_KEY= your_metamask_private_key
```
Note: replace your_metamask_private_key with the private key of the metamask account which is on fuji network.
3. Now open second terminal and enter the following commands to start the hardhat node::

```shell
npx hardhat node
```

4. Finally in the third terminal, deploy the contract on fuji Network, using the following command:

```shell
npx hardhat run scripts/deploy.js --network fuji
```
This will deploy the contract on fuji successfully.

6. To run it on remix IDE install the following dependency:

```shell
npm install -g @remix-project/remixd
```

7. now type the following command:

```shell
remixd -s "shared folder path" -u https://remix.ethereum.org/
```
Note: replace the shared folder path with the root path of the project.
## Help

* To Understand the Hardhat commands on can use this command in terminal:

npx hardhat help

* To understand about avalance go the the docs section by visiting: https://docs.avax.network/

## Authors

* Name: Prakhar Sahu
* MetacrafterID: Prakhar1410 (1410sahu.prakhar@gmail.com)
* (Latest) Loom Video Link Attempt (Demonstrating all the functions mint, burn, redeem, transfer): https://www.loom.com/share/8cb7cecafd5f4bdfab7284c28f14a41a?sid=a645882f-0e58-4ac7-8282-3762b4299b01
