# 🐶 Basic NFT (ERC-721) -- Sepolia Testnet

A minimal ERC-721 NFT smart contract built with Solidity and deployed
using Foundry.

This project demonstrates:

-   ERC-721 implementation using OpenZeppelin
-   IPFS metadata integration
-   Deployment to Sepolia testnet
-   NFT minting via Foundry scripts
-   Successful wallet display verification

------------------------------------------------------------------------

## 📜 Contract Details

**Contract Name:** BasicNft\
**Token Name:** Dogie\
**Symbol:** DOG\
**Standard:** ERC-721

### 🔗 Deployed on Sepolia Testnet

**Contract Address:**

0x37783C572c52f99892789A3AD9C023Db3cd5f3BE

**View on Etherscan:**

https://sepolia.etherscan.io/address/0x37783C572c52f99892789A3AD9C023Db3cd5f3BE

------------------------------------------------------------------------

## 🧠 How It Works

Each NFT stores a `tokenURI` pointing to IPFS metadata.

Mint Flow:

Smart Contract\
→ Metadata (IPFS CID)\
→ Image (IPFS CID)

Example metadata structure:

``` json
{
  "name": "Pug",
  "description": "A cute pug NFT",
  "image": "ipfs://<IMAGE_CID>",
  "attributes": []
}
```

------------------------------------------------------------------------

## 🖼 Minted NFT

-   **Token ID:** 0\
-   **Network:** Sepolia\
-   **Standard:** ERC-721

The NFT was successfully minted and is visible in the connected wallet
on the Sepolia network.

### View on OpenSea Testnet:

https://testnets.opensea.io/assets/sepolia/0x37783C572c52f99892789A3AD9C023Db3cd5f3BE/0

------------------------------------------------------------------------

## 🛠 Tech Stack

-   Solidity \^0.8.18
-   OpenZeppelin ERC-721
-   Foundry
-   IPFS
-   Pinata
-   Sepolia Testnet

------------------------------------------------------------------------

## 🚀 Deployment

Deploy contract:

``` bash
forge script script/DeployBasicNft.s.sol:DeployBasicNft --rpc-url <SEPOLIA_RPC_URL> --private-key <PRIVATE_KEY> --broadcast
```

Mint NFT:

``` bash
forge script script/Interactions.s.sol:MintBasicNft --rpc-url <SEPOLIA_RPC_URL> --private-key <PRIVATE_KEY> --broadcast
```

------------------------------------------------------------------------

## 📂 Smart Contract

``` solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import {ERC721} from "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract BasicNft is ERC721 {
    uint256 private s_tokenCounter;
    mapping(uint256 => string) private s_tokenIdToTokenURI;

    constructor() ERC721("Dogie", "DOG") {
        s_tokenCounter = 0;
    }

    function mintNft(string memory tokenUri) public {
        s_tokenIdToTokenURI[s_tokenCounter] = tokenUri;
        _safeMint(msg.sender, s_tokenCounter);
        s_tokenCounter++;
    }

    function tokenURI(
        uint256 tokenId
    ) public view override returns (string memory) {
        return s_tokenIdToTokenURI[tokenId];
    }
}
```

------------------------------------------------------------------------

## 🎯 What This Project Demonstrates

-   Understanding of ERC-721 internals
-   Manual tokenURI storage
-   IPFS-based decentralized metadata
-   Testnet deployment workflow
-   Smart contract interaction using Foundry
-   Successful on-chain mint + wallet verification

------------------------------------------------------------------------

## ⚠️ Note

This contract is deployed on **Sepolia Testnet**, not Ethereum Mainnet.\
Test ETH was used for deployment and minting.

------------------------------------------------------------------------

## 👨‍💻 Author

Built as a Web3 learning project using Foundry and OpenZeppelin.
