# Unit Test Specification of the Interface "dllCalHMAC"

## TG_dllCalHMAC

### 6.1 TC_dllCalHMAC_invalid_digest_name
**Purpose:** To check the function behaviors when an invalid cipher name is input<br>
**Test setup:** key = "akey"; akeyLen = 4; source text = "Hello World!"; source text length = 16; <br>
**Sub test cases 1: Input an invalid cipher name**
* input: digest algorithm name = "md6”
* expected output: / 
* expected return: 0 (the function is abort)

**Sub test cases 2: Input a null cipher name**
* input: digest algorithm name = null
* expected output: null (the function is abort)
* expected return: 0 (the function is abort)

### 6.2.1 TC_dllCalHMAC_md5_normal 
**Purpose:** To check whether the function works normally<br>
**Test setup:** digest algorithm name = "md5”; key = "akey"; akeyLen = 4; source text = "Hello World!"; source text length = 12; <br>
**Sub test cases 1: Normal operation**
* input: /
* expected output: digest text = “e18ef6f39af8457c1e0c90c9e555e54e”; digest text length = 16;
* expected return: 1 (operation succeeds)

### 6.2.2 TC_dllCalHMAC_md5_akey 
**Purpose:** To check whether the function works normally with various key values<br>
**Test setup:** digest algorithm name = "md5”;  source text = "Hello World!"; source text length = 12; <br>
**Sub test cases 1: Calculte the HMAC value with a short key value**
* input: key = "akey"; akeyLen = 4;
* expected output: digest text = “e18ef6f39af8457c1e0c90c9e555e54e”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Calculte the HMAC value with a long key value**
* input: key = "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"; akeyLen = 160;
* expected output: digest text = “73e9edb010e88d157c43edd5081df7c5”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Calculte the HMAC value with a null key value**
* input: key = ""; akeyLen = 0;
* expected output: digest text = “72d422b3c98cc57b12d204a4eb935c4b”; digest text length = 16;
* expected return: 1 (operation succeeds)

### 6.2.3 TC_dllCalHMAC_md5_akeylen 
**Purpose:** To check whether the function works normally with various key length values<br>
**Test setup:** digest algorithm name = "md5”;  source text = "Hello World!"; source text length = 12; key = "akey"; <br>
**Sub test cases 1: Calculte the HMAC value with a correct key length**
* input:  akeyLen = 4;
* expected output: digest text = “e18ef6f39af8457c1e0c90c9e555e54e”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Calculte the HMAC value with a incorrect key length**
* input:  akeyLen = 3;
* expected output: digest text = “a0e5b555cdb90afdf7dd2a66ccb8c95b”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Calculte the HMAC value with a zero key length**
* input:  akeyLen = 0;
* expected output: digest text = “72d422b3c98cc57b12d204a4eb935c4b”; digest text length = 16;
* expected return: 1 (operation succeeds)

### 6.2.4 TC_dllCalHMAC_md5_in_plaintext 
**Purpose:** To check whether the function works normally with various input text values<br>
**Test setup:** digest algorithm name = "md5”;   key = "akey"; akeyLen = 4;<br>
**Sub test cases 1: Calculte the HMAC value of a short text**
* input: source text = "Hello World!"; source text length = 12;
* expected output: digest text = “e18ef6f39af8457c1e0c90c9e555e54e”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Calculte the HMAC value of a long text**
* input: source text = "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"; source text length = 160;
* expected output: digest text = “51ea71f71d7c82003ece18e4bdee5df1”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Calculte the HMAC value of null text**
* input: source text = ""; source text length = 0;
* expected output: digest text = “eaff3652fb057e9cff6ceed45c483c6c”; digest text length = 16;
* expected return: 1 (operation succeeds)


### 6.2.5 TC_dllCalHMAC_md5_in_plainlen_wrong 
**Purpose:** To check whether the function works normally with various input text length values<br>
**Test setup:** digest algorithm name = "md5”;   key = "akey"; akeyLen = 4; source text = "Hello World!";<br>
**Sub test cases 1: Calculte the HMAC value with a correct input text length**
* input:  source text length = 12;
* expected output: digest text = “e18ef6f39af8457c1e0c90c9e555e54e”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 2: Calculte the HMAC value with a incorrect input text length**
* input:  source text length = 11;
* expected output: digest text = “18d87654d75c8aff82c98f37eefb7acf”; digest text length = 16;
* expected return: 1 (operation succeeds)

**Sub test cases 3: Calculte the HMAC value with a zero input text length**
* input:  source text length = 0;
* expected output: digest text = “eaff3652fb057e9cff6ceed45c483c6c”; digest text length = 16;
* expected return: 1 (operation succeeds)

