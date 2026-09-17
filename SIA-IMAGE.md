# BK-B Blake2b / AlphaPool image notes

Warehouse: keep clock at 400 MHz. Do not overclock.

Pool (Sia-firmware ASIC, including Baikal BK-B):

    stratum+tcp://us1.alphapool.tech:7777
    user: <bc1-payout-address>.<worker>
    pass: x
    algorithm: sia   (alias: blake2b)

Port 5555 is for Goldshell-style clients. Do not use it on the BK-B.

## Published image (no custom rebuild)

Use published Blakestream BKB v2.1:

    https://bootstrap.blakestream.io/firmware/Blakestream-BKB-v2.1.img.xz

Flash with Balena Etcher. Keep a copy of factory PiZero_GB_180105_V1.0.img.

Do not use the Giant-B / GaintB image URL on a BK-B.

## Build a new image with patch 0012 (Ubuntu box)

Needs ~10 GB disk, sudo, and the factory 3.9 GB image. Do not build this
binary on a modern x86 host and copy it to the Pi.

    git clone https://github.com/SidGrip/Blakestream-Baikal-BKB.git
    cd Blakestream-Baikal-BKB
    git clone https://github.com/cod3gen/sgminer-baikal sgminer-build/src
    cd sgminer-build/src && git checkout dev
    for p in ../patches/[0-9]*.patch; do patch -p1 < "$p"; done
    patch -p1 < ../patches/0012-baikal-sia-blake2b-work-fill.patch
    cd ../..

    docker pull --platform linux/arm/v7 arm32v7/ubuntu:16.04
    docker run --rm --platform linux/arm/v7 \
      -v "$PWD/sgminer-build/src:/src" \
      arm32v7/ubuntu:16.04 \
      bash -c '
        DEBIAN_FRONTEND=noninteractive apt-get update -qq
        DEBIAN_FRONTEND=noninteractive apt-get install -y -qq \
          sed coreutils build-essential autoconf automake libtool pkg-config \
          libcurl4-openssl-dev libudev-dev libusb-1.0-0-dev libjansson-dev \
          libncurses5-dev libssl-dev
        cd /src
        make CFLAGS="-g -O1 -Wall -DTRUE=1 -DFALSE=0"
      '

    cp sgminer-build/src/sgminer overlay/opt/scripta/bin/sgminer
    cp sgminer-build/src/sgminer sgminer-build/sgminer.patched

Then Path A in Blakestream BUILD.md (fetch factory 3.9 GB image, overlay, repack, xz).

## Faster than a new card: drop in sgminer only

    cp /opt/scripta/bin/sgminer /opt/scripta/bin/sgminer.bak
    cp sgminer /opt/scripta/bin/sgminer
    chmod +x /opt/scripta/bin/sgminer

License: GPLv3. Keep SidGrip / Blakestream and cod3gen/sgminer-baikal credit
if you publish a fork.
