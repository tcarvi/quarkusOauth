## Basic idea
    - If we follow OAuth2 correctly, we shouldn't have problems with what is defined in the specification.
    - But, during Grant Authentication, we can't loose control over "client_id" and "client_secret" variables.
    - So, we must criate an ADDITIONAL AND INDEPENDENT LAYER OF SECURITY to protect these variables.
    - If we implement OAuth2 correctly and if we protect our network AND THESE VARIABLES, we are secured.
    - Following OAuth 2.0, we must, of course, pay attention to its RFC6819 "Threat Model and Security Considerations" too.

### Java Cryptography Architecture (JCA) Reference Guide
- https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html