# thirdweb Play-to-Earn Example

This example project is a simple Play-to-Earn (P2E) game!

## The Idea

The game to be played by farmers which leads to being incentivized is a "mining" game, where your character mines for gold gems!

In the beginning, you start out with nothing! In order to play the game, you need to:

1. Mint your character NFT (ERC-1155 using the [Edition Drop](https://portal.thirdweb.com/pre-built-contracts/edition-drop) contract)
2. Purchase a pickaxe NFT from the "Shop" (Another ERC-1155 using an [Edition Drop](https://portal.thirdweb.com/pre-built-contracts/edition-drop) contract)
3. "Equip" (stake) the pickaxe NFT in the [Mining](./contracts/contracts/Mining.sol) contract (built with [thirdweb deploy](https://portal.thirdweb.com/thirdweb-deploy))
4. Start earning "Gold Gems"; ERC-20 tokens (using the [Token](https://portal.thirdweb.com/pre-built-contracts/token) contract)

<!-- Image of miner -->
<img src='./application/public/mine.gif' height='48'>
<img src='./application/public/pickaxe.png'  height='48'>
<img src='./application/public/gold-gem.png' height='48'>


## Using this Example

You can create your own copy of this project by running the following command:

```bash
npx thirdweb create --template play-to-earn
```

Inside the [contractAddresses](./application/const/contractAddresses.ts) file, you can change the contract addresses to your own contracts.

This project uses 4 contracts built with thirdweb:

| Name      | Contract Type            | Description                    | Link                                                                                                                        |
| --------- | ------------------------ | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| Gold Gems | Token (ERC-20)           | Gold Gems Rewards Token        | [View on thirdweb dashboard](https://thirdweb.com/dashboard/mumbai/token/0x18B18e5D2375c592997e1eaFf6C77A6bd24F5c44)        |
| Pickaxes  | Edition Drop (ERC-1155)  | Pickaxe NFTs                   | [View on thirdweb dashboard](https://thirdweb.com/dashboard/mumbai/edition-drop/0x9d33597aD43bE6295Fe7626baDBF72B862F71bB2) |
| Miners    | Edition Drop (ERC-1155)  | Character NFTs                 | [View on thirdweb dashboard](https://thirdweb.com/dashboard/mumbai/edition-drop/0x16A131b7e5a62E8fe83f0993aAF2ECCaBF519382) |
| Mining    | Custom (thirdweb deploy) | Staking and rewarding contract | [View on thirdweb dashboard](https://thirdweb.com/dashboard/mumbai/0x90E438ba4Bf62573FEC13F792F051E8c96C41636/)             |



## Guide

Below, you can find an explanation of the key areas of the project and code snippets explained!

### Project Structure

The project is divided into two parts:

1. The [application](./application) folder contains the code for the front-end of the application.

2. The [contracts](./contracts) folder contains our smart contract set up, including our [Mining](./contracts/contracts/Farm.sol) contract. We're using [Hardhat](https://hardhat.ethereum.org/) so that we can write tests or scripts to interact with the smart contracts locally.

### Deploying the Farm Contract

We can deploy the `Farm` contract using [thirdweb deploy](https://portal.thirdweb.com/thirdweb-deploy)!

```bash
# Change to the contracts folder
cd contracts

# Deploy the Mining contract
npx thirdweb deploy
```

## Application

The application interacts with all `4` of the contracts we created by using the thirdweb SDK.

You can learn more about the thirdweb SDK's here:

- [React](https://portal.thirdweb.com/react)
- [TypeScript](https://portal.thirdweb.com/typescript)

### Connecting to Wallets eg Trust Wallet

To allow users to interact with our contracts and make transactions, we need to connect to their wallets. Firstly, we wrap our application in the `ThirdwebProvider`:

```tsx
function MyApp({ Component, pageProps }: AppProps) {
  return (
    <ThirdwebProvider activeChain="mumbai">
      <Component {...pageProps} />
    </ThirdwebProvider>
  );
}
```


