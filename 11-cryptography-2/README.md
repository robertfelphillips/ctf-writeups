# HW11: Cryptography II

| Challenge | Flag | Summary |
|-----------|------|---------|
| Liars Dice | `fsuCTF{800t57r4p_8i11_y0u_4r3_4_1i4r_4nd_y0u_wi11_5p3nd_4n_37ernity_0n_7hi5_5hip}` | Brute-force the microsecond PRNG seed from leaked dice, predict every roll |
| RSA Master | `fsuCTF{You_Can_Do_CRT_For_Any_E_If_You_Have_Enough_Ciphertexts}` | Håstad's broadcast attack: CRT over 7 ciphertexts, integer 7th root |
| Jack The Ripper | `fsuCTF{John_Work_Well_With_Rockyou}` | Crack legacy ZipCrypto with rockyou.txt |

## Liars Dice

The server seeds Python's `random` with `int(time.time() * 1000000)` and leaks the player's first 10 dice — the first 10 MT19937 outputs. Brute-forcing nearby microsecond timestamps until a seed reproduces those 10 values recovers the full PRNG state. With it I can predict every die for both players each round and always bid a statement the AI cannot safely call, forcing it to lose.

**Flag:** `fsuCTF{800t57r4p_8i11_y0u_4r3_4_1i4r_4nd_y0u_wi11_5p3nd_4n_37ernity_0n_7hi5_5hip}`

## RSA Master

Each connection encrypts the same plaintext with `e = 7` under a different modulus. Collecting 7 coprime `(c, n)` pairs and applying CRT reconstructs `m^7` over the integers; since `m^7` is smaller than the product of the moduli, the exact integer 7th root recovers `m`. This is the classic Håstad broadcast attack.

**Flag:** `fsuCTF{You_Can_Do_CRT_For_Any_E_If_You_Have_Enough_Ciphertexts}`

## Jack The Ripper

A password-protected ZIP using legacy ZipCrypto (not AES), which is vulnerable to dictionary attacks. The name hinted at John the Ripper and rockyou.txt; using the correct header check byte (`0x06`) to reject wrong candidates quickly, the password cracked from rockyou.txt and decrypted `flag.txt`.

**Flag:** `fsuCTF{John_Work_Well_With_Rockyou}`
