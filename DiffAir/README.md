#Stéganographie
# Diff'air
j'ai oublié de reccup le sujet oupsi

## Fichier
[airPort](./airPort.jpg) et [Airport](./Airport.jpg)

et il n'y as pas de différence notable visible.

vu que le nom c'est diff'air on pense desuite au soft diff.

sauf que diff nous dit
```
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯❯diff airPort.jpg Airport.jpg 
Binary files airPort.jpg and Airport.jpg differ
```

on en deduis qu'une vu hexa pourrais aider

hexdump et xxd sont les 2 soft que je connais pour faire du dump hexa de fichier sans me prendre la tête donc 
```
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯❯diff airPort.jpg > airPort.hex 
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯❯diff Airport.jpg > Airport.hex 
```

et finalement on utilise diff sur les deux fichier hexa

```
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯❯diff Airport.txt airPort.txt 
3529,3545c3529,3545
< 0000dc80: 714e f97f 09bf f09f ffc4 002c 1001 0001  qN.........,....
< 0000dc90: 0302 0405 0501 0101 0100 0000 0001 1100  ................
< 0000dca0: 2131 4151 6171 c1f0 1081 91a1 f120 3040  !1AQaq....... 0@
< 0000dcb0: 50b1 d1e1 6070 ffda 0008 0101 0001 3f10  P...`p........?.
< 0000dcc0: fc0f 7a57 6ddf ff00 9681 59fe 9349 d88d  ..zWm.....Y..I..
< 0000dcd0: 0a8d 3536 a109 0ee3 f38a 8062 c67a 5f31  ..56.......b.z_1
< 0000dce0: 9541 26d5 6397 8310 1d93 0f2a cdde 1326  .A&.c......*...&
< 0000dcf0: 0a60 1c22 0021 3ae7 c8ad 1217 820d b059  .`.".!:........Y
< 0000dd00: 7675 a77d 1581 96c9 8acd e752 9e0a 2081  vu.}.......R.. .
< 0000dd10: 9558 be02 f163 3148 9c0c ac0a 9301 2ade  .X...c1H......*.
< 0000dd20: 20de a3f5 77a0 0430 a0dd 51b5 1557 8c83   ...w..0..Q..W..
< 0000dd30: 684d d91b 7bcd 349d 9311 9124 dc00 c469  hM..{.4....$...i
< 0000dd40: 351c e90c 920c ed0a 145e 2ad5 303c 3cc2  5........^*.0<<.
< 0000dd50: a183 6508 74a7 0850 930a 3fa9 f7a5 765d  ..e.t..P..?...v]
< 0000dd60: ff00 f964 ea60 4201 81f2 a3e8 8404 c15d  ...d.`B........]
< 0000dd70: c2ca 40d0 d136 3454 5b36 628c 26c7 fb56  ..@..64T[6b.&..V
< 0000dd80: 7310 19a4 5b59 0603 4e82 cef6 a5ec a02e  s...[Y..N.......
---
> 0000dc80: 0000 0000 0000 0000 0000 0000 0000 0000  ................
> 0000dc90: 0000 0000 0000 0000 0000 5455 4e55 5200  ..........TUNUR.
> 0000dca0: 0000 0000 0000 0000 0000 6e74 744d 5800  ..........nttMX.
> 0000dcb0: 0000 0000 0000 0000 0000 4a79 4d48 4a00  ..........JyMHJ.
> 0000dcc0: 0000 0000 0000 0000 0000 664d 5731 6800  ..........fMW1h.
> 0000dcd0: 0000 0000 0000 0000 0000 5a7a 4e66 5900  ..........ZzNfY.
> 0000dce0: 0000 0000 0000 0000 0000 7a42 7463 4400  ..........zBtcD.
> 0000dcf0: 0000 0000 0000 0000 0000 5279 4e47 6b00  ..........RyNGk.
> 0000dd00: 0000 0000 0000 0000 0000 314d 4734 6866  ..........1MG4hf
> 0000dd10: 513d 3d00 0000 0000 0000 0000 0000 0000  Q==.............
> 0000dd20: 0000 0000 0000 0000 0000 0000 0000 0000  ................
> 0000dd30: 684d c399 2e7b c38d 342e 2e2e 2e24 c39c  hM...{..4....$..
> 0000dd40: 2ec3 8469 352e c3a9 2e2e 2ec3 ad0a 2e5e  ...i5..........^
> 0000dd50: 2ac3 9530 3c3c c382 c2a1 2e65 2e74 c2a7  *..0<<.....e.t..
> 0000dd60: 2e50 2e0a 3fc2 a9c3 b7c2 a576 5dc3 bf2e  .P..?......v]...
> 0000dd70: c3b9 64c3 aa60 422e 2ec3 b2c2 a3c3 a82e  ..d..`B.........
> 0000dd80: 2ec3 815d 5b59 0603 4e82 cef6 a5ec a02e  ...][Y..N.......
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯❯
```

il y'as une différence dans le rendu de xxd on pense avec le "Q==" que c'est une base64 

avec vim je fais un peu de nétoyage pour avoir la string au complet
`TUNURnttMXJyMHJfMW1hZzNfYzBtcDRyNGk1MG4hfQ==`

et finalement:
```
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯❯echo -n "TUNURnttMXJyMHJfMW1hZzNfYzBtcDRyNGk1MG4hfQ==" | base64 -d
MCTF{m1rr0r_1mag3_c0mp4r4i50n!}%
kawaegle@~/Midnight_BlackBox/steganography/DiffAir:❯❯;
```
