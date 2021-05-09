# NFT on NEAR
## Prerequisites
  * Make sure Rust is installed per the prerequisites in [`near-sdk-rs`](https://github.com/near/near-sdk-rs).
  * Make sure [near-cli](https://github.com/near/near-cli) is installed.

## Functions
 * mint
 * change color

## Build
```bash
cd contract
./build.sh
```

## Test
*Unit Tests*
```bash
cargo test -- --nocapture
```

## Available CLI

    near login

    near create-account lander.example.near --masterAccount example.testnet

    ID=MY_ACCOUNT_NAME

    echo $ID

    near deploy --wasmFile res/lander_near_nft_ncd.wasm --accountId $ID

    near call $ID new_default_meta '{"owner_id": "'$ID'"}' --accountId $ID

    near view $ID nft_metadata

### Mint
    near call $ID nft_mint '{"token_id": "0", "receiver_id": "'$ID'", "token_metadata": { "title": "Lander", "description": "3landers", "media": "https://bafybeihgivtoptr34zxvnf6xvvkvontr23ohtkqk52nfazb2a7hj4wlqxq.ipfs.dweb.link/purple-3lander-nft.png", "media_hash": "N2Y4OWY0ZTdlMGQ4ZThmNTU5NWI0MTM0ZDNkNDc1MzMxMWM3NDhhZTJkZmU2NWJkM2I5YzRmMmFjNzEyYmM1Yw==", "copies": 1}}' --accountId $ID --deposit 0.1

    near view $ID nft_token '{"token_id": "0"}' --accountId $ID

### Change color
    near call $ID change_color '{"token_id": "0", "color": "Yellow"}' --accountId $ID
    near call $ID change_color '{"token_id": "0", "color": "Red"}' --accountId $ID
    near call $ID change_color '{"token_id": "0", "color": "Purple"}' --accountId $ID

    near view $ID nft_token '{"token_id": "0"}' --accountId $ID



### Transfer
    near create-account alice.$ID --masterAccount $ID --initialBalance 10

    near view $ID nft_tokens_for_owner '{"account_id": "'alice.$ID'"}'

    near call $ID nft_transfer '{"token_id": "0", "receiver_id": "alice.'$ID'", "memo": "transfer ownership"}' --accountId $ID --depositYocto 1
