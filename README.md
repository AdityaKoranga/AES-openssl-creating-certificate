# AES-openssl-creating-certificate

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
Now if you will now run:  **`tree ca`** , then you will be able to see a structure like this:
<!-- ![image1](./images/Screenshot%20from%202022-05-02%2000-31-46.png) -->
<img src="./images/Screenshot%20from%202022-05-02%2000-31-46.png" alt="drawing" width="300"/>

And if this doesn't appear then **install tree** on your system , by running this command: 
```
sudo apt install tree  
```
Now again try the same command `tree ca`
___
## 2. Making the private named directory ,private
>  chmod 700 Protects a file against any access from other users, while the issuing user still has full access.
```
chmod -v 700 ca/{root-ca,sub-ca,server}/private
```
<img src="./images/Screenshot%20from%202022-05-05%2000-26-28.png" alt="drawing" width="600"/>

## 2. Creating index file
The index file will be only needed to *root-ca* amd *sub-ca*. The sub-ca
 