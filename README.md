# Viem-Ethers-Replace-Web3Modal-NextJS
A simple straightforward addon using Viem to replace the deprecated Web3Modal on your NextJS Web3 Project with Ethers

<h3>Step 1</h3>

Navigate to your NextJS Project and Install Viem.

```shell
cd myproject
npm i viem
```

<h3>Step 2</h3>

Create a new js file 'web3provider.js' on your NextJS project "components" folder.
and paste the following:

FYI if you don't have a components folder, please create one.

```shell
import { createWalletClient, custom } from "viem";
import { polygonMumbai } from "viem/chains";

export const web3Provider = async () => {
  const [account] = await window.ethereum.request({
    method: "eth_requestAccounts",
  });

  const client = createWalletClient({
    account,
    chain: polygonMumbai,
    transport: custom(window.ethereum),
  });
  return client;
};

```

Important, in the code, modify the chain to your preferred choice:

```shell
import { polygonMumbai } from "viem/chains";

//under client: 
 chain: polygonMumbai,
```
Save file.

<h3>Step 3/h3>

import the function where needed:

```shell
// example index.js
import { web3Provider } from '@/components/web3provider';
```
Replace web3modal and pass directly web3Provider

Example, This is before with web3modal:

```shell
async function ethConnect() {
    const web3Modal = new Web3Modal()
    const connection = await web3Modal.connect()
    const provider = new ethers.providers.Web3Provider(connection);

```

After replacing with web3Provider:

```shell
async function ethConnect() {
    const connection = await web3Provider()
    const provider = new ethers.providers.Web3Provider(connection);

```

Dont forget to save and test! 

Enjoy!!
