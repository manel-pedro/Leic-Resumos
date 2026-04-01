### Trusted Computing Base
* CA must fix and validate all data referred to in the certificate
    * Bob’s identity + Bob’s public key
    * Specific CA information: CA identity and PKC serial number
    * Validity (start date and validation date)

* CA signs digital document with this information


### Verifying Certificates
Context - Bob sends Alice a certificate with:
* Bob’s identity and pkB
* Validity period (start date and validation)
* Additional metadata
* Signed with a CA trusted by Alice

Step-by-step verification by Alice
* Purely technological:
    * Verify if Bob’s key and identity matches the certificate
    * Verify if the current time is within validity window
    * Verify metadata (depends on the application’s needs)
* Solved by relying on PKIs:
    * Verify if the CA is trusted
    * Obtain pkCA and verify the certificate’s signature

