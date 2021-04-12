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

### 1.2.2 TC_dllSymmetryEncrypt_aes_128_ecb_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-128-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 16 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input key length = 16 bytes**
* input: key = "0123456789abcdef"
* expected output: cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 16 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* expected output: cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = ""
* expected output: cipher text = “ fc041974581f3bfede58b726b4f88941”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.2.3 TC_dllSymmetryEncrypt_aes_128_ecb_iv
**Purpose:** To check the function behaviors when various iv values are input<br>
**Test setup:** cipher name = “aes-128-ecb”; key = "akey"; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input iv = NULL**
* input: iv = “”
* expected output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input iv != NULL**
* input: iv = "iv"
* expected output: cipher text = “ c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.2.4 TC_dllSymmetryEncrypt_aes_128_ecb_in_plaintext
**Purpose:** To check the function behaviors when various plaintexts are input<br>
**Test setup:** cipher name = “aes-128-ecb”; key = "akey"; iv = “” <br>
**Sub test cases 1: Input plaintext length < 15 bytes**
* input: plain text = "Hello World!”;  plain text length = 12
* expected output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input plaintext length = 15 bytes**
* input: plain text = "Hello World!abc”; plain text length = 15
* expected output: cipher text = “7fa7e1d6be5ce919632dbf4d94a1034d”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input plaintext length = 16 bytes**
* input: plain text = “Hello World!abcd”; ; plain text length = 16
* expected output: cipher text = “b5010356ddc39e4afaf4ffa91c649a5b030ced986a5d728cacf2b449c00d06ea”; cipher text length = 32;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input plaintext length = 2000 bytes (a large number)**
* input: plain text = “01234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789”; plain text length = 2000
* expected output: cipher text = “90d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f490d07376652ce39366f1e7aa786f40bc3c2d918643bd79aa73f1d1581126a59b115023b798abea591e7f810b21e3c9ba9729c1564ae1598b5b3e52b64ee35afe4a490213f0234111093cf68cf5d292f4030ced986a5d728cacf2b449c00d06ea”; cipher text length = 2016;
* expected return: 1 (operation succeeds)

**Sub test cases 5: Input plaintext length = null**
* input: plain text = “”; ; plain text length = 0
* expected output: /
* expected return: 101 (error code)


### 1.3.1 TC_dllSymmetryEncrypt_aes_128_cbc_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-128-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “aef47c964afeeff4e89b19f3cead8da0”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.3.2 TC_dllSymmetryEncrypt_aes_128_cbc_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-128-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 16 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “aef47c964afeeff4e89b19f3cead8da0”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input key length = 16 bytes**
* input: key = "0123456789abcdef"
* expected output: cipher text = “ fa5d630d9e7e1e46cff407ee7a3cd19f”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 16 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* expected output: cipher text = “ fa5d630d9e7e1e46cff407ee7a3cd19f”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = ""
* expected output: cipher text = “ 7a95e22960303400ba5c8ba8d8c07e46”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.3.3 TC_dllSymmetryEncrypt_aes_128_cbc_iv
**Purpose:** To check the function behaviors when various iv values are input<br>
**Test setup:** cipher name = “aes-128-cbc”; key = "akey"; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input iv = NULL**
* input: iv = “”
* expected output: cipher text = “c1a9d48932d01b10913b29e6e43f3126”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input iv < 16 bytes**
* input: iv = "iviv"
* expected output: cipher text = “ 0b42d85418563df583315f5628e38407”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input iv = 16 bytes**
* input: iv = "0123456789abcdef"
* expected output: cipher text = “ 75d031abe04420f6707d50c4ea7ecce7”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input iv > 16 bytes**
* input: iv = "0123456789abcdef12345"
* expected output: cipher text = “ 75d031abe04420f6707d50c4ea7ecce7”; cipher text length = 16;
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

**Sub test cases 2: Input key length = 24 bytes**
* input: key = "0123456789abcdef11223344"
* expected output: cipher text = “ cd7760c08725a7af16e49ca9b4f7e322”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 24 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* expected output: cipher text = “ cd7760c08725a7af16e49ca9b4f7e322”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = ""
* expected output: cipher text = “ cd7760c08725a7af16e49ca9b4f7e322”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.4.3 TC_dllSymmetryEncrypt_aes_192_ecb_iv
**Purpose:** To check the function behaviors when various iv values are input<br>
**Test setup:** cipher name = “aes-192-ecb”; key = "akey"; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input iv = NULL**
* input: iv = “”
* expected output: cipher text = “2c41845afcd4c369899868e4781fee9a”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input iv != NULL**
* input: iv = "iv"
* expected output: cipher text = “ 2c41845afcd4c369899868e4781fee9a”; cipher text length = 16;
* expected return: 1 (operation succeeds)


