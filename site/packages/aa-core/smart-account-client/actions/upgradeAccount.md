---
outline: deep
head:
  - - meta
    - property: og:title
      content: upgradeAccount
  - - meta
    - name: description
      content: Overview of the upgradeAccount method on SmartAccountClient
  - - meta
    - property: og:description
      content: Overview of the upgradeAccount method on SmartAccountClient
---

# upgradeAccount

Upgrades smart accounts to a new implementation if the smart contract account supports upgradeability using [UUPSUpgradeable](https://docs.openzeppelin.com/contracts/4.x/api/proxy#UUPSUpgradeable) Pattern.

## Usage

::: code-group

```ts [example.ts]
import { smartAccountClient as lightAccountClient } from "./lightAccountClient";
import { getMSCAUpgradeToData } from "@alchemy/aa-accounts";

const { createMAAccount, ...upgradeToData } = await getMSCAUpgradeToData(
  lightAccountClient,
  { account: lightAccountClient.account }
);

// [!code focus:99]
const hash = await lightAccountClient.upgradeAccount({
  upgradeTo: upgradeToData,
  waitForTx: true,
});

const upgradedAccount = await createMAAccount();
```

<<< @/snippets/aa-alchemy/light-account-client.ts [lightAccountClient.ts]

:::

## Returns

### `Promise<Hash>`

A Promise that resolves to the user operation hash (transaction hash if `waitForTx` is true) sent to the network

## Parameters

### `client: SmartContractClient`

The [`SmartContractClient`](/packages/aa-core/smart-account-client/) instance

### `args: UpgradeAccountParams`

- `upgradeTo: UpgradeToData`

  - `implAddress: Address`

  Address of new implementation contract address to upgrade to

  - `initializationData: Hex`

  Encoded contract initiation data for the new implementation contract

- `overrides?: `[UserOperationOverrides](/packages/aa-core/smart-account-client/types/userOperationOverrides.md)

  Optional overrides for the user operation

- `waitForTx?: boolean`

  If true, the method would wait for the user operation transaction to be mined
