# HW10: Cryptography I

| Challenge | Flag | Summary |
|-----------|------|---------|
| one_byte | `fsuCTF{0h_n0_r3v3r5i813_3ncryp7i0n}` | Base64 decode, brute-force all 256 single-byte XOR keys |
| My Public Key | `fsuCTF{A_Big_N_Does_Not_Matter_If_Its_Factors_Are_Known}` | Factor a 512-bit RSA modulus, compute `d`, decrypt |
| The Cooler Cipher | `fsuCTF{You_Know_What_ROT13_Aint_Cool_Enough_Have_ROT47}` | Recognize ROT47 and rotate across printable ASCII |

## one_byte

The ciphertext was Base64. The name "one byte" hints at single-byte XOR, which is trivially brute-forced since there are only 256 keys and XOR is its own inverse. Trying every key and checking for `fsuCTF` in the result finds the flag.

**Flag:** `fsuCTF{0h_n0_r3v3r5i813_3ncryp7i0n}`

## My Public Key

RSA with a weak 512-bit modulus. Factoring `n` into `p` and `q` (via factordb / a factoring tool) breaks it: compute `phi = (p-1)(q-1)`, `d = e^-1 mod phi`, then `m = c^d mod n` and decode the integer to bytes.

**Flag:** `fsuCTF{A_Big_N_Does_Not_Matter_If_Its_Factors_Are_Known}`

## The Cooler Cipher

The hint referenced ROT13 but implied something stronger. ROT47 rotates all 94 printable ASCII characters (codes 33–126) by 47. Applying ROT47 to the ciphertext decodes the flag.

**Flag:** `fsuCTF{You_Know_What_ROT13_Aint_Cool_Enough_Have_ROT47}`
