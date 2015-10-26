# Transaction insurance in OpenBazaar - The first application of RiskBazaar

The first application of RiskBazaar will provisionally be to provide transaction insurance on OpenBazaar. This insurance coverage relates to transactions where there is a dispute between buyer and vendor prior to completion of the transaction and the arbiter rules "incorrectly" in favour of one of the parties. The insurance contract will compensate the wronged party if they have purchased transaction insurance and have a valid claim.

__September 29th (OpenBazaar Slack)__

Discussion on what should be hashed in the OP_RETURN of an OpenBazaar transaction

Bitcoin's scripting language contains the ```OP_RETURN``` operator which allows 40 bytes of additional data to be added to a transaction output and recorded on the blockchain.

There has been much discussion on the OpenBazaar Slack channel on what should be included in the ```OP_RETURN``` balancing efficiency and security concerns. 

@austin proposed storing ```hash(RA || hash (TR))``` rather than ```hash(RA)``` in the ```OP_RETURN``` addressing the vulnerability of one party keeping the same rating data but swapping out the rest of the completed TR. This would allow the insurance adjuster to be sure that he is looking at the relevant TR.

TR = fully completed trade receipt

RA = signed rating (which is contained in the TR)

All other users would only need to download the rating and ```hash(TR)``` to be able to verify the rating without needing to download and verify the entire TR.

An unalterable public commitment to the TR needs to be public and on the blockchain for moderator review, transaction insurance and other potential services that require analysing the details of the trade itself.

__October 2nd__

It was not possible to fit all the necessary data in the 40 bytes of the ```OP_RETURN``` operator.

The alternative plan as described by @cpacia is to create compact proofs that a buyer was in a trade with a vendor (mini trade receipt). 

1) Buyer sends order to vendor

2) Vendor responds with a signature covering the bitcoin address, amount to be paid, listing hash and a buyer public key (which is used to sign a public review)

3) Once the buyer has funded the address a review can be created:

```
-----BEGIN OPENBAZAAR VENDOR RATING-----
Version: OpenBazaar-Server 0.1

Vendor: e2fdb78bca93788ff073df029badcaeab622594a
Vendor Signed Public Key: 72c3f7ee7cfc90f3b40903b2f2a294860599928272c3f7ee7cfc90f3b40903b2f2a294860599928272c3f7ee7cfc90f3b40903b2f2a2948605999282e7cfc90fca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48bb
Listing: 59668109f673e96303a8e82948d6df65da67be75
Bitcoin Address: 3HB5XMLmzFVj8ALj6mfBsbifRoD4miY36v
Amount: 0.15 BTC
Buyer Public Key: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
Transaction: e6612e701d1b073d28514fb1dcb545bc522b312265f8c2ad3e3e3a2555931767
Vendor Signature: 4c286e182bc4d1832a8739b18c19ecaf9262c37a4c286e182bc4d1832a8739b18c19ecaf9262c37a4c286e182bc4d1832a8739b18c19ecaf9262c37ae182bc4d

Feedback: 4
Quality: 5
Description: 4
Delivery Time: 2
Customer Service: 3

Review: "Good stuff. Took long to deliver tho"
-----BEGIN BUYER SIGNATURE-----
Hash: Hash160

30c2507be3fb5ad077a8227031dfd329d9641ab430c2507be3fb5ad077a8227031dfd329d9641ab430c2507be3fb5ad077a8227031dfd329d9641ab431dfd3
-----END OPENBAZAAR VENDOR RATING-----
```
This review block can be validated to prove the person who created it was in a transaction with the vendor. Provisionally the vendor will be required to store it but these will eventually need to be securely stored by OpenBazaar. (In the meantime the buyer still has proof the trade took place). 

__October 3rd__

@austin 
Preventing vendors from creating fake trades/reviews is not possible (otherwise platform would be censorship resistant) so the focus is on detecting and ignoring fake trades after they occur. There are many techniques to identify fake trades such as detecting the same coins being sent back and forth via trades with sybils and analyzing the time coins are held in escrow before being released.

It is important that a vendor's identity (if only a pseudonym) is publicly attached to every trade so that their reputation can be assessed. The vendor is always known via his GUID and this is available in the contract and trade receipt. So we can always get the set of all transactions associated with any vendor. The vendors are pseudonymous by default, and can optionally tie their real world identity to their pseudonym. (though once this is done, it's permanent).

For the buyer, we've designed things so they remain ​_anonymous_​ by default (at least w.r.t. contract data... an adversary observing the network could still get their IP address). They can optionally become pseudonymous (linking together whatever subset of their trades they desire). If they want to, they can even reveal their meatspace ID and attach it to whatever subset of trades they want.

Online identity is tricky. It's often thought of as one problem, but in reality it is an entire family of problems. Some of those are solved problems, and some are not. Soon I'll write a few high-level articles explaining the family of problems, how they are related, which are solved and which aren't, and how some are at direct odds with others.

As for transaction insurance (and insurance in general), I strongly suspect that insurers will only deal with vendors/buyers/moderators that have confirmed their meatspace ID, and I think that's totally doable within the OB framework. It's just something that isn't ​_by default_​.

__October 4th__


1. Can we have the transaction summary formatted in JSON instead of the PGP style? It will just be easier to parse the data (thinking of 3rd party tools as well). 
2. Can we include the trade receipt hash in the transaction summary? Just means we can use that for the applications that Austin, @michaelfolkson and I want to develop.

Since metadata isn't being put into `OP_RETURN`, this means that the Vendor can sign the payout transaction from escrow in stage 3 of the trade flow, and the Buyer can make the final signature and broadcast for stage 4. Whether or not the partially and fully signed tx are included in the trade receipt is up for grabs, but probably unnecessary. (edited)
:+1:1  

drwasho [4:42 PM] 
Ok, I've been reviewing the transaction summary schema. I formatted the tx summary to JSON, nested a couple of fields where it made sense. One bit that I nested under an object called `transaction` are the fields that the Vendor's signature is covering.  I also added:

1) the vendor's pubkey (not just their GUID, otherwise you can't verify the vendor's signature),  
2) the trade receipt hash

JSON formatting instead of PGP

```{
  "tx_summary" : {
      "vendor" : {
        "guid" : "e2fdb78bca93788ff073df029badcaeab622594a",
        "pubkey" : "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      },
      "transaction" : {
        "listing" : "59668109f673e96303a8e82948d6df65da67be75",
        "bitcoin_address" : "3HB5XMLmzFVj8ALj6mfBsbifRoD4miY36v",
        "price" : "0.15",
        "buyer_pubkey" : "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"
      },
      "vendor_tx_signature" : "72c3f7ee7cfc90f3b40903b2f2a294860599928272c3f7ee7cfc90f3b40903b2f2a294860599928272c3f7ee7cfc90f3b40903b2f2a2948605999282e7cfc90fca978112ca1bbdcafac231b39a23dc4da786eff8147c4e72b9807785afee48bb",
      "txid" : "e6612e701d1b073d28514fb1dcb545bc522b312265f8c2ad3e3e3a2555931767",
      "trade_receipt_hash160" : "yyyyyyyyyyyyyyyyyy",
      "rating" : {
        "feedback": 4,
        "quality" : 5,
        "description" : 4,
        "delivery_time" : 2,
        "customer_service" : 3,
        "review" : "Good stuff. Took long time to delivery though."
      }
  },
  "buyer_signature" : "30c2507be3fb5ad077a8227031dfd329d9641ab430c2507be3fb5ad077a8227031dfd329d9641ab430c2507be3fb5ad077a8227031dfd329d9641ab431dfd3"
}
