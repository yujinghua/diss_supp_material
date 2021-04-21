# Unit test specificatipn of dllRSAPrivateDecrypt & dllRSAPublicEncrypt

## 3 TG_dllRSAPrivateDecrypt
### 3.1 TC_dllRSAPrivateDecrypt_normal 
Purpose: To check the function behaviors when an invalid cipher name is input
Test setup: cipher text = "45ea2de117fb55ee22578b58a7251abcb725b6c9d75eea2a7080dbafe1195370120c45e9e70169d8e987c7ece01c6cf76e4b1be884dad7a1e050a5b7f7ed9485b12ff58386b6f02a2cccf6244c2d08828bffaa5d689f952c420bad6438e432934d72a3a6a3e50217dbcaee1eb1f08b167deca114a9fdeec9ff6e9dcbde647eed”; cipher text length = 128; priKeyFile = "C:\\Userspath\\capl_dll_sec\\RSAKeyPair\\rsa_prikey.pem";
Sub test cases 1: Normal operation

- input: /
- expected output: plain text = “Hello World!”; plain text length = 12;
- expected return: error code = 1 (operation succeeds)

### 3.2 TC_dllRSAPrivateDecrypt_priKeyFile 
Purpose: To check the function behaviors when various key files are input
Test setup: cipher text = "45ea2de117fb55ee22578b58a7251abcb725b6c9d75eea2a7080dbafe1195370120c45e9e70169d8e987c7ece01c6cf76e4b1be884dad7a1e050a5b7f7ed9485b12ff58386b6f02a2cccf6244c2d08828bffaa5d689f952c420bad6438e432934d72a3a6a3e50217dbcaee1eb1f08b167deca114a9fdeec9ff6e9dcbde647eed”; cipher text length = 128; 
Sub test cases 1: Correct private key

- input: priKeyFile = "C:\\correctpath\\rsa_prikey.pem";
- expected output: plain text = “Hello World!”; plain text length = 12;
- expected return: 1 (operation succeeds)

Sub test cases 2: Wrong private key file path

- input: priKeyFile = "C:\\wrongpath\\rsa_prikey.pem";
- expected output: /
- expected return: 0 (operation is abort)

Sub test cases 3: Wrong private key file

- input: priKeyFile = "C:\\correctpath\\rsa_prikey_wrong.pem";
- expected output: /
- expected return: 0 (operation is abort)

Sub test cases 4: null private key file path

- input: priKeyFile = "";
- expected output: /
- expected return: 0 (operation is abort)

### 3.3 TC_dllRSAPrivateDecrypt_priKeyFile_pw 

### 3.4 TC_dllRSAPrivateDecrypt_in_cipher 

### 3.5 TC_dllRSAPrivateDecrypt_in_cipherlen_wrong 


## 4 TG_dllRSAPublicEncrypt
### 4.1 TC_dllRSAPublicEncrypt_normal 

### 4.2 TC_dllRSAPublicEncrypt_pubKeyFile

### 4.3 TC_dllRSAPublicEncrypt_in_plaintext 

### 4.4 TC_dllRSAPublicEncrypt_in_plainlen\_wrong 
