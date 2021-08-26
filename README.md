# pycryption

Dockerized Python Encryption

### PLEASE NOTE 
#### You can use `raze.png` OR `document.txt` for Encryption 
#### If you wish to use your own files for encryption, you need to move them to this directory, and add this line to Dockerfile 
#### `COPY filename.ext .`

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 1 -> Build The Docker Image

  ```sh
  docker build -t pycryptor .
  ```



---------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 2 -> Start The Docker Container

### PLEASE NOTE
#### Before running the below docker command, make sure to replace '/my/dir' with the path of the directory where you want to have the Keys & Encrypted/Decrypted files
  ```sh
  docker run -d --name pycryption -v /my/dir:/usr/src/app -ti pycryptor
  ```
### Example 
  ```sh
  docker run -d --name pycryption -v /home/playground/Bloom/pycryptor:/usr/src/app -ti pycryptor
  ```

---------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 3 [RECEIVER] -> Creating Public And Private Keys For Receiver

  ```sh
  docker exec -it pycryption python create_keys.py
  ```

### *** RECEIVER'S PUBLIC KEY IS SHARED TO THE SENDER ***
#### Only `publickey.key` is shared
#### `privatekey.key` is not shared 

---------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 4 [SENDER] -> Sender Encrypts & Signs The File

#### 1. Perform Symmetric Encryption on the file you choose
#### 2. Symmetric Key is encrypted using Receiver's Public Key
#### 3. Create Public & Private Keys for Sender
#### 4. Encrypted data is signed using Sender's Private Key

  ```sh
  docker exec -it pycryption python encrypt.py
  ```
#### When Prompted, Enter name of document to be encrypted [with extension] 
#### Example: `raze.png` OR `document.txt`  `[filename.ext]`

### *** 4 FILES ARE SHARED TO RECEIVER ***
#### *** ENCRYPTED FILE ***  `enc_raze.png` OR `enc_document.txt` `[enc_filename.ext]`
#### *** ENCRYPTED SYMMTERIC KEY *** `encrypted_key`
#### *** SENDER'S PUBLIC KEY *** `public_verify.key`
#### *** SIGNATURE *** `sign.txt`

---------------------------------------------------------------------------------------------------------------------------------------------------------------------


## Step 5 [RECEIVER] -> Receiver Decrypts File & Verifies The Signature

#### 1. Encrypted data is verified using Sender's Public Key
#### 2. Encrypted Symmetric Key is decrypted using Receiver's Private Key
#### 3. Decrypting the encrypted file using symmetric key

  ```sh
  docker exec -it pycryption python decrypt.py
  ```

#### When Prompted, Enter name of document to be decrypted [with extension] 
#### Example: `enc_raze.png` OR `enc_document.txt` `[enc_filename.ext]`

### You can check the decrypted files 
### Example: `decrypted_enc_raze.png` OR `decrypted_enc_document.txt` `[decrypted_enc_filename.ext]`

---------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 6 [RECEIVER/SENDER] -> Stop The Container 
  ```sh
  docker stop pycryption
  ```


---------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Step 7 [RECEIVER/SENDER] -> Remove The Container & Image
### Remove the Container
  ```sh
  docker rm pycryption
  ```

### Remove the Image
  ```sh
  docker rmi pycryptor
  ```

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
