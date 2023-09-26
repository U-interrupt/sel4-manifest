<!--
     Copyright 2018, Data61, CSIRO

     SPDX-License-Identifier: CC-BY-SA-4.0
-->

sel4-manifest
=================

sel4test-manifest
-----------------

The sel4test project aims to test sel4 and some of its user libraries on many different targets.

For general instructions on using this repository, see [Getting Started](https://docs.sel4.systems/GettingStarted)
and the [seL4Test page](https://docs.sel4.systems/seL4Test) on the docsite.

See [Host Dependencies](https://docs.sel4.systems/HostDependencies) for required dependencies.

sel4bench-manifest
------------------

Manifest of the seL4bench project, which contains a set of microbenchmarks for seL4.

sel4service-manifest
--------------------

Manifest of the sel4service project, which runs sqlite3 benchmark with xv6 fs server and ramdisk server.

```sh
mkdir sel4service-manifest
cd sel4service-manifest
repo init -u https://github.com/U-interrupt/sel4-manifest.git -m service.xml
repo sync

# Run on QEMU
mkdir build
../init-build.sh -DPLATFORM=qemu-riscv-virt -DQEMU_BINARY=<Your path to QEMU> -DSIMULATION=1 -DQEMU_MEMORY=2g -DLibSel4MuslcSysMorecoreBytes=1048576 -DNUM_NODES=4 -DLibSel4UtilsStackSize=262144 -DUINTR=1 -DSMP=1
<Your path to QEMU> -machine virt -cpu rv64 -nographic -m size=2g -smp 4 -bios none -kernel images/sel4service-rootserver-image-riscv-qemu-riscv-virt

# Build image for Rocket Chip
mkdir build-rocket
../init-build.sh -DPLATFORM=rocketchip -DRISCV64=1 -DLibSel4MuslcSysMorecoreBytes=1048576 -DNUM_NODES=4 -DLibSel4UtilsStackSize=262144 -DUINTR=1 -DSMP=1
ls -lh images
```