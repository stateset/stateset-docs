# Invoices

{% swagger method="get" path="" baseUrl="https://rest-api.stateset.zone/#/Query/StatesetCoreInvoiceInvoiceAll" summary="" %}
{% swagger-description %}
Invoices
{% endswagger-description %}
{% endswagger %}

### Create an Invoice

Creating an Invoice from your own React / Next.js client can be done with the following code.&#x20;

First create the protobufjs type:

```javascript
import { Type, Field } from "protobufjs";

const MsgCreateInvoice = new Type("MsgCreateInvoice")
    .add(new Field("creator", 1, "string"))
    .add(new Field("id", 2, "string"))
    .add(new Field("did", 3, "string"))
    .add(new Field("amount", 4, "string"))
    .add(new Field("state", 5, "string"));
```

Then make a call out to the Stateset Zone RPC:

```javascript
   const handleOnSubmit = async() => {
        setStatus(prevStatus => ({ ...prevStatus, submitting: true }))

        const myRegistry = new Registry(defaultStargateTypes);
        myRegistry.register("/stateset.core.invoice.MsgCreateInvoice", MsgCreateInvoice);

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

            var _uuid = uuid();

            const message = {
                typeUrl: "/stateset.core.invoice.MsgCreateInvoice",
                value: {
                    creator: creator_address,
                    id: _uuid,
                    did: "did:stateset:inv:" + _uuid,
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

            const result = await client.signAndBroadcast(creator_address, [message], "auto", 'uploading a invoice from stateset zone');

            console.log(result)
            if (result) {
                setConfirm(true);
            } else if (result.error) {
                setError(true);
            } else {
                null
            }

        }
    }
```
