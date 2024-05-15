# Types-of-Functions-Project-Create-and-Mint-Token

An ERC20 token is implemented via the Solidity smart contract MyToken. By adding functions like minting, burning, and ownership control, it expands the capabilities of the ERC20 standard token.

# Features

ERC20 Compatibility: MyToken can be seamlessly integrated with a range of Ethereum-based platforms and apps because it is completely compliant with the ERC20 standard.

Minting: Using the mint function, the contract owner can create fresh tokens and allocate them to a certain account. More tokens can be created as needed thanks to this capability.

Burning: Token holders have the option to permanently remove their own tokens from circulation by using the burn mechanism. Token holdings and the supply of tokens can both be managed with this functionality.

Ownership Control: Only the contract owner may call some of the functions included in the agreement. The control over token maintenance and security are improved by this ownership control approach.

Transfer of Tokens: Using the transfer function, token holders can move tokens to different addresses.

## Usage

Implementation:


Deploy the MyToken contract, which includes the token's name, symbol, and initial supply, to a blockchain network that is compatible with Ethereum.
Minting:


By invoking the mint function and providing the recipient account and the quantity of tokens to be minted, the contract owner can create new tokens.
Flamming:

By invoking the burn function and passing in the desired quantity of tokens to burn, token holders can burn their own tokens.
Changes:

By using the transfer function and providing the recipient address and the quantity of tokens to be transferred, token holders can send tokens to different addresses.
Transfer and Allowance From:

Token holders can use the approve function to authorize a different address to transfer tokens on their behalf.
Tokens from the token holder's account may then be transferred to another by the authorized address.

### Executing program


```
code blocks for commands
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Aquino {
    string public name;
    string public symbol;
    uint8 public decimals;
    uint256 public totalSupply;
    
    mapping(address => uint256) public balanceOf;

    address public owner;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Burn(address indexed from, uint256 value);
    event Mint(address indexed to, uint256 value);

    constructor(string memory _name, string memory _symbol, uint8 _decimals, uint256 _initialSupply) {
        name = _name;
        symbol = _symbol;
        decimals = _decimals;
        totalSupply = _initialSupply * 10 ** uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Only contract owner can call this function");
        _;
    }

    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");
        require(_to != address(0), "Invalid recipient address");

        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
        emit Transfer(msg.sender, _to, _value);
        return true;
    }

    function burn(uint256 _value) public {
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");

        balanceOf[msg.sender] -= _value;
        totalSupply -= _value;
        emit Burn(msg.sender, _value);
    }

    function mint(address _to, uint256 _value) public onlyOwner {
        require(_to != address(0), "Invalid recipient address");

        totalSupply += _value;
        balanceOf[_to] += _value;
        emit Mint(_to, _value);
        emit Transfer(address(0), _to, _value);
    }
}




## Authors



. Alber C Aquino  
. https://www.facebook.com/DBGTK


## License

This project is licensed under the [SPDX-MIT] License - see the LICENSE.md file for details
