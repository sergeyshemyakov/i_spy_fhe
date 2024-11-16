![Cover picture](pics/cover.png)

# I spy (fhe / fhim)

**Cypherpunk exploration of Fully Homomorphic Encryption that compares dev experience on Inco and Fhenix.**

ETHGlobal project from Bangkok 2024.

### Description

There are 4 encrypted bytes on a fully homomorphically encrypted blockchain, which 
can be decrypted and viewed only by spy address. Each byte can
be independently and privately set or updated by a corresponding police checkpoint address. 

### Cypherpunk description

![Spy passes](pics/pic.png)

*It's night in unnamed cypherpunk city and an undercover spy meets an informant in the corp district. 
Police checkpoints are on high alert as usual, but they will let the spy go through.*

*Each policeman chooses a predefined condition for a spy to satisfy to pass,
their decisions are private and completly independent. Checkpoint can decide to
let everybody in red jackets to pass (but not green), or only let
motorcyclists by. Policemen are free to update their requirements at any moment. 
Only the spy knows all conditions set at checkpoints 
so he can find his way in unnamed cypherpunk city.*

![Passer by detained](pics/pic2.png)

### Specification

I programmed a smart contract and verified the correctness by running tests with deployments on corresponding testnets.

|    Component     |    Implementation on Inco| Implementation on Fhenix|
|------------------|--------------------|--------------------|
|Smart contract     |[Spy.sol](https://github.com/sergeyshemyakov/fhevm-hardhat-template-rivest/blob/main/contracts/Spy.sol)            |       [Spy.sol](https://github.com/sergeyshemyakov/fhenix-hardhat-example/blob/main/contracts/Spy.sol) |
|Testing script     |[Spy.ts](https://github.com/sergeyshemyakov/fhevm-hardhat-template-rivest/blob/main/test/SpyTests/Spy.ts)            |       [Spy.ts](https://github.com/sergeyshemyakov/fhenix-hardhat-example/blob/main/test/Spy.ts) |

#### State

- Encrypted `uint32 secretRequirements` encodes 4 bytes. 
- Array of 4 addresses `checkpointAddresses` can modify the corresponding 
byte of secret requirements (starting from least significant).
- Address `spyAddress` can view `secretRequirements` offchain.

#### Functions

- Constructor sets all address from parameters and initializes secret state to zero.
- Function `setSecretRequirement` allows checkpoint address to set their byte to any value. 
It checks that the value fits in a byte and updates the encrypted
state using bit operations.
- Function `getSecretRequirements` allows spy to view the encrypted state.

#### Tests

- Check that not a checkpoint address can not set an encrypted byte.
- Check that only spy address can decrypt the private state.
- Check that 0th checkpoint address can set an encrypted byte 
and it is correctly viewed by the spy address.
- Check that 3rd checkpoint address can set an encrypted byte 
and it is correctly viewed by the spy address.
- Check that if the encrypted byte is bigger than 255, it is truncated to fit in a byte.
- Check that all checkpoint address separately set their encrypted bytes
and the total result is correctly viewed by the spy address.

#### Test transactions

You can see test transactions that went through on corresponding testnet explorers.

|       Entity          |       Address on Inco Rivest          | Address on Fhenix Nitrogen           |
|-----------|----------------|----------------|
|Spy / Deployer           |[0xabadc4402C14844431fC7521613b6922c7bdde80](https://explorer.rivest.inco.org/address/0xabadc4402C14844431fC7521613b6922c7bdde80)|[0xabadc4402C14844431fC7521613b6922c7bdde80](https://explorer.nitrogen.fhenix.zone/address/0xabadc4402C14844431fC7521613b6922c7bdde80)|
|Checkpoint 1   |[0x70C3f7fd4c9bECA84c5e3Ff117e41c7219f7a84D](https://explorer.rivest.inco.org/address/0x70C3f7fd4c9bECA84c5e3Ff117e41c7219f7a84D)|[0x70C3f7fd4c9bECA84c5e3Ff117e41c7219f7a84D](https://explorer.nitrogen.fhenix.zone/address/0x70C3f7fd4c9bECA84c5e3Ff117e41c7219f7a84D)|
|Checkpoint 2   |[0xe900053491381d51c343Cc799f177A7c7CEA5BE3](https://explorer.rivest.inco.org/address/0xe900053491381d51c343Cc799f177A7c7CEA5BE3)|[0xe900053491381d51c343Cc799f177A7c7CEA5BE3](https://explorer.nitrogen.fhenix.zone/address/0xe900053491381d51c343Cc799f177A7c7CEA5BE3)|    
|Checkpoint 3   |[0xcABEabea42780204dCB3E399CE9226f589Db3E4C](https://explorer.rivest.inco.org/address/0xcABEabea42780204dCB3E399CE9226f589Db3E4C)|[0xcABEabea42780204dCB3E399CE9226f589Db3E4C](https://explorer.nitrogen.fhenix.zone/address/0xcABEabea42780204dCB3E399CE9226f589Db3E4C)|    
|Checkpoint 4   |[0x98Ede4324cB3A413b620A0B0d3267Ee68202e581](https://explorer.rivest.inco.org/address/0x98Ede4324cB3A413b620A0B0d3267Ee68202e581)|[0x98Ede4324cB3A413b620A0B0d3267Ee68202e581](https://explorer.nitrogen.fhenix.zone/address/0x98Ede4324cB3A413b620A0B0d3267Ee68202e581)|    

![Logo](pics/logo.png)

