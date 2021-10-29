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

1 Importing dependencies for the smart contract
2 The FlashLoanV1 contract is inheriting from the FlashLoanReceiverBaseV1 contract.
3 We passed the address of one of the Lending Pool Providers of Aave. In this case, we are providing the address of DAI Lending Pool. 



4 We have defined a function called flashLoan. It takes the address of the asset we want to flash loan. In this case the asset is DAI.
    5 We don't have any need of data for the flash loan, so we are passing an empty string.
    6 We are defining the number of DAI(in terms of wei which is 10^18) we want to loan.
    7 We initialize the LendingPool interface which is ILendingPoolV1 provided by Aave so that we can call the flashLoan function.
    8. Finally, we call our flashLoan function. The function takes 4 main parameters. First we pass the address which will receive the loan. In our case, it's our own contract.              Second, we pass the address of the asset. In our case, it's the address of DAI in the Kovan network. Third, we pass the amount of assets, and in our case it's 1 “ether” amount       of units(or 10^18 in “wei” units). Last but not least, we pass the data value which in our case is an empty string.
    9 Next, we define the second function which is executeOperation. It’s where we utilize the flash loan. It’s called internally after the flashLoan function is successfully                executed. It takes 4 main parameter which are -
        1. The address of reserve to which we will have to pay back the loan.
        2. The amount of asset
        3. The fee that is charged by the protocol
        4. Additional parameter which is used internally by the function.
    10. It checks if we received the appropriate amount of loan or else it will throw an error message.
    11. At this point, this is where you would implement logic for any arbitrary use case.
    12. We add the fee along with the loan amount by using add function provided by SafeMaths library.
    13.At last we pay back the total debt or loan amount back to the lending pool.

