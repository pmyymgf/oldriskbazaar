# The business case for using blockchains in the insurance industry

A Decision Tree for Blockchain Applications: Problems, Opportunities or Capabilities by William Mougayar
http://startupmanagement.org/2015/11/30/a-decision-tree-for-blockchain-applications-problems-opportunities-or-capabilities/

"Reengineering processes, rethinking intermediaries, bundling services, unbundling services, new flows of value, decentralized governance, new legal frameworks, running smart contracts on the blockchain, sharing a distributed ledger, creating/issuing digital assets, embedding trust rules inside transactions and interactions, time-stamping, implementing digital signatures, notarizing data/documents to produce proof, creating records of a business process, event or activity, verifying authenticity of data/ownership/documents/assets, confirming authenticity of transactions, ensuring that contractual conditions are undeniably met, reconciling accounts, finalizing settlements, digital identity, providing escrow or custodian services, enabling smart things to transact securely."

Programmable blockchains in context: Ethereum's future by Vinay Gupta
https://medium.com/@ConsenSys/programmable-blockchains-in-context-ethereum-s-future-cd8451eb421e#.3aohk3jyz

"But the databases and the networks never really learn to get on...could not find a common world model which allowed them to inoperate smoothly. Interacting with a single database is easy enough: forms and web applications of the kinds you use every day. But the hard problem is getting databases working together, invisibly for our benefit, or getting the databases to interact smoothly with processes running on our own laptops."

"Those technical problems are usually masked by bureaucracy but we experience their impact every single day of our lives.... Perhaps you want your car insurance to get access to a policy report about your car getting broken into. In all probability you will have to get the data out of one database in the form of a handful of printouts, and then mail them to the company yourself: there's no real connectivity in the systems. You can't drive the process from your laptop, except by the dumb process of filling in forms. There's no sense of using real computers to do things, only computers abused as expensive paper simulators. Although in theory information could just flow from one database to another with your permission, in practice the technical costs of connecting databases are huge, and your computer doesn't store your data so that it can do all this work for you. Instead it's just something you fill in forms on."

"The human factors - the mindsets which generate the software - don't fit together. Each enterprise builds their computer system in their own image and these images disagree about what is vital and what is incidental and truth does not flow between them easily. When we need to translate from one world model to another, we put humans in the process and we're back to processes which mirror filling in paper forms rather than genuinely digital cooperation.... Every process requires filling in the same damn name and address data, twenty times a day and more often if you are moving house. How often do you shop from Amazon rather than some more specialized store just because they know where you live?"

Tell me who you are by Vinay Gupta

https://medium.com/@ConsenSys/tell-me-who-you-are-258268bf3180#.6ngiqpk5q

"What does the world really need to know about us? What do specific agencies really need to know about us? Can we get through life revealing less about ourselves using these technologies?

"Blockchains are great for pointing out things that we want to prove to other people: "look, it is right here, in the blockchain." This is great for things like property registers, but perhaps not quite so great when it comes to all the things we want to selectively disclose. So what if the architecture is a little different: what goes in the blockchain isn't the data - or, in many cases, even the hash of the data. Instead, we store a signed statement from a seriously credible source, or the necessary information required for a zero knowledge proof. A thing we might often store would be a public key, or a set of statements-and-signatures on a public key. It might be a script to perform some function but without tons of personal information on it."

"This is the transactional vision of the blockchain: something that's a little less about storing the entirety of our being on a permanent record, but more focussed on disclosing the minimum required for people to be able to do business (or critical functions) together."

"Maybe information is partitioned: your school grades, but not your name, all separated with a zero knowledge proof. If you have to prove that those are, in fact, your grades - well, that's what the public key is for. You demonstrate possession of the relevant private key - you know the secret - without the revealing the key. Every piece of personal information about you is stored with a different public key: you have a big fat keyring and each key reveals only a single fact."

"And maybe those keys have blind signatures or proxies or similar arrangements which prevent somebody noticing that Applicant for Job 1 has the same "see my proven grades" key as Applicant for Job 2..... information partitioning, database translucency, use of temporary credentials for passing needs, being economic with disclosures, even guarded."

"I believe in a simple division of the identity space into two parts. 1. Profiles 2. Actions. Profiles are a set of opinions that somebody has about me. These might include things like medical records, which are stories about me.... I cannot validate it. I might not even know it exists and it might be filled with utter stuff and nonsense. Your profile is your business, even if it is about me."

