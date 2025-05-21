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

## Tool Descriptions (to be added)

> _Placeholder_: Tool descriptions provided by the server will be published here after plugin configuration is finalized.

## Example Prompts for AI Agents (to be added)

> _Placeholder_: Practical examples of prompts for chats or IDEs to retrieve and analyze blockchain data via the MCP server will be added in this section.
