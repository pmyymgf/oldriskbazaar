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

