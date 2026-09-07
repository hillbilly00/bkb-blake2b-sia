# Mining Rig Rentals — listing copy

## Short (top of listing)

```
READ FIRST — AlphaPool / Knots BLAKE2b:
Use port 7777 ONLY.

us1.alphapool.tech:7777
(us2 / eu1 / sg1 also :7777)

Do NOT use port 5555. That port is for Goldshell.
This is a Baikal BK-B (Sia firmware). On 5555 you will see 0 hash and think the rental is dead.

Algo: Blake2b-Sia
Clock: 400 MHz stock (warehouse — no OC)
If dashboard is 0, switch 5555 → 7777 before opening a ticket.
```

## Welcome / auto message

```
Thanks for the rent.

This rig is a Baikal BK-B (Sia-firmware ASIC), not a Goldshell.

AlphaPool / BTCB2b:
  stratum+tcp://us1.alphapool.tech:7777
  worker: your_bc1_address.worker
  password: x

Port 5555 will not hash on this machine. Use 7777.
```
