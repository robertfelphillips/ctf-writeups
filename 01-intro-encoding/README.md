# HW1: Introduction, Python for CTF, and Encoding Basics

| Challenge | Flag |
|-----------|------|
| Looking Under Rock | `fsuCTF{YouLookedUnderSomeRocksAndFoundAWordlistThisWillBeVeryImportantLaterIReallyHopeYouDidntDoThisManually}` |
| The Mathening | `fsuCTF{n3w_new_n3w_m4th_tm_p4rt_2}` |
| Waiter | `fsuCTF{T0_0ff3nd_4_Co0k_47_S34_Is_4_F001s_Mist4k3}` |
| Endangered Program | `fsuCTF{7hi5_I5_7h3_P3rf3c7_3nvir0nm3n7}` |

## Looking Under Rock

Clues pointed at the RockYou breach (`rockyou-45.txt`), and the puzzle file was a list of `row, col` pairs. Each pair indexes a word in the wordlist and a character in that word. A short Python script walks the coordinates, collects the characters, and wraps them in the flag format.

**Flag:** `fsuCTF{YouLookedUnderSomeRocksAndFoundAWordlistThisWillBeVeryImportantLaterIReallyHopeYouDidntDoThisManually}`

## The Mathening

A remote service streams math problems using three custom bitwise operators (`@`, `#`, `?`). I implemented each operator in Python and answered over a socket, parsing problems with a regex and replying automatically. When the server printed the correct answer after a miss, the script echoed it back.

**Flag:** `fsuCTF{n3w_new_n3w_m4th_tm_p4rt_2}`

## Waiter

The note was layered Base64 (hints: "base", "labels", "JUMP ship", trailing `=`). The script repeatedly Base64-decodes while the output still looks like Base64, then decodes the final layers to plaintext.

**Flag:** `fsuCTF{T0_0ff3nd_4_Co0k_47_S34_Is_4_F001s_Mist4k3}`

## Endangered Program

A string in the binary read `VIRTUAL_ENV The endangered program loves this environment.` The program only prints the flag when run inside an active Python virtual environment:

```bash
python3 -m venv gift
source ~/gift/bin/activate
```

**Flag:** `fsuCTF{7hi5_I5_7h3_P3rf3c7_3nvir0nm3n7}`
