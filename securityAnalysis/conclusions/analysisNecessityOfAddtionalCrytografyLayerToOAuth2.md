## Planning of Implementation:
    - If we follow OAuth2 correctly, we shouldn't have problems with what is defined in the specification.
    - But, during Grant Authentication, we can't loose control over "client_id" and "client_secret" variables.
    - So, we must criate an ADDITIONAL AND INDEPENDENT LAYER OF SECURITY to protect these variables.
    - If we implement OAuth2 correctly and if we protect our network AND THESE VARIABLES, we should have a secure implementation.
    - Following OAuth 2.0, we must, of course, pay attention to its RFC6819 "Threat Model and Security Considerations".
    - And we must make analysis of possible unsecure scenarios like the ones presented in https://arxiv.org/abs/1601.01229.

### Etapa 1 da Implementação:
- Seguir fluxo básico de OAuth2 para a autenticação, mas com "***authorization code grant"***.

### Etapa 2 da Implementação: (melhoria depois da implementação básica)
- Uso de critografia, para armazenar e usar as variáveis "client_id" e "client_secret". 
- [Java Cryptography Architecture (JCA) Reference Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html)

### Etapa 3 da Implementação: (melhoria depois da implementação básica)
- Atenção aos possíveis ataques indicados em [OAuth 2.0 Threat Model and Security Considerations](https://datatracker.ietf.org/doc/html/rfc6819.html)
- Compreensão e uso do que foi analisado em [A Comprehensive Formal Security Analysis of OAuth 2.0](https://arxiv.org/abs/1601.01229), escrito por Daniel Fett, Ralfk Küsters e Guido Schmitz.