# HW5: Forensics

| Challenge | Flag | Summary |
|-----------|------|---------|
| dossier_101 | `fsuCTF{p1ca55o_w0u1dv3_l0v3d_m5pa1n7}` | Mount a VHD with qemu-nbd, browse NTFS, find `masterpiece.bmp` in Paint app data |
| Jaws | `fsuCTF{Y0ur3_G0nn4_N33d_A_B1g3r_Bo4t}` | Inspect PCAP protocol hierarchy, filter HTTP to a suspicious IP, Base64-decode URI parameters |
| What's the Title Again? | `fsuCTF{1_d0n7_w4n7_t0_pl4y_4nym0r3}` | Run strings on a memory dump, find Media Player playing `Sleep Away.mp3`, read the in-memory title |

## dossier_101

A VHD of a Windows XP machine. I connected it with `qemu-nbd`, mounted the NTFS partition read-only, and browsed to the `daniel` user profile. An RTF referenced a saved "masterpiece", which `find` located at `Application Data/Microsoft/Paint/masterpiece.bmp`. The flag is drawn in the image.

**Flag:** `fsuCTF{p1ca55o_w0u1dv3_l0v3d_m5pa1n7}`

## Jaws

A packet capture. `tshark -z io,phs` showed HTTP traffic with repeated requests to `178.63.67.153`. Filtering those requests and extracting `http.request.uri` gave Base64 data split across requests; reassembling, fixing URL encoding and padding, and decoding revealed the flag.

**Flag:** `fsuCTF{Y0ur3_G0nn4_N33d_A_B1g3r_Bo4t}`

## What's the Title Again?

Memory dumps (`.raw` core dumps). Running wide-char `strings | grep -i mp3` showed Media Player references; narrowing to `/Play` found:

```
wmplayer.exe /Relaunch /Play "C:\Users\Public\Music\Sample Music\Sleep Away.mp3"
```

Searching memory around the playback context surfaced the in-memory title string, which was the flag.

**Flag:** `fsuCTF{1_d0n7_w4n7_t0_pl4y_4nym0r3}`