### 1.5.1 TC_dllSymmetryEncrypt_aes_192_cbc_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-192-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “be3295ab58454b0e7d7b75da0d16f954”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.5.2 TC_dllSymmetryEncrypt_aes_192_cbc_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-192-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 24 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “be3295ab58454b0e7d7b75da0d16f954”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input key length = 24 bytes**
* input: key = "0123456789abcdef11223344"
* expected output: cipher text = “ 237d3058ca49ff3c9206d5b12a3a7049”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 24 bytes # cut the overflow part**
* input: key = "0123456789abcdef112233445566778899"
* expected output: cipher text = “ 237d3058ca49ff3c9206d5b12a3a7049”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = ""
* expected output: cipher text = “ 9b89a72c0caef9baf8ca229ec0e847fd”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.5.3 TC_dllSymmetryEncrypt_aes_192_cbc_iv
**Purpose:** To check the function behaviors when various iv values are input<br>
**Test setup:** cipher name = “aes-192-cbc”; key = "akey"; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input iv = NULL**
* input: iv = “”
* expected output: cipher text = “2c41845afcd4c369899868e4781fee9a”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input iv < 16 bytes**
* input: iv = "iviv"
* expected output: cipher text = “ e7c898cddd013bc39129e008283799f7”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input iv = 16 bytes**
* input: iv = "0123456789abcdef"
* expected output: cipher text = “ b8106bc6f6f6b0ea2896a5af981bd79f”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input iv > 16 bytes**
* input: iv = "0123456789abcdef12345"
* expected output: cipher text = “ b8106bc6f6f6b0ea2896a5af981bd79f”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.6.1 TC_dllSymmetryEncrypt_aes_256_ecb_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-256-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “67b706d84807d187971d7890e91f8cca”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.6.2 TC_dllSymmetryEncrypt_aes_256_ecb_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-256-ecb”; iv = “”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 24 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “67b706d84807d187971d7890e91f8cca”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input key length = 24 bytes**
* input: key = "0123456789abcdef0123456789abcdef"
* expected output: cipher text = “ 3ddb0416ef5b0131594001173529e4ac”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 24 bytes # cut the overflow part**
* input: key = "0123456789abcdef0123456789abcdef11223344"
* expected output: cipher text = “ 3ddb0416ef5b0131594001173529e4ac”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = ""
* expected output: cipher text = “ c10e6d561c7afaa57f3f44b2f79dbf14”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.6.3 TC_dllSymmetryEncrypt_aes_256_ecb_iv
**Purpose:** To check the function behaviors when various iv values are input<br>
**Test setup:** cipher name = “aes-256-ecb”; key = "akey"; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input iv = NULL**
* input: iv = “”
* expected output: cipher text = “67b706d84807d187971d7890e91f8cca”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input iv != NULL**
* input: iv = "iv"
* expected output: cipher text = “ 67b706d84807d187971d7890e91f8cca”; cipher text length = 16;
* expected return: 1 (operation succeeds)


### 1.7.1 TC_dllSymmetryEncrypt_aes_256_cbc_normal
**Purpose:** To check the function behaviors when using it normally <br>
**Test setup:** cipher name = “aes-256-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Use the interface normally**
* input: key = "akey"
* expected output: cipher text = “37e52c9833b6421935d7cade306ee629”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.7.2 TC_dllSymmetryEncrypt_aes_256_cbc_aKey
**Purpose:** To check the function behaviors when various key values are input<br>
**Test setup:** cipher name = “aes-256-cbc”; iv = “iv”; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input key length < 32 bytes # padding the rest with 0x00**
* input: key = "akey"
* expected output: cipher text = “37e52c9833b6421935d7cade306ee629”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input key length = 32 bytes**
* input: key = "0123456789abcdef0123456789abcdef"
* expected output: cipher text = “ 6df35ea65ca34ba37f65b0fb89b644ea”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 32 bytes # cut the overflow part**
* input: key = "0123456789abcdef0123456789abcdef11223344"
* expected output: cipher text = “ 6df35ea65ca34ba37f65b0fb89b644ea”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = ""
* expected output: cipher text = “ 23177e07b29e8fc7a8732daf6af8ef9e”; cipher text length = 16;
* expected return: 1 (operation succeeds)

### 1.7.3 TC_dllSymmetryEncrypt_aes_256_cbc_iv
**Purpose:** To check the function behaviors when various iv values are input<br>
**Test setup:** cipher name = “aes-256-cbc”; key = "akey"; plain text = "Hello World!”; plain text length = 12; <br>
**Sub test cases 1: Input iv = NULL**
* input: iv = “”
* expected output: cipher text = “67b706d84807d187971d7890e91f8cca”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Input iv < 16 bytes**
* input: iv = "iviv"
* expected output: cipher text = “ c071cd49c69283678ef09c3c8e5b9307”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Input iv = 16 bytes**
* input: iv = "0123456789abcdef"
* expected output: cipher text = “ 5fac8df3e10e02248f54a6fb7f6138ec”; cipher text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 4: Input iv > 16 bytes**
* input: iv = "0123456789abcdef12345"
* expected output: cipher text = “ 5fac8df3e10e02248f54a6fb7f6138ec”; cipher text length = 16;
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

**Sub test cases 2: Input key length = 16 bytes**
* input: key = “0123456789abcdef”; cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)

**Sub test cases 3: Input key length > 16 bytes # cut the overflow part**
* input: key = “0123456789abcdef112233445566778899”; cipher text = “ 73e56da23fc5187b64566ba6e3def67e”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)

**Sub test cases 4: Input key = null**
* input: key = “”; cipher text = “ fc041974581f3bfede58b726b4f88941”; cipher text length = 16;
* output: plain text = "Hello World!”; plain text length = 12;
* return: 1 (operation succeeds)
