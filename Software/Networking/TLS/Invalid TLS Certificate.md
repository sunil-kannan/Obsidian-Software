---
date: 2024-09-27
tags: 
link: "[[Networking]]"
---

# Invalid TLS Certificate

> If your website is showing as "not secure" despite adding security measures like HTTPS or TLS certificates, a few common reasons might explain this:

1. **Expired or Invalid Certificate**: Ensure that your certificate is still valid. Certificates have an expiration date, and if expired, browsers will show the site as insecure.
    
2. **Self-Signed Certificates**: If you're using a self-signed certificate (rather than one from a trusted Certificate Authority), browsers will mark the connection as insecure because they don't trust the certificate issuer.
    
3. **Mixed Content**: If your website loads assets (like images, scripts, or stylesheets) over HTTP instead of HTTPS, browsers will flag this as a security risk. Ensure all resources are loaded over HTTPS.
    
4. **Certificate Configuration Issues**: Check that the certificate is correctly installed and configured for all domains (including subdomains). Some websites have issues if the certificate isn't covering all relevant domain names.
    
5. **CA Not Trusted**: If the Certificate Authority (CA) that issued your TLS certificate is not trusted by the browser, this could result in a "not secure" message.
    
6. **Intermediate Certificates Missing**: Sometimes, an incomplete certificate chain (missing intermediate certificates) can cause the site to appear insecure.

## Without TLS Certificate Https is not possible 

If there is no TLS certificate at all or if the certificate is completely invalid, the connection cannot be established as HTTPS. Browsers will treat the site as an unsecured HTTP connection and will not encrypt the data being transferred. Users will typically see a warning that indicates the site is not secure.

## Https is possible incase if the TLS is expired

If a TLS certificate has expired, the connection can still technically be established as HTTPS, but the browser will warn users that the certificate is not valid. Users may see messages indicating that the connection is insecure, and many modern browsers will block access to the site entirely until the certificate is renewed. Therefore, while HTTPS may be in place, it is not effectively secure without a valid certificate.