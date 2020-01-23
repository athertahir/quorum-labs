# Create your own smart contract
Are you interested in the blockchain technology? Do you want to learn solidity programming? This beginner tutorial will teach you how to create a simple cryptocurrency token based on Ethereum, the next-generation smart contract and decentralized application platform, on your local virtual machine.
Fundamentally, token systems and currencies are databases with one primary operation, which is subtracting X units from database A, and correspondingly adding X units to database B, with the following provision:
1. Database A has at least X units before the transaction.
2. The transaction is approved by A.

Because this logic can be easily implemented into a contract based on Ethereum smart contract platform, many tokens have already been created and utilized for ICO (Initial Coin Offering) projects. In this article, let’s create a cryptocurrency token by writing some Solidity codes. Note that all executions in this article are running on the browser based IDE. In our next article, we will explain in details on how to publish your token on the main blockchain.

As a Solidity new learner, a light-weight and easy development environment would be a good starting point. In this tutorial, we use Remix Solidity IDE to create a new token.
Open the Remix Solidity IDE link: https://remix.ethereum.org/ , you will see the layout of Remix IDE, as shown below.

Remix Solidity IDE interface
The left side shows a list of Solidity files. The middle is the code writing and editing section, which also provides syntax highlighting mapped to Solidity keywords. Compilation warnings and errors will be displayed in the gutter. On the right side, there are some buttons for compiling and running Solidity codes. You can also choose which VM you are about to use.
Now, let’s create a new Solidity file, called “HelloCoin”. The code we wrote to create a new currency is shown as below.

```
pragma solidity ^0.4.18;
contract HelloCoin {
string public name = 'HelloCoin'; 
//currency name. Please feel free to change it
string public symbol = 'hc'; 
//choose a currency symbol. Please feel free to change it
mapping (address => uint) balances; 
//a key-value pair to store addresses and their account balances
event Transfer(address _from, address _to, uint256 _value); 
// declaration of an event. Event will not do anything but add a record to the log
constructor() public { 
//when the contract is created, the constructor will be called automatically
balances[msg.sender] = 10000; 
//set the balances of creator account to be 10000. Please feel free to change it to any number you want.
}
function sendCoin(address _receiver, uint _amount) public returns(bool sufficient) {
if (balances[msg.sender] < _amount) return false;  
// validate transfer
balances[msg.sender] -= _amount;
balances[_receiver] += _amount;
emit Transfer(msg.sender, _receiver, _amount); 
// complete coin transfer and call event to record the log
return true;
}
function getBalance(address _addr) public view returns(uint) { 
//balance check
return balances[_addr];
}
}
```

Above is a simple example of a cryptocurrency contract. The code is very straightforward. We create some variables to record our currency’s name and symbol — “HelloCoin” and “hc”. We use mapping to keep track of the balances of all addresses. In the constructor, it gives the initial creator 10,000 value of tokens. It’s consistent with the basic definition of currency as I mentioned in the beginning — a database with one operation, that is subtracting X units from A and adding X units to B. However, the above example is not standard compatible and cannot be expected to talk to other coin/token contracts, unless your implement your coins with standards, for instance ERC20.
Now, let’s compile our code and run it on Remix IDE using the button on the right.

It seems like everything works well without fault or exception. Then, we click “Run” button on the right side. It generates a new transaction with parameters that we can set by using buttons on the right side.

Let’s take a close look at the transaction:

The above table includes contract’s address, sender’s address, recipient’s address, gas limit, gas cost for transaction and execution, and other information.
Remember that all executions mentioned above only run on the browser based IDE. Read our next blog about Truffle and Ganache CLI tools for setting a running contract on your local machine. They both are user-friendly platforms for the personal blockchain creation. Ganache even provides a GUI for you to see how each block and transaction is created.If your contract wants to be recorded in the public blockchain, you need to set up other configurations with helpful tools like Go Ethereum or MyEtherWallet.
You can always play around with Solidity and practice it on the local environment before you feel confident enough to deploy your codes on the public blockchain. A journey of a thousand miles begins with a single step. We hope this article can help you start the Solidity programming.
