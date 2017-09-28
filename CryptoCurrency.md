
# Steps of creating our own CryptoCurrency with Ethereum:



### We are going to create a digital Token which is  instantly compatible with the ethereum wallet and any other client or contract that uses the same standards.

1- Open the Wallet app, go to the Contracts tab and then Deploy New Contract. On the Solidity Contract Source code text field, type the code below:


```
    contract MyToken {

    /* This creates an array with all balances */

    mapping (address => uint256) public balanceOf;}

```


A mapping means an associative array.

2- create a few tokens on startup, supply it as a parameter for the function Add this code before the last closing bracket, just under the mapping.. line.

```
    function MyToken(uint256 initialSupply) {`

    balanceOf[msg.sender] = initialSupply;}
```

Take a look at the right column besides the contract and you'll see a drop down, written pick a contract. Select the "MyToken" contract and you'll see that now it shows a section called Constructor parameters. These are changeable parameters for your token, so you can reuse the same code and only change these variables in the future.

3- Write transfer function, which  has a recipient and a value as the parameter and whenever someone calls it, it will subtract the _value from their balance and add it to the _to balance.

```
    function transfer(address _to, uint256 _value) {

    /* Add and subtract new balances */

    balanceOf[msg.sender] -= _value;

    balanceOf[_to] += _value;}

```

4- Add basic information about the contract:

```
    string public name;

    string public symbol;

    uint8 public decimals;

```

5- update the constructor function to allow all those variables to be set up at the start:

```
/* Initializes contract with initial supply tokens to the creator of the contract */

function MyToken(uint256 initialSupply, string tokenName, string tokenSymbol, uint8 decimalUnits) {

    balanceOf[msg.sender] = initialSupply;              // Give the creator all initial tokens

    name = tokenName;                                   // Set the name for display purposes

    symbol = tokenSymbol;                               // Set the symbol for display purposes

    decimals = decimalUnits;                            // Amount of decimals for display purposes

}

```

6- Finally we now need something called Events. These are special, empty functions that you call to help clients like the Ethereum Wallet keep track of activities happening in the contract. Events should start with a capital letter. Add this line at the beginning of the contract to declare the event:

```
event Transfer(address indexed from, address indexed to, uint256 value);
```

And then you just need to add these two lines inside the "transfer" function:

```
    /* Notify anyone listening that this transfer took place */

    Transfer(msg.sender, _to, _value);	
```

### How to deploy

open the Ethereum Wallet, go to the contracts tab and then click "deploy new contract".

Now get the token source from above and paste it into the "Solidity source field". If the code compiles without any error, you should see a "pick a contract" drop down on the right. Get it and select the "MyToken" contract. On the right column you'll see all the parameters you need to personalize your own token. You can tweak them as you please, but for the purpose of this tutorial we recommend you to pick these parameters: 10,000 as the supply, any name you want, "%" for a symbol and 2 decimal places. Your app should be looking like this:


![Image](https://www.ethereum.org/images/tutorial/Ethereum-Wallet-Screenshot-2015-12-03-at-3.50.36-PM-10.png)


Scroll to the end of the page and you'll see an estimate of the computation cost of that contract and you can select a fee on how much ether you are willing to pay for it. Any excess ether you don't spend will be returned to you so you can leave the default settings if you wish. Press "deploy", type your account password and wait a few seconds for your transaction to be picked up.

![Image](https://www.ethereum.org/images/tutorial/Ethereum-Wallet-Screenshot-2015-12-03-at-3.50.36-PM-11.png)

You'll be redirected to the front page where you can see your transaction waiting for confirmations. Click the account named "Etherbase" (your main account) and after no more than a minute you should see that your account will show that you have 100% of the shares you just created.  To send some to a few friends: select "send", and then choose which currency you want to send (ether or your newly created share), paste your friend's address on the "to" field and press "send".

![Image](https://www.ethereum.org/images/tutorial/Screen-Shot-2015-12-03-at-9.48.15-AM.png)


If you send it to a friend, they will not see anything in their wallet yet. This is because the wallet only tracks tokens it knows about, and you have to add these manually. Now go to the "Contracts" tab and you should see a link for your newly created contract. Click on it to go to its page. Since this is a very simple contract page there isn't much to do here, just click "copy address" and paste the contract address on a text editor, you'll need it shortly.

To add a token to watch, go to the contracts page and then click "Watch Token". A pop-up will appear and you only need to paste the contract address. The token name, symbol and decimal number should be automatically filled but if it's not you can put anything you want (it will only affect how it displays on your wallet). Once you do this, you'll automatically be shown any balance you have of that token and you'll be able to send it to anyone else.

![Image](https://www.ethereum.org/images/tutorial/Screen-Shot-2015-12-03-at-9.44.42-AM.png)

And now you have your own crypto token! Tokens by themselves can be useful as value exchange on local communities, ways to keep track of worked hours or other loyalty programs.