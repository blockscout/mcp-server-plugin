# NFT tokens list format

The NFT tokens list contains the list of collections of nonfunginle tokens.

Each element of the list contains the following fields:

- `token` - the object describing the NFT collection contract
- `amount` - the amount of NFTs owned by the same address
- `token_instances` - the list of NFT instances owned by the same address in the collection

The following fields of the `token` object are relevant for us:

- `type` - the type of the NFT collection (ERC-721, ERC-404, ERC-1155)
- `address_hash` - the hash of the token address
- `name` - the name of the NFT collection
- `symbol` - the symbol of the NFT collection
- `holders_count` - the number of unique holders of the NFT collection
- `total_supply` - the total supply of the NFT collection

The following fields of each element of the `token_instances` list are relevant for us:

- `id` - the ID of the NFT instance
- `metadata.description` (if present) - the description of the NFT instance
- `metadata.name` (if present) - the name of the NFT instance
- `metadata.external_url` (if present) - the URL to a marketplace page or application page relevant to the NFT instance

Although it could be useful to include `metadata` as is it can include very large fields like `image` that could overload the LLM context window.
