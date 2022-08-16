# Purchase Orders

### Get Purchase Orders

{% swagger method="get" path="" baseUrl="https://rest-api.stateset.zone/#/Query/StatesetCorePurchaseorderPurchaseorderAll" summary="" %}
{% swagger-description %}
Purchase Orders
{% endswagger-description %}
{% endswagger %}

### Creating a Purchase Order

Creating a Purchase Order from your own React / Next.js client can be done with the following code.&#x20;

First create the protobufjs type:

```javascript
import { Type, Field } from "protobufjs";

const MsgRequestPurchaseorder = new Type("MsgRequestPurchaseorder")
    .add(new Field("creator", 1, "string"))
    .add(new Field("did", 2, "string"))
    .add(new Field("uri", 3, "string"))
    .add(new Field("amount", 4, "string"))
    .add(new Field("state", 5, "string"));
```

Then make a call out to the Stateset Zone RPC:

```javascript
    const handleOnSubmit = async() => {
        setStatus(prevStatus => ({ ...prevStatus, submitting: true }))

        const myRegistry = new Registry(defaultStargateTypes);
        myRegistry.register("/stateset.core.purchaseorder.MsgRequestPurchaseorder", MsgRequestPurchaseorder);

        const mnemonic = process.env.NEXT_PUBLIC_MNEMONIC;

        const wallet = await DirectSecp256k1HdWallet.fromMnemonic(
            mnemonic,
            { prefix: "stateset" },
        );

        console.log(wallet);

        const firstAccount = await wallet.getAccounts();

        console.log(firstAccount[0].address);

        var creator_address;

        if (firstAccount) {

            creator_address = firstAccount[0].address;
        
        }

        const rpcEndpoint = "https://rpc.stateset.zone";

        const client = await SigningStargateClient.connectWithSigner(rpcEndpoint, wallet, { registry: myRegistry, gasPrice: "0.025state" });

        if (client) {

            const message = {
                typeUrl: "/stateset.core.purchaseorder.MsgRequestPurchaseorder",
                value: {
                    creator: creator_address,
                    did: "did:stateset:po:" + uuid(),
                    uri: inputs.uri,
                    amount: inputs.amount,
                    state: "request"
                },
            };

            // Fee
            const fee = {
                amount: [
                    {
                        denom: "state",
                        amount: "0",
                    },
                ],
                gas: "10000",
            };

            const response = await client.signAndBroadcast(creator_address, [message], "auto", 'uploading a po request from stateset zone');

            console.log(response);
        }
    }
```
