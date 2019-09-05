---
github: Learn_Groovy
---
<kbd class="imgtitle">Contents</kbd>

1. [Objective](#objective)
1. [Important Points](#important-points)
1. [Simple Steps](#simple-steps)
1. [Certificates and Managers](#certificates-and-managers)
1. [Using CLI](#using-cli)
1. [References](#references)
{: .contentBorder .txt-pad}

### Objective

Getting **HttpsURLConnection** successfully using the <mark>SSL Certificates</mark> is the ultimate aim. After a long struggle
i came up with this post which is very useful for those who are all looking for this and may have all the files or some of the files
which are listed below.

- SomeThing-CA.crt 
- SomeThing.crt
- SomeThing.key
- SomeThing.jks
- SomeThing.p12 or SomeThing.pfx
- SomeThing.pem
- SomeThing.csr 

These are Certificate file formats often confuses the person who is novice. This post explains the basic and easy way to get connected HTTPS url
with small work around.

### Important Points

- Ultimately you only need <mark>SomeThing-CA.crt</mark>, <mark>SomeThing.crt</mark> and <mark>SomeThing.key</mark>.
- Other formats are combined (or) converted form of this 3 basic certificates.
- <mark>SomeThing-CA.crt</mark> needs to be added inside the **Trust Store** of user machine.
- The Other two ( <mark>SomeThing.crt</mark> and <mark>SomeThing.key</mark>) needs to be added inside the **Key Store**.
 
### Simple Steps

**Step 1** : Create a *p12* or *pfx* from *.key* and *.crt* using the command,
So the created file **SomeThing.pfx** normally contains the all three files inside it in binary form.

**Step 2** : Create a **KeyStore** in the instance of <mark>JKS</mark> for the **TrustManager** and load the Certificate **SomeThing-CA.crt**
in to the true store.

**Step 3** : Create a **KeyStore** in the instance of <mark>PKCS12</mark> for the **KeyManager** and load the Certificate **SomeThing.pfx**
in to the key store.

**Step 4** : Load these Two Managers (TrustManager, KeyManager) to the *SSLContext* and the *SocketFactory* for the HttpsURLConnection

**Step 5** : Now We can use the *HttpsURLConnection* and set the SSLFactory from the certificate generated.

These steps are now implemented in normal Java / Groovy code to get the <mark>SSLSocketFactory</mark>.

**Step 1 : openssl command to export as pfx file**

```
openssl pkcs12 -export -in SomeThing.crt -inkey SomeThing.key -out SomeThing.pfx -certfile  SomeThing-CA.crt
```

**Step 2 : Getting Trust Manager**

```groovy
String caCertPath = "/path/to/SomeThing-CA.crt";
String certPath = "/path/to/SomeThing.crt";
String passWord = "changeit";

private Certificate getCertificate (String path) throws Exception
{
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    InputStream caInput = new FileInputStream(new File(path));
    Certificate c = cf.generateCertificate(caInput);
    caInput.close();
    return c;
}
private TrustManager [] getTrustManagers() throws Exception
{
    KeyStore tKeyStore = KeyStore.getInstance("JKS")      
    tKeyStore.load (null, null);
    tKeyStore.setCertificateEntry ("CA-Cert", getCertificate (caCertPath));
    TrustManagerFactory tmf = TrustManagerFactory.getInstance (TrustManagerFactory.getDefaultAlgorithm());
    tmf.init (tKeyStore);
    return tmf.getTrustManagers();
}
```

**Step 3 : Getting Key Manager**

```groovy
private KeyManager [] getKeyManagers() throws Exception
{
    KeyStore keyStore = getPKCSKeyStore();
    keyStore.load (new FileInputStream(new File(certPath)), passWord.toCharArray());
    KeyManagerFactory kmf = KeyManagerFactory.getInstance (KeyManagerFactory.getDefaultAlgorithm());
    kmf.init (keyStore, passWord.toCharArray());
    return kmf.getKeyManagers();
}
```

**Step 4 : Getting SocketFactory**

```groovy
SSLSocketFactory getSocketFactory(){
    SSLContext sslContext = SSLContext.getInstance("TLS");
    sslContext.init(getKeyManagers(), getTrustManagers(), new SecureRandom());
    return sslContext.getSocketFactory();
}
```

**Step 5 : Creating HttpsURLConnection**

```groovy
HttpsURLConnection connection = (HttpsURLConnection) new URL(u).openConnection()
connection.setSSLSocketFactory getSocketFactory()
```

### Certificates and Managers

Formats of certificate files shown below,

> **.crt .cer .der .p12 .jks .pfx .pem .key**

In these formats, **.crt** and **.key** are the primary formats from which other all can be generated using 
**openssl** command. 

<img src="/images/certificates.png" style="width:50%"/>

The types of managers used are,

- Trust Manager / Store
- Key Manager / Store

Those files which are all added in **KeyStore**, the related CA-Certificate need to be added in **Trust Store**.
Generally **$JAVA_HOME/jre/lib/security/cacerts** is the basic jre's trust store. you can add a certificate using command line like
shown below,

```
keytool -importcert -file SomeThing.crt -keystore $JAVA_HOME/jre/lib/security/cacerts -storepass changeit
``` 

If you skip this or didn't added the **CA-Certificate** inside the trust store, you will get the exception as,

> sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target.

In another method, By setting the values in System Property can solve the issue but <mark>Not Recommended</mark>.

The related System properties need to be assigned are,

```groovy
System.setProperty("javax.net.debug", "ssl")
System.setProperty("javax.net.ssl.trustStore", "$JAVA_HOME/jre/lib/security/cacerts")
System.setProperty("javax.net.ssl.trustStorePassword", "changeit") // commonly used password
System.setProperty("javax.net.ssl.trustStoreType", "JKS")
System.setProperty("javax.net.ssl.keyStoreType", "PKCS12")
System.setProperty("javax.net.ssl.keyStore", "/path/to/SomeThing.pfx")
System.setProperty("javax.net.ssl.keyStorePassword", "password_created_for_pfx")
```

These init process need be done before doing openConnection in java code.

### Using CLI

These connection can be implemented with normal **curl** command like shown below,

```
curl -k https://url/path --cacert /path/to/SomeThing-CA.crt --cert /path/to/SomeThing.crt  --key /path/to/SomeThing.key  
```

or even without using trust store certificate, we can connect by only **.crt** and **.key** files in curl

```
curl -k https://url/path --cert /path/to/SomeThing.crt  --key /path/to/SomeThing.key  
```

### References
---

Thanks to the references...
    - [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority)
    - [java-client-certificates-over-https-ssl](https://stackoverflow.com/questions/875467/java-client-certificates-over-https-ssl)
    - [SSL Converter](https://www.httpcs.com/en/ssl-converter)
{: .refbox}