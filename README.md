One of the areas of blockchain adoption I see is still underdeveloped is the enforcement of legal agreements via smart contracts.

It's an intentional gap - nobody likes to talk legalese. So I'm putting together a repo including some of the most typical use cases for contracts that a code developer would encounter - NDAs, Intellectual Property/Copyright disclaimer, licensing agreements, code review services, etc. The juice is not in the content, but in the execution: I'm adding a twist and making them executable via smart contracts. 

Taking the NDA as the illustration point, think of it as having two layers:

Contract Content (pre-populated from my own template library):
- Confidential Information definition
- Permitted uses
- Exceptions
- Duration
- Governing law
- Remedies
- Monetary liquidated damages, if legally appropriate

Blockchain layer (executable when you run this repo in your machine):
- Identify the parties by wallet
- Cryptographically sign the exact NDA
- Establish that both parties accepted exactly the same version
- Record execution timestamp
- Lock certain agreed parameters
- Create an immutable audit trail of subsequent actions



All blueprints are based on international principles of law that are generally applied across jurisdictions. This is not legal advice nor tailored contracts - if you require legal assistance, please contact qualified counsel. Contributions are very welcome - feel free to add deep dive readmes, new contract types or specific jurisdictions that regulate the topic differently.

Hopefully this will make us a little less scared of talking legalese. This is a live repo, so watch this space for new things to be added up!
