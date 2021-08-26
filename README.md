# pycryption
Dockerized Python Encryption

## Step 1

## `docker build -t pycryptor .`

## Step 2

Before running the below docker command, make sure to replace '/my/dir' with the path of the directory where you want to have the Keys & Encrypted/Decrypted files

## `docker run -d --name pycryption -v /my/dir:/usr/src/app -ti pycryptor`

### EXAMPLE -> `docker run -d --name pycryption -v /home/playground/Bloom/pycryptor:/usr/src/app -ti pycryptor`


## Step 3 [RECEIVER'S SIDE]
### Create Public & Private Keys for Receiver
docker exec -it pycryption python create_keys.py

## ---- RECEIVER'S PUBLIC KEY IS SHARED TO THE SENDER ----

## Step 4 [SENDER'S SIDE]

### Perform Symmetric Encryption on the file you choose
### Symmetric Key is encrypted using Receiver's Public Key
### Create Public & Private Keys for Sender
### Encrypted data is signed using Sender's Private Key

## `docker exec -it pycryption python encrypt.py`
## Enter name of document to be encrypted such as -> 'document.txt' OR 'raze.png'


## ---- ENCRYPTED FILE, ENCRYPTED_SYMMTERIC_KEY AND SENDER'S PUBLIC KEY ARE SHARED TO THE RECEIVER ----

## Step 5
### Encrypted data is verified using Sender's Public Key
### Symmetric Key is decrypted using Receiver's Private Key
### Decrypting the encrypted file using symmetric key

## `docker exec -it pycryption python decrypt.py`
## Enter name of document to be decrypted -> [Example: 'enc_document.txt' OR 'enc_raze.png']

## You can check the decrypted files -> [Example: 'decrypted_enc_document.txt' OR 'decrypted_enc_raze.png']
