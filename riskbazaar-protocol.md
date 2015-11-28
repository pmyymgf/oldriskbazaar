#The RiskBazaar protocol#

Multichain white paper (Gideon Greenspan)
http://www.multichain.com/download/MultiChain-White-Paper.pdf

"...authenticated and notarized messaging, using a similar approach to the CoinSpark protocol for bitcoin. There are two main uses for messaging. First, it can be used to add important context for an on-blockchain financial transaction, such as a contract, receipt or invoice. Alternatively, it can be used for pure notarized communication with no related movement of funds. In either case, information on the blockchain enables both the sender and the recipient to prove the timing and content of the correspondence that took place."

"A message is sent from the originator to the recipient as follows:

1. The originating MultiChain node sends a message transaction to the recipient with metadata containing its IP address and a hash of the message's content.
2. The receiving node receives the transaction and decodes this metadata.
3. The receiving node contacts the originating node via its IP address to retrieve the message, signing the request in order to prove its identity as the intended recipient. This communication takes place using the blockchain's existing peer-to-peer protocol.
4. The receiving node verifies the message's validity by checking its hash against the hash embedded in the original transaction.
5. If the message is valid, the receiving node completes the loop by sending back a second transaction to the sender containing the same message hash."


