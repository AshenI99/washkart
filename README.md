# WASHKART

Washkart is a dapp that help users to get their clothes (laundry) washed just by clicking few buttons from the comfort of their homes.

Demo link: https://washkart.vercel.app/

App features:

1. Role-based access control (customer, admin)
2. Free pickup and delivery
3. Status updates (confirmed, in-progress, delivered, cancelled)
4. Full refunds for cancelled orders
5. Fast, secure, and reliable

# Quick Start

If you haven't installed dependencies during setup:

    npm run deps-install

Build and deploy your contract to TestNet with a temporary dev account:

    npm run deploy

Test your contract:

    npm test

If you have a frontend, run `npm start`. This will run a dev server.

# Exploring The Code

1. The smart-contract code lives in the `/contract` folder. See the README there for
   more info. In blockchain apps the smart contract is the "backend" of your app.
2. The frontend code lives in the `/frontend` folder. `/frontend/index.html` is a great
   place to start exploring. Note that it loads in `/frontend/index.js`,
   this is your entrypoint to learn how the frontend connects to the NEAR blockchain.
3. Test your contract: `npm test`, this will run the tests in `integration-tests` directory.

# Deploy

Every smart contract in NEAR has its [own associated account][near accounts].
When you run `npm run deploy`, your smart contract gets deployed to the live NEAR TestNet with a temporary dev account.
When you're ready to make it permanent, here's how:

## Step 0: Install near-cli (optional)

[near-cli] is a command line interface (CLI) for interacting with the NEAR blockchain. It was installed to the local `node_modules` folder when you ran `npm install`, but for best ergonomics you may want to install it globally:

    npm install --global near-cli

Or, if you'd rather use the locally-installed version, you can prefix all `near` commands with `npx`

Ensure that it's installed with `near --version` (or `npx near --version`)

## Step 1: Create an account for the contract

Each account on NEAR can have at most one contract deployed to it. If you've already created an account such as `your-name.testnet`, you can deploy your contract to `washkart.your-name.testnet`. Assuming you've already created an account on [NEAR Wallet], here's how to create `washkart.your-name.testnet`:

1. Authorize NEAR CLI, following the commands it gives you:

   `near login`

2. Create a subaccount (replace `YOUR-NAME` below with your actual account name):

   `near create-account washkart.YOUR-NAME.testnet --masterAccount YOUR-NAME.testnet`

## Step 2: deploy the contract

Use the CLI to deploy the contract to TestNet with your account ID.
Replace `PATH_TO_WASM_FILE` with the `wasm` that was generated in `contract` build directory.

    near deploy --accountId washkart.YOUR-NAME.testnet --wasmFile ./contract/build/release/washkart.wasm --initFunction init --initArgs '{"admin_account_id": "YOUR-NAME.testnet"}'

## Step 3: set contract name in your frontend code

Modify the line in `src/config.js` that sets the account name of the contract. Set it to the account id you used above.

    const CONTRACT_NAME = process.env.CONTRACT_NAME || 'washkart.YOUR-NAME.testnet'

# Troubleshooting

On Windows, if you're seeing an error containing `EPERM` it may be related to spaces in your path. Please see [this issue](https://github.com/zkat/npx/issues/209) for more details.

[create-near-app]: https://github.com/near/create-near-app
[node.js]: https://nodejs.org/en/download/package-manager/
[jest]: https://jestjs.io/
[near accounts]: https://docs.near.org/concepts/basics/account
[near wallet]: https://wallet.testnet.near.org/
[near-cli]: https://github.com/near/near-cli
[gh-pages]: https://github.com/tschaub/gh-pages
