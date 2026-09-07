# Baikal BK-B — Blake2b / Sia (AlphaPool Knots)

Notes and a small sgminer patch for a warehouse-rented **Baikal BK-B** on Blake2b (Sia-firmware).

This is **not** a replacement for [SidGrip/Blakestream-Baikal-BKB](https://github.com/SidGrip/Blakestream-Baikal-BKB). Firmware stays GPLv3; credit SidGrip / Blakestream and `cod3gen/sgminer-baikal`.

## Renters: use port 7777

AlphaPool default `us1.alphapool.tech:5555` is for Goldshell-style clients.
This BK-B is a Sia-firmware ASIC (~80 GH/s class). Use:

```
stratum+tcp://us1.alphapool.tech:7777
user: <bc1-payout-address>.<worker>
pass: x
algorithm: sia
```

Same on `us2` / `eu1` / `sg1` — still **:7777**.

If the pool dashboard shows 0 hash, you used **5555**. Change to **7777** before opening a ticket.

## Warehouse clock

Keep **400 MHz**. Do not overclock for rental "max pay." Extra MHz in a warehouse adds heat and HW errors, which causes more refunds than it earns.

## Files

| File | What |
| --- | --- |
| `RENTAL.md` | Paste-ready Mining Rig Rentals listing text |
| `SIA-IMAGE.md` | How to flash Blakestream v2.1 or rebuild `sgminer` |
| `patches/0012-baikal-sia-blake2b-work-fill.patch` | Explicit Sia work-FIFO fill (apply on top of Blakestream 0001–0011) |

`0012` does **not** make port 5555 work. The pool split those ports on purpose.
