[https://bitcoin.stackexchange.com/questions/4724/what-is-a-transactions-step-by-step-life-cycle](https://bitcoin.stackexchange.com/questions/4724/what-is-a-transactions-step-by-step-life-cycle)



The lifetime of a transaction would be something like this:

1. You start with a client, a wallet that contains your keypairs, and some unspent transactions \(you get those from other people or through mining\).
2. You create a new transaction spending some of your unspent Bitcoins, sign it with your private keys. Your client will store a copy of it.
3. Your client starts to broadcast the new transaction through the Bitcoin Network. As far as I remember it doesn't broadcast it to every peer, but to every 8th peer in order to protect your anonymity. Every minute the client will also broadcast all transactions it knows about to one of its peers, which would also include your new transaction.
4. Every client that receives your transaction scrutinizes it - they check whether the signature is okay, whether there are any errors, and whether you are trying to perform a double-spend. If your transaction fails any of the criteria, it is ignored by the client entirely. Otherwise the client keeps a note of the transaction in temporary memory.
5. All the clients that know about your transaction follow a similar route of broadcasting as you did - send it to 1/8 peers, and then to one peer every minute. They will also not broadcast your transaction if its fee is too small at a given time \(which varies on the amount of transactions to be included in a block and so forth\). Generally, if you don't pay fees, you get punished with slow transaction broadcast rate right here.
6. Eventually your transaction reaches some mining pools and the recipients of the transactions. The latter will see the new transaction in their wallets and store a copy of it indefinitely, but it will appear as 0 confirmations. The mining pools will see it as a new transaction and \(most likely\) will include it in every block they try to create. They will store a local copy of the temporary blocks and give out the corresponding work to solve to their miners.
7. The miners don't know anything about your transaction, other than with one or more transaction it hashes to a given merkle root. Their job is to crunch numbers, not to check for block validity, as that's a task for the pool.
8. Eventually your transaction is included in a block that gets solved. It gets broadcasted proudly through the Bitcoin network and everyone keeps a note of it from now on \(to know if some new transaction conflicts with it in a double-spend attempt\). Now your transaction has 1 confirmations.
9. The block creation process continues, and as more and more blocks build atop the block your transaction gets included, it gains more confirmations. Eventually reaching 6 and more confirmations, it is considered fully confirmed.
10. The transaction finishes its live cycle once it is spent by another transaction, meaning that its outputs can be forgotten from the "unspent" memory and disregarded for any other attempts to spend them. It will, however, remain in the blockchain for as long as people will keep track of the full chain.

There are a few complications during 51% attacks and so forth, but this is the main flow of a standard transaction.

