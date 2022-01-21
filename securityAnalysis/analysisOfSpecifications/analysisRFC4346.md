## Especificação "The Transport Layer Security (TLS) Protocol - Version 1.1"
- Apenas síntese de informações relevantes, para requisição HTTP de autenticação OAuth2, usando java Quarkus.
- https://datatracker.ietf.org/doc/html/rfc4346

- This document specifies Version 1.1 of the Transport Layer Security (TLS) protocol.  The TLS protocol provides communications security over the Internet.  The protocol allows client/server applications to communicate in a way that is designed to prevent eavesdropping, tampering, or message forgery.

#### Glossário:
- application protocol
  - An application protocol is a protocol that normally layers directly on top of the transport layer (e.g., TCP/IP).  Examples include HTTP, TELNET, FTP, and SMTP. 
- **Obs.:** 
  - Há uma camada de Transporte: TCP/IP, cujos protocolos possuem padrões e formas de específicas de comunicação.
  - Sobre esta camada, pode-se usar outra camada de padrões: uma camada de ***application protocol***.
  - Como exemplo de ***application protocol***, tem-se o HTTP. 
    - HTTP nomalmente usa a porta 80. (redirecionamento automático pelo browser)
  - O HTTP pode se apresentar com algumas mudanças de padrão, tendo mais segurança.
  - HTTPS é isso: um ***application protocol*** similar a HTTP, mas com o acréscimo de padrões mais seguros.
    - HTTPS nomalmente usa a porta 443. (redirecionamento automático pelo browser)
  - O SSL representa este acréscimo de segurança.
    - O TSL representa uma atualização do SSL em que se tem padrões ainda mais seguros.
  - Em resumo, o (HTTPS+TSL) é um protocolo de comunicação que se apresenta na camada de ***application protocol*** sobre a camada de TCP/IP.
  -  O que é relevante saber, para implementação Java Quarkus?
    - Para requisições (HTTPS+TSL), deve-se criar um HttpClient indicando um SSLContext configurado, no mínimo, com os padrões TLS 1.0. Esta análise busca explicar como configurar corretamente uma instância de SSLContext. Depois basta usar, na sua implementação do OAuth2, a sua instância do SSLContext.

- For historical reasons and in order to avoid a profligate consumption of reserved port numbers, application protocols that are secured by TLS 1.1, TLS 1.0, SSL 3.0, and SSL 2.0 all frequently share the same connection port.  For example, the https protocol (HTTP secured by SSL or TLS) uses port 443 regardless of which security protocol it is using.  Thus, some mechanism must be determined to distinguish and negotiate among the various protocols.
