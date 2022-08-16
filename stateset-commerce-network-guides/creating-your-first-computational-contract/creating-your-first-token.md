---
description: Create a token using CosmWasm from the Stateset Zone
---

# Creating your first token

Here is a quick introduction into creating an interacting with an erc20 like token on Stateset.



**1) Upload the CosmWasm Contract**

`statesetd tx wasm store cw_erc20.wasm --from dom --chain-id=stateset-1-testnet --gas-prices 0.1ustate --gas auto --gas-adjustment 1.3 -b block -y`



**1.5) Optimize the Contract**

```
sudo docker run --rm -v "$(pwd)":/code \
    --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
    --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
    cosmwasm/rust-optimizer:0.12.6
```



**2) Instantiate the Token**

`statesetd tx wasm inst 1 '{"name":"Dom Coin","symbol":"DOM","decimals":6,"initial_balances":[{"address":"stateset1mz337yp22zxje75f5gw2mfupems5cx3p2p2pax","amount":"2800000000"}]}' --label "dom coin" --from dom --chain-id stateset-1-testnet --gas auto --gas-adjustment 1.3 -b block -y`



**3) Query Balances**

`statesetd query wasm contract-state smart stateset1yyca08xqdgvjz0psg56z67ejh9xms6l436u8y58m82npdqqhmmtqr9zaus '{"balance":{"address":"stateset1mz337yp22zxje75f5gw2mfupems5cx3p2p2pax"}}' --chain-id stateset-1-testnet`



**4) Transfer Tokens**

`statesetd tx wasm execute stateset1yyca08xqdgvjz0psg56z67ejh9xms6l436u8y58m82npdqqhmmtqr9zaus '{"transfer":{"amount":"2000","owner":"stateset1mz337yp22zxje75f5gw2mfupems5cx3p2p2pax","recipient":"stateset1j57jhj3t6322sm8lwsnxcme8af8yrghp8jf9k7"}}' --from dom --chain-id stateset-1-testnet --gas auto --gas-adjustment 1.3 -b block -y`
