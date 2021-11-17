# ⭐️ Dalgona Swap in Testnet

This project was made by forking [Pancake Swap](https://github.com/pancakeswap/pancake-swap-interface-v1).

## Setup & Run
### 1. Compile
```Bash
# node -v: 10.24.1
# yarn -v: 1.22.17
>> yarn install
```

### 2. Deploy contracts
```Bash
>> cd contracts/
>> ls
PancakeFactory.sol  PancakeRouter.sol  PancakeRouter01.sol  WBNB.sol  tokens
```
> You can deploy on [remix](https://remix.ethereum.org). Compile according to the compiler version. The deploy's environment is `Injected Web3` (Your Metamask wallet must be connected to the `Binance Smart Chain Testnet`).
1. Deploy `WBNB.sol`
2. Deploy `PancakeFactory.sol`
    * `feeToSetter`: Your Address
3. Deploy `PancakeRouter01.sol`
    * `INIT_CODE_PAIR_HASH` in `pairFor` function: Hash from `PancakeFactory`
    * Parameters: `PancakeFactory` address, `WBNB` address
4. Deploy `PancakeRouter.sol`
    * `INIT_CODE_PAIR_HASH` in `pairFor` function: Hash from `PancakeFactory`
    * When compiling it: `Enable optimization: 200`
    * Parameters: `PancakeFactory` address, `WBNB` address

### 3. Setup Front-end
* `src/constants/index.ts`: Update `PancakeRouter` address
* `node_modules/@pancakeswap-libs/sdk/dist/constants.d.ts`: Update `PancakeFactory` address and `INIT_CODE_PAIR_HASH`
* `node_modules/@pancakeswap-libs/sdk/dist/sdk.cjs.development.js`: Update `PancakeFactory` address, `INIT_CODE_PAIR_HASH`, and `WBNB` address
* `node_modules/@pancakeswap-libs/sdk/dist/sdk.cjs.production.min.js`: Update `PancakeFactory` address, `INIT_CODE_PAIR_HASH`, and `WBNB` address
* `node_modules/@pancakeswap-libs/sdk/dist/sdk.esm.js`: Update `PancakeFactory` address, `INIT_CODE_PAIR_HASH`, and `WBNB` address
* `src/state/swap/hooks.ts`
    * `v2 factory`: `PancakeFactory` address
    * `v2 router 01`: `PancakeRouter01` address
    * `v2 router 02`: `PancakeRouter` address

### 4. Deploy Tokens
```Bash
>> cd contracts/tokens/
>> ls
BUSDToken.sol  DAIToken.sol  DalgonaToken.sol  EthereumToken.sol  USDTToken.sol
```
> After issuing the token, add the token to the file below.
* `src/constants/token/pancakeswap.json`: Token list
* `src/constants/index.ts`: Token to be posted on the web

### 5. Run
```Bash
>> yarn start
```

<br>

## Binance Smart Chain Testnet Address
### Contract
* WBNB: 0xf6219e90c22cd1517535FC4F2f7E71B043792B51
* PancakeFactory: 0xE68fDB2041CA05504E460e7297BaFdF759911eFe
* PancakeRouter01: 0xC4d2F12422d81883DF1963c48D86ae168802Ac0b
* PancakeRouter: 0x4Ba5E9311dC389d8daFa0586792c6d7017B71971
* INIT_CODE_HASH: 0xbb600ba95884f2c2837114fd2f157d00137e0b65b0fe5226523d720e4a4ce539
### Token
* Ethereum token contract: 0x11f0160E24d4523b5124149d0833dBdb5deC3A9d
* USDT token contract: 0xf5FE2Ef051222C8D83b218faC4d041d90cb6B377
* BUSD token contract: 0xfC75E4C492E73922C8f9D2e07013945C248033D8
* DAI token contract: 0xdd5c7bFD6D7f681b1C29Bd41854cD4Ad5BB9A663
* Dagona token contract: 0xCF894cf0bBC64Ae84208D826dF99C247D15B7018
