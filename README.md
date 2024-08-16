# Project Title: Degen Token

A Smart Contract for Degen Token (custom ERC 20 Token) deployed on Fuji Network. It has Features like mint, burn , transfer token, Redeem token for NFTs, check token Balance.

## Description

The Contract DegenTokens.sol has custom Token Degen Token with Symbol "DEGEN". Along with the token, the contract also has a market place of items collection along with their price. Which can be acquired by any user by redeeming their token.

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
    function burn( uint256 val) public {
        require(balanceOf(msg.sender) >= val, "You don't have enough Degen tokens to burn");
        _burn(msg.sender, val);
    }
    ```

    * transferToken() function: It allows user to transfer their token to another user/address on the chain, can be done by any user on the network. The function automatically approves sender the amount of val to be transfered. 

    ```shell
    function transferToken(address sender, address _receiver, uint256 val) external {
        require(balanceOf(sender) >= val, "You don't have enough Degen tokens to transfer");
        approve(sender, val);
        _transfer(sender, _receiver, val);
    }
    ```

    * redeemToken() function: It allows user to redeem their tokens for any nft from the marketplace. it takes one parameter that the index of nft msg.sender wants to buy and check if token balance is enough. If so, that nft is added to the user's collection and can be viewed by calling showUserCollection() function.

    ```shell
    function redeemToken(uint256 carId) external payable {
        require(redeemableCars[carId].price <= balanceOf(msg.sender), "Insufficient funds");
        require(balanceOf(msg.sender) >= redeemableCars[carId].price, "You don't have enough Degen tokens to redeem");
        _burn(msg.sender, redeemableCars[carId].price);
        CarsNftCollection[msg.sender][carId] += 1;
        userCollections[msg.sender].push(UserCollection(carId));
    }
    ```

    * showUserCollection() function takes only one parameter that is the address and return an array demonstrating the nfs bought and their quantity by that address.

    shell
    function showUserCollection(address user) public view returns (uint256[] memory) {
        uint256[] memory userCollection = new uint256[](8);

        for (uint256 i = 1; i <= 8; i++) {
            userCollection[i-1] = CarsNftCollection[user][i]; 
        }

        return userCollection;
    }
