# Unit Test Specification of OpenSSL_CAPL_Sec.dll Functions

## TG_dllSymmetryEncrypt

### 1.1 TC_dllSymmetryEncrypt_invalid_cipher_name
**Purpose:** To check the function behaviors when an invalid cipher name is input <br>
**Test setup:** key = “akey”; plain text = "Hello World!”; plain text length = 12; iv = “”;  <br>

**Sub test case 1: Input an invalid cipher name**
* input: cipher name = "bes-128-ecb” 
* expected output: null (the function is abort) 
* expected return: error code = 100 (cipher name is invalid) 

**Sub test case 2: Input a null cipher name** 
* input: cipher name = null 
* expected output: null (the function is abort)
* expected return: error code = 100 (cipher name is invalid)

### 1.2.1 TC_dllSymmetryEncrypt_aes_128_ecb_normal
**Purpose:** To check whether the function works normally <br>
**Test setup:** cipher name = “aes-128-ecb”; key = “akey”; iv = “”; plain text = "Hello World!”; plain text length = 12;<br>
**Sub test cases 1: Normal operation**
* input: /
* expected output: cipher text = “ c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.2.1 TC_dllSymmetryEncrypt_aes_128_ecb_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-128-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.2.2 TC_dllSymmetryEncrypt_aes_128_ecb_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-128-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 16 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 1: Input key length = 16 bytes**
* input: key = "0123456789abcdef"
* expected output: cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 1: Input key length > 16 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* expected output: cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 1: Input key = null**
* input: key = ""
* expected output: cipher text = “ fc041974581f3bfede58b726b4f88941”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.3.1 TC_dllSymmetryEncrypt_aes_128_cbc_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-128-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “aef47c964afeeff4e89b19f3cead8da0”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.4.1 TC_dllSymmetryEncrypt_aes_192_ecb_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-192-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “2c41845afcd4c369899868e4781fee9a”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.4.2 TC_dllSymmetryEncrypt_aes_192_ecb_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-192-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 24 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “2c41845afcd4c369899868e4781fee9a”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 1: Input key length = 24 bytes**
* input: key = "0123456789abcdef11223344"
* expected output: cipher text = “ cd7760c08725a7af16e49ca9b4f7e322”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 1: Input key length > 24 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* expected output: cipher text = “ cd7760c08725a7af16e49ca9b4f7e322”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 1: Input key = null**
* input: key = ""
* expected output: cipher text = “ cd7760c08725a7af16e49ca9b4f7e322”; cipher text length = 16;
* expected return: 1 (operation succeeds)


### 1.5.1 TC_dllSymmetryEncrypt_aes_192_cbc_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-192-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “be3295ab58454b0e7d7b75da0d16f954”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.6.1 TC_dllSymmetryEncrypt_aes_256_ecb_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-256-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “67b706d84807d187971d7890e91f8cca”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.7.1 TC_dllSymmetryEncrypt_aes_256_cbc_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-256-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “37e52c9833b6421935d7cade306ee629”; cipher text length = 16;
* expected return: 1 (operation succeeds)


## TG_dllSymmetryDecrypt

### 2.1 TC_dllSymmetryDecrypt_invalid_cipher_name
**Purpose:** To check the function behaviors when an invalid cipher name is input<br>
**Test setup:** key = “akey”; iv = “”; cipher text = "c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16; <br>
**Sub test cases 1: Input an invalid cipher name**
* input: cipher name = "bes-128-ecb”
* output: null (the function is abort)
* return: error code = 100 (cipher name is invalid)

**Sub test cases 2: Input a null cipher name**
* input: cipher name = null
* output: null (the function is abort)
* return: error code = 100 (cipher name is invalid)

### 2.2.1 TC_dllSymmetryDecrypt_aes_128_ecb_normal 
**Purpose:** To check whether the function works normally<br>
**Test setup:** cipher name = “aes-128-ecb”; key = “akey”; iv = “”; cipher text = "c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;  <br>
**Sub test cases 1: Normal operation**
* input: /
* output: plain text = “Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)

### 2.2.2 TC_dllSymmetryDecrypt_aes_128_ecb_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-128-ecb”; iv = “”;   <br>
**Sub test cases 1: Input key length < 16 bytes # padding the rest with 0x00**
* input: key = “akey”; cipher text = “ c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)

**Sub test cases 1: Input key length = 16 bytes**
* input: key = “0123456789abcdef”; cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)

**Sub test cases 1: Input key length > 16 bytes # cut the overflow part**
* input: key = “0123456789abcdef112233445566778899”; cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)

**Sub test cases 1: Input key = null**
* input: key = “”; cipher text = “ fc041974581f3bfede58b726b4f88941”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)
