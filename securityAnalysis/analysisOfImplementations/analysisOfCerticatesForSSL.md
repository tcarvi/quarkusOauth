## Como configurar uma requisição HTTP com protocolo (HTTPS+TLS_1_1) e com certificados do cliente?

Conforme especificação "The OAuth 2.0 Authorization Framework" ([RFC6749](https://datatracker.ietf.org/doc/html/rfc6749))
- ***TLS Version***
  - Whenever Transport Layer Security (TLS) is used by this specification, the appropriate version (or versions) of TLS will vary over time, based on the widespread deployment and known security vulnerabilities.
  - At the time of this writing, TLS version 1.2 [RFC5246] is the most recent version, but has a very limited deployment base and might not be readily available for implementation.
  - TLS version 1.0 [RFC2246] is the most widely deployed version and will provide the broadest interoperability.
  - Implementations MAY also support additional transport-layer security mechanisms that meet their security requirements.
- Em resumo, ***Para OAuth 2, implementações do "Authorization Server" devem, no mínimo, aceitar requisições HTTP criadas com autenticação TLS 1.0.***
- Implemento análise sobre este protocolo de comunicação e indico forma de se configurar a requisição HTTP com o parâmetro SSLContext.
- Busco identificar a forma correta de se configurar o HttpClient e o HttpRequest para se usar o TLS 1.0.
  - Não há qualquer tipo de "informação sigilosa" nesta implementação. Apenas busco codificar corretamente o protocolo TLS 1.0. 

- Classes Java11:
  - Classe: HttpClientBuilder
    - https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.Builder.html. 
    ```shell. 
    HttpClient client = HttpClient.newBuilder()   
        .version(Version.HTTP_1_1)  
        .followRedirects(Redirect.NORMAL)  
        .connectTimeout(Duration.ofSeconds(20))  
        .sslContext(sslContextObject)
        .proxy(ProxySelector.of(new InetSocketAddress("proxy.example.com", 80)))  
        .authenticator(Authenticator.getDefault())  
        .build();   
    ```
  - Método: HttpClientBuilder.sslContext
    - https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.Builder.html#sslContext(javax.net.ssl.SSLContext). 
    ```shell  
    Assinatura: (HttpClient.Builder builder).sslContext(SSLContext sslContext)  
    Sets an SSLContext  
    If this method is not invoked prior to building, then newly built clients will use the default context, which is normally adequate for client applications that do not need to specify protocols, or require client authentication  .
    Parameters: sslContext - the SSLContext  
    Returns: this builder  
    ``` 
  - Classe: SSLContext
    - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/javax/net/ssl/SSLContext.html
    ```shel  
    // Creates an SSLContext object  
    SSLContext sslContextobject = new SSLContext(SSLContextSpi contextSpi, Provider provider, String protocol)  
    ```  
  - Método: SSContext (constructor)
    ```shell  
    Assinatura: protected SSLContext​(SSLContextSpi contextSpi, Provider provider, String protocol)
    Creates an SSLContext object.
    Parameters:
        contextSpi - the delegate
        provider - the provider
        protocol - the protocol
    ``` 
  - Método: SSLContext.init
    - https://docs.oracle.com/en/java/javase/11/docs/api/java.base/javax/net/ssl/SSLContext.html#init(javax.net.ssl.KeyManager%5B%5D,javax.net.ssl.TrustManager%5B%5D,java.security.SecureRandom)
    ```shel  
    Assinatura: public final void init​(KeyManager[] km, TrustManager[] tm, SecureRandom random) throws KeyManagementException
    Initializes this context. Either of the first two parameters may be null in which case the installed security providers will be searched for the highest priority implementation of the appropriate factory. Likewise, the secure random parameter may be null in which case the default implementation will be used.
    Only the first instance of a particular key and/or trust manager implementation type in the array is used. (For example, only the first javax.net.ssl.X509KeyManager in the array will be used.)
    Parameters:
        km - the sources of authentication keys or null
        tm - the sources of peer authentication trust decisions or null
        random - the source of randomness for this generator or null
    Throws:
        KeyManagementException - if this operation fails
    ``` 
  - SSLContext.setDefault
    - url
    ```shell
    Assinatura: public static void setDefault​(SSLContext context)
    Sets the default SSL context. It will be returned by subsequent calls to getDefault(). The default context must be immediately usable and not require initialization.
    Parameters:
        context - the SSLContext
    Throws:
        NullPointerException - if context is null
        SecurityException - if a security manager exists and its checkPermission method does not allow SSLPermission("setDefaultSSLContext")
    ```
  - HttpClient:
    - https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html  
    ```shell
       HttpClient client = HttpClient.newBuilder()  
        .version(Version.HTTP_1_1) 
        .followRedirects(Redirect.NORMAL)  
        .connectTimeout(Duration.ofSeconds(20))  
        .proxy(ProxySelector.of(new InetSocketAddress("proxy.example.com", 80)))  
        .authenticator(Authenticator.getDefault())  
        .build();   
    ```