"Much of the direction of our society right now it towards merging profiles - credit records and social media to give even more accurate forecasts of loan risk, that sort of thing. The problem is that each profile contains withint in it a set of assumptions (a hidden frame, a perspective) which is incommensurable with much of the other data in such a combined profile. While these errors are small at first, the inevitable semantic problems of profile combining will always lead to problems which people (in most cases) will never be able to correct, because the profiles about them are largely secret, private or shared between cartels but never shown to the people they are about. Public profiles (for example, a university which publically lists student grades) might have quite a bit of utility in some cases - see "privileged profiles" below."

"Actions started out being called, in my mind, a volitional register - a log of the places where I have made choices. These would typically be key life decisions, like signing an employment contract, where the evidence that the signature was valid and accepted is a visible flow of money ideally across the blockchain itself. Another good example would be a mortgage payment. In all cases actions ideally lead to a stream of payments into or (better still) out of an account, something which shows that the contract was actually performed."

"If I'm looking for an identity, the person who's paid the mortgage for 18 years is a very, very tangible person - a person who's got 216,000 GBP of evidence over almost two decades as an escrow, a proof of trust. It's not even about the property, it's about the sheer historical fact of the payments which, particularly in a blockchain environment, constitute a visible, transparent impact of a decision made. You sign the contracts, you make the payment and  that identity is very solid. Same thing applies to student loans and almost any other major contractual commitment. We should not be surprised that the same foundational pillars which banks have been using for generations turn out to still provide support in this new world."

"Now in a pre-blockchain environment, actions and profiles get confused because more or less the only way I can get your actions is by asking somebody else (your bank) what you did. This confusion is pervasive. On a blockchain, because my actions are self-certifying, like performative speech acts, I can present you with proof of what I have done without any third party having to vouch for me. This identity is all mine: self-sovereign."

"So we have to mentally separate it all out: my proof of what I did is on the blockchain, and you can see it if I tell you which public key corresponds to my actions. Other people's profiles of my behaviour might even be on blockchains but if I didn't sign the transaction, it's not"me" in the same way as my digital signature is "me"."

"Now profiles, as noted, are other people's stories about me and my behaviour. They could be riddled with errors, or bound to me by mistake: somebody else uses my health insurance number because of identity fraud, resulting in me having medical records showing I've been prescribed drugs which, in fact, I have never taken."

"Similarly, my actions are not my stories about myself: they are the evidential trail of things I have done and preferably are bound to a keypair."

"On the other hand, there's privileged profiles. These might include profiles about me from people you trust more than me: if Harvard says I did a degree there, most people will believe them. My proof-of-payments on a student loan is pretty good evidence too, but most people would prefer to hear about my grades from Harvard itself. Of course, the combination of their privileged profile and my action records is pretty much unbeatable: "they say I got a law degree, and here's my evidence that I've paid for one."

"In the more general case, a privileged profile is a profile that I sign, stating that I (as the person this profile information is about) currently considers it to be correct, as far as I can see. Examples of privileged profiles we might see a lot of: medical records, tax records, court transcripts but also less official documents like my score record as a player of baseball in the local neighbourhood team could be privileged profiles."

"You make a statement about me. I approve that statement about me. That's a privileged profile. It's privileged because I said it's true, not because it was signed off on by the Supreme Court!"

"Put some things into blockchains, particularly things like the public keys of major organizations and certificate revocations for people whose keys have been stolen or whatver. Use additional cryptography to provide things like zero knowledge proofs of age without revealing identity. Compartmentalize information about our various roles in ways which make it hard to join profiles without our consent."

Blockchain in the Investment Bank by Accenture
https://www.accenture.com/t20150811T015521__w__/th-en/_acnmedia/Accenture/Conversion-Assets/DotCom/Documents/Global/PDF/Dualpub_13/Accenture-Blockchain-Investment-Bank.pdf#zoom=50

* Secure transaction ledger database shared by all parties in an established, distributed network
* Trusted third party elimination - assets are held "in the cloud" and are tied to their owners' identities rather than institutional custodians
* Automation - execution is open to the Internet and settlement is automatic, can run without any human interference and under control of an incorruptible set of business rules
* Smart controls - computer protocols facilitate, verify, or enforce the negotiation or performance of a contract and obviate the need for contractual clause
* Cost reduction - infrastructure, transaction costs
* Eliminates error handling - eliminates reconciliation, real time track and trace audit trail
