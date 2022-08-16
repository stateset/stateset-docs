---
description: Key Management for Stateset Network Nodes
---

# Key Management

Create a New Key

`statesetd keys add <wallet_name>`

The key comes with a "mnemonic phrase", which is serialized into a human-readable 24-word mnemonic. User can recover their associated addresses with the mnemonic phrase.

**WARNING**

It is important that you keep the mnemonic for address secure, as there is **no way** to recover it. You would not be able to recover and access the funds in the wallet if you forget the mnemonic phrase.

### Restore existing key by seed phrase <a href="#restore-existing-key-by-seed-phrase" id="restore-existing-key-by-seed-phrase"></a>

```
statesetd keys add <key_name> --recover
```

You can restore an existing key with the mnemonic.

### List your keys <a href="#list-your-keys" id="list-your-keys"></a>

```
statesetdkeys list
```

Multiple keys can be created when needed. You can list all keys saved under the storage path.

### Retrieve key information <a href="#retrieve-key-information" id="retrieve-key-information"></a>

```
statesetd keys show <key_name>
```

You can retrieve key information by its name:

### Delete a key <a href="#delete-a-key" id="delete-a-key"></a>

```
statesetd keys delete <key_name>
```

You can delete a key in your storage path.

**WARNING**

Make sure you have backed up the key mnemonic before removing any of your keys, as there will be no way to recover your key without the mnemonic.

### Export private keys <a href="#export-private-keys" id="export-private-keys"></a>

```
statesetd keys export <key_name>
```

### The keyring-backend option <a href="#the-keyring-backend-option" id="the-keyring-backend-option"></a>

Interacting with a node requires a public-private key pair. Keyring is the place holding the keys. The keys can be stored in different locations with specified backend type.

```
$ statesetd keys [subcommands] --keyring-backend [backend type]
```
