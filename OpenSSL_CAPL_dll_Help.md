# OpenSSL_CAPL.dll Help File
OpenSSL_CAPL.dll is a CAPL dll file supported by the CANoe environment. It acts as the interface for calling OpenSSL algorithms in CANoe.

# List
* [dllSymmetryEncrypt](#dllSymmetryEncrypt)
* [dllSymmetryDecrypt](#dllSymmetryDecrypt)
* [dllRSAPublicEncrypt](#dllRSAPublicEncrypt)
* [dllRSAPrivateDecrypt](#dllRSAPrivateDecrypt)

### dllSymmetryEncrypt

**Definition**
Item|Content
----|------- 
Class | CryptoBasis 
Function Name| dllSymmetryEncrypt
Syntax|dword dllSymmetryEncrypt (char[] ciphername, byte[] aKey, byte[] iVec, byte[] in, long inlen, byte[] out, long& poutlen)
Description|This function encrypts the string by the specified symmetry encryption algorithm.
Parameters| - ciphername: the name of the encryption algorithm. (supported algorithms see todo ）<br> - aKey: symmetry envryption key <br> - iVec: iv value <br> - in: input plain text <br> - inlen: length of the plain text <br> - out: output cipher text <br> - poutlen: length of the cipher text
Return Values| Return 1 if no error occurs. |

**Example Codes**
 ```
  char ciphername[32] = "aes-128-cbc";
  byte plaintext[64];
  byte ciphertext[64];
  byte decryptedtext[64];
  byte akey[64];
  byte iv[16];
  long plainlen, cipherlen, decryptedlen;
 
  int len, i;
  char plaintextStr[133]; //64*2+5
  char ciphertextStr[133];
  char decryptedtextStr[133];
  char akeyStr[133]; //64*2+5
  char ivStr[37]; //16*2+5
  char tmpC[3];
  
 // clear the byte array before a new round start
  for(i = 0; i < elCount(plaintext); i++){plaintext[i] = 0;} 
  for(i = 0; i < elCount(ciphertext); i++){ciphertext[i] = 0;} 
  for(i = 0; i < elCount(decryptedtext); i++){decryptedtext[i] = 0;} 
  //for(i = 0; i < 64; i++){akey[i] = 0x00;} //clean akey
  //for(i = 0; i < 16; i++){iv[i] = 0x00;} //clean iv
  for(i = 0; i < elCount(plaintextStr); i++){plaintextStr[i] = 0;}
  for(i = 0; i < elCount(ciphertextStr); i++){ciphertextStr[i] = 0;}
  for(i = 0; i < elCount(decryptedtextStr); i++){decryptedtextStr[i] = 0;}
 
  //set the key
  for(i = 0; i < elcount(akey); i++){
    //akey[i] = random(256);
    //akey[i] = i;
    akey[i] = 'k';
    snprintf(tmpC, elcount(tmpC), "%02x", akey[i]);
    strncat(akeyStr, tmpC, (64*2+1));
  }
  write("akey = %s", akeyStr);
 
  //set the iv
  for(i = 0; i < elcount(iv); i++){
    //iv[i] = i;
    iv[i] = 'i';
    snprintf(tmpC, elcount(tmpC), "%02x", iv[i]);
    strncat(ivStr, tmpC, (16*2+1));
  }
  write("iv = %s", ivStr);
 
  //get plain text from sysvar
  sysGetVariableString( sysvar::Sender::TxText, plaintextStr, elcount(plaintextStr) ); 
  len = strlen(plaintextStr);
  plainlen = len;
  write("plainlen = %d", plainlen);
  write("plaintext = %s", plaintextStr);
  for(i = 0; i < len; i++){
    plaintext[i] = plaintextStr[i];
    //write("%x", plaintext[i]);
  }
 
  // encrypt plaintext
  dllSymmetryEncrypt(ciphername, akey, iv, plaintext, plainlen, ciphertext, cipherlen);
  write("cipherlen = %d", cipherlen);
  //print cipher text in hex
  for(i = 0; i < cipherlen; i++){ //
    //write("%d %x %c", i, ciphertext[i], ciphertext[i]);
    snprintf(tmpC, elcount(tmpC), "%02x", ciphertext[i]);
    strncat(ciphertextStr, tmpC, (cipherlen * 2 + 1)); //elcount(ciphertextStr)
  }
  write("%s", ciphertextStr);
 
  // decrypt ciphertext
  dllSymmetryDecrypt(ciphername, akey, iv, ciphertext, cipherlen, decryptedtext, decryptedlen);
  write("decryptedlen = %d", decryptedlen);
  //print decrypted test
  for(i = 0; i < decryptedlen; i++){
    decryptedtextStr[i] = decryptedtext[i];
    //write("%d %x %c", i, decryptedtext[i], decryptedtext[i]);
    //snprintf(tmpC, elcount(tmpC), "%02x", decryptedtext[i]);
    //strncat(decryptedtextStr, tmpC, (decryptedlen + 1));
  }
  write("decryptedtextStr = %s", decryptedtextStr);
 ```

### dllSymmetryDecrypt
**Definition**
Item|Content
----|------- 
Class | CryptoBasis
Function Name| dllSymmetryDecrypt
Syntax|dword dllSymmetryDecrypt (char[] ciphername, byte[] aKey, byte[] iVec, byte[] in, long inlen, byte[] out, long& poutlen)
Description|This function decrypts the string by the specified symmetry encryption algorithm.
Parameters| - ciphername: the name of the decryption algorithm. (supported algorithms see TODO <br> - aKey: symmetry envryption key <br> - iVec: iv value <br> - in: input cipher text <br> - inlen: length of the input cipher text <br> - out: output decrypted text <br> - poutlen: length of the output decrypted text 
Return Values| Return 1 if no error occurs. 

**Example Codes**
See dllSymmetryEncrypt- > Example Codes

### dllRSAPublicEncrypt
**Definition**
Item|Content
----|------- 
Class | CryptoBasis
Function Name | dllRSAPublicEncrypt
Syntax|dword dllRSAPublicEncrypt(byte plaintext[], long plainLen, char pubKeyFile[], byte ciphertext[], long* cipherLen)
Description|This function encrypts the input plaintext into the ciphertext by the RSA public key.
Parameters | - plaintext: input plaintext <br> - plainLen: length of the input plaintext <br> - pubKeyFile: path of the public key file(*.pem) <br> - ciphertext: the output cipher text <br> - cipherLen: the length of the output cipher text 
Return Values | Return 1 if no error occurs. 

**Example Codes**
```
byte plaintext[245];
  byte ciphertext[260];
  byte decryptedtext[245];
  char pubKeyFile[256] = "C:\\rsa_pubkey_pw.pem";
  char priKeyFile[256] = "C:\\rsa_prikey_pw.pem";
  char priKeyPW[256] = "1234";
  long plainlen, cipherlen, decryptedlen;
  
  char plaintextStr[495]; //plaintext[]length * 2 + 5
  char ciphertextStr[517];
  char decryptedtextStr[495];
  
  int i;
  int len;
  char tmpC[3];
  
  for(i = 0; i < elCount(plaintext); i++){plaintext[i] = 0;} // clear the byte array before a new round start
  for(i = 0; i < elCount(ciphertext); i++){ciphertext[i] = 0;} // clear the byte array before a new round start
  for(i = 0; i < elCount(decryptedtext); i++){decryptedtext[i] = 0;} // clear the byte array before a new round start
  for(i = 0; i < elCount(plaintextStr); i++){plaintextStr[i] = 0;}
  for(i = 0; i < elCount(ciphertextStr); i++){ciphertextStr[i] = 0;}
  for(i = 0; i < elCount(decryptedtextStr); i++){decryptedtextStr[i] = 0;}
  
  //get plain text
  sysGetVariableString( sysvar::Sender::TxText, plaintextStr, elcount(plaintextStr) ); // get string from sysvar 
  plainlen = strlen(plaintextStr);
  write("plainlen = %d", plainlen);
  write("plaintext = %s", plaintextStr);
  for(i = 0; i < plainlen; i++){
    plaintext[i] = plaintextStr[i];
    //write("%x", plaintext[i]);
  }
  
  // encrypt plaintext
  dllRSAPublicEncrypt(plaintext, plainlen, pubKeyFile, ciphertext, cipherlen);
  write("cipherlen = %d", cipherlen);
  //print cipher text in hex
  write("cipher text = ");
 for(i = 0; i < cipherlen; i++){ //
    //write("%d %x %c", i, ciphertext[i], ciphertext[i]);
    snprintf(tmpC, elcount(tmpC), "%02x", ciphertext[i]);
    strncat(ciphertextStr, tmpC, (cipherlen * 2 + 1)); //elcount(ciphertextStr)
  }
  write("%s", ciphertextStr);
  
 // decrypt ciphertext
  dllRSAPrivateDecrypt(ciphertext, cipherlen, priKeyFile, priKeyPW, decryptedtext, decryptedlen);
  write("decryptedlen = %d", decryptedlen);
  //print decrypted test
  for(i = 0; i < decryptedlen; i++){
    decryptedtextStr[i] = decryptedtext[i];
    //write("%d %x %c", i, decryptedtext[i], decryptedtext[i]);
    //snprintf(tmpC, elcount(tmpC), "%02x", decryptedtext[i]);
    //strncat(decryptedtextStr, tmpC, (decryptedlen + 1));
  }
  write("decrypted text = %s", decryptedtextStr);
```

### dllRSAPrivateDecrypt
**Definition**
Item|Content
----|------- 
Class | CryptoBasis 
Function Name | dllRSAPrivateDecrypt
Syntax|dword dllRSAPrivateDecrypt(byte ciphertext[], long cipherLen, char priKeyFile[], char priKeyFilePW[], byte decryptedtext[], long* dectextLen)
Description|This function decrypts the input ciphertext by the RSA private key.
Parameters| - ciphertext: input ciphertext <br> - cipherLen: length of the input ciphertext <br> - pubKeyFile: path of the public key file(*.pem) <br> - priKeyFilePW: password of the private key file  <br> - decryptedtext: the output decrypted text <br> - dectextLen: the length of the output decrypted text 
Return Values | Return 1 if no error occurs. 

**Example Codes**
See dllRSAPublicEncrypt -> Example Codes
Return Values| Return 1 if no error occurs. 
