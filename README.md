# Moonbase Alpha - Escrow
The Polkadot based Escrow dApp is based on Moonbase Alpha test network. 

# Smart contract deployment
To deploy the smart contract on your own, execute the following commands. If want to use the existing smart contract skip this step.
```
cd hardhat
npm install
mv .env.example .env
```

Provide you private key in the `.env` file. The account must have test tokens on its balance. Then execute:
```
npx hardhat run scripts/deploy.js --network moonbase
```

When done, in the console one can find the address under which the smart contract has been deployed. Copy it and replace with the existing address assigned to the `CONTRACT_ADDRESS` constant in `frontend/src/components/Trade.js`

If any changes have been made to the smart contract interface, one has to update the `frontend/src/abi/Escrow.json` with up to date ABI.


# Run frontend
To run the frontend app execute the following commands:
```
cd Polkadot/frontend
npm install
npm start
```

Open your browser and go to the following link to use the dApp:
```
http://localhost:3000/
```

There are three roles within the dApp:
- escrow owner - the account used to deploy the contract
- buyer - the account transferring funds to the escrow
- seller - the account designated by the buyer when transferring the funds

The dApp responds to the connected account change so that it always shows the UI related to the connected account's role. Possible actions based on the role:
- escrow owner - can mediate and send funds to either buyer or seller if they disagree
- buyer - after funds are sent to the escrow contract, can only release funds to the seller
- seller - can only refund buyer