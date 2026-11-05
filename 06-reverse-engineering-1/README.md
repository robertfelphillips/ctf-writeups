# HW6: Reverse Engineering I

| Challenge | Flag | Summary |
|-----------|------|---------|
| nuclear_pasta | `fsuCTF{sp4ghett1_c0d3_15_a_d3fens3_mech4n1sm}` | `convert()` reduces to XOR `0xBB`; XOR the `.data` ciphertext to recover the flag |
| old_school_gauntlet | `fsuCTF{b3tt3r_7h4n_cry5t41_4rm0r}` | Bypass anti-debug checks, rebuild the XOR loop (key `dc 4e 72 9d`, extra `0x40`) |
| Upper Management | `fsuCTF{5ti11_b3tter_7h4n_73ch_supp0r7}` | Trace the runtime flag construction, replay the layered XOR and arithmetic |

## nuclear_pasta

The binary runs each input byte through a deliberately convoluted `convert()` and compares against a constant array in `.data`. Reversing it, the only meaningful step is `if byte != 0: byte ^= 0xBB`. So `input = ct ^ 0xBB` — XOR each `ct` byte with `0xBB` to recover the flag.

**Flag:** `fsuCTF{sp4ghett1_c0d3_15_a_d3fens3_mech4n1sm}`

## old_school_gauntlet

Three anti-debug checks guarded the flag logic: parent-process inspection via `/proc/<pid>/exe`, a `ptrace(PTRACE_TRACEME)` check, and a sub-second timing check. After accounting for those, the flag routine was an XOR loop with a 4-byte key (`dc 4e 72 9d`) plus an additional `0x40` XOR applied to an embedded cipher blob.

**Flag:** `fsuCTF{b3tt3r_7h4n_cry5t41_4rm0r}`

## Upper Management

The flag is built at runtime, not stored statically. The binary applies layered XOR and arithmetic transformations over constants scattered across the file. Tracing the construction step by step and replaying the operations recovers the flag.

**Flag:** `fsuCTF{5ti11_b3tter_7h4n_73ch_supp0r7}`
