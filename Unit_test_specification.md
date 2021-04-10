# Unit Test Specification of OpenSSL_CAPL_Sec.dll Functions

## TG_dllSymmetryEncrypt

### 1.1 TC_dllSymmetryEncrypt_invalid_cipher_name
**Purpose:** To check the function behaviors when an invalid cipher name is input <br>
**Test setup:** key = “akey”; plain text = "Hello World!”; plain text length = 12; iv = “”;  <br>

**Sub test case 1: Input an invalid cipher name**
* input: cipher name = "bes-128-ecb” 
* output: null (the function is abort) 
* return: error code = 100 (cipher name is invalid) 

**Sub test case 2: Input a null cipher name** 
* input: cipher name = null 
* output: null (the function is abort)
* return: error code = 100 (cipher name is invalid)

### 1.2.1 TC_dllSymmetryEncrypt_aes_128_ecb_normal
**Purpose:** To check whether the function works normally<br>
**Test setup:** cipher name = “aes-128-ecb”; key = “akey”; iv = “”; plain text = "Hello World!”; plain text length = 12;<br>
**Sub test cases 1: Normal operation**
* input: /
* output: cipher text = “ c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* return: 1 (operation succeeds)

### 1.2.2 TC_dllSymmetryEncrypt_aes_128_ecb_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-128-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 16 bytes # padding the rest with 0x00**
* input: key = "akey"
* output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* return: 1 (operation succeeds)
**Sub test cases 1: Input key length = 16 bytes**
* input: key = "0123456789abcdef"
* output: cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* return: 1 (operation succeeds)
**Sub test cases 1: Input key length > 16 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* output: cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* return: 1 (operation succeeds)
**Sub test cases 1: Input key = null**
* input: key = ""
* output: cipher text = “ fc041974581f3bfede58b726b4f88941”; cipher text length = 16;
* return: 1 (operation succeeds)


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
