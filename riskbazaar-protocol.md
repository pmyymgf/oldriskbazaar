#The RiskBazaar protocol#

__CheckLockTimeVerify__

https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki

https://bitcoinmagazine.com/articles/checklocktimeverify-or-how-a-time-lock-patch-will-boost-bitcoin-s-potential-1446658530

__Blockchain messaging__

CoinSpark
http://coinspark.org
https://github.com/coinspark

Multichain white paper (Gideon Greenspan)
http://www.multichain.com/download/MultiChain-White-Paper.pdf

"...authenticated and notarized messaging, using a similar approach to the CoinSpark protocol for bitcoin. There are two main uses for messaging. First, it can be used to add important context for an on-blockchain financial transaction, such as a contract, receipt or invoice. Alternatively, it can be used for pure notarized communication with no related movement of funds. In either case, information on the blockchain enables both the sender and the recipient to prove the timing and content of the correspondence that took place."

"A message is sent from the originator to the recipient as follows:

1. The originating MultiChain node sends a message transaction to the recipient with metadata containing its IP address and a hash of the message's content.
2. The receiving node receives the transaction and decodes this metadata.
3. The receiving node contacts the originating node via its IP address to retrieve the message, signing the request in order to prove its identity as the intended recipient. This communication takes place using the blockchain's existing peer-to-peer protocol.
4. The receiving node verifies the message's validity by checking its hash against the hash embedded in the original transaction.
5. If the message is valid, the receiving node completes the loop by sending back a second transaction to the sender containing the same message hash."

"Once the first transaction is confirmed on the blockchain, the recipient can prove: (a) who sent the message, since the sender reveals their address when signing the transaction, (b) the time the message was sent, since the transaction is embedded in a timestamped block and (c) the message's content since the hash is part of the transaction that was signed. However, none of this is sufficient for the sender to prove that a particular message was received by the recipient. Indeed malicious senders could even embed a hash of one message while sending a completely different message in step 3 above. Therefore we require a second transaction in which the recipient sends back a receipt containing the same hash. Once this transaction is confirmed, both parties can prove all the details of the correspondence that took place."

"As with public messages in CoinSpark, such a system could also be used to broadcast information openly to all network participants, with the message hash on the blockchain serving as proof of the message's content and publication time. In this case we simply skip the restriction on who may retrieve the message from the originating node, and do not require a second transaction to confirm the message's receipt. Each message also contains a unique random "salt" which affects the hash but is not displayed to the user. This prevents message snooping via dictionary attacks."


