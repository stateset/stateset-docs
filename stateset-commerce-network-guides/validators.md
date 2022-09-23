---
description: Joining the Stateset Validator Set
---

# Validators

**Stateset Network is currently partnering with validators for our stateset-1-testnet. If you are interested in joining the validator set please get in touch.**

**Download the Stateset Binary from:**

****[**https://github.com/stateset/core/releases**](https://github.com/stateset/core/releases)****

### **Setting Up a Genesis Stateset Validator**

&#x20;Thank you for becoming a genesis validator on Stateset!

This guide will provide instructions on setting up a node, submitting a gentx, and other tasks needed to participate in the launch of the Stateset testnet.

The primary point of communication for the genesis process and future updates will be the #validators channel on the Stateset Discord.

This channel is private by default in order to keep it free of spam and unnecessary noise. To join the channel, please send a message to @domsteil to add yourself and any team members.

Some important notes on joining as a genesis validator:&#x20;

_Gentxs must be submitted by End of Day UTC on November 25th, 2022._&#x20;

We highly recommend only experienced validators who have run on past Cosmos SDK chains and have participated in a genesis ceremony before become genesis validators on Stateset. All Stateset validators should be expected to be ready to participate active operators of the network.

### Hardware

We recommend selecting an all-purpose server with:

4 or more physical\[1] CPU cores&#x20;

At least 500GB of SSD disk storage&#x20;

At least 16GB of memory&#x20;

At least 100mbps network bandwidth

As the usage of the blockchain grows, the server requirements may increase as well, so you should have a plan for updating your server as well.

\[1]: You'll often see 4 distinct physical cores as a machine with 8 logical cores due to hyperthreading. The distinct logical cores are helpful for things that are I/O bound, but threshold decryption will have validators running significant, non-I/O bound, computation, hence the need for physical cores.

We are not launching with this parallelism, but we include the requirement as we expect parallelism in some form to be needed by validators in a not-so-distant future.

### Instructions&#x20;

These instructions are written targeting an Ubuntu 20.04 system.

Relevant changes to commands should be made depending on the OS/architecture you are running on.

Install Go Stateset is built using Go and requires Go version 1.17+.

In this example, we will be installing Go on the above Ubuntu 20.04

**Download the Stateset Binary from:**

****[**https://github.com/stateset/core/releases**](https://github.com/stateset/core/releases)****

You can now build Stateset node software.

Running the following command will install the executable statesetd (Stateset node daemon) to your GOPATH.

`statesetd version --long`&#x20;

name: stateset server\_name: statesetd version: '"0.0.8"' commit: 19 build\_tags: netgo,ledger go: go version go1.17.0 darwin/amd64

If the software version does not match, then please check your $PATH to ensure the correct statesetd is running.

Save your Chain ID in statesetd config

We recommend saving the testnet chain-id into your statesetd's client.toml. This will make it so you do not have to manually pass in the chain-id flag for every CLI command.

`statesetd config chain-id stateset-1-testnet`

Initialize your Node

Now that your software is installed, you can initialize the directory for statesetd.

`statesetd init --chain-id=stateset-1-testnet <your_moniker>`

This will create a new .statesetd folder in your HOME directory.

Download Pregenesis File You can now download the "pregenesis" file for the chain. This is a genesis file with the chain-id and airdrop balances.

`cd $HOME/.statesetd/config/`&#x20;

`curl https://raw.githubusercontent.com/stateset/networks/main/stateset-1-testnet/pregenesis.json > $HOME/.statesetd/config/genesis.json`

**Import Validator Key**

The create a gentx, you will need the private key to an address that received an allocation in the airdrop. There are a couple options for how to import a key into statesetd. You can import such a key into statesetd via a mnemonic or exporting and importing a keyfile from an existing CLI.

Import Via Mnemonic

To import via mnemonic, you can do so using the following command and then input your mnemonic when prompted.

`statesetd keys add <key_name> --recover`

Import From Another CLI If you have the private key saved in the keystore of another CLI (such as gaiad), you can easily import it into statesetd using the following steps.

Export the key from an existing keystore. In this example we will use gaiad. When prompted, input a password to encrypt the key file with.

gaiad keys export \<original\_key\_name> Copy the output starting from the line that says BEGIN TENDERMINT PRIVATE KEY and ending with the line that says END TENDERMINT PRIVATE KEY into a txt file somewhere on your machine.

Import the key into statesetd using the following command. When prompted for a password, use the same password used in step 1 to encrypt the keyfile.&#x20;

`statesetd keys import <new_key_name> ./path/to/key.txt`&#x20;

Delete the keyfile from your machine.

Import via Ledger&#x20;

To import a key stored on a ledger, the process will be exactly the same as adding a ledger key to the CLI normally. You can connect a Ledger device with the Cosmos app open and then run:&#x20;

`statesetd keys add <key_name> --ledger`&#x20;

and follow any prompts.

**Get your Tendermint Validator Pubkey**&#x20;

You must get your validator's consensus pubkey as it will be necessary to include in the transaction to create your validator. If you are using Tendermint's native priv\_validator.json as your consensus key, you display your validator public key using the following command Statesetd tendermint show-validator&#x20;

The pubkey should be formatted with the bech32 prefix statesetvalconspub1.

If you are using a custom signing mechanism such as tmkms, please refer to their relevant docs to retrieve your validator pubkey. Create GenTx Now that you have you key imported, you are able to use it to create your gentx. To create the genesis transaction, you will have to choose the following parameters for your validator: moniker commission-rate commission-max-rate commission-max-change-rate min-self-delegation (must be >1) website (optional) details (optional) identity (keybase key hash, this is used to get validator logos in block explorers. optional) pubkey (gotten in previous step)

`statesetd gentx <key_name> 1000000ustate \ --chain-id="stateset-1-testnet" \ --moniker=statesetwhale \ --website="https://stateset.zone" \ --details="We love Stateset” \ --commission-rate="0.1" \ --commission-max-rate="0.20" \ --commission-max-change-rate="0.01" \ --min-self-delegation="1" \ --identity="5B5AB9D8FBBCEDC6" \ --pubkey="statesetvalconspub1zcjduepqnxl4ntf8wjn0275smfll4n4lg9cwcurz2qt6dkhrjzf94up8g4cspyyzn9"`

It will show an output something similar to: Genesis transaction written to "/Users/ubuntu/.statesetd/config/gentx/gentx-eb3b1768d00e66ef83acb1eee59e1d3a35cf76fc.json"

The result should look something like this sample gentx file.

**Submit Your GenTx**&#x20;

To submit your GenTx for inclusion in the chain, please upload it to the github.com/stateset/networks repo by End of Day, November 23.

To upload the your genesis file, please follow these steps: Rename the gentx file just generated to gentx-{your-moniker}.json (please do not have any spaces or special characters in the file name)

Fork this repo by going to https://github.com/stateset/networks, clicking on fork, and choose your account (if multiple).

Clone your copy of the fork to your local machine&#x20;

`git clone https://github.com/<your_github_username>/networks`

Copy the gentx to the networks repo (ensure that it is in the correct folder)&#x20;

`cp ~/.statesetd/config/gentx/gentx-.json`

networks/stateset-1-testnet/gentxs/

Commit and push to your repo.

`cd networks`

`git add stateset-1-testnets/gentxs/*`

`git commit -m " gentx"`

`git push origin master`

Create a pull request from your fork to master on this repo. Let us know on Discord when you've completed this process.

### Validators

If you decide you want to turn your node into a validator, you will first need to add a wallet to your keyring.

While you can add an existing wallet through your seed phrase, we will create a new wallet in this example (replace KEY\_NAME with a name of your choosing):

```
statesetd keys add KEY_NAME
```

Ensure you write down the mnemonic as you can not recover the wallet without it. To ensure your wallet was saved to your keyring, the WALLET\_NAME is in your keys list:

```
statesetd keys list
```

The last thing needed before initializing the validator is to obtain your validator public key which was created when you first initialized your node. To obtain your validator pubkey:

```
statesetd tendermint show-validator
```

### Create Validator Command <a href="#create-validator-command" id="create-validator-command"></a>

Ensure you have a small amount of STATE on the wallet address you are using on your keyring in order to successfully send a transaction. Once you have have a balance on the address on your keyring, you can now send the create-validator transaction.

Here is the empty command:

```
statesetd tx staking create-validator \
--from=[KEY_NAME] \
--amount=[staking_amount_ustate] \
--pubkey=$(statesetd tendermint show-validator) \
--moniker="[moniker_id_of_your_node]" \
--security-contact="[security contact email/contact method]" \
--chain-id="[chain-id]" \
--commission-rate="[commission_rate]" \
--commission-max-rate="[maximum_commission_rate]" \
--commission-max-change-rate="[maximum_rate_of_change_of_commission]" \
--min-self-delegation="[min_self_delegation_amount]" \
--gas="auto" \
--gas-prices="[gas_price]" \

```

Here is the same command but with example values:

```
stated tx staking create-validator \
--from=wallet1 \
--amount=400000000ustate \
--pubkey=statesetvalconspub1zcjduepqrevtrgcntyz04w9yzwvpy2ddf2h5pyu2tczgf9dssmywty0tzqzs0gwu0r  \
--moniker="Albert" \
--security-contact="albert@stateset.labs" \
--chain-id="stateset-1" \
--commission-rate="0.1" \
--commission-max-rate="0.2" \
--commission-max-change-rate="0.05" \
--min-self-delegation="400000000" \
```



If you need further explanation for each of these command flags:

* the `from` flag is the KEY\_NAME you created when initializing the key on your keyring
* the `amount` flag is the amount you will place in your own validator in ustate (in the example, 500000000ustate is 500state)
* the `pubkey` is the validator public key found earlier
* the `moniker` is a human readable name you choose for your validator
* the `security-contact` is an email your delegates are able to contact you at
* the `chain-id` is whatever chain-id you are working with (in the stateset mainnet case it is stateset-1)
* the `commission-rate` is the rate you will charge your delegates (in the example above, 10 percent)
* the `commission-max-rate` is the most you are allowed to charge your delegates (in the example above, 20 percent)
* the `commission-max-change-rate` is how much you can increase your commission rate in a 24 hour period (in the example above, 5 percent per day until reaching the max rate)
* the `min-self-delegation` is the lowest amount of personal funds the validator is required to have in their own validator to stay bonded (in the example above, 500state)
* the `gas-prices` is the amount of gas used to send this create-validator transaction

### Track Validator Active Set <a href="#track-validator-active-set" id="track-validator-active-set"></a>

To see the current validator active set:

```
statesetd query staking validators --limit 300 -o json | jq -r '.validators[] |
[.operator_address, .status, (.tokens|tonumber / pow(10; 6)),
.commission.update_time[0:19], .description.moniker] | @csv' | column -t -s","
```



You can search for your specific moniker by adding grep MONIKER at the end:

```
statesetd query staking validators -o --limit 300 json | jq -r '.validators[] |
[.operator_address, .status, (.tokens|tonumber / pow(10; 6)),
.commission.update_time[0:19], .description.moniker] | @csv' | column -t -s"," | grep Albert

```

If your bond status is `BOND_STATUS_BONDED`, congratulations, your validator is part of the active validator set!

Please note, as of this writing, you must be in the top 100 validators (in other words, must have more STATE delegated to your validator than the 100th validator in the active validator set) to be bonded. If you did everything above correct but do not have more STATE delegated to your validator than the 100th validator, you will stay unbonded.

### Track Validator Signing <a href="#track-validator-signing" id="track-validator-signing"></a>

To track your validator's signing history, copy the validator public key:

```
statesetd tendermint show-validator

```

Use your validators public key queried above as the validator-pubkey below:

```
statesetd query slashing signing-info [validator-pubkey]

```

Example:

```
statesetd query slashing signing-info '{"@type":"/cosmos.crypto.ed25519.PubKey","key":"HlixoxNZBPq4pBOYEimtSq9Ak4peBISVsIbI5ZHrEAU="}'

```
