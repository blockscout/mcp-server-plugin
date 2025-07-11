# MCP Server Plugin for Blockscout

## Introduction to MCP and Higress

The Model Context Protocol (MCP) is an open protocol designed to allow AI agents, IDEs, and automation tools to consume, query, and analyze structured data through context-aware APIs. In Higress, the MCP server provides a flexible and extensible gateway for exposing custom data models and operations to these tools via plugins.

**Higress** is a powerful, open-source cloud-native gateway supporting advanced API management, traffic control, and seamless plugin extensibility.  
Learn more: [Higress MCP Server Documentation](https://higress.cn/en/ai/mcp-server/)

## About MCP for Blockscout

This plugin wraps Blockscout APIs and exposes blockchain data—balances, tokens, NFTs, contract metadata—via MCP so that AI agents and tools (like Claude, Cursor, or IDEs) can access and analyze it contextually.

**Key Features:**

- Contextual blockchain data access for AI tools
- Multi-chain and single-chain support via configuration
- Extensible tool configurations with customizable descriptions and response templates

## Repository Structure

- `api-to-mcp-mainnet.yml`  
  Configuration file for MCP server in **single-chain mode**. Use this to connect to a specific Blockscout instance and expose its data through MCP.

- `api-to-mcp.yml`  
  Configuration file for MCP server in **multi-chain mode**. Use this to enable access to multiple Blockscout instances and aggregate data in one server.

- `local-mcp.md`  
  Step-by-step instructions to install Higress locally and test your MCP server/plugin with example configuration files.

## Publishing Your MCP Server

To publish your MCP server/plugin to the official Higress MCP Hub (`mcp.higress.ai`), follow the detailed instructions in this issue:  
[How to Publish MCP Server to mcp.higress.ai](https://github.com/alibaba/higress/issues/2113)

## Tool Descriptions

The multi-chain mode is implemented by using the REST API of the official Blockscout MCP server: [`https://mcp.blockscout.com/`](https://mcp.blockscout.com/). The repo with the server is available at [`https://github.com/blockscout/mcp-server/`](https://github.com/blockscout/mcp-server/).

The following tools are available in the multi-chain configuration (`api-to-mcp.yml`).

1. `__get_instructions__()` - Must be called before any other tool. Initializes the MCP server session.
2. `get_chains_list()` - Gets the list of supported blockchain chains and their IDs.
3. `get_address_by_ens_name(name)` - Converts an ENS domain name to its corresponding Ethereum address.
4. `lookup_token_by_symbol(chain_id, symbol)` - Searches for token addresses by symbol or name.
5. `get_contract_abi(chain_id, address)` - Retrieves the ABI (Application Binary Interface) for a smart contract.
6. `get_address_info(chain_id, address)` - Gets comprehensive information about an address (balance, contract status, etc.).
7. `get_tokens_by_address(chain_id, address)` - Returns detailed ERC20 token holdings for an address.
8. `get_latest_block(chain_id)` - Returns the latest indexed block number and timestamp.
9. `get_transactions_by_address(chain_id, address, age_from, age_to, methods)` - Gets native currency transfers and smart contract interactions for an address.
10. `get_token_transfers_by_address(chain_id, address, age_from, age_to, token)` - Returns ERC-20 token transfers for an address.
11. `transaction_summary(chain_id, transaction_hash)` - Provides a human-readable summary of a transaction.
12. `nft_tokens_by_address(chain_id, address)` - Retrieves NFT tokens owned by an address.
13. `get_block_info(chain_id, number_or_hash)` - Returns block information (timestamp, gas used, etc.).
14. `get_transaction_info(chain_id, transaction_hash)` - Gets comprehensive transaction information.
15. `get_transaction_logs(chain_id, transaction_hash)` - Returns transaction logs with decoded event data.
16. `get_address_logs(chain_id, address)` - Gets logs emitted by a specific address with decoded event data.

### Single-Chain Mode

The following tools are available in the single-chain configuration (`api-to-mcp-mainnet.yml`).

1. `__get_instructions__()` - Must be called before any other tool. Initializes the MCP server session.
2. `get_address_by_ens_name(name)` - Converts an ENS domain name to its corresponding Ethereum address.
3. `lookup_token_by_symbol(symbol)` - Searches for token addresses by symbol or name, returning multiple potential matches.
4. `get_contract_abi(address)` - Retrieves the ABI (Application Binary Interface) for a smart contract.
5. `get_address_info(address)` - Gets comprehensive information about an address including balance, ENS association, contract status, and token details.
6. `get_tokens_by_address(address)` - Returns detailed ERC20 token holdings for an address with enriched metadata and market data.
7. `get_latest_block()` - Returns the latest indexed block number and timestamp.
8. `get_transactions_by_address(address, age_from, age_to, methods)` - Gets transactions for an address within a specific time range with optional method filtering.
9. `get_token_transfers_by_address(address, age_from, age_to, token)` - Returns ERC-20 token transfers for an address within a specific time range.
10. `transaction_summary(hash)` - Provides human-readable transaction summaries using Blockscout Transaction Interpreter.
11. `nft_tokens_by_address(address)` - Retrieves NFT tokens owned by an address, grouped by collection.
12. `get_block_info(number_or_hash)` - Returns block information including timestamp, gas used, burnt fees, and transaction count.
13. `get_transaction_info(hash)` - Gets comprehensive transaction information with decoded input parameters and detailed token transfers.
14. `get_transaction_logs(hash)` - Returns transaction logs with decoded event data.
15. `get_address_logs(address)` - Gets logs emitted by a specific address with decoded event data.

## Example Prompts for AI Agents

```plaintext
On which popular networks is `ens.eth` deployed as a contract?
```

```plaintext
What are the usual activities performed by `ens.eth` on the Ethereum Mainnet? Since it is a contract, what is the most used functionality of this contract? Which address interacts with the contract the most?
```

```plaintext
Calculate the total gas fees paid on Ethereum by address `0xcafe...cafe` in May 2025.
```

```plaintext
Which 10 most recent logs were emitted by `0xFe89cc7aBB2C4183683ab71653C4cdc9B02D44b7` before `Nov 08 2024 04:21:35 AM (-06:00\u00a0UTC)`?
```
