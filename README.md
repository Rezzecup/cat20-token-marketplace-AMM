# cat20-token-marketplace-AMM
This is an automatic market maker for CAT20 tokens on the Fractal Bitcoin network, where users can list their CAT20 tokens, and buyers can purchase or order CAT20 tokens, with transactions being executed automatically.  

## Overview
This project implements an Automatic Market Maker (AMM) for CAT20 tokens on the Fractal Bitcoin network. Users can list and trade CAT20 tokens, facilitating decentralized and automated transactions.

The CAT20 Token Marketplace AMM enables users to:

- List CAT20 tokens for sale.
- Purchase CAT20 tokens from other users.
- Automatically execute buy and sell orders.

The system is designed for security, scalability, and ease of use, leveraging the power of the Fractal Bitcoin network.

## Features

- **Automatic Market Maker**: Liquidity is provided automatically by the AMM mechanism, ensuring trades can be executed at any time.
- **Decentralized Ledger**: Transactions are secure and trustless, processed on the Fractal Bitcoin network.
- **User-Friendly Interface**: Simple interfaces for listing and purchasing tokens.

## Prerequisites

Before proceeding, ensure you have the following installed:

- [Node.js](https://nodejs.org/)
- [TypeScript](https://www.typescriptlang.org/)
- [NPM](https://www.npmjs.com/)

## Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/rezzecup/cat20-token-marketplace-AMM.git
   cd cat20-token-marketplace-AMM
   ```

2. **Install Dependencies**

   ```bash
   npm install
   ```

## Configuration

Configure your Fractal Bitcoin network settings in the `config.ts` file. You'll need access keys and any specific network parameters relevant to your deployment.

## Usage

### Start the Server

Run the server using:

```bash
npm start
```

### Listing Tokens

To list CAT20 tokens, navigate to the `/list` endpoint with the appropriate token metadata.

### Purchasing Tokens

Tokens can be purchased from the `/purchase` endpoint, specifying the desired token parameters.

## System Architecture

- **Backend**: Node.js with Express for handling API requests.
- **Frontend**: React for a responsive client-side interface.
- **Smart Contracts**: Implemented with Solidity, deployed on the Fractal Bitcoin network.

## Detailed Code Explanation

```typescript
import { AMM } from './amm';
import { Token } from './token';
import { FractalNetwork } from './network';

// Initialize the network
const network = new FractalNetwork({
  apiKey: 'YOUR_API_KEY',
});

// Initialize the AMM
const amm = new AMM(network);

// List a new token
const listToken = async (tokenId: string, amount: number) => {
  const token = new Token(tokenId, amount);
  await amm.listToken(token);
};

// Purchase a token
const purchaseToken = async (tokenId: string, amount: number) => {
  await amm.purchaseToken(tokenId, amount);
};

// Example usage
(async () => {
  await listToken('cat20-xyz', 100);
  await purchaseToken('cat20-xyz', 10);
})();
```

Creating a detailed codebase for an Automated Market Maker (AMM) involves several components, including smart contracts for handling the logic on the blockchain, a backend to interact with the blockchain, and potentially a frontend for user interaction. Below is a more detailed TypeScript example for the backend and an outline for smart contracts. 

### Directory Structure

```
cat20-token-marketplace-AMM/
│
├── backend/
    ├── src/
    │   ├── amm.ts
    │   ├── index.ts
    │   ├── network.ts
    │   └── token.ts
    ├── package.json
    └── tsconfig.json
```

### `backend/src/amm.ts`

This file implements the core logic of the AMM.

```typescript
import { Token } from './token';
import { FractalNetwork } from './network';

class AMM {
  private network: FractalNetwork;

  constructor(network: FractalNetwork) {
    this.network = network;
  }

  async listToken(token: Token): Promise<void> {
    // Logic to list token on the market
    console.log(`Listing token: ${token.id}`);
    await this.network.sendTransaction({
      from: this.network.adminAccount,
      to: 'AMM_CONTRACT_ADDRESS',
      data: token.encodeListingData(),
    });
  }

  async purchaseToken(tokenId: string, amount: number): Promise<void> {
    // Logic to purchase token
    console.log(`Purchasing ${amount} of token: ${tokenId}`);
    await this.network.sendTransaction({
      from: 'USER_ADDRESS',
      to: 'AMM_CONTRACT_ADDRESS',
      data: Token.encodePurchaseData(tokenId, amount),
    });
  }
}

export { AMM };
```

### `backend/src/network.ts`

Handles the connection and interactions with the Fractal Bitcoin network.

```typescript
class FractalNetwork {
  adminAccount: string;
  apiKey: string;

  constructor({ apiKey }: { apiKey: string }) {
    this.apiKey = apiKey;
    this.adminAccount = 'ADMIN_WALLET_ADDRESS';
  }

  async sendTransaction(transaction: { from: string; to: string; data: string }): Promise<void> {
    // Implement sending a transaction to the blockchain
    console.log(`Sending transaction from ${transaction.from} to ${transaction.to}`);
    // Connect to network and perform transaction logic here
  }
}

export { FractalNetwork };
```

### `backend/src/token.ts`

Defines the token model and utility functions.

```typescript
class Token {
  id: string;
  amount: number;

  constructor(id: string, amount: number) {
    this.id = id;
    this.amount = amount;
  }

  encodeListingData(): string {
    // Encode the data necessary for listing a token
    return `list:${this.id}:${this.amount}`;
  }

  static encodePurchaseData(tokenId: string, amount: number): string {
    // Encode the data necessary for purchasing a token
    return `buy:${tokenId}:${amount}`;
  }
}

export { Token };
```

## Contact Info:

If you have technical issues and development inquiries, please contact here.
- Twitter: https://x.com/rez_cats/
- Telegram: https://t.me/rizz_cat/
