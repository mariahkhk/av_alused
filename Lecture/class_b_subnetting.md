# CLASS B SUBNETTING

## Mis on Class B võrk?

Class B algab **128.0.0.0 - 191.255.255.255**

**Vaikimisi mask: /16 = 255.255.0.0**

```
172.16.0.0 /16
└─┬──┘ └──┬──┘
Võrk   Hostid
(fikseeritud) (256×256 = 65536 hosti)
```

## Kuidas jagada?

### Näide 1: Jaga 172.16.0.0 /16 → 4 alamvõrku

**Samm 1:** Mitu biti?
- 2² = 4 võrku → 2 biti

**Samm 2:** Uus mask
```
Algne:  /16 = 255.255.0.0
                      ↓
Laename 2 biti kolmandasse oktetti:

Biti väärtused:  128  64  32  16   8   4   2   1
                  ─────────────────────────────────
                  1   1   0   0   0   0   0   0  = 192

Uus: /18 = 255.255.192.0
```

**Samm 3:** Võlunumber
- Huvitav oktet: kolmas (192)
- Võlunumber: 256 - 192 = **64**

**Samm 4:** Alamvõrgud

| Võrk | Võrgu aadress | Broadcast | Esimene host | Viimane host | Hoste kokku |
|------|---------------|-----------|--------------|--------------|-------------|
| 1    | 172.16.0.0    | 172.16.63.255 | 172.16.0.1 | 172.16.63.254 | 16382 |
| 2    | 172.16.64.0   | 172.16.127.255 | 172.16.64.1 | 172.16.127.254 | 16382 |
| 3    | 172.16.128.0  | 172.16.191.255 | 172.16.128.1 | 172.16.191.254 | 16382 |
| 4    | 172.16.192.0  | 172.16.255.255 | 172.16.192.1 | 172.16.255.254 | 16382 |

```
Kolmas oktet:
0                                                               255
├───────────────┼───────────────┼───────────────┼───────────────┤
     Võrk 1          Võrk 2          Võrk 3          Võrk 4
    (0-63)         (64-127)       (128-191)       (192-255)
    
    Hüppab 64 võrra (võlunumber!)
```

**Hoste arv:** 
- Iga alamvõrgus on 64 × 256 = 16384 aadressi
- Miinus 2 (võrgu aadress ja broadcast) = **16382 hosti**

---

### Näide 2: Jaga 10.50.0.0 /16 → 8 alamvõrku

**Samm 1:** Mitu biti?
- 2³ = 8 võrku → 3 biti

**Samm 2:** Uus mask
```
Biti väärtused:  128  64  32  16   8   4   2   1
                  ─────────────────────────────────
Laename 3 biti:   1   1   1   0   0   0   0   0  = 224

Uus: /19 = 255.255.224.0
```

**Samm 3:** Võlunumber
- 256 - 224 = **32**

**Samm 4:** Alamvõrgud (esimesed 4)

| Võrk | Võrgu aadress | Broadcast | Esimene host | Viimane host | Hoste |
|------|---------------|-----------|--------------|--------------|-------|
| 1    | 10.50.0.0     | 10.50.31.255 | 10.50.0.1 | 10.50.31.254 | 8190 |
| 2    | 10.50.32.0    | 10.50.63.255 | 10.50.32.1 | 10.50.63.254 | 8190 |
| 3    | 10.50.64.0    | 10.50.95.255 | 10.50.64.1 | 10.50.95.254 | 8190 |
| 4    | 10.50.96.0    | 10.50.127.255 | 10.50.96.1 | 10.50.127.254 | 8190 |

**Hoste arv:**
- 32 × 256 = 8192 aadressi
- Miinus 2 = **8190 hosti**

---

## Peamised erinevused Class C-st

| Aspekt | Class C (/24) | Class B (/16) |
|--------|---------------|---------------|
| Huvitav oktet | Neljas | Kolmas |
| Vaikimisi hoste | 254 | 65534 |
| Broadcast arvutamine | Lihtsam (1 oktet) | Raskem (2 oktetti) |

## Broadcast aadressi leidmine

**Reegel:** Järgmine võrk miinus 1

Näide: Kui võrk on 172.16.64.0 ja võlunumber 64:
- Järgmine võrk: 172.16.128.0
- Broadcast: 172.16.127.255 (128.0 - 0.1 = 127.255)

---

## Harjutus

Jaga võrk **192.168.0.0 /16** kuueteistkümneks alamvõrguks.

1. Mitu biti? ___
2. Uus mask? /___
3. Kolmas oktet? ___
4. Võlunumber? ___
5. Esimene võrk: 192.168.___.0
6. Teine võrk: 192.168.___.0
7. Kui palju hoste ühes võrgus? ___
