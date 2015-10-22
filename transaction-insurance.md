### Transaction insurance in OpenBazaar - The first application of RiskBazaar

The first application of RiskBazaar will provisionally be to provide transaction insurance on OpenBazaar. This insurance coverage relates to transactions where there is a dispute between buyer and vendor prior to completion of the transaction and the arbiter rules "incorrectly" in favour of one of the parties. The insurance contract will compensate the wronged party if they have purchased transaction insurance and have a valid claim.

__September 29th__

Discussion on what should be hashed in the OP_RETURN of an OpenBazaar transaction

Bitcoin's scripting language contains the ```OP_RETURN``` operator which allows 40 bytes of additional data to be added to a transaction output and recorded on the blockchain.

There has been much discussion on the OpenBazaar Slack channel on what should be included in the ```OP_RETURN``` balancing efficiency and security concerns. 

@austin proposed storing ```hash(RA || hash (TR))``` rather than ```hash(RA)``` in the ```OP_RETURN``` addressing the vulnerability of one party keeping the same rating data but swapping out the rest of the completed TR. This would allow the insurance adjuster to be sure that he is looking at the relevant TR.

TR = fully completed trade receipt

RA = signed rating (which is contained in the TR)

All other users would only need to download the rating and ```hash(TR)``` to be able to verify the rating without needing to download and verify the entire TR.

An unalterable public commitment to the TR needs to be public and on the blockchain for moderator review, transaction insurance and other potential services that require analysing the details of the trade itself.



