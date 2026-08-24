One of the areas of blockchain adoption I see is still underdeveloped is the enforcement of legal agreements via smart contracts.

It's an intentional gap - nobody likes to talk legalese. So I'm putting together a repo including some of the most typical use cases for contracts that a code developer would encounter - NDAs, Intellectual Property/Copyright disclaimer, 1-year licensing agreement, etc. The juice is not in the content, but in the execution: I'm adding a twist and making them executable via smart contracts. 

While in regular practice the terms of a contract can be tailored to each case, in order to keep the smart contracts in here simple and universal, I'm choosing one-size-fits all **deterministic** templates without party arbitration, oracles or canonicalisation. The variables [party A], [party B], [effective date] will be recorded by the on-chain transaction confirmation itself; the other variables will be predetermined at the text template level, using England and Wales as the default governing law and the London Court of International Arbitration (“LCIA”) as the seat for dispute resolution based on its Rules. The default duration (when an end date is advised) is 1 year.

Think of the legal contracts in this repo as having two layers:

Contract Terms (pre-filled from my template library)
- Confidential Information definition: standard
- Permitted uses: standard
- Exceptions: standard
- Duration: standard (1 year / illimited)
- Governing law: _England and Wales (UK)_ (deterministic)
- Dispute resolution: _by arbitration at the LCIA_ (deterministic)
- Remedies: standard

Blockchain layer (non-deterministic, on-chain execution):
- PARTY_A       = msg.sender;
- PARTY_B       = [function of second signing wallet];
- EXECUTION_DATE = block.timestamp

In essence, the blockchain layer allows us to cryptographically sign the NDA by 2 wallets; establish that both parties accepted exactly the same version; record the execution timestamp as the date when it starts being effective; lock the default agreed parameters; and create an immutable audit trail of subsequent actions.

We're gonna use **EIP-712** for the smart wallet design because of its capabilities to let wallets sign structured, human-readable typed data rather than an opaque blob. The contract templates themselves will be stored on **Arweave** which enables permanent, long form, data storage.

All blueprints are based on international principles of law that are generally applied across jurisdictions. This is not legal advice nor tailored contracts - if you require legal assistance, please contact qualified counsel. Contributions are very welcome - feel free to add deep dive readmes, new contract types or specific jurisdictions that regulate the topic differently.

Hopefully this will make us a little less scared of talking legalese. This is a live repo, so watch this space for new things to be added up!
