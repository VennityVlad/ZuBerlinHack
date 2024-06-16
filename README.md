# zksubscribe
Creating a newsletter subscription list on chain needs to preserve the privacy of subscribers. Additionally, we improve upon existing email list management systems by using hashed emails, commitments and zk proofs to create a secure and privacy preserving way for user to subscribe to multiple mail lists. An off chain service with hashed emails will be required when the smart contract is called to send an email to subscribers.

A self-contained library for generating claim proofs and interacting with these contracts can be found at [a16z/zkdrops/zkdrops-lib](zkdrops-lib/), and an example front-end can be found at [a16z/zkdrops/client-ex](client-ex/).

The smart contract for distributions is forked from the a16z repo (`zkdrops-contracts/contracts/PrivateAirdrop.sol`) includes an `updateRoot` function which allows the owner to modify the Merkle tree after launch, but can be made immutable by removing that function if desired.

## How This Works
- Users type in their email addresses, and we concatenate `hash(nonce + email)` to create the `commitment`.
- The `commitment` can then be transmitted across a public or private channel without leaking information.
- An admin assembles a Merkle tree of these `commitments` and deploys the smart contracts.
- Users can then redeem with a zero-knoweldge proof that they belong in the Merkle tree without revealing which `commitment` is associated with their public key.
- Note that on-chain verification requires ~350k gas.

## Installation
- `gh repo clone a16z/zkdrops`
- `yarn install`
- For generating circuits: [Circom 2.0 install + snarkjs](https://docs.circom.io/getting-started/installation/)

## Client demo
- `yarn compile`
- `yarn start-backend`
- (new terminal window)
- `yarn deploy`
- `yarn start-client`
- Navigate to `localhost:3000` and point wallet at `localhost:8545`

## Related Work and Credits
- [Tornado.cash](https://tornado.cash/): the methods, tools, and concepts come from a simplified version of the original tornado cash protocol. Much of the circuit is lifted directly.
- [circom](https://github.com/iden3/circom) for compiling zkSnarks.
- [snarkjs](https://github.com/iden3/snarkjs) for various utilities.
- [circomlibjs](https://github.com/iden3/circomlibjs) for JavaScript equivalents of cryptographic functions.
- [Polygon Hermez's PowersOfTau](https://blog.hermez.io/hermez-cryptographic-setup/) ptau file in `./zkdrops-contracts/build/pot16_final.ptau` for trusted setup.

## Disclaimer
_These smart contracts are being provided as is. No guarantee, representation or warranty is being made, express or implied, as to the safety or correctness of the user interface or the smart contracts. They have not been audited and as such there can be no assurance they will work as intended, and users may experience delays, failures, errors, omissions or loss of transmitted information. In addition, any airdrop using these smart contracts should be conducted in accordance with applicable law. Nothing in this repo should be construed as investment advice or legal advice for any particular facts or circumstances and is not meant to replace competent counsel. It is strongly advised for you to contact a reputable attorney in your jurisdiction for any questions or concerns with respect thereto. a16z is not liable for any use of the foregoing, and users should proceed with caution and use at their own risk. See a16z.com/disclosure for more info._
