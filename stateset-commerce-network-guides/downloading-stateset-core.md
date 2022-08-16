---
description: Stateset Core
---

# Downloading Stateset Core

Stateset Commerce Network is comprised of a network of nodes, commonly known as the validator set, that are running the Stateset Core open-source blockchain software.

Go to [https://github.com/stateset/core](https://github.com/stateset/core) and download the repo to your local machine or a VM of your choice.

Install the Ignite Cli

`curl https://get.ignite.com/cli! | bash`

Once, downloaded, go into the core directory and run:

`ignite chain serve --reset-once`

You will then see the following output:

🔄 Resetting the app state...&#x20;

🛠️ Building proto...&#x20;

📦 Installing dependencies...&#x20;

🛠️ Building the blockchain...&#x20;

💿 Initializing the app...

You can the run

`ignite chain build`

To build the binary statesetd:

`statesetd`

`statesetd status`

