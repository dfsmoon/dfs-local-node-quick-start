# dfs-local-node-quick-start

A local development environment for DFS Chain, For learning purposes only.

The project is based on an online project.：https://github.com/DFSNetwork/dfs-node-quick-start

### Start
```sh
docker compose up -d
```

### Stop
When stopping for a long time (e.g. a few days), the block production catches up with the current time after restarting before it can be used normally.
```sh
docker compose down
```

### View Log
```sh
docker compose logs -f
```

### View block information
```
http://192.168.101.104:8887/v1/chain/get_info
```

When the blockchain is started, it is currently an empty chain with no contracts deployed, so for testing purposes, a token contract can be deployed

Token contract I used the yfc contract, the address is https://github.com/DFSNetwork/yfc_token_contract, You can also use eosio.token contracts, both are possible.

# Deploy token contract
###  Deploy a DFS contract
```sh
# Create an account
cleos create account eosio eosio.token EOS7ap72uddq1n6o39rEhvrDAYqLGj6NSVdv8wkNvB3FAZeWfpFAJ

## Deploy contract
cleos set contract eosio.token ./token_contract/build/yfctokenos -p eosio.token

# Token issuance
cleos push action eosio.token create '["tokenissuera", "10000000.00000000 DFS"]' -p eosio.token@active

# Supply 
cleos get table eosio.token DFS stat

# issue
cleos push action eosio.token issue '["tokenissuera", "1000.00000000 DFS", "initial issue"]' -p tokenissuera@active

# Check balance
cleos get currency balance eosio.token tokenissuera DFS


# Transfer
cleos push action eosio.token transfer '["tokenissuera", "aaaaaaaaaaa1", "50.00000000 DFS", "transfer"]' -p tokenissuera@active

cleos push action eosio.token transfer '["tokenissuera", "aaaaaaaaaaa2", "500.00000000 DFS", "transfer"]' -p tokenissuera@active

cleos get currency balance eosio.token aaaaaaaaaaa1 DFS
```

### Deploy a USDT contract
```sh
# Create account
cleos create account eosio usdtusdtusdt EOS7ap72uddq1n6o39rEhvrDAYqLGj6NSVdv8wkNvB3FAZeWfpFAJ

## Deploy contract
cleos set contract usdtusdtusdt ./token_contract/build/yfctokenos -p usdtusdtusdt

# Token Create
cleos push action usdtusdtusdt create '["tokenissuera", "10000000.00000000 USDT"]' -p usdtusdtusdt@active

# Supply
cleos get table usdtusdtusdt USDT stat

# issue
cleos push action usdtusdtusdt issue '["tokenissuera", "1000.00000000 USDT", "initial issue"]' -p tokenissuera@active


# Check Balance

cleos get currency balance usdtusdtusdt tokenissuera USDT


# Transfer
cleos push action usdtusdtusdt transfer '["tokenissuera", "aaaaaaaaaaa1", "500.00000000 USDT", "transfer"]' -p tokenissuera@active

  
cleos get currency balance usdtusdtusdt aaaaaaaaaaa1 USDT

```

### Deploy a JIU contract

```sh
# Create account
cleos create account eosio jiutokenmain EOS7ap72uddq1n6o39rEhvrDAYqLGj6NSVdv8wkNvB3FAZeWfpFAJ

## Deploy contract
cleos set contract jiutokenmain ./token_contract/build/yfctokenos -p jiutokenmain

# token create
cleos push action jiutokenmain create '["tokenissuera", "100000000000.0000 JIU"]' -p jiutokenmain@active

# supply
cleos get table jiutokenmain JIU stat

# issue some token
cleos push action jiutokenmain issue '["tokenissuera", "1000000000.0000 JIU", "initial issue"]' -p tokenissuera@active

# Check Balance
cleos get currency balance jiutokenmain tokenissuera JIU

# Transfer
cleos push action jiutokenmain transfer '["tokenissuera", "aaaaaaaaaaa1", "50000000.0000 JIU", "transfer"]' -p tokenissuera@active

cleos get currency balance jiutokenmain aaaaaaaaaaa1 JIU
```