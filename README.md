# Wonderland-MCP

# Wonderland MCP by Cheshire Terminal

## The First AI-Native Web3 Integration Platform for Solana

![Wonderland MCP](https://i.imgur.com/placeholder.png)

## Table of Contents

- [Introduction](#introduction)
- [System Architecture](#system-architecture)
- [Components](#components)
  - [Solana Trading Server](#solana-trading-server)
  - [Solana Explorer Server](#solana-explorer-server)
  - [CheshMCP Notes Server](#cheshmcp-notes-server)
- [Integration with AI Models](#integration-with-ai-models)
- [Deployment Guide](#deployment-guide)
- [Use Cases](#use-cases)
- [Future Roadmap](#future-roadmap)

## Introduction

Wonderland MCP (Model Context Protocol) by Cheshire Terminal represents a revolutionary approach to Web3 integration with AI systems. It's the first comprehensive platform that enables AI models like Claude to directly interact with the Solana blockchain without requiring complex middleware or extensive user intervention. 

By leveraging the Model Context Protocol, Wonderland creates a seamless bridge between AI language models and blockchain functionality, opening up new possibilities for automated trading, portfolio management, risk analysis, and decentralized application interaction.

## System Architecture

Wonderland MCP is built on a modular architecture with specialized servers that handle different aspects of Solana blockchain interaction:

```
┌─────────────────────┐     ┌─────────────────────┐
│                     │     │                     │
│   AI Language Model │◄────►  Wonderland MCP    │
│   (Claude, etc.)    │     │   Integration      │
│                     │     │                     │
└─────────────────────┘     └─────────┬───────────┘
                                      │
                                      ▼
┌─────────────────────┐     ┌─────────────────────┐
│                     │     │                     │
│  Solana Explorer    │◄────►  Solana Trading    │
│  Server             │     │  Server            │
│                     │     │                     │
└─────────────────────┘     └─────────────────────┘
          │                           │
          │                           │
          ▼                           ▼
┌─────────────────────┐     ┌─────────────────────┐
│                     │     │                     │
│  Solana Blockchain  │     │  Jupiter DEX       │
│  RPC Providers      │     │  Aggregator        │
│                     │     │                     │
└─────────────────────┘     └─────────────────────┘
```

Each server is containerized using Docker for easy deployment and scalability. The MCP protocol enables standardized communication between AI models and these specialized servers.

## Components

### Solana Trading Server

The Solana Trading Server is a specialized MCP server that enables AI models to perform trading operations on the Solana blockchain.

**Key Features:**

- **Wallet Management**: Create new wallets or import existing ones using private keys
- **Token Balance Checking**: Query token balances for any wallet address
- **Swap Quotes**: Get quotes for token swaps using Jupiter DEX aggregator
- **Trade Execution**: Execute token swaps with customizable slippage tolerance
- **Secure Key Management**: Private keys can be securely stored and used for transactions

**Tools Available:**

- `create_wallet`: Generate a new Solana wallet
- `import_wallet`: Import an existing wallet using a private key
- `get_token_balance`: Check token balance for a specific wallet and token mint
- `get_swap_quote`: Get a quote for swapping tokens
- `execute_swap`: Execute a token swap based on a quote

**Technical Implementation:**

The Trading Server is built using TypeScript and leverages the following technologies:
- `@solana/web3.js` for Solana blockchain interaction
- `@solana/spl-token` for SPL token operations
- Jupiter API for swap quotes and execution
- Model Context Protocol for AI integration

### Solana Explorer Server

The Solana Explorer Server provides comprehensive blockchain exploration and analysis capabilities to AI models.

**Key Features:**

- **Token Analysis**: Analyze tokens for risk factors and metadata
- **Wallet Exploration**: View token holdings and balances for any wallet
- **Transaction Inspection**: Get detailed information about transactions
- **Risk Assessment**: Evaluate tokens based on supply, holders, and metadata

**Tools Available:**

- `search_token`: Search for a token by address and analyze its risk profile
- `search_wallet`: Search for a wallet address and get its token holdings
- `search_transaction`: Search for a transaction and get its details

**Technical Implementation:**

The Explorer Server uses:
- `@solana/web3.js` for blockchain data retrieval
- Jupiter API for token metadata
- Helius RPC for enhanced Solana data access
- Custom risk analysis algorithms

### CheshMCP Notes Server

The CheshMCP Notes Server provides a persistent storage and organization system for AI-generated insights and analysis.

**Key Features:**

- **Structured Note Storage**: Create and organize notes with tags and categories
- **Search Capabilities**: Search notes by content, tags, or categories
- **Export Functionality**: Export notes to markdown or JSON formats
- **Analysis Tools**: Analyze notes for trends and insights

**Tools Available:**

- `create_note`: Create a new note with tags and category
- `search_notes`: Search notes by text, tags, or category
- `export_notes`: Export notes to markdown files
- `analyze_notes`: Analyze notes to get insights and statistics

## Integration with AI Models

Wonderland MCP's revolutionary approach lies in its seamless integration with AI language models. Using the Model Context Protocol, AI models can directly call functions on the Solana blockchain without requiring custom API development or complex middleware.

**Example Integration with Claude:**

```javascript
// Analyze a token's risk profile
const tokenAnalysis = await use_mcp_tool({
  server_name: "solana-explorer-server",
  tool_name: "search_token",
  arguments: {
    address: "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v" // USDC
  }
});

// If risk is acceptable, execute a swap
if (tokenAnalysis.riskScore < 7) {
  // Get a swap quote
  const quoteResponse = await use_mcp_tool({
    server_name: "solana-trading",
    tool_name: "get_swap_quote",
    arguments: {
      inputMint: "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v", // USDC
      outputMint: "So11111111111111111111111111111111111111112", // SOL
      amount: "1000000", // 1 USDC
      slippage: 1 // 1% slippage
    }
  });
  
  // Execute the swap
  const swapResult = await use_mcp_tool({
    server_name: "solana-trading",
    tool_name: "execute_swap",
    arguments: {
      quote: quoteResponse,
      walletPrivateKey: "YOUR_PRIVATE_KEY"
    }
  });
  
  // Save the transaction details as a note
  await use_mcp_tool({
    server_name: "cheshmcp",
    tool_name: "create_note",
    arguments: {
      title: "USDC to SOL Swap",
      content: `Swapped 1 USDC to SOL\nTransaction ID: ${swapResult.txid}\nStatus: ${swapResult.status}`,
      tags: ["swap", "usdc", "sol"]
    }
  });
}
```

## Why Wonderland MCP is Revolutionary

Wonderland MCP represents a paradigm shift in how AI systems interact with blockchain technology for several key reasons:

1. **Direct AI-to-Blockchain Communication**: Eliminates the need for complex middleware or custom API development.

2. **Composable Architecture**: Modular servers can be combined to create complex workflows that were previously impossible.

3. **AI-Native Design**: Built specifically for AI language models to leverage their reasoning capabilities for blockchain operations.

4. **Risk Analysis Integration**: Combines financial analysis with execution capabilities in a single unified system.

5. **Memory and Context Awareness**: The notes system allows for persistent memory across sessions, enabling long-term strategy development.

6. **Democratized Access**: Makes sophisticated trading strategies and blockchain analysis accessible to non-technical users through natural language.

7. **First of its Kind**: The first comprehensive solution that bridges AI language models with Solana's high-performance blockchain.

## Deployment Guide

### Deploying to Smithery AI

Smithery AI provides a serverless platform for hosting MCP servers. To deploy Wonderland MCP to Smithery:

1. Package each server as a separate function:

```bash
# For each server directory
zip -r server.zip . -x "node_modules/*" ".git/*"
```

2. Upload to Smithery using their CLI tool:

```bash
smithery deploy --function solana-trading-server --file ./solana-trading-server.zip --env HELIUS_API_KEY=your_api_key
```

3. Configure the function to use the MCP protocol handler.

4. Set up environment variables for API keys and RPC endpoints.

### Deploying to Glama AI

Glama AI offers specialized hosting for AI-integrated applications:

1. Create a Glama account and set up a new project.

2. Connect your GitHub repository to Glama for CI/CD.

3. Configure the deployment settings:
   - Set container specifications
   - Configure environment variables
   - Set up networking rules

4. Deploy using the Glama dashboard or CLI.

### Deploying to Composio

Composio specializes in hosting composable AI services:

1. Package each server as a Docker container:

```bash
# Build Docker images
docker build -t solana-trading-server ./solana-trading-server
docker build -t solana-explorer-server ./solana-explorer-server
docker build -t cheshmcp ./cheshmcp
```

2. Push to Composio's container registry:

```bash
composio login
composio push solana-trading-server
composio push solana-explorer-server
composio push cheshmcp
```

3. Create a composition file that defines how the servers interact.

4. Deploy the composition:

```bash
composio deploy -f wonderland-composition.yaml
```

## Use Cases

Wonderland MCP enables a wide range of use cases that were previously difficult or impossible:

1. **AI-Powered Trading Assistant**: Help users analyze tokens, assess risks, and execute trades through natural language conversations.

2. **Portfolio Management**: Automatically monitor and rebalance portfolios based on market conditions and risk parameters.

3. **Risk Analysis Service**: Provide detailed risk assessments of tokens and projects on Solana.

4. **Educational Tool**: Help newcomers understand blockchain concepts through interactive exploration.

5. **DeFi Strategy Automation**: Create and execute complex DeFi strategies through simple conversations.

6. **Blockchain Data Analysis**: Extract insights from on-chain data for research or investment purposes.

7. **Transaction Monitoring**: Monitor specific wallets or tokens for suspicious activity.

## Future Roadmap

The Wonderland MCP ecosystem will continue to evolve with these planned enhancements:

1. **Additional Blockchain Support**: Expand beyond Solana to other major blockchains.

2. **Enhanced Risk Models**: Incorporate more sophisticated risk assessment algorithms.

3. **Strategy Templates**: Pre-built trading and investment strategies that can be customized.

4. **Multi-Model Support**: Extend beyond Claude to support other AI models.

5. **Governance Integration**: Tools for interacting with DAOs and governance systems.

6. **NFT Support**: Comprehensive tools for NFT creation, trading, and analysis.

7. **Advanced Analytics**: More sophisticated on-chain data analysis capabilities.

---

## Conclusion

Wonderland MCP by Cheshire Terminal represents a fundamental shift in how AI systems interact with blockchain technology. By creating a direct bridge between AI language models and the Solana blockchain, it opens up new possibilities for automation, analysis, and accessibility in the Web3 space.

Whether you're a developer looking to build AI-powered DeFi applications, a trader seeking to automate strategies, or a researcher analyzing on-chain data, Wonderland MCP provides the tools and infrastructure to make your vision a reality.

---

© 2025 Cheshire Terminal. All rights reserved.
