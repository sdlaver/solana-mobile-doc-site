import BlogImageRow from "../../src/components/BlogImageRow/"
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Targeting Seeker Users

## Introduction

This article provides information about the Solana Mobile Chapter 2 Preorder Tokens NFTs. The non-transferrable Chapter 2 Preorder Tokens allow for the identification of wallets that have participated in preordering Seeker, known as Chapter 2 when preorders first launched.

Everyone who preorders the Seeker receives this Chapter 2 Preorder Token NFT, which is a way for ecosystem teams to target those who preordered the Seeker through rewards programs, incentives, and other benefits.

Solana Mobile does not currently have a rewards program in connection with the Chapter 2 Preorder Token. Ecosystem teams are entirely free to decide if (and if so, how) they wish to interact with the holders of these non-transferable tokens.

## Chapter 2 Preorder Token holders

The Chapter 2 Preorder Token NFT is a non-transferable NFT distributed to the wallets of anyone who has preordered Seeker.

As of the time this article was written, there are 140,000+ holders of the Preorder Token. The preorder phase is still active and any new Tokens will be issued in waves.

## Targeting Chapter 2 Preorder Token Holders

<Tabs>
<TabItem value="Targeting Seeker with Airship" label="Targeting Seeker with Airship">

### Airship

[Airship](https://airship.helius.dev/) is a tool developed by [Helius](https://www.helius.dev/) that enables cost-effective and simplified SPL token airdrops. For more information on how it works, check out the official [Airship docs](https://github.com/helius-labs/airship).

You can use the tool to:

- Generate a list of Chapter 2 Preorder Token holders.
- Distribute a specified amount of compressed SPL tokens to a list of wallets.
- Claim any distributed compressed tokens that belong to your wallet.

#### Usage

1. Select "Create new airdrop" to enter the tool.
2. Provide an RPC URL and the private key of the wallet containing the tokens for distribution.
3. Select "Import Chapter 2 Preorder Token Holders" then press the "Import" button.
4. The list of wallet addresses of Chapter 2 Preorder Token Holders will be generated.
5. Select the SPL token you want to distribute and specify either a fixed amount of tokens or a percent of available tokens.
6. Review the airdrop details and press "Send" to initiate the airdrop.

#### Claiming compressed tokens

After an airdrop is intiated, recipients will need to decompress their distributed tokens using the [Airship decompress tool](https://airship.helius.dev/decompress).

- Recipients can connect their wallets and view a list of the available compressed tokens they can claim.
- After signing a transaction to claim, the tokens will appear as normal in the users wallet.

</TabItem>
<TabItem value="Querying manually" label="Querying manually">

:::tip
This script can return duplicates of the same owner's wallet address.
This is because it is possible for a single wallet address to own more than one Preorder Token, if they preordered multiple Chapter 2 products.
:::

You can follow these steps to manually query the Chapter 2 Preorder Token list and save it into a JSON file:

#### 1. Access your RPC provider.

Any RPC provider with the [DAS (Digital Asset Standard)](https://github.com/metaplex-foundation/digital-asset-standard-api) APIs should work. If you don't have one, the Helius Free plan (helius.dev/pricing) should be sufficient for this query.

#### 2. Add your API Key to the following query:

```js
import { writeFileSync } from "fs";

const DAS_API_URL = "https://mainnet.helius-rpc.com/?api-key=<API_KEY>";
const TOKEN_MINT_ADDRESS = "2DMMamkkxQ6zDMBtkFp8KH7FoWzBMBA1CGTYwom4QH6Z";
const OUTPUT_FILE = `out.json`;

let tokens = [];

let page = 0;
while (true) {
  page++;
  console.log(`Fetching page ${page}`);
  const response = await fetch(DAS_API_URL, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      jsonrpc: "2.0",
      id: "my-id",
      method: "getTokenAccounts",
      params: {
        mint: `${TOKEN_MINT_ADDRESS}`,
        page: page, // Starts at 1
        limit: 1000,
      },
    }),
  });
  const { result } = await response.json();
  if (result.total === 0) {
    console.log("Done!");
    break;
  }
  for (const item of result.token_accounts) {
    tokens.push({ owner: item.owner, count: item.amount });
  }
}

console.log(`Writing to ${OUTPUT_FILE}`);
writeFileSync(OUTPUT_FILE, JSON.stringify(tokens, null, 2));
```

#### 3. Perform the Query

Run the script to perform the query and you can find the results in the output file `out.json`.

#### 4. Further querying (optional)

In order to query a subset of the Preorder Token Holders, you may write a script to fetch wallet activity data using blockchain explorers and analytics tools based on the subset criteria. You can use their APIs to retrieve transaction history, token balances, and other relevant information, such as:

- Length of their engagement with the applicable protocol (i.e. The date of the first transaction)
- Participation in applications within the ecosystem that are adjacent or complementary to your project

</TabItem>
</Tabs>

## NFT Details

The Chapter 2 Preorder Tokens are non-transferable NFTs enabled by the _[NonTransferable](https://solana.com/developers/guides/token-extensions/non-transferable)_ extension.

### Mint Address

The Chapter 2 Preorder Token mint address is:

- `2DMMamkkxQ6zDMBtkFp8KH7FoWzBMBA1CGTYwom4QH6Z`

This mint address is shared by all token accounts of the Chapter 2 Preorder Token.

### Metadata

Each Chapter 2 Preorder Token NFT utilizes the [Metadata and Metadata Pointer](https://solana.com/developers/guides/token-extensions/metadata-pointer) extension to define
its NFT metadata.

```
Metadata
    Uri: https://arweave.net/WHyy5Fo8vUC7FqFfzqkuYAmDi-BfOMBjZSXIwwO7P6g
    Mint: 2DMMamkkxQ6zDMBtkFp8KH7FoWzBMBA1CGTYwom4QH6Z
    Name: Chapter 2 Preorder Token
    Symbol: CHAPTER2
    Update Authority: GRR6BquJZYWgUqWpNJekBZHDHgxVQ56iZ2P2nWjDFRSn
    Additional Metadata
Metadata Pointer
    Authority: GRR6BquJZYWgUqWpNJekBZHDHgxVQ56iZ2P2nWjDFRSn
    Metadata Address: 2DMMamkkxQ6zDMBtkFp8KH7FoWzBMBA1CGTYwom4QH6Z
```
