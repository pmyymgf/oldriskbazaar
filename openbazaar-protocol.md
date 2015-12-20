# Leveraging the OpenBazaar protocol for RiskBazaar

There are three components to the OpenBazaar protocol
* Kademlia style peer-to-peer (P2P) network architecture
* Trade protocol governing the rules of trade
* Application for users to access network and execute trade protocol

How do you buy a contract on OpenBazaar?

1. Seller creates a contract and puts it out on the network
2. Buyer digitally signs the contract (PGP) and sends it back to the seller
3. Seller agrees by signing the buyer's version of the contract
4. Notary agrees to mediate the transaction by signing the contract and creating a multisig 2 of 3 address
5. The notary transfers this signed contract and multisig address to both the buyer and seller
6. Buyer sends money to the multisig address and confirms payment
7. Seller acknowledges payment and ships goods or delivers service
8. Upon successful delivery signs and sends a 'closed' contract to the seller
9. Seller checks to make sure all is right and broadcasts the multisig transaction to the Bitcoin network; payment is released to seller

What happens during a dispute?

1. Buyer/seller flags transaction for dispute
2. Notary is notified and participants provide evidence for either side to the notary
3. Notary makes a judgement and creates a transaction to reverse payment or signs original contract or whichever solution all parties decide on

(Fees for dispute resolution are paid to notary. Notary can command a high or low fee based on reputation and skill set.)

Bibliography

1.	Sanchez, W. (2015). Protocol https://github.com/drwasho/openbazaar-documentation/blob/master/03%20Protocol.md#3-protocol
