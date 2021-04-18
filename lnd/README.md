Lightning node by LND implementation https://github.com/lightningnetwork/lnd.

opening channels on docker compose:

1. docker exec -ti lnd bash
2. lncli -n regtest walletbalance
3. lncli -n regtest newaddress p2wkh
4. (from core) bitcoin-cli generatetoaddress 101 {address 3.}
5. (from host browser) aprire http://localhost:9737/#/node e copiare la pubkey
6. lncli -n regtest connect {pubkey 5.}@lightningd:9735
7. lncli -n regtest openchannel {pubkey 5.} 100000
8. (from host browser) open http://localhost:9737/#/channels 
9. (from core) bitcoin-cli generatetoaddress 6 $(bitcoin-cli getnewaddress)
10. (from host browser) aprire http://localhost:9737/#/channels 

To connect a channel to this LN node

1. docker exec -ti lnd bash
2. lncli -n regtest getinfo | jq '.identity_pubkey'
3. on electrum from channels tab click on "Open Channel"
4. as "Remote node ID" do specify {pubkey 2.}@127.0.0.1:19735

At this moment ln-cli does not support a configfile: https://github.com/lightningnetwork/lnd/issues/533.
