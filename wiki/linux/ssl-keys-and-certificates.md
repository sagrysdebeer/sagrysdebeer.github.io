---
layout: wiki
title: ssl keys and certificates
---

### Relative Distinguised Name

Various interpretations of the RDN attributes exist, but these are commonly accepted:

C = ISO3166 two character country code

ST = state or province

L = Locality; generally - city

O = Organization - Company Name

OU = Organization Unit - typically certificate type or brand

CN = CommonName - typically product name/brand

### Generating keys, certs, and self-signing

Generate CA key:
```
openssl genrsa -out ca.key 4096
```

Generate CA certificate:
```
openssl req -new -x509 -days 7300 -key ca.key -out ca.crt -subj  "/C=ZA/ST=Western Cape/L=Cape Town/O=AcmeCompany/OU=IT/CN=AcmeCompanyCA"
```

Generate server key:
```
openssl genrsa -out server.key 4096
```

Generate signing request:
```
openssl req -new -key server.key -out server.csr -subj  "/C=ZA/ST=Western Cape/L=Cape Town/O=AcmeCompany/OU=IT/CN=whatever.acme.com"
```
or with an IP:
```
openssl req -new -key server.key -out server.csr -subj  "/C=ZA/ST=Western Cape/L=Cape Town/O=AcmeCompany/OU=IT/CN=1.2.3.4"
```

Self-sign certificate:
```
openssl x509 -req -days 7300 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt
```

Remember to chmod 600 the key files.

### Overriding ssl validation

##### python and requests library

Either add verify=false as a parameter to the get function, or set REQUESTS_CA_BUNDLE environment variable to the path to where the ca.crt file is located.

[python-requests](http://docs.python-requests.org/en/master/user/advanced/)

##### node.js

Can set the environment variable NODE_TLS_REJECT_UNAUTHORIZED to 0.

Better solutions:
- [Create server options](https://nodejs.org/api/tls.html#tls_tls_createserver_options_secureconnectionlistener)
- [Check server identity](https://nodejs.org/api/tls.html#tls_tls_checkserveridentity_host_cert)

