# AES256-openssl-creating-certificate

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
<img src="./images/tree1.png" alt="drawing" width="300"/>

And if this doesn't appear then **install tree** on your system , by running this command: 
```
sudo apt install tree  
```
Now again try the same command `tree ca`
___
## 2. Making the **private** named directory *private*
>  chmod 700 Protects a file against any access from other users, while the issuing user still has full access.
```
chmod -v 700 ca/{root-ca,sub-ca,server}/private
```
<img src="./images/chmod.png" alt="drawing" width="600"/>

## 3. Creating index file
The index file will be only needed to *root-ca* and *sub-ca*. The sub-ca is intermediate certificate authority authorized by the parent root.
```
touch ca/{root-ca,sub-ca}/index
```
## 4. Making serial files for **root-ca** and **sub-ca**
Serial entries are the files that we need while issuing and signing certificate requests.
```
openssl rand -hex 16 > ca/root-ca/serial
openssl rand -hex 16 > ca/sub-ca/serial
```
 > Again run `tree ca` to see the structure of files.

 > The public key of a server would be signed by a trusted certificate auhtority to have a trusted relationship with it and as his clients we would automatically trust any server that have been signed with the trusted key.
 ## 5. Time to create **private key** for **root-ca** and we'll use **AES256** for encryption.
 >AES algorithm is considered to be quite safe.
 ```
 cd ca
 openssl genrsa -aes256 -out root-ca/private/ca.key 4096
 ```
 Now you will be asked to enter a pass phrase which is a part of our encryption . So type a solid pass phrase and don't forget it as it will be used further too. Then press enter and rewrite again to verify.
 * this will look something like this :
<img src="./images/privateroot_ca.png" alt="drawing" width="900"/>
>4096 is the length of bits of the private key of root-ca.

Again follow the same step for making the private-key for sub-ca.
```
openssl genrsa -aes256 -out sub-ca/private/sub-ca.key 4096
 ```
Now we will do the same for server key but this time we will take key size of 2048 bits and we don't want any encryption system also.
>This is because the server will be dealing with the encrypted data all the time , so for reducing the load we'll be taking key of less size and we don't want to enter the pass phrase whenever the server starts, so we will not use AES encyption this time .
```
openssl genrsa -out server/private/server.key 2048
```
## 6. Time for **public key**
*public key* is going to be generated from *private key*.


