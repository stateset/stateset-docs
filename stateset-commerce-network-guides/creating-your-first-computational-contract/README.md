# Creating your first Computational Contract

Smart contracts can be programmed on the Stateset Commerce Network using CosmWasm.

Cosmwasm is a smart contract framework that leverages Rust.

To create the smart contract:

* Generate the initial project
* Compile the smart contract
* Run unit tests
* Optimize the wasm contract bytecode to prepare for deployment
* Deploy the smart contract to local Stateset Network
* Instantiate it with contract parameters

{% hint style="info" %}
**Good to know:** In the future other languages will be able to be used for writing smart contracts including JavaScript, GO, Kotlin and many more.
{% endhint %}

## The cw20 basic token

Once you have the Stateset Network running on your local machine it should be very easy to create your own token.

Here is a quick introduction into creating an interacting with an erc20 like token on Stateset.

### Download

We're going to grab the `stateset-contracts` repo and compile our chosen contract.

```bash
# get the code
git clone https://github.com/stateset/stateset-contracts
cd stateset-contracts
cd contracts/cw20
```

### Compile

We can compile our contract like so:

```
# compile the wasm contract with stable toolchain
rustup default stable
cargo wasm
```

However, we want to create an optimized version to limit gas usage, so we're going to run:

```bash
sudo docker run --rm -v "$(pwd)":/code \
    --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
    --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
    cosmwasm/rust-optimizer:0.12.6
```

This will result in an artifact called `cw_erc20.wasm` being created in the `artifacts` directory.

### **Upload**

`statesetd tx wasm store cw_erc20.wasm --from dom --chain-id=stateset --gas-prices 0.1ustate --gas auto --gas-adjustment 1.3 -b block -y`



#### _Optimize the Contract_

```
sudo docker run --rm -v "$(pwd)":/code \
    --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target \
    --mount type=volume,source=registry_cache,target=/usr/local/cargo/registry \
    cosmwasm/rust-optimizer:0.12.6
```

### **Instantiate**

`statesetd tx wasm inst 1 '{"name":"Dom Coin","symbol":"DOM","decimals":6,"initial_balances":[{"address":"stateset1mz337yp22zxje75f5gw2mfupems5cx3p2p2pax","amount":"2800000000"}]}' --label "dom coin" --from dom --chain-id stateset --gas auto --gas-adjustment 1.3 -b block -y`

### **Query - Query Balances**

`statesetd query wasm contract-state smart stateset1yyca08xqdgvjz0psg56z67ejh9xms6l436u8y58m82npdqqhmmtqr9zaus '{"balance":{"address":"stateset1mz337yp22zxje75f5gw2mfupems5cx3p2p2pax"}}' --chain-id stateset`

### **Execute - Transfer Tokens**

`statesetd tx wasm execute stateset1yyca08xqdgvjz0psg56z67ejh9xms6l436u8y58m82npdqqhmmtqr9zaus '{"transfer":{"amount":"2000","owner":"stateset1mz337yp22zxje75f5gw2mfupems5cx3p2p2pax","recipient":"stateset1j57jhj3t6322sm8lwsnxcme8af8yrghp8jf9k7"}}' --from dom --chain-id stateset --gas auto --gas-adjustment 1.3 -b block -y`

