## Transaction insurance in OpenBazaar - The first application

Some notes so far....

September 29th

Discussion on what should be hashed in the OP_RETURN
Efficiency vs Security
@austin proposed hash(RA || hash (TR)) in OP_RETURN
TR = fully completed trade receipt
RA = signed rating (which is contained in the TR)

My spidey senses are tingling at the thought of OP_RETURNing a hash of only a ​_subset_​ of the completed TR (that is, OP_RETUNRing only the hash of the ratings and not the hash of the fully completed TR). I'm concerned this could leave us open to a vulnerability that would allow people keep the same rating data but swap out the rest of the completed TR.

This may be relevant, for example, in the case of transaction insurance when an adjuster asks to see the trade receipt for the trade in question... and one of the parties keeps the ratings data the same but swaps out other parts of the completed contract. Since the insurance adjuster, looking at the BC, can only see a commitment to the ratings data (and not the rest of the TR) he can only be sure that the ​_rating_​ is correct... not that he actually has the correct corresponding TR.

I also understand and agree with @cpacia's efficiency concerns and so I propose the following modification that would satisfy @cpacia's  requirements as well as quell my security concerns:

Let `TR` be the fully completed trade receipt.
Let `RA` be the signed rating (which is contained in the `TR`).
Then instead of OP_RETURNing `hash(RA)`, we would instead OP_RETURN `hash(RA || hash(TR))`

This satisfies @cpacia's requirement that casual users need only download the rating (actually, they'd need to download the rating AND hash(TR), but that is a trivial difference w.r.t. bandwidth). Such 'trusting' users can verify the rating without downloading and verifying the entire TR.

Moreover, we're still committing to the entire TR (which is what I want), so we don't have to worry about any 'swapping out all-but-the-ratings" attacks later on -- and 'fully validating' users still be able to verify that they have the correct completed TR for that corresponds to each trade.

Thoughts?
