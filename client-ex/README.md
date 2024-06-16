# zkconnect-client: React + NextJS + Webpacking
Example of computing proofs for the [zkdrops-contracts](/zkdrops-contracts) sample repo in the browser. The majority of the work is done by the [zkdrops-lib](/zkdrops-lib) which in turn uses the work of the iden3 team's Circom libraries. 

# zkconnect front end edits
Edited client from zkdrops repo to reflect using email to create commitment and a "Subscribe" button to submit the commitment the smart contract merkle tree.

Proof computation takes 20-60s in the browser depending on the machine.

<img width="919" alt="image" src="https://github.com/VennityVlad/ZuBerlinHack/assets/44687547/97c9eb0b-11e1-4a39-8252-ccb7de9d29e0">



*[source](https://github.com/a16z/zkdrops/zkdrops-contracts/blob/master/test/temp/mt_keys_8192.csv)*

## Adding Hardhat local dev chain to Metamask
- Click the "Networks" drop down and then click "Add Network"
- Fill out with the following settings:
![local-metamask-settings](imgs/local-metamask-settings.png)

*When using hardhat + metamsk and the local chain is rebooted, you will need to go to Settings -> Advanced -> Reset account to reset your account nonce to 0.*
