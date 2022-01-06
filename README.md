# MetaversePlaceCoin
https://remix.ethereum.org/#optimize=true&amp;runs=200&amp;evmVersion=null&amp;version=builtin
pragma solidity ^0.8.7;
contract MetaversePlace{
    mapping(address=>uint) public balances;
 mapping(address => mapping(address=>uint)) public allowance;



    uint public totalSupply = 1000 * 10 ** 18;
    string public name = "MetaversePlaceCoin";
    string public symbol = "MPC";
    uint public decimal = 18;
    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);
    constructor(){
        balances[msg.sender] = totalSupply;
    }

    function balanceOf(address owner) public view returns(uint){
        return balances[owner];
    }
    function transfer(address to, uint value) public returns(bool){
        require(balanceOf(msg.sender)>=value, 'Insufficient funds');
        balances[to] +=value;
        balances[msg.sender] -=value;
        emit Transfer(msg.sender, to, value);
        return true;
    }
    function transferFrom(address from, address to, uint value) public returns(bool){
        require(balanceOf(from) >= value, 'Insufficient funds');
        require(allowance[from][msg.sender] >= value, 'Insufficient funds');
        balances[to] += value; 
        balances[from] -=value;
        emit Transfer(from, to , value);
        return true;
    }
    function approve(address spender, uint value) public returns(bool){
        allowance[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }
}

