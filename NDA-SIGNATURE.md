// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

/// @title **Unilateral NDA Contract**
/// @author claracam
/// @notice Enables Ethereum users to digitally sign a predefined unilateral NDA
/// @dev This contract refers to the NDA document stored in the same GitHub repo/branch

contract NDASignature {

    address public owner;
    string public ndaDocumentHash; // Hash or reference to the NDA (see README for full version)
    string public documentVersion;

    mapping(address => Signature) public signatures;

    struct Signature {
        uint256 timestamp;
        string name;
        string title;
        bool signed;
    }

    event NDASigned(address indexed signer, string name, string title, uint256 timestamp);

    modifier onlyOnce() {
        require(!signatures[msg.sender].signed, "NDA already signed by this address");
        _;
    }

    /// @notice Contract constructor
    /// @param _ndaDocumentHash Keccak256 or IPFS hash of the NDA text
    /// @param _documentVersion Version identifier of the NDA
    constructor(string memory _ndaDocumentHash, string memory _documentVersion) {
        owner = msg.sender;
        ndaDocumentHash = _ndaDocumentHash;
        documentVersion = _documentVersion;
    }

    /// @notice Sign the NDA by providing name and title
    /// @param name Full name of the signer
    /// @param title Title/role of the signer
    function signNDA(string calldata name, string calldata title) external onlyOnce {
        signatures[msg.sender] = Signature({
            timestamp: block.timestamp,
            name: name,
            title: title,
            signed: true
        });

        emit NDASigned(msg.sender, name, title, block.timestamp);
    }

    /// @notice Checks if an address has signed the NDA


## Legal Commentary

The smart contract above facilitates digital acknowledgment of the attached unilateral NDA. You can deploy the contract with ndaDocumentHash: use the keccak256 hash of the NDA text or store the full PDF on IPFS and use the CID.

The NDA template is attached [here](./Unilateral-NDA.docx).


**Claracam's legal notes:**
- This is a UNILATERAL ⬅️ contract. This means that only one of the parties has to commit to keeping secret, not the other. And why, may you ask? Because in some cases only one of the parties is about to share sensitive information with the other, and not vice versa.
- > i.e. Service providers who work on integrations or dev work of a company. The company opens up its entire code and infrastructure to the service provider, who in turn doesn't have to disclose any of their internal data to the company.
- If you want a BILATERAL ↔️ contract, leave a comment and I'll provide.
- Digital signature is not always accepted as a valid form of signing. It depends on the jurisdiction and the type of contract. 
- > i.e. In Germany, employment contracts must be signed in wet ink by both the employer and the employee. It's not the case for freelancers, who can have an electronically signed contract.
- However, NDAs are a private contract that does not have minimum requirements under general law. This means that the content and validity of the contract is essentially up to the parties, so as long as they both accept the contract as valid, it is. ✅
- If any of the parties wanted to contest it, a court would look into conversations between the parties that happened around the time of signing, parties' behaviour and other signs of whether the contesting party did act assuming that the contract was valid - in which case, he/she cannot contest it now. 👩🏻‍⚖️
- Timestamped signing on-chain is verifiable but not equivalent to notarization. This is the same for e-signing platforms such as DocuSign, HolaSign, DropboxSign, etc.
