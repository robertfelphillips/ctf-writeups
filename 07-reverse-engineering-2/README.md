# HW7: Reverse Engineering II

| Challenge | Flag | Summary |
|-----------|------|---------|
| spec ops | `fsuCTF{b14ck_bel7_in_b1ackb0x}` | Regenerate the `srand(42)` key, reverse the XOR-and-byte-reverse transform |
| coffee grinder | `fsuCTF{1m_g0nn4_n33d_n3w_k1dn3y5}` | Decompile the JAR, find `SHA-256("adenosine")` + AES/ECB, decrypt the blob |
| chicken scratch | `fsuCTF{7hi5_Is_Ju5t_Chick3n_Scr47ch}` | Unpack the PyInstaller binary, extract the substitution dictionary, decode the symbols |

## spec ops

The binary requires `./input.txt`, then transforms it: it seeds `srand(42)`, generates a 32-byte key from `rand() & 0xFF`, XORs each input byte with the key, writes the result reversed, and compares against stored ciphertext. Recreating the key, XORing the ciphertext, and reversing the bytes recovers the correct input, which contains the flag.

**Flag:** `fsuCTF{b14ck_bel7_in_b1ackb0x}`

## coffee grinder

A Java JAR with `Main.class`, `CryptUtils.class`, and `encrypted_secret.bin`. Decompiling showed the key was `SHA-256("adenosine")` and the cipher was `AES/ECB/PKCS5Padding`. Computing the key and decrypting the blob gave the flag.

**Flag:** `fsuCTF{1m_g0nn4_n33d_n3w_k1dn3y5}`

## chicken scratch

A PyInstaller-packed executable. `pyinstxtractor` + `pycdc` recovered the source, which held a substitution dictionary mapping symbol strings to characters and a stored sequence of symbols for the flag. Applying the dictionary to the sequence (instead of the intended interactive prompt) decoded the flag.

**Flag:** `fsuCTF{7hi5_Is_Ju5t_Chick3n_Scr47ch}`
