# AES-openssl-creating-certificate
<!-- heading -->
## 1. Creating directory CA with Sub-CA and Root-CA

Firstly let us start by creating a directory **ca** consisting  of **root-ca**, **sub-ca** and **server** . Each of these sub-directories will contain:
* **private key**
* **certs** (certificate)
* **newcerts** (new certificate)
* **crl** (certificate revocation list)
* **csr** (certificate signing request)

```
mkdir -p ca/{root-ca,sub-ca,server}/{private,certs,newcerts,crll,csr}
```
___
