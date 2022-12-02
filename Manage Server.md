# Manage Server Through SSH

### Log into server through ssh
`ssh -i prinsiri-web-server.pem ubuntu@18.139.106.113`  
Note:
- username: ubuntu  
- Ip: 18.139.106.113  
- pem file: prinsiri-web-server.pem  


### Update applications in the server
```
sudo apt update
sudo apt upgrade
```

### Navigate to root directory  
`cd /`

### Create keys  
`ssh-keygen -t rsa`  
Note: create keys on local machine and copy it to the server


## Generate CSR (Prerequisite for SSL Certificate)  
  
### Create CSR on the server (do this while on the server)  
`openssl req -newkey rsa:2048 -nodes -keyout prinsiri.com.key -out prinsiri.com.csr`

### view the csr file
`cat prinsiri.com.csr`

More information about commands: 
https://gist.github.com/bradtraversy/f03df587f2323b50beb4250520089a9e



## Installing SSL Certificate

1. Convert private key file to pem file (this file is usally located in the server)  
`openssl rsa -in prinsiri.com.key -out prinsiri.com.pem`

2. Convert crt or cer files to pem files  
`openssl x509 -in www_prinsiri_com_94312292www_prinsiri_com.crt -out www_prinsiri_com_94312292www_prinsiri_com.pem -outform PEM`

3. Upload certificates to server  
Template/example
```
aws iam upload-server-certificate --server-certificate-name ExampleCertificate
                                    --certificate-body file://Certificate.pem
                                    --certificate-chain file://CertificateChain.pem
                                    --private-key file://PrivateKey.pem
```

Actual
```
aws iam upload-server-certificate --server-certificate-name Thawte_Certificate --certificate-body file://www_prinsiri_com_94312292www_prinsiri_com.pem --certificate-chain file://My_CA_Bundle.ca-bundle.pem --private-key file://prinsiri.com.pem

```

Note: The original CSR file and private key are stored in in the home directory inside csr_privatekey folder (On the server)



## Creating a New User

1. SSH into EC2 instance
2. Create user `$ sudo adduser new_user --disabled-password`
4. Switch to new user `$ sudo su - new_user`
5. Create folder and name it .ssh `$ mkdir .ssh`
6. Create a file names authorized_keys `$ touch .ssh/authorized_keys`
7. Change .ssh folder permissions so that only this user can read, write or open it `chmod 700 .ssh'
8. Change authorized_keys file permissions so that only this user can read or write it `$ chmod 600 .ssh/authorized_keys`
9. Generate key pair using the AWS GUI as mentioned in below section
10. Create public key from the private key `openssl rsa -in mykey.pem -pubout > mykey.pub`
11. Copy the contents of 'mykey.pub' from the above step, to authorized_keys file: `$ cat >> .ssh/authorized_keys`, and paste it at the end (ctrl-d to finish). Or use `nano .ssh/authorized_keys` and past it and save it (ctrl-s -> ctrl-x)


Links 
 - https://aws.amazon.com/premiumsupport/knowledge-center/new-user-accounts-linux-instance/
 - https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/managing-users.html
 - https://www.devco.net/archives/2006/02/13/public_-_private_key_encryption_using_openssl.php
