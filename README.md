# FlashloanV1

# About Flash Loans
The Flash Loan is a new way of borrowing assets on the blockchain. Initially implemented by Aave, other trending DeFi protocols such as dYdX quickly followed suit in adding this new feature. There is a property that all Ethereum transactions share that enable Flash Loans to be possible. And this key feature is atomicity.
The Flash Loan leverages atomicity to allow a user to borrow without posting collateral.There are two caveats to mention. First of all, whenever you borrow an asset in a Flash Loan you have to pay a fee of 0.09% of the amount loaned. Secondly, you must pay back the loan in the same transaction in which you borrowed. While this ability is great, it is somewhat limited in its use. Flash Loans are primarily used for arbitrage between assets.


# Remix Setup
For the sake of simplicity, we will be using the Remix IDE.

This is a browser-based IDE. Also known as an Integrated Development Environment.
Remix comes with the ability to write, debug, deploy, and otherwise manipulate Ethereum Smart Contracts.

# MetaMask Setup 
Setup MetaMask and inject web3 in remix compiler 




# Now to break down the code line by line.

 1. Importing dependencies for the smart contract
 2. The FlashLoanV1 contract is inheriting from the FlashLoanReceiverBaseV1 contract.
 3. We passed the address of one of the Lending Pool Providers of Aave. In this case, we are providing the address of DAI Lending Pool. 
 4. We have defined a function called flashLoan. It takes the address of the asset we want to flash loan. In this case the asset is DAI.
 5. We don't have any need of data for the flash loan, so we are passing an empty string.
 6. We are defining the number of DAI(in terms of wei which is 10^18) we want to loan.
 7. We initialize the LendingPool interface which is ILendingPoolV1 provided by Aave so that we can call the flashLoan function.
 8. Finally, we call our flashLoan function. The function takes 4 main parameters. First we pass the address which will receive the loan. In our case, it's our own contract.              Second, we pass the address of the asset. In our case, it's the address of DAI in the Kovan network. Third, we pass the amount of assets, and in our case it's 1 “ether”              amount  of units(or 10^18 in “wei” units). Last but not least, we pass the data value which in our case is an empty string.


#### Next, we define the second function which is executeOperation. It’s where we utilize the flash loan. It’s called internally after the flashLoan function is successfully                executed. It takes 4 main parameter which are -
        1. The address of reserve to which we will have to pay back the loan.
        2. The amount of asset
        3. The fee that is charged by the protocol
        4. Additional parameter which is used internally by the function.
 10. It checks if we received the appropriate amount of loan or else it will throw an error message.
 11. At this point, this is where you would implement logic for any arbitrary use case.
 12. We add the fee along with the loan amount by using add function provided by SafeMaths library.
 13.At last we pay back the total debt or loan amount back to the lending pool.




Deploying The Contract

    First, open your MetaMask and set your network to "Kovan Test Network".



2. Use this gist for defining the dependencies for flashloan smart contracts. Click each of the links and paste the code into the corresponding Solidity file you made earlier.
        a.ILendingPool
        b.IFlashLoanReceiver
        c. ILendingPoolAddressesProvider
        d. FlashLoanReceiverBase
        e. Withdrawable


3. Switch to the "Solidity Compiler" tab. Set the compiler to 0.6.6 and click on "Compile FlashLoan.sol".



4. You should see some warnings but no error message.

5. Now, we are all set to deploy the contract to the Kovan network. Switch to "Deploy & Run Transactions" tab. Under the environment field, change it from JavaScript VM to Injected Web3. This should open MetaMask asking for your permission.



6. Make sure the “CONTRACT” field is set to FlashLoan.sol. Provide the address of LendingPool in the text field that is next to the deploy button. In our case, it will be 0x506B0B2CF20FAA8f38a4E2B524EE43e1f4458Cc5. Then click “Deploy”. It should open up MetaMask. 

    Note: A list of all deployed contract addresses can be found here. There, you can find the addresses of various Lending Pools supported by Aave. Though the addresses are different for every token, the procedure remains the same.




7. Click on “Confirm”. Upon doing so, you should see a success notification from MetaMask. There should now be a “Deployed Contracts” in the side panel.
Funding The Flash Loan



Under the new “Deployed Contracts” tab, you will be able to copy the deployed contract's address. We will come back to this step later; in the meantime we need to add some DAI to our Flash Loan contract. This is because Flash Loans need funds in the contract to successfully execute. For that, you can jump to this link to get some DAI tokens (be sure to connect to the “Aave v2 Market” with a little “K” in the top right corner). Click on the faucet, paste in your MetaMask wallet address, and wait for confirmation.


After obtaining confirmation, we are going to add the DAI token to MetaMask. For that, open your MetaMask. Click on “Add Token” at the bottom. In the “Token Contract Address” field enter 0xFf795577d9AC8bD7D90Ee22b6C1703490b6512FD. This is the contract address for DAI in Kovan. After clicking “Next”, It should display the DAI you got from the faucet earlier.


Next up, click on the DAI token. Click on “Send” and it should open a window similar to the picture below.



Enter our Flash Loan’s contract address, which we found out where to obtain earlier. Enter the amount which we want to send. In our case, we will send 10 DAI. Then click on "Next". Click on "Confirm"! You have now successfully given your Flash Loan contract 10 DAI.
Executing The Flash Loan
Head back to Remix. Under the deployed Flash Loan contract, there’s another “flashloan” text field. This field takes a contract address of the asset we want to use. In our case it’s the Kovan Testnet’s DAI contract, which is 0xFf795577d9AC8bD7D90Ee22b6C1703490b6512FD. With that field correctly filled in, you can now hit the “transact” button as shown below.


Upon clicking the button, MetaMask should pop up asking for approval of the transaction. Confirm the transaction and you should be greeted by a success message. In Remix’s terminal you should see an URL. Click on that and you should be redirected to Etherscan.


Under “Tokens Transferred”, you should see three different transactions.


    The First one highlights the transfer of 1 DAI from LendingPool to our contract.
    The Second one indicates the payback of 1 DAI along with the fees back to the Landing pool.
    The Third arrow shows the interest generated DAI which has its separate utility.

Conclusion
We were successfully able to write the smart contract for a Flash Loan! We were able to borrow DAI from the pool, pay the Flash Loan fee, and then repay the borrowed amount all in a single transaction. You just borrowed money with no collateral!

Subscribe to our newsletter for more articles and guides on Ethereum. If you have any feedback, feel free to reach out to us via Twitter. You can always chat with us on our Discord community server, featuring some of the coolest developers you’ll ever meet :)

