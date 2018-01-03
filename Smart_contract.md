# Using [Remix](https://remix.ethereum.org), a Solidity web browser based IDE that allows us to write and debug Solidity smart contracts.

### First: We made a simple smart contract that shows the address of the contract's creator and displays a greeting:


```
pragma solidity ^0.4.0;
contract helloWorld{
    
     address owner;
     string greeting;

function helloWorld()
    {  owner = msg.sender; }
    
    function creatorAdd()public constant returns (address)
    {  if(owner == msg.sender)
            return owner; }
            
    function greet(string _greeting)public constant returns (string)
    {   greeting =_greeting;
        return greeting;
    }
}
```
### Second: We made a smart contract that enables us to save new contract's addresses and display them:
```
pragma solidity ^0.4.0;

contract registration
{
     address[] newAdds;
    
    function storeAdds(address registerAdd)public 
    {   newAdds.push(registerAdd);}
    
    
    function getAll()public constant returns (address[])
    { return newAdds;}
   
    function getValue(uint8 x) constant returns (address)
    {  return newAdds[x]; }
    
}
```