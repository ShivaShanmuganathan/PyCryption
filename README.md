# pycryption
Dockerized Python Encryption

## Step 1 -> BUILD THE DOCKER IMAGE

### `docker build -t pycryptor .`

## Step 2 -> START THE DOCKER CONTAINER


### Before running the below docker command, make sure to replace '/my/dir' with the path of the directory where you want to have the Keys & Encrypted/Decrypted files
### `docker run -d --name pycryption -v /my/dir:/usr/src/app -ti pycryptor`
### EXAMPLE 
### `docker run -d --name pycryption -v /home/playground/Bloom/pycryptor:/usr/src/app -ti pycryptor`


## Step 3 [RECEIVER] -> CREATING PUBLIC AND PRIVATE KEYS FOR RECEIVER

### `docker exec -it pycryption python create_keys.py`

### *** RECEIVER'S PUBLIC KEY IS SHARED TO THE SENDER ***

## Step 4 [SENDER] -> SENDER ENCRYPTS & SIGNS THE FILE

#### 1. Perform Symmetric Encryption on the file you choose
#### 2. Symmetric Key is encrypted using Receiver's Public Key
#### 3. Create Public & Private Keys for Sender
#### 4. Encrypted data is signed using Sender's Private Key

### `docker exec -it pycryption python encrypt.py`
### When Prompted, Enter name of document to be encrypted such as -> 'document.txt' OR 'raze.png'

### *** 3 FILES ARE SHARED TO RECEIVER ***
### *** ENCRYPTED FILE ***
### *** ENCRYPTED_SYMMTERIC_KEY ***
### *** SENDER'S PUBLIC KEY ***

## Step 5 [RECEIVER] -> RECEIVER DECRYPTS FILE & VERIFIES THE SIGNATURE

#### 1. Encrypted data is verified using Sender's Public Key
#### 2. Symmetric Key is decrypted using Receiver's Private Key
#### 3. Decrypting the encrypted file using symmetric key

### `docker exec -it pycryption python decrypt.py`
### When Prompted, Enter name of document to be decrypted -> [Example: 'enc_document.txt' OR 'enc_raze.png']

### You can check the decrypted files -> [Example: 'decrypted_enc_document.txt' OR 'decrypted_enc_raze.png']

## Step 6 [RECEIVER/SENDER] -> STOP THE CONTAINER 
### `docker stop pycryption`

## Step 7 [RECEIVER/SENDER] -> REMOVE THE CONTAINER & IMAGE
### Remove the Container
### `docker rm pycryption`

### Remove the Image
### `docker rmi pycryptor`
